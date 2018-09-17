---
title: 'Analytical Databases'
date: "2018-09-15T19:45:59-04:00"
url: "/blog/analytic-databases"
description: "A list of analytical or OLAP databases: designed for mining insights from extremely large datasets."
credit: "https://unsplash.com/photos/eH_ftJYhaTY"
image: "/media/2018/09/unsplash-photos-eH_ftJYhaTY.jpg"
thumbnail: "/media/2018/09/unsplash-photos-eH_ftJYhaTY.tn-500x500.jpg"
categories:
- Databases
---
For various reasons, I've become interested in analytical databases.
These are traditionally called OLAP (online analytics processing) and are designed to extract insights from very large datasets, often with expectations of long response times (hours).
More recently, though, various databases capable of running relatively interactive queries over large datasets have emerged.
This post is more-or-less a list of analytic databases, with somewhat of a taxonomy added.
<!--more-->

As with any list of this type, categories are inexact, and I'm sure this is only partial.
I'm making some value judgments about what to mention and what to omit; this is mostly guided by my intuition.
However, if you think I should list something I've left out, please let me know.
I may have simply failed to think of it, so omission shouldn't be considered a negative opinion!
I welcome your feedback and suggestions.

### Traditional Analytics Databases

These are the canonical names in the previous generation of big data analytics, and are still widely deployed and in many cases regarded as the gold standard in various ways.

* [HP Vertica](https://www.vertica.com/)
* [Pivotal Greenplum](https://pivotal.io/pivotal-greenplum)
* [Teradata](https://www.teradata.com/)
* [Paraccel / Actian](https://www.actian.com/)
* [Netezza](https://www.ibm.com/analytics/netezza)
* [SAP IQ](https://www.sap.com/products/sybase-iq-big-data-management.html)

### Open-Source Analytics Databases

These databases aren't easy to group into other categories for one reason or another, but all are open source.
(Note that many of the databases in other categories are also open source.)

* [MariaDB ColumnStore](https://mariadb.com/products/technology/columnstore) (formerly InfiniDB)
* [Clickhouse](https://clickhouse.yandex/)
* [LocustDB](https://github.com/cswinter/LocustDB)

### GPU-Accelerated Databases

At the vanguard of hardware-accelerated databases, GPUs are being used to speed up analytical workloads.

* [MapD](https://www.mapd.com/platform/)
* [SQream](https://sqream.com/)
* [BrytlytDB](https://www.brytlyt.com/)
* [BlazingDB](https://blazingdb.com/)

### Hadoop / Big Data Ecosystem

The “big data” ecosystem includes a number of databases designed for analytics and BI workloads. At their simplest, these can be seen as access layers over massive datasets stored in distributed filesystems, especially columnar storage layouts such as Parquet and Arrow. Some, however, are more distant from the raw bytes, such as Presto, which is more of a query engine than a database.

* [HBase](https://hbase.apache.org/)
* [Presto](https://prestodb.io/)
* [Kudu](https://kudu.apache.org/)
* [Druid](http://druid.io/)
* [Spark](https://spark.apache.org/)
* [Amazon Athena](https://aws.amazon.com/athena/)
* [Parquet](https://parquet.apache.org/)
* [Arrow](https://arrow.apache.org/)
* [Actian Vector](https://www.actian.com/)

### NoSQL and Multi-Model Analytics Databases

Most NoSQL databases don’t really fall into the analytics category, but some are used for analytics purposes regardless.

* [MongoDB](https://www.mongodb.com/)
* [ScyllaDB](https://www.scylladb.com/)
* [ElasticSearch](https://www.elastic.co/)
* [Cassandra](https://cassandra.apache.org/)
* [Couchbase](https://www.couchbase.com/)
* [Aerospike](https://www.aerospike.com/)
* [FaunaDB](https://fauna.com/)
* [CrateDB](https://crate.io/)

### Time Series Databases

Time series is often a simpler case of full-fledged analytics, with some limitations on the complexity of queries and use cases.

* [InfluxDB](https://www.influxdata.com/)
* [TimescaleDB](https://www.timescale.com/)
* [IRONdb](https://www.irondb.io/)
* [Prometheus](https://prometheus.io/)
* [kdb+](https://kx.com/)

### Cloud Analytics Databases

* [Google BigQuery](https://cloud.google.com/bigquery/)
* [Amazon Redshift](https://aws.amazon.com/redshift/)
* [Azure SQL Data Warehouse](https://azure.microsoft.com/en-us/services/sql-data-warehouse/)
* [Snowflake](https://www.snowflake.com/)
* [SAP HANA](https://www.sap.com/products/hana.html)
* [New Relic Insights](https://newrelic.com/insights)

### Custom-Built Analytics and Event Databases

Many analytics and security companies, finding nothing existing that was well suited for their purposes, have built at least part of their own analytics platforms in-house. Here are some that I’m aware of to varying levels of detail.

* [Honeycomb](https://www.honeycomb.io/)
* [Kentik](https://www.kentik.com/)
* [Segment](https://segment.com/)
* [Heap](https://heapanalytics.com/)
* [Interana](https://www.interana.com)
* [Mode](https://modeanalytics.com/)
* [Facebook SCUBA](https://research.fb.com/publications/scuba-diving-into-data-at-facebook/)
* [VividCortex](https://www.vividcortex.com/)

### NewSQL Databases

Many so-called NewSQL databases are more transactional or OLTP than analytical, or otherwise blur the lines of this article, but I list them here nonetheless.

* [TiDB](https://www.pingcap.com/en/)
* [CitusDB](https://www.citusdata.com/)
* [MemSQL](https://www.memsql.com/)
* [CockroachDB](https://www.cockroachlabs.com/)
* [Clustrix](https://www.clustrix.com/)
* [NuoDB](http://www.nuodb.com/)
* [VoltDB](https://www.voltdb.com/)
* [MySQL NDB Cluster](https://www.mysql.com/products/cluster/)

### Other

* [Vitess](https://vitess.io/)
* [MonetDB](https://www.monetdb.org/)
* ScaleDB
* DeepDB
* [Infobright](http://www.ignitetech.com/solutions/information-technology/infobrightdb)

### In-Memory Data Grids

TODO
