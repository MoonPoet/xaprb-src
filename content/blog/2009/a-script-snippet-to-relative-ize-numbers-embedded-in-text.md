---
title: A script snippet to relative-ize numbers embedded in text
date: "2009-09-01"
url: /blog/2009/09/01/a-script-snippet-to-relative-ize-numbers-embedded-in-text/
categories:
  - Databases
  - Open Source
---
A lot of times I'm looking at several time-series samples of numbers embedded in free-form text, and I want to know how the numbers change over time. For example, two samples of SHOW INNODB STATUS piped through `grep wait` might contain the following:

```
Mutex spin waits 0, rounds 143359179688, OS waits 634106844
RW-shared spins 1224152309, OS waits 38278807; RW-excl spins 2432166425, OS waits 35264871
Mutex spin waits 0, rounds 143386303439, OS waits 634292093
RW-shared spins 1224197048, OS waits 38281423; RW-excl spins 2432347936, OS waits 35271423
```

How much have the numbers changed in the second sample? My head is too lazy to do that math. So Daniel Nichter and I whipped up Yet Another Snippet to self-discover patterns of text and numbers, and compare each line against the previous line that matches the same pattern. Let's fetch it:

```
wget [http://maatkit.googlecode.com/svn/trunk/util/rel](http://maatkit.googlecode.com/svn/trunk/util/rel)
```

Now give it the above input, and it'll print out something useful (emphasis mine):

```
Mutex spin waits 0, rounds 143359179688, OS waits 634106844
RW-shared spins 1224152309, OS waits 38278807; RW-excl spins 2432166425, OS waits 35264871
Mutex spin waits 0, rounds 27123751, OS waits 185249
RW-shared spins 44739, OS waits 2616; RW-excl spins 181511, OS waits 6552
```

My lazy brain likes that much better.


