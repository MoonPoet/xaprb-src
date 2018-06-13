---
title: 'How to Monitor Your Database'
date: "2018-06-13T17:00:00-04:00"
url: "/slides/velocity-2018-how-to-monitor-your-database/"
image: "/slides/velocity-2018-how-to-monitor-your-database/cover.jpg"
description: "Learn how you can monitor your database so you can learn what it’s really doing. When you can do this, you’ll become a much better engineer, not only building better systems but also making your team members heroes too."
ratio: "16:9"
theme: "monobloc"
---
class: title,no-number
background-image: url(cover.jpg)
background-size: cover

.smokescreen[
# How to Monitor Your Database 
## Baron Schwartz &bullet; May 2018
]

<div style="position: absolute; right: 20px; top: 20px; width: 250px;
background-color: rgba(0,0,0,.7); padding: 10px; border-radius: 10px">
<img src=vividcortex-horizontal-white-rgb.svg>
</div>

---
layout: true
<div class="remark-slide-number" style="left: 20px; right: unset">@xaprb</div>
<div class="remark-slide-number" style="left: 566px; width: 85px; padding: 5px">
<img src=vividcortex-horizontal-web.svg>
</div>

---
class: img-right
# Logistics and Contact Info

.col[
- Ask questions anytime
- Write me baron@vividcortex.com
- Tweet me at @xaprb
- Slides at [xaprb.com/talks/](https://www.xaprb.com/talks/)
]

.rc[<img src=headshot.jpg style="width: 100%; height: 100%; object-fit: cover">]

---
class: img-right
.col[
# Introduction & Agenda

- What is QoS and Why Does it Matter?
- The 4 Golden QoS Signals
- The 3 Golden Resource Signals
- The Zen of Performance
- The 3 Types of Performance Problems
- How To Diagnose Performance Problems
- Don’t Get Cut On Sharp Edges
- Conclusions and Resources
]

.rc[<img src=unsplash-photos-FoKO4DpXamQ.jpg style="height: 100%; width: 100%; object-fit: cover">]

???

- Who is this talk for
- What it's about, it's a general framework
- It comes from my philosophy, what I built VividCortex on
- How to make sense out of the sea of data you might look at
- Nagios plugin has dozens of checks, should I? No
- The goal is to cut down the confusion and get to what matters

---
class: title
background-image: url(unsplash-photos-5AiWn2U10cw.jpg)
background-size: cover

.smokescreen[
# Quality of Service
]

---
# Why Quality of Service Matters

* QoS is the most important thing to monitor about your database.
* Your database exists to a) store data b) answer questions.
* So you should measure *request* performance above all.
* *To know if there’s a problem, measure work-getting-done.*

???
- QoS is literally whether the database is doing its job right
- DB's job is to handle requests: "store" "answer"

---
# What is Quality of Service?

Approach performance from the *user’s* perspective:

> “I sent a request. I want a correct reply, fast.”

Users care about *request* performance.
The definition is *latency* in units of seconds per request.

???

- QoS is correctness and speed
- Care about the user's perspective
- Singular
- Definition of performance is unambiguous, based on laws

---
class: img-right

.col[
# You Must Care About All Requests

Users care about their own requests, but you have to make sure the
**population** of requests is getting good QoS.

This is **workload QoS**.
]

.rc[<img src=unsplash-photos-ZuV4bPalclY.jpg style="width: 100%; height: 100%; object-fit: cover">]

???

- Workload is the interaction between the users/app/database
- Measuring across that boundary

---
# The 4 Golden Signals of QoS

The **CELT metrics** reveal everything about workload QoS.

1. **Concurrency** is the number of simultaneous requests \\(N\\)
2. **Error Rate** is what it sounds like
3. **Latency** is response time, as previously defined \\(R\\)
4. **Throughput** is requests per second \\(X\\)

These can all be calculated as average (or p99) during intervals or as they
apply to individual requests (except for Throughput).

???

- This is a superset of RED method, SRE golden signals, etc.
- The names are standardized for clarity. Clarity matters a lot.
- The Site Reliability Engineering book
- Philosophy: less is more, the basics; Google can run on a few metrics, so can
  you
- Key: you can characterize individual + population, summary statistics
- The math-letter variable names are part of Little's Law

---
# Aside: Concurrency, The Magic Metric

