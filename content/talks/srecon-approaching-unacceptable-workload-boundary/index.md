---
draft: true
title: "Approaching the Unacceptable Workload Boundary"
author: Baron Schwartz
date: 2018-03-29T11:25:00-07:00
ratio: "16:9"
event: "USENIX SREcon18 Americas"
location: "Hyatt Regency Santa Clara, 5101 Great America Parkway, Santa Clara, CA 95054, USA"
site: "https://www.usenix.org/conference/srecon18americas/presentation/schwartz"
abstract: "We've all stared in frustration at a system that degraded into nonresponsiveness, to the point that you couldn't even kill-dash-nine whatever was responsible for the problem. A key fact we all recognize, but may not recognize as significant, is that this isn't a sharp boundary. There's a gradient of deteriorating performance where the system becomes less predictable and stable. In this talk I'll explain: what the unacceptable workload boundary is; how to recognize and predict the signs; how to measure and model this simply; what causes nonlinear performance degradation; and how to use this to architect more scalable systems."
theme: "monobloc"
thumbnail: scalability-is-quantifiable.jpg
video: ""
---
layout: true
<div class="remark-slide-number" style="left: 20px; right: unset">@xaprb</div>

---
class: title
background-image: url(action-balance-fun-305250.jpg)
background-size: cover

<div class="smokescreen" style="bottom: 100px; top:unset">
<h2>Approaching the Unacceptable Workload Boundary
<h3>Baron Schwartz &bullet; SREcon18 Americas
</div>

---
class: image-right
# Logistics & Stuff

.col[
Slides are at [xaprb.com/talks/](https://www.xaprb.com/talks/).

Ask questions anytime.

Please get in touch: [@xaprb](https://twitter.com/xaprb) or baron@vividcortex.com.
]

.rc[
![headshot](headshot.jpg)
]

---
class: bigger
# Introduction

What happens as systems get bigger and more heavily loaded?

--
* What is a system's operating domain?

--
* How is load defined?

--
* Where is the load limit? How can you see it coming?

--
* How does the system behave near this limit?

--
* Can you measure and model this behavior?

---
class: center, img-300h
# Operating Domain and Failure Boundaries

Rasmussen's model describes an operating domain bounded by economic risk, effort, and
safety. The system's operating state is a point within the domain, always moving
around.

![Rasmussen's Model](rasmussens-model.jpg)

---

background-image: url(rasmussens-model.jpg)

---
class: img-450h, center
# The Actual Boundaries Are Unknown

![Real Boundaries](real-boundaries.svg)

---
class: img-450h, center
# We Draw Limits Where We Think It's Safe

![Real Boundaries](real-boundaries.svg)

<div style="position: absolute; top: 45%; left: 27%">Margin of Error</div>
<div style="position: absolute; top: 38%; left: 56%">Overdraft Protection</div>
<div style="position: absolute; top: 81%; left: 45%">Overprovisioning</div>

---
class: img-450h, center, two-column
# The Buffer Zone Is Nonlinear

.col[
![Margins of Error](shaded-boundaries.jpg)
]

--

.col[
We think the gradient looks like this.

![Ramp](ramp.svg)

It really looks more like this.

![Nonlinear](nonlinear.svg)
]

---
# Complex Systems Run In Degraded Mode

Richard Cook lists 18 precepts of system failure in [How Complex Systems
Fail](http://web.mit.edu/2.75/resources/random/How Complex Systems Fail.pdf).

Precepts 4) and 5) are especially relevant.

--

> **4) Complex systems contain changing mixtures of failures latent within them.**
> The complexity of these systems makes it impossible for them to run without
> multiple flaws being present.
> 
> **5) Complex systems run in degraded mode.**
> A corollary to the preceding point is that complex systems run as broken systems.

--

Systems can and do function beyond their load limits.

---
# What Is The Definition Of Load?

There's no one right answer to this question, but there's a useful answer for
this discussion.

--

Load is the sum of task residence times during an observation interval \\(T\\).

--

You can use Little's Law to prove that this definition of load is equivalent to
average concurrency of tasks queued or in service:

\\[
N = \frac{\sum_{}^{}{R}}{T}
\\]

---
# Load, Utilization, And Queueing

Load (concurrency) is related to utilization and queue length, but it's not the
same.

--
* Concurrency is the number of requests in process simultaneously.

--
* Average concurrency is an average over an observation interval \\(T\\).

