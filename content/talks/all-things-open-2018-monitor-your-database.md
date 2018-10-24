---
title: 'How To Monitor Your Database'
date: "2018-10-23"
url: "/talks/all-things-open-2018-monitor-your-database/"
event: "All Things Open 2018"
location: "Raleigh Convention Center, Raleigh, NC, USA"
site: "https://allthingsopen.org/talk/how-to-monitor-your-database/"
video: "https://www.youtube.com/watch?v=KTBVGELBc04"
slides: "/slides/all-things-open-2018-monitor-your-database/"
thumbnail: "/slides/all-things-open-2018-monitor-your-database/cover.jpg"
image: "/slides/all-things-open-2018-monitor-your-database/unsplash-photos-99neAF8kqhg.jpg"
description: "Learn how to monitor a database by understanding the difference between workload and resource monitoring---and the golden signals for each"
tldr: "In this talk I explain how to monitor a database by paying attention to the golden signals of workload quality-of-service and resource performance, unifying both the internal and customer-facing definitions of performance to find problems reliably. I categorize the different types of performance problems, and show how to use profiles to solve each of them."
---
The first time I tried to monitor a database, I was overwhelmed. There were hundreds of variables to monitor, and there were lots of Nagios check scripts that had dozens of checks. I wasn't sure what alerts I should set up, so I set up too many and got a bunch of noise as a result. A couple of years later, I returned to that company and found all those alerts still in place, still spamming everyone --- but they'd just filtered every alert to the trash.
<!--more-->

In this talk, I'll share how I learned to do this better, so you won't make the same mistakes I made! Any sophisticated system like a database has many more instrumentation points than you should actively monitor. The trick is approaching it with a sound monitoring framework in mind. This talk explains the framework I've developed over many years, which breaks monitoring into a holistic approach that's easy to understand and makes it obvious what kinds of data are useful for what purposes.

You'll learn the 7 golden signals (yes, seven and not four), how workload and resource performance are complementary and necessary for a complete understanding of database health and performance, and how to monitor technology-specific "sharp edges." I'll also cover some of those for a few popular databases: MySQL, PostgreSQL, and MongoDB.
