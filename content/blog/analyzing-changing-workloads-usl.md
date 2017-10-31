---
author: Baron Schwartz
categories:
- Scalability
- Databases
tags:
- USL
- Performance
- Metrics
- Monitoring
- Analytics
- Clustering
date: 2017-04-09T20:30:04-04:00
description: "System behavior is complex and multivariate, but most visualizations of systems are one-dimensional and hide subtleties."
image: "media/2017/04/row-36-ts.png"
title: Analyzing Changing Workloads with the USL
---

Production servers often have much more dynamic, complex workload and behaviors
than you might be accustomed to seeing, because most monitoring products
aggregate system behavior into high-level global metrics, losing all the detail.
Multivariate analysis by another dimension often reveals something unexpected
about server behavior. This can prompt you to explore the system, and sometimes
leads to a deeper understanding of it. Here's one such example.

![row-36-ts](/media/2017/04/row-36-ts.png)

<!--more-->

That's a plot of MySQL database queries per second (throughput) over a one-day interval.
Nothing looks unusual about that chart, but that is only because queries per
second is one-dimensional.

While the server was working to satisfy those queries, at times it behaved very
differently.  Plotting the server's throughput versus the average concurrency
highlights the variations. (Concurrency is the average number of queries
in-process at a time.)

![row-36-scatter](/media/2017/04/row-36-scatter.png)

What is the meaning of these distinct clusters of points, seemingly two separate
workloads?
You might recognize that the axes I chose are the same as those of the
[Universal Scalability
Law](https://www.vividcortex.com/resources/universal-scalability-law/) (USL).
Applying the USL to each group of measurements will reveal that workloads, not
just servers and software, have scalability characteristics. At times, this
server's workload itself is more or less scalable.

As an exercise in visualization, I divided the clusters of points and
color-coded them, then mapped those back to the time-series plot. The result
follows:

![row-36.png](/media/2017/04/row-36.png)

It would not have been possible to guess that the less-scalable, longer-running
queries run at the highlighted times of the day. Applying the USL in this
fashion can help you understand what types of queries make your system behave
less optimally, but to do that you need more granular data---you need per-query
measurement, not global summary measurements. I'm only showing the global
summaries in this post, but with a system such as VividCortex you can drill down
into these types of details.
