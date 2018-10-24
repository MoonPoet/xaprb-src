---
title: 'How to Monitor Your Database'
date: "2018-09-05T17:00:00-07:00"
url: "/slides/all-things-open-2018-monitor-your-database/"
image: "/slides/all-things-open-2018-monitor-your-database/cover.jpg"
description: "Learn how to monitor your database effectively, focusing on the right things to make the server efficient, meet performance and cost goals, and empower the engineering team to develop effectively against the database."
ratio: "16:9"
themes:
- apron
- descartes
- adirondack
---
class: title, no-footer, fogscreen, shelf
background-image: url(unsplash-photos-99neAF8kqhg.jpg)

# How to Monitor Your Database
## Baron Schwartz &bullet; All Things Open 2018

![Logo](vividcortex-horizontal-white-rgb.svg# smokescreen pa-2 br-3 mt-8)

---
layout: true
name: footer

.footer[
- @xaprb
- ![logo](vividcortex-horizontal-web.svg)
]

---
class: img-right-full

![headshot](headshot.jpg)

# Introduction, Getting Started

- Ask questions anytime
- Write me baron@vividcortex.com
- Tweet me at @xaprb
- Slides at [xaprb.com/talks/](https://www.xaprb.com/talks/)

---
class: img-right-full

# Agenda

![Agenda](unsplash-photos-FoKO4DpXamQ.jpg)

- What is QoS and Why Does it Matter?
- The 4 Golden Signals of QoS
- The 3 Golden Signals of Resource Sufficiency
- The Zen of Performance
- The 3 Types of Performance Problems
- How To Diagnose Performance Problems
- Don't Get Cut On Sharp Edges
- Conclusions and Resources

???

- Who is this talk for
- What it's about, it's a general framework
- It comes from my philosophy, what I built VividCortex on
- How to make sense out of the sea of data you might look at
- Nagios plugin has dozens of checks, should I? No
- The goal is to cut down the confusion and get to what matters

---
class: title, smokescreen
background-image: url(unsplash-photos-5AiWn2U10cw.jpg)

# Quality of Service

---
class: roomy

# Why Quality of Service Matters

* QoS is the most important thing to monitor about your database.
* Your database exists to a) store data b) answer questions.
* So you should measure *request* performance above all.
* *To know if there's a problem, measure work-getting-done.*

???
- QoS is literally whether the database is doing its job right
- DB's job is to handle requests: "store" "answer"

---
class: roomy
# What is Quality of Service?

Approach performance from the *user's* perspective:

> "I sent a request. I want a correct reply, fast."

Users care about *request* performance.
The definition is *latency* in units of seconds per request.

???
- QoS is correctness and speed
- Care about the user's perspective
- Singular
- Definition of performance is unambiguous, based on laws

---
class: img-right-full, fit-h1

![Flock of Sheep](unsplash-photos-ZuV4bPalclY.jpg)

# You Must Care About All Requests

Users care about their own requests, but you have to make sure the
**population** of requests is getting good QoS.

This is **workload QoS**.

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
class: roomy, fit-h1
# Aside: Concurrency, The Magic Metric

Concurrency is the single best metric of **demand** or load.

By Little's Law, \\(N=XR\\), average concurrency during a time interval \\(T\\) is
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
class: roomy

# What About CPU Utilization?

To be clear: performance is **how well users are being served**.

But CPU utilization, network saturation, etc aren't useless, either.

Isn't high CPU utilization a performance problem?

???
- War story about mutexes causing low CPU utilization
- Again, look at work-getting-done

---
class: roomy

# These Are Resource Metrics

The **workload** places **demand** on four key **resources**.

1. CPU cycles
2. Memory
3. Storage
4. Network

The way resources respond to demand often explains performance.

???
- I'll show you next how to figure out if resources are adequate.

---
class: roomy, fit-h1

# The Three Golden Signals of Resource Sufficiency

