---
title: "How To Read Linux Iostat's Output And Interpret System Performance"
date: "2010-01-09"
url: /blog/2010/01/09/how-linux-iostat-computes-its-results/
image: "media/2010/01/layers.jpg"
credit: https://www.flickr.com/photos/doug88888/3139395660
description: "How to really understand the Linux iostat output, and how it computes metrics such as await, queue size, and utilization."
categories:
  - Databases
  - Open Source
  - Operations
  - Monitoring
tags:
  - PostgreSQL
---

The primary tool for inspecting Linux disk performance is iostat. The output
includes many important statistics, but they're difficult for beginners to
understand. This article explains what they mean and how they're calculated.

![Layers](/media/2010/01/layers.jpg)

<!--more-->

I usually run iostat like this:

    iostat -dx 5

This makes iostat print an extended disk device report every 5 seconds forever
until you cancel it. The first report will be over the time interval since the
system was booted; subsequent reports will be for just that 5-second interval.

The input data comes from [/proc/diskstats](http://www.mjmwired.net/kernel/Documentation/iostats.txt), which contains a number of fields that, when interpreted correctly, reveal the inner workings of disk (block) devices.

The order and location of fields in /proc/diskstats varies between kernels, but
since 2.6, there's at least the following for both reads and writes:

- the number of operations completed
- the number of operations merged because they were adjacent
- the number of sectors read/written
- the number of milliseconds spent reading/writing

There's also the following fields, which are *not* available separately for reads and writes:

- the number of operations in progress as of the instant of reading /proc/diskstats
- the total number of milliseconds during which I/Os were in progress
- the weighted number of milliseconds spent doing I/Os

With the exception of operations in progress, all of the fields are
cumulative counters that increase over time. The last field, the weighted number
of milliseconds spent doing I/O operations, is special because it includes
operations currently in-flight; it is basically the sum of the time spent for
every operation, plus those not yet completed:

> Field 11 -- weighted # of milliseconds spent doing I/Os This field is incremented at each I/O start, I/O completion, I/O merge, or read of these stats by the number of I/Os in progress (field 9) times the number of milliseconds spent doing I/O since the last update of this field. This can provide an easy measure of both I/O completion time and the backlog that may be accumulating. 

To interpret the output of iostat, you need to know a little performance
terminology:

- **Throughput** is the rate at which a system completes operations, in units of
  *operations per second*.
- **Concurrency** is the number of operations in progress at a time, either as
  an instantaneous measure or an average over an interval of time.
- **Latency** is the total time operations require to complete, from the
  perspective of the user or system who requested them. It is in units of
  *seconds per operation.* Latency is the *round-trip*
  time between making the request and getting the response. It is also called
  *residence time* because it's how long the request was resident in the system
  that was doing the work. Latency is composed of two parts, as follows...
- **Queue time** is the first component of latency: the time the request spends
  waiting, queued for service, after the request is made but before the work begins.
  It is sometimes called "wait" time, however, there's ambiguity in this term in
  the context of iostat, so beware.
- **Service time** is the second component of latency, after the device accepts
  a request from the queue and does the actual work.
- **Utilization** is the portion of time during which the device is busy
  servicing requests. It is a fraction from 0 to 1, usually expressed as a
  percentage.

The iostat tool works by capturing a snapshot of /proc/diskstats and all its fields,
then waiting and grabbing another snapshot. It subtracts the two snapshots and
does some computations with the differences.

Here's how iostat computes the output fields, and what each of them means:

*   There are a number of throughput metrics: rrqm/s, wrqm/s, r/s, w/s, rsec/s, and wsec/s. These are per-second metrics whose names indicate what they mean (read requests merged per second, and so on). These are computed by simply dividing the delta in the fields from the file by the elapsed time during the interval.
*   avgrq-sz is the number of sectors divided by the number of I/O operations.
*   avgqu-sz is average concurrency overall during the interval. It is computed from the last field in the file---the weighted number of milliseconds spent doing I/Os---divided by the milliseconds elapsed. As per Little's Law, the units cancel out and you just get the average number of operations in progress during the time period, which is a good measure of load or backlog. The name, short for "average queue size", is misleading. This value does not show how many operations were queued but not yet being serviced---it shows how many were *either* in the queue waiting, *or* being serviced. The exact wording of the kernel documentation is "...as requests are given to appropriate struct request\_queue and decremented as they finish."
*   %util is utilization: the total time during which I/Os were in progress, divided by the sampling interval. This tells you how much of the time the device was busy, but it doesn't really tell you whether it's reaching its limit of throughput, because the device could be backed by many disks and hence capable of multiple I/O operations simultaneously.
*   await is average latency: the total time for all I/O operations summed, divided by the number of I/O operations completed. It includes queue wait and service time. It's important to note that "await" stands for "average wait," but this is not what a performance engineer might understand "wait" to mean. A performance engineer might think wait is queue time; here it's total latency.
*   svctm is the average service time. It is the most confusing to derive, because to understand that it's valid you need to know Little's Law and the Utilization Law. It is the utilization divided by the throughput. You saw utilization above; the throughput is the number of I/O operations in the time interval.

Although the computations and their results seem both simple and cryptic, it turns out that you can derive a lot of information from the relationship between these various numbers.

I've shown how the numbers are computed, but now you might ask, why are those things true? Why are those the correct relationships to use when computing these metrics?

The answer lies in several interrelated theories and properties:

1. Queueing Theory. This is the study of "customers" arriving at "servers" to be
	serviced. In the disk's case, the customers are I/O requests, and the disks
	are the servers. Queueing theory explains the relationship between the length
	of the queue, the time spent waiting in the queue, and the system's
	utilization.
2. Little's Law, which 
	states that in a stable system, where all requests eventually complete, then
	over the long run, L = &lambda;W, or as I prefer to state it, N=XR. The number of
	requests (customers) resident in the system (whether queued or in service) is
	L or N. It is equal to the arrival rate &lambda; (or throughput X) times the
	residence time W (or response time R).
3. The utilization law, &rho; = &lambda;S. This states that utilization is
	throughput times service time.

If you'd like to learn more about queueing theory and these relationships, I
encourage you to do so. I wrote a free [introduction to queueing
theory](https://www.vividcortex.com/resources/queueing-theory/).
I also wrote a replacement for iostat, called
[pt-diskstats](https://www.percona.com/doc/percona-toolkit/LATEST/pt-diskstats.html),
which exposes additional insight into disk device behavior and performance;
iostat computes a lot of valuable metrics, but there's more that it doesn't
compute.


