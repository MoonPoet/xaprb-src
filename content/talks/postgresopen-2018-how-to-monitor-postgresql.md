---
title: 'PostgresOpen 2018: How to Monitor PostgreSQL'
date: "2018-09-06T15:00:00-07:00"
url: "/talks/postgresopen-2018-how-to-monitor-postgresql/"
event: "PostgresOpen SV 2018"
location: "55 Cyril Magnin St, San Francisco, CA 94102"
site: "https://postgresql.us/events/pgopen2018/schedule/session/531-how-to-monitor-your-database/"
video: ""
slides: "/slides/postgresopen-2018-how-to-monitor-postgresql/"
thumbnail: "/slides/postgresopen-2018-how-to-monitor-postgresql/thumbnail.png"
image: "/slides/postgresopen-2018-how-to-monitor-postgresql/cover.jpg"
description: "Learn how to monitor PostgreSQL effectively, focusing on the right aspects of Postgres to make the server efficient, meet performance and cost goals, and empower the engineering team to develop effectively against the database."
---
The first time I tried to monitor a database, I was overwhelmed. There were hundreds of variables to monitor, and there were lots of Nagios check scripts that had dozens of checks. I wasn't sure what alerts I should set up, so I set up too many and got a bunch of noise as a result. A couple of years later, I returned to that company and found all those alerts still in place, still spamming everyone---but they'd just filtered every alert to the trash.
<!--more-->

In this talk, I'll share how I learned to do this better, so you won't make the same mistakes I made! Any sophisticated system like a database has many more instrumentation points than you should actively monitor. The trick is approaching it with a sound monitoring framework in mind. This talk explains the framework I’ve developed over many years, which breaks monitoring into a holistic approach that’s easy to understand and makes it obvious what kinds of telemetry are useful for what purposes.

You’ll learn the 7 golden signals (yes, seven and not four), how workload and resource performance are complementary and necessary for a complete understanding of database health and performance, and how to monitor the technology-specific "sharp edges."