Concurrency is the single best metric of **demand** or load.

By Little’s Law, \\(N=XR\\), average concurrency during a time interval \\(T\\) is
also

\\[
N = \frac{\sum_{}^{}{R}}{T}
\\]

???

- Concurrency is the best metric of load
- Normalized, comparable, dimensionless
- Related to every performance equation; load average and other familiar things
- Queue depth, queue length, load, -- all concurrency
- Throughput isn't a very good load metric.

---
# What About CPU Utilization?

To be clear: performance is **how well users are being served**.

But CPU utilization, network saturation, etc aren’t useless, either.

Isn’t high CPU utilization a performance problem?

???
- War story about mutexes causing low CPU utilization
- Again, look at work-getting-done

---
class: two-column
# These Are Resource Metrics

.col[
The **workload** places **demand** on **resources**.

The way resources respond to demand often explains performance.
]

???

- I'll show you next how to figure out if resources are adequate.

--

.col[
There are **four key resources**.

1. CPU cycles
2. Memory
3. Storage
4. Network
]

???

- Follow the link to learn tech-specific ways to apply the USE method

---
# The Three Golden Signals of Resource Sufficiency

The three golden signals are [Brendan Gregg’s USE
method](http://www.brendangregg.com/usemethod.html):

* Utilization
* Saturation
* Errors

---
class: smaller, two-column

# The Zen of Performance: Non-Duality
.col[

External (customer’s) view is singular:

* Request, and its latency and success.

Internal (operator’s) view is plural:

* Requests and their latency distribution, rates, and concurrency.
* System resources/components and their throughput, utilization, and backlog.
* Errors.
]

.rc[
![Yin and Yang](yin-yang.png)
]

---
class: two-column

# CELT + USE Together

.col[
The CELT and USE metrics are the **seven golden signals** of overall *system*
health and performance, unifying the external (customer, workload) and internal
(resource) perspectives.
]

.col[
![Day and Night](day-and-night.jpg)
]

???

- Errors are both user-facing and internal (e.g. kernel logs)

---
# What Exactly Is A System?

My view is that *system* is the totality of all interacting parts:

* The customers or users
* The workload they generate
* The services handling that workload
* The resources the services need
* All dependent services etc.

If you're not monitoring all of these, you're not **monitoring the system**.

???

- "We're getting reports of outages."
- "Let me check... the database looks fine, CPU is fine."

---
class: title
background-image: url(unsplash-photos-iuqxv7kFj64.jpg)
background-size: cover

.smokescreen[
# Your Mental Models Are Wrong
]

---
# System As Imagined, System As Existing

As we build and operate systems, we form **mental models** of them.

These help us conceptualize and predict system behavior.

But **the map is not the territory**. Mental models are always wrong.

---
class: img-450h
# Pete’s Mental Model

[![Pete’s For Loop](petes-for-loop.jpg)](https://twitter.com/toomuchpete/status/1001213344207040512)

---
# Your Mental Model Of Your Databases

* The purge cron job runs at 4am once a day for 2-3 minutes
* There’s an add-to-cart query that precedes read-from-cart queries
* Users constantly check for messages from users they follow
* Our most expensive query is the leaderboard
* The most frequent queries come from the product listings page

???

- The only way to refine your mental models is to measure and see where they're
  wrong.

---
# What’s Isn’t Measured… Is Imagined

If you haven’t measured your application/database interaction, **you will be
surprised.**

--

Just like Pete’s `for` loop, the gap between your mental models and reality is
real, and measuring (or using the debugger) will show you what you’re imagining
wrong.

---
# Are You Monitoring Workload QoS?

You probably have good resource monitoring, but poor (or no) workload
monitoring.

---
class: smaller, img-right

.col[
## How To Measure Workload

There are three primary ways to measure requests (workload):

1. Turn on full query logging
   1. Pros: it works, it’s widely supported
	2. Cons: often severe performance overhead
2. Use internal statistics tables/views, if they exist
	1. Pros: built in/native; moderate impact
	2. Cons: often doesn’t exist; only gives aggregate data
3. Sniff network traffic
	1. Pros: near-zero load added, super-detailed
	2. Cons: technically hard; doesn’t measure internals
]

.rc[<img src=unsplash-photos-tf0jFfbg03U.jpg style="width: 100%; height: 100%; object-fit: cover">]


---
class: title
background-image: url(unsplash-photos-t7YycgAoVSw.jpg)
background-size: cover

.smokescreen[
# Fixing Performance Problems
]

---
# The Three Performance Problems

1. Latency too high
2. Resource usage too high
3. Collateral damage / noisy neighbor problems

---
# Causes of Performance Problems

- Needless requests
- Too-frequent requests
- Too-slow requests
- Resource starvation or stalls

---
class: two-column
# The Performance Swiss-Army Knife

.col[

A **profile** is an all-purpose tool for finding signal in the noise.

1. Group related requests together
2. Rank them by a metric
3. Look at the top items
]

.col[
![Profile](profile.png)
]

---
background-image: url(profile.png)
background-size: contain

---
# Finding Performance Problems

- Finding needless and too-frequent requests
	- Profile by frequency (throughput), ranking by `SUM(count)`
	- Are they useless, e.g. driver look-before-leap `ping` queries?
- Finding too-slow requests
	- Profile by `SUM(latency)`, then look at outliers
	- Profile by `P99(latency)`

---
class: img-right

.col[
# Prioritizing What You Find

How do you know whether “optimizing” a query is worth it?

Rule of thumb:
* To conserve resources / reduce collateral damage, look at % of total
* To make customers happy, look at p99 latency
]


.rc[<img src=unsplash-photos-OgvqXGL7XO4.jpg style="width: 100%; height: 100%; object-fit: cover">]

---
class: img-right, smaller

.col[
# Inspecting Individual Requests

You don’t learn much from aggregate data.

There’s no “average” request.

You need to drill into individual examples (individual log lines or samples).

You also need to look at the *distribution* of request latencies.
]

.rc[<img src=unsplash-photos-vWI1kTcMcDI.jpg style="width: 100%; height: 100%; object-fit: cover">]

---
# How To Fix A “Bad” Query

If a query is too slow, why?

- Is it slower than it *should* be?
- What is it *doing*? Working, waiting?
- There’s only three possible solutions: eliminate work, reduce work, or work
  faster

---
# Technology Sharp Edges

Every database technology has its Kryptonite.

* MySQL: the query cache, replication, the buffer pool…
* PostgreSQL: VACUUM, connection overhead, shared buffers…
* MongoDB: missing indexes, lock contention…

---
# Technology-Specific Resources

Many of the “sharp edges” are special resources.

* Connection pools: fixed # of connections is a fixed resource.
* Buffer pools / caches: finite size to hold the working set.
* Etc.

Usually only a few things matter much. (But it depends.)

---
# Conclusions

- Monitor workload, not just resources
- Measure what matters: work getting done, customer experience
- Focus on the 7 Golden Signals (CELT + USE)
- Profile to focus, triage, and prioritize
- Drill down to individual request details
- Cover the basics of your technology’s “sharp edges”

---
# Related: What Should I Monitor?

… and how should I do it?

<iframe width="621" height="350" src="https://www.youtube.com/embed/zLjhFrUhqxg" frameborder="0" allowfullscreen></iframe>

---
class: three-column, smaller

# Resources: Free EBooks

.col[
[![Practical Query Optimization](pqo-ebook.png)](https://www.vividcortex.com/resources/practical-query-optimization)
]
.col[
[![Making VividCortex Work For You](vividcortex-ebook.jpg)](https://www.vividcortex.com/resources/6-ways-to-make-vividcortex-work-for-you-download)
]
.col[
[![Observability](observability-ebook.jpg)](https://www.vividcortex.com/resources/architecting-highly-monitorable-apps)
]


Your artisanal hand-brewed free copy is waiting at https://vividcortex.com/resources

---
class: three-column,center,img-450h

# More Resources

.col[
[![SRE Book](sre-book.jpg)](https://landing.google.com/sre/book.html)
]

.col[
&nbsp;
]

.col[
[![DBRE Book](dbre.jpg)](http://shop.oreilly.com/product/0636920039761.do)
]

---
class: two-column
# Slides and Contact Information

.col[
Slides are at https://www.xaprb.com/talks/ or you can scan the QR code. To export as PDF, print with Chrome.

Contact: @xaprb or baron@vividcortex.com

]

.col[
<div id="qrcode"></div>
]
