---
title: 'Track Host, Distributed Data'
date: "2018-10-02"
url: "/talks/velocity-nyc-2018-track-host-distributed-data/"
event: "Velocity NYC 2018"
location: "New York Hilton Midtown, 1335 Avenue of the Americas, New York, New York, 10019"
site: "https://conferences.oreilly.com/velocity/vl-ny/public/schedule/topic/2708"
image: "/media/2018/09/marc-olivier-jodoin-291607-unsplash.jpg"
thumbnail: /media/2018/09/marc-olivier-jodoin-291607-unsplash.tn-500x500.jpg
credit: "https://unsplash.com/photos/NqOInJ-ttqM"
description: "How we leverage distributed data and state is today's key competitive advantage. This track explored the technical challenges and lessons learned in managing distributed state in large-scale applications."
tldr: "I was a Velocity NYC 2018 program committee member, and the track host for the Distributed Data track on Tuesday. I did not present at this conference, but I composed remarks to help weave the presentations in this track into a cohesive narrative throughout the day. What follows is a lightly edited version of my introductory remarks for the day's sessions, as well as my introductions to each session."
---
Leveraging distributed data and state is today's key competitive advantage. This track explored the technical challenges and lessons learned in managing distributed state in large-scale applications that reliably process millions of events per second. Attendees learned proven strategies and gained new insights from leading practitioners into how to handle real-time data in streams and events. 
<!--more-->

