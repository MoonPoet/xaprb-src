---
title: "Scalability Is Quantifiable: The Universal Scalability Law"
author: Baron Schwartz
date: 2017-11-01T15:00:00-08:00
ratio: "16:9"
event: "USENIX LISA17"
location: "Hyatt Regency San Francisco, 5 Embarcadero Center, San Francisco, CA"
site: "https://www.usenix.org/conference/lisa17/conference-program/presentation/schwartz"
abstract: "Do you know what scalability really is? It's a mathematical function that's simple, precise, and useful. REALLY useful. It describes the relationship between system performance and load. In this talk you'll learn the function (the Universal Scalability Law), how it describes and predicts system behavior you see every day, and how to use it in practice. I'll show you how to understand the function, how to capture the data you need to measure your own system's behavior (you probably already have that), and how to analyze the data with the USL. You'll leave this talk knowing exactly what scalability is and what causes non-linear scaling. There are two factors, and you'll start seeing those everywhere, too. As a result, when systems don't scale you'll know what kind of problem to look for, and you'll avoid building bottlenecks into your systems in the first place. Final note: this talk requires zero mathematical skill."
theme: "monobloc"
thumbnail: scalability-is-quantifiable.jpg
video: "https://youtu.be/lZU6RK0oazM"
---
class: title
background-image: url(ThinkstockPhotos-480085336.jpg)

.smokescreen[
# Scalability is Quantifiable
## The Universal Scalability Law<br>Baron Schwartz &bullet; November 2017
]

---
class: img-right
layout: true

---
# Logistics & Stuff

.col[
Slides will be posted. Ask questions anytime.

Founder of VividCortex. Author of High Performance MySQL.

Love to hear from you: [@xaprb](https://twitter.com/xaprb) and
baron@vividcortex.com

[xaprb.com](https://www.xaprb.com/)
]

.rc[
![headshot](headshot.jpg)
]

---
layout:false
# How Systems Fail Under Load

You’ve seen systems become sluggish under high load.

How can we describe and reason about what’s happening?

---
layout: true
class: two-column

---
# Failure Boundaries

.col[
Cook and Rasmussen describe failure boundaries around the operating domain

One such is the unacceptable workload boundary
]

.col[
![Cook & Rasmussen](cook-rasmussen.jpg)
]

---
class: smaller
# Workload Failure Isn’t Crisp

.col[
Unacceptable workload is not sharply defined, it’s a _gradient_

Cook lists 18 precepts of system failure in [How Complex Systems Fail](web.mit.edu/2.75/resources/random/How Complex Systems Fail.pdf)

\#5: **Complex systems run in degraded mode**
]

.rc[
![Cook & Rasmussen](cook-rasmussen.jpg)
]

--

Cook introduces _error margin_. What’s the _workload margin_?

What if you drift into it?

---
layout: true
class: center

---
# The Failure Boundary Is Nonlinear

This region is _highly_ nonlinear and unintuitive. It’s analogous to post-elastic material behavior.

![Failure Boundary](failure-boundary.png)

---
# Capacity

Systems can, and do, function beyond their capacity limits.

Capacity limits are scalability limits.

--

How can we define and reason about system capacity?

Ditto, for scalability?

---
# Queueing Theory

There’s a branch of operations research called queueing theory.

It analyzes what happens to customers when systems get busy.

It’s difficult to apply in “the real world” of capacity & ops.

---
# The Hockey Stick Curve

The “hockey stick” queueing curve is hard to use in practice. And the sharpness
of the “knee” is very nonlinear and hard for humans to intuit.

![Hockey Stick](hockey.svg)

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
class: two-column
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
class: two-column
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
class: center, img-300h
# Crosstalk Penalty Grows Fast

Coherence (red) grows slowly, but crosstalk (blue) grows rapidly. At saturation, \\(\\kappa\\) is creating nonlinear behavior.

![USL Regions](regions.png)

---
layout: false
# More About Crosstalk

Q: Isn’t crosstalk just a design flaw?

A: Yes and no. Real-life: consensus, 2-phase commit, NUMA, etc…

Q: Doesn’t it seem odd to assume that crosstalk is a constant?

A: It’s not, the amount of crosstalk-related work is a function of N

---
class: center, smaller
# How Do You Measure Parameters?

You can’t measure serialization & crosstalk directly; use regression to estimate them.

![Curve Fitting](fitting.png)

---
class: center, middle
# Experiment Interactively

[desmos.com/calculator/3cycsgdl0b](https://www.desmos.com/calculator/3cycsgdl0b)

---
class: center
# What is Scalability?

The USL is a mathematical definition of scalability.

It’s a function that turns workload into throughput.

It’s formally derived and has real physical meaning.

\\[
X(N) = \frac{\\lambda N}{1+\\sigma(N-1)+\\kappa N(N-1)}
\\]

---
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
class: center
# 1. Forecast Workload Failure Boundary

Coda Hale wrote about the USL.
https://codahale.com/usl4j-and-you/

![Coda Hale Prediction](coda-hale.jpg)

---
# 1. Forecast Workload Failure Boundary

- By estimating the parameters, you can forecast what you can’t see.
- This means you can “load test” under load you don’t yet experience.
- The USL is a pessimistic model.
--

  - Your systems _should_ scale better than the USL predicts.
  - But _you_ should be even more pessimistic than the USL.

---
class: center, img-300h
# 2. Characterize Non-Scalability 
Why doesn’t your system scale perfectly?<br>
The USL reveals the amount of serialization & crosstalk.

![USL Regions](regions.png)

---
class: img-center, smaller
# 2. Characterize Non-Scalability

Paypal’s NodeJS vs Java benchmarks are a good example!
https://www.vividcortex.com/blog/2013/12/09/analysis-of-paypals-node-vs-java-benchmarks/

![Paypal vs. NodeJS](paypal-node.jpg)

---
# 3. How Scalable Should It Be?

The USL is a framework for making systems look really bad.

Many 10+ node MPP databases barely do anything per-node.

Calculate per-node a) clients b) data size c) throughput.

