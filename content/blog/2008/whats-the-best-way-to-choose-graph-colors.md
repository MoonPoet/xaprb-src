---
title: "What's the best way to choose graph colors?"
date: "2008-03-22"
url: /blog/2008/03/22/whats-the-best-way-to-choose-graph-colors/
categories:
  - Monitoring
---
I have an issue I hope someone can help me with.  I am generating [RRDtool](http://oss.oetiker.ch/rrdtool/) graphs (for [Cacti](http://www.cacti.org/) monitoring templates for MySQL, which I'll release soon) that have up to 11 different metrics on them.  With that many lines or areas on a graph, it becomes very hard to pick colors that are easy to see and easy to distinguish from each other.  What's a good way to choose such colors?  Is there a way to do it automatically---is there a formal method that will produce good results?

> Note: [VividCortex](https://vividcortex.com/) is the startup I founded in 2012. It's the easiest way to monitor what
> your servers are doing in production. VividCortex offers [MySQL performance
> monitoring](https://vividcortex.com/monitoring/mysql/) and [PostgreSQL
> performance management](https://vividcortex.com/monitoring/postgres/) among many
> other features.

I know some color theory and I have read about how you can distinguish colors from each other (hue, value etc).  But I am unsure the best way to choose this many colors.  Trying by hand produces garish results or graphs that are just hard to read.

My first [attempt to solve this with a program](/media/2008/03/color-chooser.html) was to simply create a list of every possible completely saturated color in a 32-bit space---essentially, the "pure" colors around the rim of the color wheel---and divide it into the desired number of evenly spaced intervals.  This produces pure colors, which is not ideal.  They are hard to look at.  Did I mention garish?

I can shuffle the order so that they're not adjacent, but that only helps avoid a "rainbow effect" if I'm stacking areas of color on top of each other, like in the following image:

![MySQL Command Counters](/media/2008/03/mysql_command_counters.png)

Ugh, rainbows (I chose those by hand, not with my program).  Lines on a white background might be placed in any order, so shuffling doesn't help with those graphs.

I modified my little script to let me vary the saturation and value.  My thinking was that lines on a white background really shouldn't be full-value, and when I'm drawing areas instead of lines, I should de-saturate them so they become more pleasing pastels.  This doesn't really help as much as I might have hoped for, either.  Colors around 80% saturation and 60% value look pretty good, but they're still ugly colors.  And I can't get over five colors without them starting to run together again.  Here's an example with only four colors that's already hard to look at:

![InnoDB I/O Activity](/media/2008/03/innodb_io.png)

Part of the problem, I'm currently thinking, is that I'm varying only one dimension.  I could be varying the saturation as well as the hue, for example.  But that might be another rabbit hole that will waste more time.

Right now I'm thinking that I should ask for help, instead of continuing to work on this myself.  So, any ideas are welcome!

By the way, beautiful colors would be nice... a lot of the colors I choose by hand are very pretty and I'm sure my impartial, evenly-distributing script will never choose them in a million years.  Also, it's actually a good thing when graphs each have their own color scheme (as long as it's attractive) because it becomes easier to identify graphs without having to read the title.  Just some extra food for thought.