--
* Utilization is the fraction of \\(T\\) that was busy.

--
* Queue length is the instantaneous or time-averaged number of tasks waiting
  to be serviced.

--
* By Little's Law, utilization and queue length are types of concurrency:
  * Utilization is the concurrency of in-service tasks.
  * Queue length is the concurrency of queued tasks.

---
class: two-column
# What Is The Load Limit?

Can utilization define the load limit? If so, queueing theory might hold an answer.

.col[
* This is appealing because utilization has a clear limit: it can't be more than
  100%.
* But:
  * Load can be unlimited
  * The “hockey stick” queueing curve is hard to use
  * The "knee" is unintuitive
]

.col[
![Hockey Stick](hockey.svg)
]

---
# Scaling A System: Ideal

Suppose a clustered system can do X work per unit of time.<br>Ideally, if you double the cluster size, it can do 2X work.

![Linear Scalability](linear1.svg)

---
class: two-column
# The Linear Scalability Equation

.col[
The equation that describes ideal scaling:

\\[
X(N) = \frac{\\lambda N}{1}
\\]

where \\(\\lambda\\) is the slope of the line.
]

.col[
![Linear Scalability](linear1.svg)
]

---
class: center
# But Our Cluster Isn’t Perfect

Speedup comes from executing tasks in parallel, e.g. ~ scatter-gather.

What happens to performance if some portion isn’t parallelizable?

![Speedup](speedup.svg)

---
class: two-column,bigger
# Amdahl’s Law

\\[
X(N) = \frac{\\lambda N}{1+\\sigma(N-1)}
\\]

.col[
Amdahl’s Law describes the fraction \\(\\sigma\\) that can’t be done in parallel.
Adding nodes provides some speedup, but there’s a ceiling.
]

.col[
![Amdahl’s Law](linear2.svg)
]

---
class: center
# But What If Workers Coordinate?

Suppose the parallel workers have dependencies on each other?

![Coordination](coordination.svg)

---
class: two-column,center, img-450h
# N Workers = N(N-1) Pairs

.col[
![Complete Graph](5-simplex_graph.svg)
]

.col[
![Complete Graph](9-simplex_graph.svg)
]

---
class: two-column, bigger
# Universal Scalability Law

\\[
X(N) = \frac{\\lambda N}{1+\\sigma(N-1)+\\kappa N(N-1)}
\\]

.col[
Represents crosstalk (coherence) penalty by coefficient \\(\\kappa\\).
The system completes _less_ work as the load increases!
]

.col[
![Universal Scalability Law](linear3.svg)
]

---
class: center, bigger, img-300h
# Crosstalk Penalty Grows Fast

Coherence (red) grows slowly, but crosstalk (blue) grows rapidly. At saturation, \\(\\kappa\\) is creating nonlinear behavior.

![USL Regions](regions.png)

---
class: bigger
# More About Crosstalk

Q: Isn’t crosstalk just a design flaw?

A: Yes and no. Real-life: consensus, 2-phase commit, NUMA, etc…

Q: Doesn’t it seem odd to assume that crosstalk is a constant?

A: It’s not, the amount of crosstalk-related work is a function of N

---
class: center
# How Do You Measure Parameters?

You can’t measure serialization & crosstalk directly; use regression to estimate them.

![Curve Fitting](fitting.png)

---
class: center, middle, bigger
# Experiment Interactively