The three golden signals are [Brendan Gregg's USE
method](http://www.brendangregg.com/usemethod.html):

* Utilization
* Saturation
* Errors

???

- Follow the link to learn tech-specific ways to apply the USE method

---
class: img-right, compact

# The Zen of Performance: Non-Duality

![Yin and Yang](yin-yang.svg# w-8-12 center mt4)

External (customer's) view is singular:

* Request, and its latency and success.

Internal (operator's) view is plural:

* Requests and their latency distribution, rates, and concurrency.
* System resources/components and their throughput, utilization, and backlog.
* Errors.

---
class: img-right, roomy

# CELT + USE Together

![Day and Night](day-and-night.jpg)

The CELT and USE metrics are the **seven golden signals** of overall *system*
health and performance, unifying the external (customer, workload) and internal
(resource) perspectives.

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

--

Crucially, systems are more than the sum of their parts. They have emergent behaviors and properties that come from the combinations of the above.

If you're not monitoring all of these, you're not **monitoring the system**.

???

- "We're getting reports of outages."
- "Let me check... the database looks fine, CPU is fine."

---
class: title, smokescreen
background-image: url(unsplash-photos-iuqxv7kFj64.jpg)

# Your Mental Models Are Wrong

---
class: roomy, fit-h1

# System As Imagined, System As Existing

As we build and operate systems, we form **mental models** of them.

These help us conceptualize and predict system behavior.

But **the map is not the territory**. Mental models are always wrong.

---
class: roomy

# Pete's Mental Model

[![Pete's For Loop](petes-for-loop.jpg# maxw-70pct center)](https://twitter.com/toomuchpete/status/1001213344207040512)

---
class: roomy, fit-h1

# Your Mental Model Of Your Databases

* The purge cron job runs at 4am once a day for 2-3 minutes
* There's an add-to-cart query that precedes read-from-cart queries
* Users constantly check for messages from users they follow
* Our most expensive query is the leaderboard
* The most frequent queries come from the product listings page

???

- The only way to refine your mental models is to measure and see where they're
  wrong.

---
class: roomy

# What's Isn't Measured… Is Imagined

If you haven't measured your application/database interaction, **you will be
surprised.**

--

Just like Pete's `for` loop, the gap between your mental models and reality is
real, and measuring (or using the debugger) will show you what you're imagining
wrong.

---
class: roomy

# Are You Monitoring Workload QoS?

You probably have good resource monitoring, but poor (or no) workload
monitoring.

---
class: compact, img-right-full

![](isis-franca-641217-unsplash.jpg)

# How To Measure Workload

There are three primary ways to measure requests (workload):

1. Turn on full query logging
	- Pros: it works, it's widely supported
	- Cons: often severe performance overhead
--

2. Use internal statistics tables/views, if they exist
	- Pros: built in/native; moderate impact
	- Cons: often doesn't exist; only gives aggregate data
--

3. Sniff network traffic
	- Pros: near-zero load added, super-detailed
	- Cons: technically hard; doesn't measure internals

---
class: title, smokescreen
background-image: url(unsplash-photos-t7YycgAoVSw.jpg)

# Fixing Performance Problems

---
class: roomy
# The Three Performance Problems

1. Latency too high
2. Resource usage too high
3. Collateral damage / noisy neighbor problems

---
class: roomy
# Causes of Performance Problems

- Needless requests
- Too-frequent requests
- Too-slow requests
- Resource starvation or stalls

---
class: img-right, roomy

# The Performance Swiss-Army Knife

![Profile](profile.png)

A **profile** is an all-purpose tool for finding signal in the noise.

1. Group related requests together
2. Rank them by a metric
3. Look at the top items

---
class: no-footer
background-image: url(profile.png)
background-size: contain

---
class: roomy
# Finding Performance Problems

Finding needless and too-frequent requests

- Profile by frequency (throughput), ranking by `SUM(count)`
- Are they useless, e.g. driver look-before-leap `ping` queries?

--

Finding too-slow requests

- Profile by `SUM(latency)`, then look at outliers
- Profile by `P99(latency)`

---
class: img-right-full

![](unsplash-photos-OgvqXGL7XO4.jpg# opc)

# Prioritizing What You Find

How do you know whether "optimizing" a query is worth it?

Rule of thumb:
* To conserve resources / reduce collateral damage, look at % of total
* To make customers happy, look at p99 latency

---
template: footer
class: img-right-full, fit-h1

![](unsplash-photos-vWI1kTcMcDI.jpg)

# Inspecting Individual Requests

You don't learn much from aggregate data.

There's no "average" request.

You need to drill into individual examples (individual log lines or samples).

You also need to look at the *distribution* of request latencies.

---
class: fullbleed, center

![Samples](samples.png)

Aggregate metrics and averages can't tell the story this picture does.

---
class: roomy

# How To Fix A "Bad" Query

If a query is too slow, why?

- Is it slower than it *should* be?
- What is it *doing*? Working, waiting?
- There's only three possible solutions: eliminate work, reduce work, or work
  faster

---
class: roomy
# Technology Sharp Edges

Every database technology has its Kryptonite.

* MySQL: the query cache, replication, the buffer pool…
* PostgreSQL: VACUUM, connection overhead, shared buffers…
* MongoDB: missing indexes, lock contention…

---
class: roomy
# Technology-Specific Resources

Many of the "sharp edges" are special resources.

* Connection pools: fixed # of connections is a fixed resource.
* Buffer pools / caches: finite size to hold the working set.
* Etc.

Usually only a few things matter much. (But it depends.)

---
class: roomy
# Conclusions

- Monitor workload, not just resources
- Measure what matters: work getting done, customer experience
- Focus on the 7 Golden Signals (CELT + USE)
- Profile to focus, triage, and prioritize
- Drill down to individual request details
- Cover the basics of your technology's "sharp edges"

---
class: roomy
# Related: What Should I Monitor?

... and how should I do it?  

[View Baron's Velocity Talk](https://www.youtube.com/watch?v=zLjhFrUhqxg)

---
class: roomy, col-3

# Resources: Free EBooks

[![Practical Query Optimization](pqo-ebook.png)](https://www.vividcortex.com/resources/practical-query-optimization)
[![Making VividCortex Work For You](vividcortex-ebook.jpg)](https://www.vividcortex.com/resources/6-ways-to-make-vividcortex-work-for-you-download)
[![Observability](observability-ebook.jpg)](https://www.vividcortex.com/resources/architecting-highly-monitorable-apps)

---
class: col-3, roomy

# More Resources

[![SRE Book](sre-book.jpg# maxw-80pct center)](https://landing.google.com/sre/book.html)

[![Chaos Engineering](chaos-engineering.jpg# maxw-80pct center)](https://www.oreilly.com/webops-perf/free/chaos-engineering.csp)

[![DBRE Book](dbre.jpg# maxw-80pct center)](https://shop.oreilly.com/product/0636920039761.do)

---
class: roomy

# Slides and Contact Information

.qrcode.db.fr.w-40pct.ml-4[]

Slides are at https://www.xaprb.com/talks/ or you can scan the QR code.

To download/export as PDF, use Chrome's print dialog to save as PDF.

Contact: @xaprb or baron@vividcortex.com

---
class: title, no-footer, smokescreen
background-image: url(unsplash-photos-99neAF8kqhg.jpg)
# Appendix

---
class: fit-h1

# Monitoring PostgreSQL for Query Performance Issues

| Metrics | Source | What To Do |
|-----------------|-------------------|------------|
| `seq_scan`, `idx_scan` | `pg_stat_user_tables` | Check for bad queries or missing indexes
| `tup_fetched`, `tup_returned` | `pg_stat_database` | Check for missing/poor indexes
| `temp_bytes` | `pg_stat_database` | Check if query rewrites can reduce sorts / temp files; check config (less often the issue)
| lock counts by type | `pg_locks` | May indicate the need for query rewrites, indexing, and/or capacity increases

---
class: fit-h1, compact

# Monitoring PostgreSQL for Capacity / Resource Issues

| Metrics | Source | What To Do |
|-----------------|-------------------|------------|
| replication delay | `pg_last_xlog_replay_location()` `pg_last_wal_replay_lsn()` functions (varies) | Check for hardware, network, and/or capacity problems
| `checkpoints_req`, `checkpoints_timed` | `pg_stat_bgwriter` | Check for resource/capacity problems or overload
| `numbackends` | `pg_stat_database` | If it approaches `max_connections` you may have capacity problems, or optimization issues causing stalls and/or pileups of inefficient queries

---
class: fit-h1

# Monitoring PostgreSQL for VACUUM Issues

| Metrics | Source | What To Do |
|-----------------|-------------------|------------|
| `n_dead_tup` | `pg_stat_user_tables` | Growth in dead rows is a warning that `VACUUM` isn't running
|`last_vacuum`, `last_autovacuum` | `pg_stat_user_tables` | Check/confirm whether `VACUUM` is working
| `numbackends` by state | `pg_stat_activity` | Look for count in `VACUUM waiting` state: indicates it's trying but blocked
| `numbackends` by state | `pg_stat_activity` | Look for `idle in transaction` state: potentially blocking `VACUUM`

