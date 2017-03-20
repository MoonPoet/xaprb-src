---
title: Defining Moments in Database History
date: '2017-03-19T20:59:17+00:00'
author: Baron Schwartz
categories:
- Databases
description: ''
image: ''
draft: true

---
I've been privileged to be intimately involved with one defining set of technology shifts in the mid-2000s, which ultimately created both a new industry-defining set of technologies and the impetus for the emergence of a contender. I'm referring to the rise of the LAMP stack. I've been reflecting recently on what perhaps were key factors in that phenomenon and what's happened since then, indeed, what's happening now.

First, what was it about the LAMP stack, anyway? All of the ingredients in that stack were interesting and signaled tectonic shifts (or were the result of them), but I'm particularly interested in MySQL, the database that came to power much of the Internet as we know it today. MySQL was remarkable for many reasons, although it's easy to forget them in hindsight. It wasn't the first or perhaps even the best open source database, but it was [just enough better](/blog/just-enough-better) that it became the best for the situation at hand. And ultimately it became a commercial success that even in hindsight seems improbable.

I've thought of many necessary conditions for MySQL to flourish in 2000-2010. The big question is which combination of those conditions were sufficient. I am not certain of the answer, but I'm certain the answer is plural.

And yet, partially because of its enormous popularity, MySQL helped spur the rise of NoSQL in 2008-2009. These databases sought to define a new moment in database history: one in which legacy relational technology was finally replaced by an utterly new generation. If you were around at the time, you might remember how vehemently people decried relational, joins, SQL, ACID, etc. It was not sufficient to lambaste a technology or implementation: you needed to have some highly-fermented bile against the concepts and foundations themselves or you weren't really a NoSQL believer.

Where do we find ourselves today? Relational implementations rapidly improved (enter NewSQL), and NoSQL was backronymed to mean "not only SQL" instead of being a rejection of SQL. Many NoSQL databases today sport SQL-like languages. The obvious question has to be addressed: was it just a flare-up? Is there any need for next-generation data storage and processing? Or is good old relational going to improve and obviate every next-gen data technology anyway?

I believe strongly that the answer is no. I see a few current trends and I'm sure that at least some of them will eventually become something enduring in some form.

### Next-Generation Databases

Relational, and SQL, are painful. SQL is a [Yoda language](/blog/2013/02/01/if-yoda-you-were-sql-you-would-invent/) that causes a lot of problems. It obscures intent, introduces illogical logic such as tri-valued truth, prompts huge books from Celko and Date about the small subset of how to do it right, and creates endless opportunities for the server to do things you didn't intend and cause performance disasters.

Not least, SQL is an open sore in a program. Think about it: you've got this nice strictly-typed language with all sorts of compiler guarantees, and in the middle of it is a meaningless string blob that isn't compiled, syntax-checked, or type-checked. It is bound to a foreign source of data through an API that isn't knowable to the program or compiler, and may change without warning. It's the programming equivalent of "I give up, random potentially correct garbage of dubious meaning goes here." It's the equivalent of an ugly CDATA in an XML document.

This should present _significant_ opportunities for improvement. One can imagine a number of sensible first steps to take: find a way for the program and the database to use the same language and toolset; design a database query language that works similarly to a programming language; memory-map the database into the program; and so on. Problems begin immediately, and indeed the relational model was created to solve many of those issues---issues that have been happily and naively reinvented ever since. Those who are ignorant of history are doomed to repeat it.

But into this fray waded a brave new generation in 2009, with map-reduce databases, key-value databases, Javascript databases, and so forth. All with some good ideas, all going in some productive direction, all with at least some aspects that could be legitimately criticized.

A while ago I [predicted](/blog/2013/01/10/bold-predictions-on-which-nosql-databases-will-survive/) that MongoDB, Redis, and Riak would survive in a meaningful way. Of these, Riak seems to have been sidelined, but MongoDB and Redis are going strong.

Which other NoSQL databases have had impact on par with those two? Perhaps Cassandra, and arguably Neo4J, but both of those are less mainstream. MongoDB and Redis are ubiquitous.

Why? It's instructive to look at the problems they solve. Redis starts with a simple conceptual foundation: label a piece of data, then you can use the label to fetch and manipulate the data. The data can be richly structured in ways that are familiar to programmers, and the operations you can perform on these structures are a Swiss Army knife of building blocks for applications. The types of things that otherwise force you to write boilerplate code or build frameworks.