[desmos.com/calculator/3cycsgdl0b](https://www.desmos.com/calculator/3cycsgdl0b)

---
class: center, bigger
# What is Scalability?

The USL is a mathematical definition of scalability.

It’s a function that turns workload into throughput.

It’s formally derived and has real physical meaning.

\\[
X(N) = \frac{\\lambda N}{1+\\sigma(N-1)+\\kappa N(N-1)}
\\]

---
class: bigger
# But What Is Load?

In most circumstances we care about, load is concurrency.

Concurrency is the number of requests in progress.

It’s surprisingly easy to measure: \\( N = \frac{\sum_{}^{}{R}}{T} \\)

Many systems emit it as telemetry:

- MySQL: `SHOW STATUS LIKE 'Threads_running'`
- Apache: active worker count

---
class: title
background-image: url(Matterhorn-mit-Morgennebel.jpg)
.smokescreen[
# Four Great Uses Of The USL
]

---
class: two-column, center
# 1. Forecast Workload Failure Boundary

The USL can reveal the workload failure boundary approaching. Use regression to
extract coefficients, then plot; or plot and eyeball to see if you’re
approaching the boundary.

.col[
![Cisco Training Set](cisco-2.svg)
]

.col[
![Cisco Full Set](cisco.svg)
]

---
class: center, bigger
# 1. Forecast Workload Failure Boundary

Coda Hale wrote about the USL.
https://codahale.com/usl4j-and-you/

![Coda Hale Prediction](coda-hale.jpg)

---
class: bigger
# 1. Forecast Workload Failure Boundary

- By estimating the parameters, you can forecast what you can’t see.
- This means you can “load test” under load you don’t yet experience.
- The USL is a pessimistic model.
--

  - Your systems _should_ scale better than the USL predicts.
  - But _you_ should be even more pessimistic than the USL.

---
class: bigger, center, img-300h
# 2. Characterize Non-Scalability 
Why doesn’t your system scale perfectly?<br>
The USL reveals the amount of serialization & crosstalk.

![USL Regions](regions.png)

---
# 2. Characterize Non-Scalability

Paypal’s NodeJS vs Java benchmarks are a good example!
https://www.vividcortex.com/blog/2013/12/09/analysis-of-paypals-node-vs-java-benchmarks/

![Paypal vs. NodeJS](paypal-node.jpg)

---
class: bigger
# 3. How Scalable Should It Be?

The USL is a framework for making systems look really bad.

Many 10+ node MPP databases barely do anything per-node.

Calculate per-node a) clients b) data size c) throughput.

One 18-node database: 4000 QPS ~220 QPS/node, 5ms latency.

---
class: bigger, img-300h
# 3. How Scalable Should It Be?

You should always measure databases; don’t simply use architectural
diagrams to intuit whether they will scale.

![CitusDB](animated-citus-738243d8.svg)

.footnote[
This diagram is from [CitusDB](https://www.citusdata.com/), and is
meant only to illustrate the point, not to imply anything about CitusDB.
]

---
class: img-450h, center
# 4. See Your Teams As Systems

![Richard Branson Tweet](rbranson-tweet.jpg)

---
class: center, bigger
# 4. See Your Teams As Systems

## “To go fast, go alone. To go far, go together.”

Adrian Colyer wrote a good blog post about teams-as-systems and USL.
https://blog.acolyer.org/2015/04/29/applying-the-universal-scalability-law-to-organisations/

---
class: image-right, bigger

.col[
# 4. See Your Teams As Systems
The USL isn’t novel in that sense... “I gave my boss two copies of the Mythical
Man-Month so they can read it twice as fast.”
]

.rc[
![Mythical Man-Month](mmm.jpg)
]

---
class: bigger
# What Else Can The USL Illuminate?

Open-plan offices: My work takes more work when others are nearby.

Map-Reduce: That’s a whole lotta overhead, but it sure is scalable.

Mutexes: Theoretically just serialize, but those damn OS schedulers.

---
class: center, bigger, img-300h
# What’s NOT Scalability?

I commonly see throughput-vs-latency charts. This seems legit till you get systems under high load.

![Not A Function](not-a-function.svg)

---
class: center, bigger, img-300h
# Scalability Isn’t Throughput-vs-Latency

The throughput-vs-latency equation has **two** solutions.

![Nose Function](nose-equation-desmos.png)

---
class: center, bigger, img-300h
# Concurrency-vs-Latency is OK

It’s a simple quadratic per Little’s Law, and is quite useful.

![Concurrency vs. Latency](cisco-3.svg)

---
class: center, two-column, bigger

.col[
# Some Resources

I wrote a
[book](https://www.vividcortex.com/resources/universal-scalability-law/).

I created an [Excel
workbook](https://www.vividcortex.com/resources/usl-modeling-workbook).

These slides are at [xaprb.com/talks](https://www.xaprb.com/talks/).
]

.col[
[![USL Ebook Cover](usl-ebook-cover.png)](https://www.vividcortex.com/resources/universal-scalability-law/)
]

---
class: center, bigger
# Conclusions

Scalability is formally definable, and black-box observable.

Scalability is nonlinear; this region is the failure boundary.

Scalability is a function with parameters you can estimate.

---
class: bigger
# Further Reading & References

- https://www.vividcortex.com/resources/ for ebook, Excel workbook.

- http://www.perfdynamics.com/Manifesto/USLscalability.html for the original source.
