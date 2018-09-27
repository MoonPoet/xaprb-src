---
title: 'System Performance Theory'
date: "2018-10-03"
url: "/talks/mongodb-tech-talks-2018-performance-theory/"
event: "MongoDB Tech Talks 2018"
video: ""
slides: "/slides/mongodb-tech-talks-2018-performance-theory/"
image: "/slides/mongodb-tech-talks-2018-performance-theory/unsplash-photos-YyWu19ab4_M.jpg"
description: "In this internal MongoDB talk, Baron Schwartz covers the basics of performance theory and how it can help you understand and build high-performance systems."
---
_Note: this event isn't open to the public._
In college Henrik Ingo got to do an exercise on queueing theory: how to optimize the number of cash registers and bathroom stalls in a McDonalds restaurant.
After graduating he never worked in a McDonalds and forgot all about this.
It was only through some writings of Baron Schwartz that he realized that queueing theory also applies directly to database performance (and systems performance).
So to start a series of internal talks at MongoDB about performance, there was no better way than to have Baron give an introduction to Queueing theory, Amdahl's law and the Universal Scalability Law.
<!--more-->


Baron Schwartz became known as a database performance expert when working at Percona, where he was one of their first employees.
In addition to numerous conference talks and blogs, he is also co-author of the 2nd to 3rd editions of the book High Performance MySQL.
Over time his methodology developed into a more data and statistics driven approach.
In one publication he reviewed and categorized the root causes for database outages in all Percona support incidents over one year.
Many of his methods and ideas were added to and popularized in the Percona Toolkit, which is the mtools of the MySQL world.
The culmination of this path was the founding of his own company VividCortex, which provides a database monitoring service for open source databases (including MongoDB).
In addition to standard performance monitoring and query analyzer dashboards, VividCortex includes fault detection algorithms based on---wait for it---queueing theory.
