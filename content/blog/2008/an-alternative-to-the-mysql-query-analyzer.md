---
title: An alternative to the MySQL Query Analyzer
date: "2008-11-20"
url: /blog/2008/11/20/an-alternative-to-the-mysql-query-analyzer/
categories:
  - Databases
  - Open Source
---
MySQL just released their new [MySQL Query Analyzer](http://www.mysql.com/trials/enterprise) (link to a trial), and recently wrote up [an interview with Mark Matthews about it](http://dev.mysql.com/tech-resources/interviews/interview_mark_matthews.html). If you haven't read that article, go ahead and do it. I have not used this software, but I fully believe its functionality is quite nice.

> [VividCortex](https://vividcortex.com/) is the startup I founded in 2012. It's the easiest way to monitor what
> your servers are doing in production and I consider it far superior to Cacti. VividCortex offers [MySQL performance
> monitoring](https://vividcortex.com/monitoring/mysql/) and [PostgreSQL
> performance management](https://vividcortex.com/monitoring/postgres/) among many
> other features.

But there is at least one alternative, which has been available for a long time. That is the [Percona patch-set](http://www.percona.com/percona-lab.html), plus analysis tools such as [mysqlsla](http://hackmysql.com/mysqlsla) or [Maatkit's query analysis tools](http://www.maatkit.org/). This is a compelling alternative, if you can live without a point-and-click interface.

Percona's patches put the metrics-gathering where it should be: in the server. That's why Percona's builds are able to measure a lot of statistics that a Proxy-based solution can't capture. This information is not possible to get outside of the server. For example, you cannot use the MySQL Query Analyzer to measure the I/O caused by a query. Externally to the server, about all you can do is time queries and measure their size. Percona's patches have no such limitations; they measure and expose an ever-richening set of meta-data about queries.

Guessing is not enough. You need to be able to measure what your queries are doing. The MySQL Query Analyzer's way to know which queries cause I/O usage is to "...graph I/O usage on the system as a whole, and when you see a spike in I/O you can see what queries were running at the time." So you're essentially reduced to lining up graphs, picking time intervals, running EXPLAIN and guessing. If you use Percona's patches, you can measure directly which queries cause I/O.

The article claims that "...With MySQL Query Analyzer we are watching from the sideline and capturing things that the MySQL server does not give you," but the irony is that since Proxy-based solutions are outside the MySQL server, they actually can't measure things the server already exposes internally. While would be possible to do so by running SHOW STATUS after each query, ask [Mark Callaghan](http://mysqlha.blogspot.com/) what he thinks of that idea.

If you've ever administered Microsoft SQL Server, you know what kind of insight you can get into a running server. Other databases have similar functionality. MySQL has decided not to build metrics into the server, and is now trying to build it outside the server---an effort that's ultimately doomed to failure because the information is only available inside.

Let's see a feature comparison. I've chosen features that were promoted in the tech article linked above, plus key features I know are in the Percona patches:

| &nbsp;                                                                                   | Percona patches&nbsp;&nbsp;           | MySQL Query Analyzer                  |
| ---------------------------------------------------------------------------------------- | ------------------------------------- | ------------------------------------- |
| Has a point-and-click interface                                                          |               | &check; |
| Freely available                                                                         | &check; |               |
| License                                                                                  | Free (GPL)                            | Proprietary                           |
| Integrated into the server                                                               | &check; |               |
| Requires a separate server                                                               |               | &check; |
| Requires an agent on monitored servers                                                   |               | &check; |
| Requires MySQL proxy with extra scripts loaded                                           |               | &check; |
| Relays queries through a single-threaded proxy                                           |               | &check; |
| Requires changing where your application connects |               | &check; |
| Captures total execution time of all queries                                             | &check; | &check; |
| Measures query execution time in microseconds                                            | &check; | &check; |
| Permits sampling of only a fraction of sessions                                          | &check; |               |
| Abstracts queries into similar forms                                                     | &check; | &check; |
| Aggregates similar queries together                                                      | &check; | &check; |
| Aggregates across multiple servers                                                       |               | &check; |
| Automatically generates EXPLAIN plans                                                    | &check; | &check; |
| Filters by query type (SELECT, UPDATE, etc)                                              | &check; | &check; |
| Calculates statistical metrics (min, max, 95th percentile etc)                           | &check; | &check; |
| Measures per-query execution time                                                        | &check; | &check; |
| Measures per-query execution count                                                       | &check; | &check; |
| Measures per-query row counts                                                            | &check; | &check; |
| Measures per-query update counts                                                         | &check; | &check; |
| Measures per-query result set sizes                                                      |               | &check; |
| Measures per-query table lock waits                                                      | &check; |               |
| Measures per-query InnoDB lock waits                                                     | &check; |               |
| Measures per-query InnoDB read operations                                                | &check; |               |
| Measures per-query InnoDB write operations                                               | &check; |               |
| Measures per-query InnoDB I/O wait                                                       | &check; |               |
| Measures per-query InnoDB queue waits                                                    | &check; |               |
| Measures per-query InnoDB pages touched                                                  | &check; |               |
| Measures per-query filesorts caused                                                      | &check; |               |
| Measures per-query temp tables caused                                                    | &check; |               |
| Measures per-query temp tables on disk                                                   | &check; |               |
| Measures per-query table usage                                                           | &check; |               |
| Measures per-query index usage                                                           | &check; |               |
| Measures per-query query cache hits                                                      | &check; |               |
| Measures per-query full scans                                                            | &check; |               |
| Measures per-query full joins                                                            | &check; |               |
| Measures per-query sort merge passes                                                     | &check; |               |
| Measures queries executed by replica SQL thread     | &check; |               |
| Measures replica SQL thread utilization[^1]                                                    | &check; |               |
| Provides per-database stats                                                              | &check; | &check; |
| Provides per-table stats[^2]                          | &check; |               |
| Provides per-index stats                                                                 | &check; |               |
| Provides per-user stats                                                                  | &check; | &check; |
| Is deployed and tested in large social network sites                                     | &check; | ?                                     |
| Is demonstrated stable by years of real-world testing                                    | &check; |               |
| Requires understanding MySQL source code                                                 |               |               |

Stay tuned. More is coming.

[^1]: The replica SQL thread's utilization is the amount of time it stays busy. This is different from measuring the queries the replica SQL thread executes. The Percona patches can do both; MySQL Query Analyzer does neither, since replication doesn't go through a proxy. Both are extremely useful in [predicting and measuring a replication replica's workload](http://www.mysqlperformanceblog.com/2008/10/08/three-ways-to-know-when-a-mysql-slave-is-about-to-start-lagging/).
[^2]: Aggregating queries and then filtering by table isn't the same thing as measuring how many Handler operations are performed against the table. The Percona patches include SHOW `TABLE_STATISTICS`, SHOW `INDEX_STATISTICS`, and SHOW `USER_STATISTICS`, which are functionality ported from Google's patches. These let you know exactly how much work is done. This is what I call per-object statistics.
