---
title: "The Root Cause Fallacy"
description: "Root cause analysis isn't very useful. It's always the CEO's fault."
date: "2014-07-21"
url: /blog/2014/07/21/root-cause-fallacy/
categories:
  - Operations
credit: "https://unsplash.com/photos/EwKXn5CapA4"
image: "/media/2014/07/jeremy-bishop-556948-unsplash.jpg"
---

Wouldn't you like to find the root cause of that downtime incident? Many people
would. But experience has taught me that there is no such thing as a single root
cause. Instead, there's a chain of interrelated conditions, each of which is
necessary but none of which is sufficient to cause the overall problem.

<!--more-->

I am often reminded of an outage years ago. It was "caused" by a failed disk.
But the disk was in a RAID5 array, so the array shouldn't have failed. But another disk in that array had failed
some time previously, and RAID5 can tolerate only one failed disk. Backups had also failed some time previously, so there
were no backups. Health checks didn't notify anyone of the degraded disk array,
due to a misconfigured alerting system. Alerting and backups failed because the
person in charge of operations was not doing their job.  The 
person was still in charge of operations because of management dysfunction.

If you really want to get to the root cause of a problem, you need to use the
Five Whys approach. I rarely do that because I already know where it ends. The
CEO or equivalent is always the problem. It's turtles all the way down (or up).
Saying that the CEO is ultimately responsible is true but useless. The CEO is
ultimately responsible for *everything*, which isn't a "cause."

That's why the search for a root cause is usually a scapegoat-hunt in disguise, trying
to find someone or something to blame. If you think there is really a single
cause, you eventually must identify a single person. If you stop short of that,
everyone knows the process was a farce. But blaming a person is also a farce.
Everyone knows that someone's being thrown under the bus, which isn't a
solution.

There are several solutions to this dilemma. One is to stop looking for a
single *root* cause, and instead identify the *system* of conditions or
dysfunctions that jointly resulted in the observed system behavior. This allows something
constructive (such as learning) to come out of the retrospective, instead of inexorably bringing
pressure to bear on a well-meaning person who will then be sacrificed at the
altar of reductionist blame-gaming.

Another is to change the culture and own failures as opportunities. Navigating
this can be tricky. I've heard from more than one person who was fired from a
workforce with a supposedly "blameless culture" policy after tripping over a
booby-trap. I haven't attended one yet, but I've heard that Dave Zwieback's
postmortem workshops are excellent.

Another helpful step is to change the language and object to the words "root"
and "cause." Both of them change how people think, and frame situations in ways
that even well-meaning people have difficulty seeing from a positive angle. It's
also more accurate: we're not dealing with *causes* as much as attributes or
properties of complex systems. For more on this, see [my review of the Chaos
Engineering book](/blog/chaos-engineering-rosenthal-hochstein-blohowiak-jones-basiri/).

More and more people I speak to are either doubtful or outright reject
root-cause analysis these days. That's a good thing. I used to be pressured for
root-cause analysis years ago, and there was always an airtight and unspoken
assumption that *of course* such a thing exists and is the right way to handle
the aftermath of an incident. I'm happy the times are changing. These days, even
some companies have stopped saying their tools or products can find root causes.
Maybe this trend will allow us to replace the manifest failures of root-cause
analysis with something more helpful.