One 18-node database: 4000 QPS ~220 QPS/node, 5ms latency.

---
class: img-300h
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
class: center
# 4. See Your Teams As Systems

## “To go fast, go alone. To go far, go together.”

Adrian Colyer wrote a good blog post about teams-as-systems and USL.
https://blog.acolyer.org/2015/04/29/applying-the-universal-scalability-law-to-organisations/

---
class: img-right

.col[
# 4. See Your Teams As Systems
The USL isn’t novel in that sense... “I gave my boss two copies of the Mythical
Man-Month so they can read it twice as fast.”
]

.rc[
![Mythical Man-Month](mmm.jpg)
]

---
# What Else Can The USL Illuminate?

Open-plan offices: My work takes more work when others are nearby.

Map-Reduce: That’s a whole lotta overhead, but it sure is scalable.

Mutexes: Theoretically just serialize, but those damn OS schedulers.

---
class: center, img-300h
# What’s NOT Scalability?

I commonly see throughput-vs-latency charts. This seems legit till you get systems under high load.

![Not A Function](not-a-function.svg)

---
class: center, img-300h
# Scalability Isn’t Throughput-vs-Latency

The throughput-vs-latency equation has **two** solutions.

![Nose Function](nose-equation-desmos.png)

---
class: center, img-300h
# Concurrency-vs-Latency is OK

It’s a simple quadratic per Little’s Law, and is quite useful.

![Concurrency vs. Latency](cisco-3.svg)

---
class: center
# Conclusions

Scalability is formally definable, and black-box observable.

Scalability is nonlinear; this region is the failure boundary.

Scalability is a function with parameters you can estimate.

---
class: two-column
# Further Reading & References

.col[

- [Neil Gunther](http://www.perfdynamics.com/Manifesto/USLscalability.html), author of the USL.
- My USL [book](https://www.vividcortex.com/resources/universal-scalability-law/).
- My USL [Excel workbook](https://www.vividcortex.com/resources/usl-modeling-workbook).
]

.col[
[![USL Ebook Cover](usl-ebook-cover.png)](https://www.vividcortex.com/resources/universal-scalability-law/)
]

---
class: two-column
# Slides and Contact Information

.col[
Slides are at [xaprb.com/talks/](https://www.xaprb.com/talks/), or scan the QR
code.

Contact:

- @xaprb on Twitter
- baron@vividcortex.com
]

.col[
<div id="qrcode"></div>
]