I was a [program committee member](https://conferences.oreilly.com/velocity/vl-ny/public/content/about), and the track host for the [Distributed Data](https://conferences.oreilly.com/velocity/vl-ny/public/schedule/topic/2708) track on Tuesday. I did not present at this conference, but I composed remarks to help weave the presentations in this track into a cohesive narrative throughout the day. What follows is a lightly edited version of my introductory remarks for the day's sessions, as well as introductions to each session. If you're interested in viewing slides or video of the sessions, you can purchase the video collection directly through O'Reilly Safari. Speakers may also post their slides, which are often linked from the [session pages](https://conferences.oreilly.com/velocity/vl-ny/public/schedule/topic/2708).
<!--more-->


Tuesday featured a great set of speakers and topics, lessons from practitioners on how to think about data at scale. The speakers are at the leading edge of their field, sharing stories about the challenges and solutions of pushing the limits of distributed data, and seeing what works and what doesn't. But although they're operating at the extremes today, these stories will be widespread and normal in a few years. This isn't just tech at Google scale that only Google needs, this is all of us.

I was particularly excited to host this track because I've been doing a lot of interviews with my own customers to hear about their data engineering practices, their 1- and 3-year data strategy, what trends they're seeing and how they're responding, and what they think the future will look like. I'm seeing that the trends in how our customers build distributed data behind and within their distributed systems are all related to macro changes industrywide.

As companies become increasingly data-intensive, and turn to next-generation architectures and data engineering culture and tooling to address it, we're seeing several consistent themes emerge strongly. These include:

* Polyglot persistence---the trend to compose data tiers of different technologies.
* The need to decouple systems for manageability and scalability.
* The core principles of SRE and how to apply them to stateful systems.
* Streaming data.
* Observability, particularly in the data tier where it's not custom code you can instrument.
* Observability and traceability of the _data flow itself_, not just the work the systems do.
* Different approaches to declarative rather than imperative composition of systems, for cleanliness and abstraction of underlying implementations.

We heard these themes echoed throughout the talks on Tuesday.

###  Smooth scaling: Slack's journey toward a new database

The first speaker was Ameet Kotian from Slack. Ameet has a background not only in building distributed systems that manage distributed data, but in building databases themselves. You probably know that Slack is one of the fastest-growing applications in history, which has placed extraordinary demands on their data infrastructure. You might not know that one of Slack's founders is Cal Henderson, who wrote one of the first books about how to operate MySQL at scale. It was the O'Reilly "fish book," and introduced a lot of people to topics like sharding and active-passive replication pairs on cheap commodity hardware.

That was more than ten years ago. Now we have the cloud, so why isn't database scaling just a solved problem? There are several reasons why companies like Slack still have to build scalable database infrastructure themselves and can't just use a turnkey, off-the-shelf solution. As I listened to Ameet's story, I was struck by the fact that although technology like Vitess is helping reduce the need to custom-build everything, most data-intensive applications both today and tomorrow will still need to grapple with some of the same challenges, so there's a lot we can learn from how Slack is approaching this.

### Managing multiple sources of truth in distributed applications

The next speaker was Adam Wolfe Gordon, from DigitalOcean. Adam works on the block storage team at DigitalOcean, among other things. One of the challenges of operating distributed systems at scale is that they tend to have a variety of different datastores that have to work together in some way. This is the trend that I call polyglot persistence, and it's something that all of us deal with in one form or another. It's often invisible until it causes problems, either operationally or in trying to mutate an app or architecture to grow.

A typical app has as many as ten different data storage technologies these days. If you do a quick count in your head, see what you come up with for your own app. Did you remember zookeeper? What about DNS? But more obviously, you often have file storage, database storage, and some key-value store for example.

These get introduced because you can't use a single database like Postgres for everything. You always end up with some particular data that's orders of magnitude better off in a specialized data store: "right tool, right job." The problem is you now have multiple sources of truth, and you need to coordinate them. Adam's talk dove into the specifics of coordinating these sources of truth at DigitalOcean, but the lessons apply broadly to every data-intensive app.

###  Trade-offs in resiliency: Managing the burden of data recoverability 

Kristina Bennett is a software engineer who has spent years working on data integrity across Google and is now on the customer reliability team.

Distributed data is hard. It's hard to build, it's hard to make it performant, it's hard to make it correct, it's hard to evolve over time. Why is it so hard? It's not just that databases are complicated systems, it's not just the technology itself. There are two things I've seen over and over as I've worked with data-intensive systems with lots of distributed data.

The first is that data has a kind of mass, and mass has inertia. We talk about systems as being stateful or stateless, and we know that stateless systems are a lot easier to manage. A big part of that is because stateless systems can be created and destroyed, but state follows the laws of conservation of mass and energy. It takes time and effort to create, move, and destroy data. It doesn't just happen instantaneously.

The second is time dependency. Many of our systems live in the here and now as constructed from the stream of events in time, storing an up-to-the-moment snapshot of the world, which constantly changes. But if anything goes wrong, it can be really hard to recover systems to a point in time from the past, and then merge that state into the current state, which has _continued to change_ while the recovery efforts were ongoing. It's like getting to the end of a homework problem, realizing that you dropped a negative, but you don't know where because you didn't show all of your work. Solving this problem is challenging in part because of the cost, performance, and other constraints that the size and scale of our systems impose upon us. 

###  Kafka Streams in practice: What works and what doesn't (yet)

Bart De Vylders is a data scientist at CoScale, a modern container monitoring platform that observes and ingests data from containers, apps, and the full stack at high velocity and applies advanced analysis to monitor them. He spoke about how CoScale converted part of their system to use the Kafka Streams API.

This talk was the first of two that deal with how data flows through your systems. If you're not yet using Kafka, my personal belief is that Kafka and the event-stream philosophy behind it is one of the most important developments in handling data at large scale in the last decade. In a nutshell, it helps solve two critical problems with data:

1. The time dependency created by systems like relational databases, that maintain a snapshot of data at a point in time (as I mentioned in my remarks to Kristina Bennett's talk).
2. The data _flow_ dependencies introduced by systems that connect to data where it lives, and thus implicitly become dependent on that data being in that location, as well as that data's snapshotty-ness being up to date.

###  Sell cron, buy Airflow: Modern data pipelines in finance 

Our final talk was by James Meickle, who's a site reliability engineer at Quantopian, and previously held roles at AppNeta and Harvard among other places.

My introductory remarks to the previous talk about Kafka shouldn't be taken to mean that everything must be a streaming data problem. Batch processing is still the right answer for a very large set of problems, and unless something else comes along to revolutionize how we process data, it probably always will be.

The common thread between these two talks is managing data dependencies. When I talk to folks at big companies who are using (for example) the Hadoop stack at scale, I often hear that their most acute pains aren't around things I'm familiar with myself, such as performance, reliability, or cost efficiency. No---their biggest pain and cost is often understanding, managing, and mutating the data _flow_ through their organization. This flow is usually manifested in a very large and complex set of ETL-like tasks, that are often invisibly dependent on each other. James spoke about how Apache Airflow can help structure and manage some of these moving pieces.
