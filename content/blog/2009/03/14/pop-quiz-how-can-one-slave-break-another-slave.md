---
title: "Pop quiz: how can one replica break another replica"
date: "2009-03-14"
url: /blog/2009/03/14/pop-quiz-how-can-one-slave-break-another-slave/
categories:
  - Databases
---
Suppose you have a MySQL master-slave replication setup. It is very straightforward, nothing exotic at all. Imagine that it is the simplest possible setup. Everything is fine, there is nothing wrong or misconfigured with either server.

Now you add another replica, and replication on your existing replica fails. You did not change anything on your existing replica or master. How did this happen?


