---
title: 'Vitess: Scaling MySQL Through Distributed Sharding'
date: "2019-02-13T20:19:24-08:00"
url: "/blog/vitess"
description: "Vitess is a sharding and scaling solution for MySQL that can make thousands of databases appear to be a single monolithic database."
tldr: "Vitess is a sharding and scaling solution for MySQL that can make thousands of databases appear to be a single monolithic database. It solves three major problems for its target users: sharding, Kubernetes deployment, and protecting the database from overload."
credit: "https://unsplash.com/photos/-gS54SWrHMg"
image: "/media/2019/02/unsplash-photos--gS54SWrHMg.jpg"
thumbnail: "/media/2019/02/unsplash-photos--gS54SWrHMg.tn-500x500.jpg"
categories:
- Databases
---
[Vitess](https://vitess.io/) is a sharding and scaling solution for MySQL that can make thousands of databases appear to be a single monolithic database.
Vitess is interesting, and promising, in a number of ways.
It's addressing an extremely hard set of problems that's been tried many times before with mixed results, but evidence points to Vitess succeeding where others have thus far failed.
<!--more-->

Vitess solves three fundamental, hard problems for its target user base:

- Sharding. Sharding is essential for scaling traditional relational databases that weren't built natively to operate as a distributed cluster of many nodes forming a single database. Every large-scale MySQL deployment---and there are thousands---uses sharding, bar none.
- Kubernetes deployment. You can't just run a database like MySQL on Kubernetes without a robust suite of operational tooling for high availability. MySQL just wasn't built to run on ephemeral machines. Vitess makes it possible to treat a MySQL node as disposable.
- Guardrails. MySQL, like most databases, is pretty easy for a badly behaved application or user to take down completely. A single runaway query or resource hog can create priority inversions and starve all the useful work. Vitess prevents this.

Vitess can be described as "sharding and HA middleware," but really it's a new distributed database that is built on the shoulders of giants.
Individual nodes run MySQL and leverage its capabilities as a leaf storage node.
The resulting database automatically shards a single application's data across many nodes, and automatically distributes a single query to run in a scatter-gather pattern in parallel across those nodes too.
It is more designed for transactional workloads, than analytics workloads.

Vitess is successfully used in production in many prominent high-scale use cases, and its userbase and community are exploding. I'm aware of a lot of companies actively migrating to it or evaluating it. It's definitely worth looking at if you're running a custom-sharded platform on MySQL.
