---
title: Why You Need to Understand Your Working Set Size
date: "2012-03-23"
url: /blog/2012/03/23/why-you-need-to-understand-your-working-set-size/
categories:
  - Databases
---
I guest-posted on Fusion-io's blog about the database's working set size and the interplay with fast Flash storage. It's written from a MySQL point of view, but it's applicable to many types of systems.

The post is gone now, but here's the content rescued from the archives:

As a MySQL consultant with Percona, I'm very happy about the recent advances in
fast storage. Faster storage fundamentally changes things for database
administrators.

Fusion ioDrives are quite popular in the MySQL world, where they are enabling
people to run databases much faster than we're accustomed to.  The reasons are
perhaps not well understood.  A common question I hear is "Will Fusion ioDrives
(or any SSD) make my database faster?"  Answering this question is simple, once
you know why databases are slow.  Much of it hinges on something called the
working set of data, and understanding the notion of your working set size can
help you predict how performance will vary as your data grows.  The principles
are the same for many types of workloads, including non-MySQL and indeed
non-database workloads.

To understand why a database might be slow, you need to understand where it
spends its time responding to queries.  The first thing to do is measure which
resources are blocking it.  Databases need four fundamental resources to do
their work: CPU, memory, network, and storage.  Each of these resources responds
to the database in some measurable amount of time, and if a resource isn't
consuming much time, then improving its performance won't make the database much
faster.  To be precise, if a query spends only 5% of its time in network
communication, then no matter how much faster you make the network, you can't
reduce the query response time by more than 5%.

The answer to the question "Will an ioDrive make my database faster in general?"
then boils down to "Is my database significantly bound by disk I/O performance?"
This is often easy to answer in a non-scientific way by looking at some
system-wide performance metrics, such as the iowait column in the mpstat
utility.  If one or more CPUs is consistently spending a lot of time in iowait
(more than 10% or so is where I start to worry, and note that the I/O can skip
between CPUs as threads are rescheduled), and the database is the main process
running on the server, then as a Guideline, there's likely to be a problem.
There are more precise ways to measure than looking at system-wide metrics such
as this, but in many cases it's so obvious that the answer is clear. If you want
to be more precise, you can use Percona Server, which logs I/O operations and
page accesses per-query, which is extremely helpful for deep analysis.

If your database server is spending a lot of time waiting for I/O to complete,
then you have two scenarios to consider: either your database is using I/O more
than it should, or you simply need more I/O capacity.  You can reduce I/O usage
by a variety of tactics, such as adding memory, changing configuration, better
indexing, query optimization, denormalization, caching, and my perennial
favorite, not running unnecessary queries. This is a good topic for a book, such
as High Performance MySQL, which I authored.  But at some point, optimization
stops delivering more gains, and you simply need more I/O capacity than you
have.  In such cases, an ioDrive can be quite a good optimization, especially
for workloads that have a lot of random I/O, which is very slow for
spindle-based disks.  A PCIe interface to flash storage is essentially a form of
durable memory, with very low latency (orders of magnitude faster than disks)
and extremely high bandwidth.  This can make I/O bound workloads simply fly.

Now, on to working set size and memory, which I've touched but not explored.  If
your database's workload is I/O bound, it really means that it doesn't fit in
memory (otherwise it'd be bound by latency to memory, CPU usage, or network
latency).  A lot of people experience great performance initially, and then as
their data grows and stops fitting in memory, performance drops off the
proverbial cliff.  When will this happen to you?

Suppose that you allocate 50GB of memory to the InnoDB buffer pool, and you
predict that your data will grow to 100GB within a month.  When will you begin
to experience significant I/O wait?  It might not happen immediately after your
database grows past 50GB.  The total size of your data matters less than the
size of the working set.  The working set is the portion of data that is
accessed frequently. Infrequently accessed data can be left on disk, and even if
it's needed every now and then, it won't slow the server down overall.  I'll
return to this notion of overall performance in a moment.

Quantifying the working set size is probably best done as a percentile over
time.  We can define the 1-hour 99th percentile working set size as the portion
of the data to which 99% of the accesses are made over an hour, for example.
This can be a bit difficult to measure, depending on the database server.
Current versions of MySQL and InnoDB don't make it easy and transparent to
measure this, but instrumentation could be added to support it.

Even if your working set size doesn't exceed the size of your buffer pool, and
you expect most accesses to go to the buffer pool instead of disk, you might
consider much lower-latency storage to be important for purposes of consistency.
It might not be good to think about the average response time over a period of
time.  If your application demands consistently low latency, then even an
infrequent slow query might not be acceptable.  In such cases, although an
ioDrive might not make the server's average performance much higher, it might be
an important investment.  I like Peter Zaitsev's analogy for illustrating why
this is important: When you go to the doctor with a fever, you don't want a
diagnosis based on the average temperature of all patients in the hospital!

Fast access to durable storage is important for another reason: It improves not
only throughput, but latency.  This allows you to run on much larger working
sets of data, experiencing many more accesses to the durable storage per second,
without significantly impacting latency.  Suppose a query will generate 10,000
cache misses that result in random access to disk.  On spindle-based storage,
this is a very slow query, because each random access can be expected to average
about 4 milliseconds on high-end conventional disks.  On an ioDrive, with
latencies in the microseconds, the query's performance will not be impacted
dramatically.  This can turn an unacceptably slow process into an acceptable
one.

In summary, very low-latency, high-bandwidth I/O performance can improve your
database's performance and/or consistency when data when the server is
significantly I/O bound, or when all accesses must be fast, and you can use the
working set size as a tool to understand when and how this is likely to affect
you.