MongoDB also starts with a simple concept, essentially that databases should store nested, structured "documents" that can map directly to the structs or objects you use in your programming language. And on top of this, MongoDB adds another power tool: the programming language you use to query the database is the ubiquitous JavaScript, arguably the most popular and flexible programming language today. There's much more, too, such as built-in scalability so you don't have to build "sharding" into your app (anyone who's done that knows that you're actually building a new custom database in your app code).

Many of the NoSQL databases that sprang up like weeds in 2009 didn't solve these types of problems in these kinds of ways. Perhaps this is what makes these two databases endure. I don't know, but I am sure it's what makes them a joy to use. And for better or for worse, from where I sit they seem to be the most viable answer to the proposition "a more modern database is a practical and useful thing to create."

### Time Series Databases

Another area where a category has emerged is time series databases. These databases store facts with timestamps, and treat the time as a native and essential part of the data model. They allow you to do time-based analysis. Not only that, they really view temporal queries as central. Many of them even make time a mandatory dimension of any query.

I wrote extensively about time series databases previously. For example, I argued that [the world is time series](/blog/2014/03/02/time-series-databases-influxdb/) and I shared my [requirements for a time series database](/blog/2014/06/08/time-series-database-requirements/) a bit later. (That latter article is not something I agree with fully today).

InfluxDB remains on a very steep growth trajectory as it seeks to define what it means for a database to be natively time oriented, and answer the question of whether that is _enough_ for a database or if there'll be a "last mile problem" that will make people want some of the stuff they can get from other types of databases too. Defining the boundaries of a database's functionality is hard. But InfluxDB seems to be doing an admirable job of it.

An alternative is ElasticSearch, which offers time series functionality in some ways, but not as the sole and central concept. It's really a distributed search engine that knows about time. This quite naturally and properly raises the question: if you're going to use a non-time-series database that knows about time, why use a search engine? Why not a relational database that has time series functionality?

There are many, many others. Time will tell what survives and what set of problems is worth solving and doesn't leave something unsatisfied. I'd bet on InfluxDB at this point, personally. But one thing is certain, in my mind at least: time series is important enough that first-class time series databases are necessary and worthwhile. It's not enough to foist this use case onto another "yeah we do that too" database.

### Stream-Oriented Databases

The final category of data technologies I think is going to end up defining a standalone category is stream-oriented, pub-sub, queueing, or messaging---choose your terminology. These databases are essentially logs or buses (and some of them have names that indicate this). Instead of permanently storing the data and letting you retrieve and mutate it, the concept is (mas o menos) insertion, immutable storage in order, and later reading it out again (potentially multiple times, potentially deleting on retrieval).

Why would you want this? It's not obvious at first glance, but this "river of data, from which everything in the enterprise can drink" architecture is at once enormously powerful and enormously virtuous. It enables you to do things you otherwise would have to go through all kinds of gyrations to accomplish, while simultaneously simplifying things greatly.

The typical enterprise data architecture ends up as a nightmare spaghetti tangle after not very long. Data flows through the architecture in weird ways that become difficult to understand and manage. And performance, reliability, and guarantees about processing order and so on are prime motivators for a lot of complexity that you can solve with a queue or streaming database.

There are a lot of concepts related to these databases and their interplay with other types of database; too many to list here. I'll just say that it's a fundamental mindset shift, similar to the type of epiphany you get the first time you really understand purely functional programming. For example, you suddenly want to abolish replication forevermore, and you never want anything to poll or batch process again, ever.

Lots of technologies such as Spark are emerging around these areas. But in my view, Apache Kafka is the undisputed game-changer. It's truly a watershed technology. Rather than try to explain why, I'll just point you to the commercial company behind Kafka, [Confluent](https://www.confluent.io/). Read their materials. I know many of the people working there; they are genuine, smart, and it's not marketing fluff. You can drink from their well. Deeply.

### Conclusions

If anyone thought that NoSQL was just a flare-up and it's died down now, they were wrong. NoSQL did flare up, and we did get a lot of non-database folks trying to write databases before learning what they were. But the pains and many of the solutions are real. A key determinant of what'll survive and what'll be lost to history is going to be [product-market fit](/blog/product-market-fit/). In my opinion, three important areas where markets aren't being satisfied by relational technologies are programmer sensibilities, time series, and streaming data. Time will tell if I'm right.

[Pic Credit](https://pixabay.com/en/crossroads-confusion-dilemma-1580168/)