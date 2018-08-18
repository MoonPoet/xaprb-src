---
title: The difference between concurrency and parallelism
date: "2013-04-29"
url: /blog/2013/04/29/the-difference-between-concurrency-and-parallelism/
credit: "https://unsplash.com/photos/nVqNmnAWz3A"
image: "/media/2013/04/unsplash-photos-nVqNmnAWz3A.jpg"
thumbnail: /media/2013/04/unsplash-photos-nVqNmnAWz3A.tn-500x500.jpg
description: "Concurrency is about dealing with lots of things at once.  Parallelism is about doing lots of things at once."
categories:
  - Programming
---
Concurrency and parallelism are different. This is really confusing. Todd Hoff of HighScalability wrote in last week's [summary](http://highscalability.com/blog/2013/4/26/stuff-the-internet-says-on-scalability-for-april-26-2013.html) post,

> Have to say, this distinction has never made sense to me: [Concurrency is not parallelism](http://blog.golang.org/2013/01/concurrency-is-not-parallelism.html): concurrency is the composition of independently executing processes, while parallelism is the simultaneous execution of (possibly related) computations. Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once.

I think the problem is that words are hard to understand. The Go blog post is confusing because of that. Pictures are easier. Look, a single-threaded, non-parallel, **concurrent** process:

![Concurrent](/media/2013/04/concurrent.jpg)

Lots of tasks can run on the system, but *only one of them makes progress at a time*. And here's one that's both concurrent and **parallel**:

![Parallel and Concurrent](/media/2013/04/parallel-concurrent.jpg)

Hopefully that clears things up.


