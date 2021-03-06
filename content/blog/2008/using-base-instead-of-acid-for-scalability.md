---
title: Using BASE instead of ACID for scalability
date: "2008-07-23"
url: /blog/2008/07/23/using-base-instead-of-acid-for-scalability/
categories:
  - Scalability
  - Databases
---
My editor [Andy Oram](http://www.oreillynet.com/pub/au/36) recently sent me an [ACM article on BASE, a technique for improving scalability](http://acmqueue.com/modules.php?name=Content&pa=showpage&pid=540) by being willing to give up some other properties of traditional transactional systems.

It's a really good read. In many ways it is the same religion everyone who's successfully scaled a system Really Really Big has advocated. But this is different: it's a very clear article, with a great writing style that really cuts out the fat and teaches the principles without being specific to any environment or sounding egotistical.

He mentions a lot of current thinking in the field, including the CAP principle, which [Robert Hodges of Continuent](http://www.continuent.com/) first turned me onto a couple months ago. [It has been proven formally](http://citeseer.ist.psu.edu/544596.html), though I have not read the proof myself.

One of the most important concepts he advances is giving up the illusion of control. As programmers and DBAs, I think we may tend to like control too much. Foreign keys are a perfect example. I think the point here is that these things make you feel safe, but they don't really make you safe. Just as with so many things in life, recognizing our inability to really control the systems we build is key to working with their strengths---instead of trying to bind them with iron bands.

Another great point is idempotency. This is a great way to help avoid problems with MySQL replication, by the way. I'll leave the "why" as an exercise for the reader, but let me just point out that the file MySQL uses to remember its current position in replication is not synced to disk, so it will almost certainly get out of whack if MySQL dies ungracefully. (Google has solved this problem.)

A highly recommended read---worth more than most case studies about how specific companies have scaled their specific systems.


