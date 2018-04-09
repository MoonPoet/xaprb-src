---
title: MySQL 6.2 is GA, but 5.1 is RC and 6.0 is alpha
date: "2008-05-23"
url: /blog/2008/05/23/mysql-62-is-ga-but-51-is-rc-and-60-is-alpha/
categories:
  - Commentary
  - Databases
---
MySQL's version numbering is getting harder and harder to understand. In fact, it's getting surreal.

Let me state up front that there's probably a lot I don't know here. But if I don't know, how on earth can the general public figure it out?

Before we begin, let's define terms: GA is completely done, ready for use. RC is a release candidate: don't change anything, just fix bugs because we're charging towards a release here. Beta is possibly unsafe code, use at your own risk. Alpha is known to have significant bugs, but if you're curious please play with it.

Now for the releases/versions game. Let's recap:

* 5.0 has version numbers that leapfrog each other in features and functionality. SHOW PROFILES -- now you see it, now you don't.
* 5.1 has been "... [released to general availability ❲as❳ a near-final release candidate](http://www.eweek.com/c/a/Database/CEO-Calls-MySQLs-the-Ferrari-of-Databases/)," whatever that means.
* 5.1 has just had drastic changes in the RC stage. ( [Remove Federated in 5.1.24](http://dev.mysql.com/doc/refman/5.1/en/news-5-1-24.html), [remove RENAME DATABASE](http://www.mysqlperformanceblog.com/2008/05/20/too-dangerous-command/), [remove Cluster](http://blogs.mysql.com/kaj/2008/05/23/mysql-clusters-improved-release-model/).) And it's going to have more changes before it's released, too: [Federated will be added back in 5.1.25](http://dev.mysql.com/doc/refman/5.1/en/news-5-1-24.html).
* 5.2 doesn't exist. Last year at the MySQL conference, someone made an abrupt decision to skip 5.2 and inflate the version numbers to 6.0, which has big changes in the query optimizer and other areas.
* [6.0 is alpha, but it includes Falcon, which is beta](http://blogs.sun.com/theaquarium/entry/mysql_6_0_is_alpha) even though [Falcon has extremely bad bugs that its developers claim are not bugs](http://bugs.mysql.com/bug.php?id=36296).
* 6.1 doesn't exist as far as I know.
* 6.2 not only exists, but it is GA. Not only that, but it just... appeared as GA, as far as I know. No RC stage, no nothing -- at least, nothing on the MySQL website that I see (certainly no manual version). It went from nonexistent to GA instantaneously as far as I know. It was created by [extracting the Cluster code from 5.1](http://johanandersson.blogspot.com/2008/05/mysql-cluster-62-officially-released.html).
* 6.2 is GA, but 5.1 is RC.
* 6.2 is GA, but 6.1 doesn't exist as far as I know.
* 6.2 is GA, but 6.0 is alpha. (Hopefully you see the pattern here.)
* 6.2 is GA, but presumably does not include the changes made in 6.0, since it was derived from 5.1′s code.
What is going on here?

How is this an [improved release model](http://blogs.mysql.com/kaj/2008/05/23/mysql-clusters-improved-release-model/)? What is improved about this?

How in the world can anyone figure out what versions of the software have what features? Who can make an educated decision about what product to use in this situation? Are people supposed to just rely on the sales people to help them figure out what to use? Boy, is that trusting the fox to guard the henhouse.

Why didn't they just release 5.1 Cluster as GA separately, if that reflected the reality in the code? They certainly missed an opportunity to show some progress on 5.1. As it is, 5.1 got robbed of its chance to have at least some of its code go GA after more than 2.5 years in development. Now 5.1 looks like even more of an embarrassment -- hey 5.1 team, how come you can't get anything out the door when these 6.2 people are releasing GA products? Not to mention 6.0 -- you guys look bad now too! (Just kidding.)

I tried to draw a timeline of MySQL's release history, in some detail in the 5.0 history and in very basic detail in the 5.1 and 6.0 and 6.2 trees. You can take a look at that. It's worth studying for 5 minutes or so, even though it's kind of ugly. There are lots of oddities to notice about it. Enjoy:

![MySQL release timeline](/media/2008/05/mysql-timeline.png)

The [inmates](http://www.mysql.com/about/contact/sales.html) are running the [asylum](http://www.mysql.com/). This gets more and more amusing as time goes on.

<p>The <a href="http://www.mysql.com/about/contact/sales.html">inmates</a> are running the <a href="http://www.mysql.com/">asylum</a>.  This gets more and more amusing as time goes on.</p>
