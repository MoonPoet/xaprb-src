---
title: JavaScript date formatting benchmarks
date: "2006-05-14"
url: /blog/2006/05/14/javascript-date-formatting-benchmarks/
categories:
  - Web
---
Two earlier articles demonstrated how to [format](/blog/2005/12/12/javascript-closures-for-runtime-efficiency/) and [parse](/blog/2005/12/20/javascript-date-parsing/) dates flexibly with JavaScript. I asserted in those articles that my approach was efficient, though I didn't provide any numbers to prove my claim. This article compares the performance of my date-formatting library against several other date-formatting libraries I've found online.

I'd like to benchmark my date-parsing library too, but I haven't seen any comparable implementations. By the way, my date-formatting and date-parsing libraries are wrapped into a single file, so even though I'm not actually executing the date-parsing functions in this benchmark, they're compiled anyway.

### Motivation

My motivation for this article is simply to demonstrate the truth of what I said earlier: writing code to write code can be very efficient. I'm explicitly *not* trying to say I'm "better" than anyone, or someone else does anything "wrong" or anything like that. This series of articles really isn't even about date manipulation! It's about demonstrating a programming technique: write a function that can write other functions, making it possible to **optimize code whose behavior depends on input that is not known until runtime**. That's why my first date-formatting article was originally titled "JavaScript closures for runtime efficiency."

Note that my motivation also isn't to make the fastest date formatting code. I haven't really tried to optimize for speed, but if I wanted to, I think I could probably find some bottlenecks and optimize my own code further.

All I'm trying to do is demonstrate the general coding methodology I used, because I often see folks using a much less optimal solution, probably because they don't know about (or aren't comfortable with) dynamic code generation. That's just my opinion.

### Setup

I ran these benchmarks on Firefox 1.5.0.2 on my home computer, a fairly new and powerful AMD64 machine running Gentoo GNU/Linux. I won't bother telling you all the hardware specs... that always makes my eyes glaze over.

I created a set of pages that do nothing but include the JavaScript files needed, and run 100,000 iterations of date-formatting. I closed my browser window between each test, and nothing else was running on my machine. I ran each test several times and averaged the results, rounding to four significant digits.

I had to increase the script timeout so Firefox wouldn't interrupt the tests. I did this by opening `about:config`, then changing `dom.max_script_run_time` to 5000 seconds.

### Results

Here's a graph of the times. The algorithms are in alphabetical order:

![JavaScript date-formatting benchmark](/media/2006/05/date-formatting-benchmark.png)

Obviously, the method I use is much faster---between 3.15 and 4.89 times faster. Here are the results as numbers in a table. **WARNING**: If you click on the links to the benchmarks, your browser will probably freeze for the better part of a minute on a fast machine---maybe longer on a slow machine.

| Algorithm | Time (sec) | Relative Time | Link to benchmark |
|-----------|-----:|--------------:|-------------------|
| [Dojo](http://www.dojotoolkit.org/) | 34.00 | 3.15 | [Link](/media/2006/05/date-formatting-benchmarks/test-dojotoolkit.html) |
| [Gazingus](http://web.archive.org/web/20050204062056/http://gazingus.org/html/Date_Formatting_Function.html) | 44.36 | 4.11 | [Link](/media/2006/05/date-formatting-benchmarks/test-gazingus.html) |
| [Matt Kruse](http://http://www.mattkruse.com/javascript/date/source.html) | 37.42 |  3.46 | [Link](/media/2006/05/date-formatting-benchmarks/test-mattkruse.html) |
| [Svend Tofte](http://www.svendtofte.com/code/date_format/) | 52.83 |   4.89 | [Link](/media/2006/05/date-formatting-benchmarks/test-svendtofte.html) |
| [Xaprb](/blog/2005/12/20/javascript-date-parsing/) |   10.80 |  1.00 | [Link](/media/2006/05/date-formatting-benchmarks/test-xaprb.html) |

### Is this an apples-to-apples comparison?

Absolutely not, and if it were, the slowness of the other methods would be even more obvious.

First of all, I'm only testing a single method of formatting---producing a date in YYYY-MM-DD format. I also haven't been scientific enough to really be accurate.

Beyond that, though, these various bits of code I've benchmarked are vastly different. The one that provides the most similar *formatting* functionality to mine is Svend Tofte's (that's probably why it's the slowest), but even that one only does *parsing*, not *formatting* (mine does both). The others are much less fully-featured, which means they'd probably be even less performant if someone extended them to implement the same set of functionality.

As I said above, I'm not doing this to pick on anyone, but the Dojo method is probably the least efficient. It's the simplest of all, providing only a few formatting characters, and it's not really that much faster than Svend Tofte's implementation. It's probably so slow because it a) uses lots of `if` statements and b) uses repeated string replacements with regular expressions. This is just a hunch, but if it had the rich feature set of my implementation or Svend Tofte's, I think it would probably be the slowest by far.
