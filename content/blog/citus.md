---
title: 'Citus: Scale-Out Clustering and Sharding for PostgreSQL'
date: "2019-02-14T20:02:02-05:00"
url: "/blog/citus"
description: "Citus is a scale-out sharding solution for PostgreSQL that turns a collection of nodes into a distributed analytical and transactional database."
tldr: "Citus is a scale-out sharding solution for PostgreSQL that turns a collection of nodes into a distributed analytical and transactional database. It solves problems of sharding, multi-tenancy, and distributing sophisticated analytical queries across multiple nodes in parallel."
credit: "https://unsplash.com/photos/fGvBIWgUifo"
image: "/media/2019/02/unsplash-photos-fGvBIWgUifo.jpg"
thumbnail: "/media/2019/02/unsplash-photos-fGvBIWgUifo.tn-500x500.jpg"
categories:
- Databases
tags:
- PostgreSQL
---
I wrote [yesterday](/blog/vitess/) about [Vitess](https://vitess.io), a scale-out sharding solution for MySQL.
Another similar product is [Citus](https://www.citusdata.com/), which is a scale-out sharding solution for PostgreSQL.
Similar to Vitess, Citus is successfully being used to solve problems of scale and performance that have previously required a lot of custom-built middleware.
<!--more-->

Citus solves the following problems for users:

- Sharding. Citus handles all of the sharding, so applications do not need to be shard-aware.
- Multi-tenancy. Applications built to colocate multiple customers' databases on a shared cluster---like most SaaS applications---are called multi-tenant. Sharding, scaling, resharding, rebalancing, and so on are common pain points in modern SaaS platforms, all of which Citus solves.
- Analytics. Citus is not exclusively an [analytical database](/blog/analytic-databases/), but it certainly is deployed for distributed, massively parallel analytics workloads a lot. Part of this is because Citus supports complex queries, building upon Postgres's own very robust SQL support. Citus can shard queries that do combinations of things like distributed `GROUP BY` and `JOIN` together.

A Citus cluster is composed of PostgreSQL nodes with one of two roles: coordinator or worker.
A coordinator receives queries, then decomposes them into smaller queries that execute on shards of data in the worker nodes.
The coordinator then reassembles the results and returns them to the client.

Citus is not middleware: it's an extension to Postgres that turns a collection of nodes into a clustered database.
This means that all of the query rewriting, scatter-gather MPP processing, etc happens within the PostgreSQL server process, so it can take advantage of lots of PostgreSQL's existing codebase and functionality.

Citus runs on standard, unpatched PostgreSQL servers.
The only modification is installing the extensions into the server.
This is a unique and extremely important advantage: most clustered databases that are derived from another database inevitably lag behind and get stuck on an old version of the original database, unable to keep up with the grueling workload of constantly refactoring to build on new releases.
Not so for Citus, which doesn't fork Postgres---it extends it with Postgres's own extension mechanisms.
This means that Citus is positioned to continue innovating on its own software, while continuing to benefit from the strong progress that the PostgreSQL community is delivering on a regular cadence too.

I know lots of companies that have been using Citus successfully to power challenging workloads in production for years.
At [VividCortex](https://www.vividcortex.com/) we even built support for Citus, because we have customers using it.

Citus is open-source, backed by a company called Citus Data, and commercially successful with a fast-growing customer base.
I've known key people at Citus for several years and have had a chance to interact with them many times.
Citus was recently acquired by Microsoft, whose cloud database offerings suggest obvious strategic possibilities for the future, and I believe Citus is positioned well to accelerate on their vision within Microsoft.
I'm excited to see how adoption of Citus can grow with the go-to-market muscle of Microsoft.
Citus is certainly worth evaluating if you like and trust PostgreSQL and have problems that can benefit from sharding, horizontal scale-out, and multi-tenant support among other things.
