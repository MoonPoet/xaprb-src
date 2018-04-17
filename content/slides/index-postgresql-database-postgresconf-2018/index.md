---
draft: true
title: "How To Index Your Database"
date: "2018-04-16T13:32:30-04:00"
url: "/slides/index-postgresql-database-postgresconf-2018/"
image: "/slides/index-postgresql-database-postgresconf-2018/cover.jpg"
description: "Do you know what database indexes are and how they work? Do they seem hard to understand? They don't have to be."
ratio: "16:9"
theme: "monobloc"
---
layout: true
<div class="remark-slide-number" style="left: 20px; right: unset">@xaprb</div>

---
class: title
background-image: url(cover.jpg)
background-size: cover

.smokescreen[
# How To Index Your Database
## Baron Schwartz &bullet; PostgresConf 2018 
]

---
class: img-right
# Logistics and Stuff

.col[
- Slides are at https://www.xaprb.com/talks/
- Ask questions anytime
- Write me at @xaprb or baron@vividcortex.com
]

.rc[
![Baron Schwartz](headshot.jpg)
]

---
# Introduction and Agenda

The purpose of this talk is to organize and understand the principles
of database indexing.

- What are indexes?
- What kinds are there?
- How do they work?
- What are the three purposes of an index?
- What are the three ways a query plan can use an index?
- How can you design the best indexes, generally speaking?

---
class: title
background-image: url(sanwal-deen-93466-unsplash.jpg)
background-size: cover

.smokescreen[
# What Are Indexes?
]

---
# Indexes Help Find Data

Indexes are fast-lookup structures for the data in a table.

They essentially do two things with the data:

1. Maintain a **search-optimized copy** of the data.
--

2. Point to the data's **original location.**

---
# Resources and References

- [RUM Conjecture](http://daslab.seas.harvard.edu/rum-conjecture/)

---
class: two-column
# Slides and Contact Information

.col[
Slides are at https://www.xaprb.com/talks/ or you can scan the QR code.

Contact:

]

.col[
<div id="qrcode"></div>
]
