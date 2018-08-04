---
title: How fast is MySQL Table Checksum?
date: "2007-05-12"
url: /blog/2007/05/12/how-fast-is-mysql-table-checksum/
categories:
  - Databases
---
A few people have asked me how fast [MySQL Table Checksum](http://code.google.com/p/maatkit/) is. As with so many other things, it depends. This article shows how long it takes to checksum real data on a production server I help manage, which might give you a rough idea of how long it'll take on your servers.

### The server and workload

This server is a replication master running MySQL 5.0.38. It is a Dell Poweredge 1800 series with dual Xeon 3.4GHz processors and 2GB RAM, with three 15K SCSI hard drives in a RAID5 configuration. It serves about 40GB of data in InnoDB tables and about 25GB in MyISAM.

I can't say too much about the workload, but I'll tell you what I can. At the time I ran these checksums, it was running many rollup and `LOAD DATA INFILE` queries on the tables I checksummed. These tend to do a lot of updates, deletes, and inserts. There are also several processes that `REPLACE` or `INSERT.. ON DUPLICATE KEY UPDATE` large parts of certain tables which are in the 2-8GB range. At the same time, there are processes running rapid-fire single-row lookups and `GROUP BY` queries against all or part of these tables. And certain other larger-than-memory tables elsewhere in the server were being updated too, probably flushing the cache.

In other words, these results are under heavy load, and not scientific or repeatable at all (there was definitely heavier load on some of the test runs than others). But it gives you an idea. Your mileage may vary.

### The results

The following table shows the number of seconds it took to checksum several heavily-used InnoDB tables with various checksum strategies: MySQL's built-in `CHECKSUM TABLE`, the ACCUM strategy with replication as an `INSERT/SELECT` (acquires share-mode locks on the whole table for replication consistency), the ACCUM strategy as a plain `SELECT` without share-mode locks, and the BIT_XOR strategy. If you wish to know more about these strategies and what they do, the MySQL Table Checksum documentation explains them in great detail.

The last column shows how long it takes to run `COUNT(*)` on the tables in question. As you can see, taking a checksum is sometimes not that much more expensive than a simple `COUNT()` on InnoDB.

|          Rows | Table Size | CHECKSUM | Replicate/ACCUM | ACCUM | BIT_XOR | COUNT |
|--------------:|-----------:|---------:|----------------:|------:|--------:|------:|
|        49,152 |        317 |          |                 |       |         |       |
|     1,589,248 |     14,472 |          |               1 |       |       1 |     1 |
|   100,843,520 |    638,144 |       15 |              12 |    13 |      25 |     8 |
|   332,316,672 |    504,652 |       52 |              56 |    43 |      77 |     4 |
| 2,167,996,416 |  4,341,475 |      258 |             303 |   335 |     541 |   151 |
|   318,636,032 |    517,406 |       31 |              10 |    45 |      92 |     1 |
|     1,064,960 |      3,105 |        1 |               1 |     1 |         |       |
|     2,818,048 |      2,369 |          |               1 |     1 |       1 |       |
