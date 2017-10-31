---
title: Your Real Database Bottleneck
date: '2015-07-21T14:46:49-07:00'
categories:
- Databases
tags:
- USL
- DevOps
description: Your database bottleneck isn't CPU, I/O, query performance or scalability
  after all.
image: "/media/2015/07/bottleneck.jpg"
author: Baron Schwartz

---
Database performance optimization is usually concerned with indexes, SQL
design, lock contention, and the like. But the real database bottleneck is the
siloed culture that accretes around the database and has far more pernicious ripple effects than you might think. The real opportunity
in database optimization is the interplay between the technology and the
team, and its communication structures.

![Bottleneck](/media/2015/07/bottleneck.jpg)

<!--more-->

I've been thinking about this for years. While I was
at Percona I always tried to consult with
[Cary's](http://carymillsap.blogspot.com/) advice in mind: don't spend $1000
optimizing a $100 dollar problem. And as
VividCortex has grown, it has taught me
a valuable series of lessons about how to apply the advice in new
ways.

As I [shared on
LinkedIn](https://www.linkedin.com/pulse/how-prioritize-anything-simple-roi-model-baron-schwartz),
the goal is to think creatively about how to make the largest impact for the
biggest portion of the business, whether that implies people, systems, customers
or other areas.

Traditional advice, which I received when beginning to develop
VividCortex, was to *hammer* on the cost of downtime during sales conversations. I was deeply
skeptical of that for the same reasons [John Allspaw
is](http://www.kitchensoap.com/2013/01/03/availability-nuance-as-a-service/).
The simplistic math isn't truthful, and we all know it. But beyond that,
avoidance of a bad outcome is not the greatest value we can create for
customers. It's limited to the size of the potential downside. The real
value we can create is adding to the top line, not the bottom line, and is
*unlimited*.

What is that impact? Think of it this way:

- Instead of making one DBA a little more productive (30% of a $200k fully
  loaded annual cost, say), what if we can make 80 developers more productive
  (5% of 80 developers at $200k annually)?
- Instead of keeping the site online and fast for 5 minutes more per year, what
  if we can actually improve engineering velocity by 18
  calendar days?
- Instead of [improving database performance](https://www.vividcortex.com/) by
  50%, what if we can reduce the cycle time for continuous delivery
  ship-measure-iterate cycles from 2 days to 15 minutes?

By understanding deeply the flow of work and communications in your teams, you can actually have this kind of impact. You do not
need any tools (this is not a vendor pitch for VividCortex).

![Hair Sticks](/media/2015/07/hairsticks.jpg)

Databases aren't the only team bottlenecks. But the database is often a pretty
central one in many teams. It's a huge lever for IT productivity.

How can breaking down visibility silos around the database
improve team performance so much?

It all goes back to the principles of operations research. But we don't need to
be all technical about it. If you've ever read *The Goal* you totally get it.
You've got processes, workflow happening, people who are special, etc. You've
got inventory and throughput and stuff like that. And your human systems are
just as influenced by these things as your technical systems are.

So when you freeze in fear after a database outage, and proclaim that there's a
new code review process or something that'll prevent it from happening again in
the future, and it just happens to go through a committee or a DBA or some other
person or thing or system with a specialized role...

Specialized... that's a dirty word. You've introduced dependencies and that's a
huge problem. Read *The Goal*, and you'll see how bad it is. All you need now is
statistical variations to complete the unholy bottlenecking of your entire
engineering team. Oops, your DBA went on maternity leave! Sounds like some
processes are going to be more variable than they were before, right?

These are the same topics that have resonated so deeply with
my readers and audiences over the last few years: [freezes don't prevent
outages](/blog/2014/11/29/code-freezes-dont-prevent-outages/), [everything is
about dependencies and statistical fluctuations](/blog/2014/05/24/the-goal/),
[databases are really complex and that's a
problem](/blog/2014/12/08/eventual-consistency-simpler-than-mvcc/), [teams are
systems too](https://vividcortex.com/blog/2015/07/05/teams-are-systems-too/).

As I said at a Meetup on this topic:

> ... your database's performance is a lot less important to your business than the
> way you structure your engineering team. The interesting thing is that a lot
> of the most serious team, communication, and process bottlenecks in your
> business (the ones that make you miss ship deadlines, crash the site, and lose
> your best team members after repeated all-nighters) are actually driven by
> database issues, but not the way you think they are.

Watch out, your database isn't bottlenecked. Your team is. And your database,
the lack of democratized access to production performance data about it, and the
way you're reacting to outages and other problems by creating cultural
scar tissue, is reducing the effectiveness of every single person on your team
by 10%, 25%, you name it---I have seen teams I personally felt were running at
less than half of the productivity they could have, because of database-related
policies and processes that backfired.

That's your *true* database bottleneck.

Further reading on this topic:
- [Silvia Botros](http://sysadvent.blogspot.com/2016/12/day-2-dbas-priesthood-no-more.html)

Photo credits: [bottleneck](https://www.flickr.com/photos/icatus/2992269179/),
[hair pins](https://www.flickr.com/photos/grizzlymountainarts/6894273425/)
