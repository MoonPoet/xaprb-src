---
title: "MySQL high availability comparison: service versus data"
date: "2012-03-02"
url: /blog/2012/03/02/mysql-high-availability-comparison-service-versus-data/
credit: "https://unsplash.com/photos/VL-OvBppmzI"
image: "/media/2012/03/unsplash-photos-VL-OvBppmzI.jpg"
description: "What is the priority: service availability, data availability, or both?"
categories:
  - Databases
---
When people ask me about high availability, I often suggest that it's helpful to understand whether you're most interested in service availability, data availability, or both. Of course, you want both---but if cost is an object, you may end up relaxing your requirements.

<!--more-->

The typical example of an application that needs service availability but doesn't have strong data availability requirements is something that's ad-supported. Who cares if the last few comments on funny cat photos are lost? What's important is that the users can see the photos, and the ads next to them.

On the other hand, if you're selling something, it's a big deal to lose records about orders or payments. In this case, if you can't have both kinds of availability, you might prefer downtime over data loss.

These questions are, in my opinion, a more approachable version of the CAP theorem.

Here's a quick comparison of some MySQL high availability technologies. All opinions are mine alone:

| Technology                          | Data Availability | Service Availability |
|-------------------------------------|-------------------|----------------------|
| MySQL Replication                   | Poor              | Fair                 |
| MySQL Semi-Sync Replication[^1]     | Fair              | Fair                 |
| MySQL Cluster (NDB)                 | Good              | Good                 |
| Percona XtraDB Cluster (Galera)[^2] | Good              | Good                 |
| DRBD                                | Good              | Fair                 |
| SAN Replication                     | Good              | Fair                 |

In a lot of cases the answer should really be "it depends." For example, depending on how you set it up, the amount of service downtime you'll experience during a DRBD failover can be quite long or quite short, due to factors such as the need to warm up the MySQL server before it's actually usable. Hopefully this (admittedly broad-brush) overview is helpful in understanding the possibilities.


[^1]: See http://www.mysqlperformanceblog.com/2012/01/19/how-does-semisynchronous-mysql-replication-work/
[^2]: See http://www.percona.com/software/percona-xtradb-cluster/
