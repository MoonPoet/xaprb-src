---
title: 'PostgreSQL Performance Theory Made Practical'
date: "2017-07-14"
url: "/talks/pgconf-philly-2017-postgresql-performance-theory-made-practical/"
event: "PGConf Local 2017"
location: "Philadelphia, PA"
site: "https://postgresconf.org/conferences/Philly2017/schedule/events"
video: ""
slides: "/slides/pgconf-philly-2017-postgresql-performance-theory-made-practical/"
image: "/slides/pgconf-philly-2017-postgresql-performance-theory-made-practical/unsplash-photos-z77FVd3_xGI.jpg"
thumbnail: "/slides/pgconf-philly-2017-postgresql-performance-theory-made-practical/thumbnail.jpg"
description: "How do I know if my PostgreSQL performance is optimized? Are we there yet?"
---
Like most people, I've Googled for advice and recommended best practices for PostgreSQL performance, but I always wondered: are we there yet? How do I know if my performance is optimized? What if I could still get better performance?
<!--more-->

Then one day I discovered Cary Millsap, the lightbulb turned on, and I found the answers. (For Oracle, but it started me on the path that led me to today.) It turns out you can (and should) answer this question easily. In fact, you are better off finding the answer before you start optimizing, not just as a check to see if you've done all you could.

In this talk I'll show you what I've learned about performance:

* What is performance, really? It's surprisingly rare to find the elusive person who knows.
* How do you measure performance? It's quite different from things like CPU utilization and cache hit ratios.
* How can you interpret the measurements and thus find, diagnose, and characterize any performance problems quickly---or prove there aren't any?

Given the time limitations this will be more how-to than practice, but it's a framework that's served me for a decade, and I've taught it to many people in turn.