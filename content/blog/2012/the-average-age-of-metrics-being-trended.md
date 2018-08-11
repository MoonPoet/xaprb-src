---
title: The average age of metrics being trended
date: "2012-10-30"
url: /blog/2012/10/30/the-average-age-of-metrics-being-trended/
credit: "https://pixabay.com/en/stock-trading-monitor-business-1863880/"
image: "/media/2012/10/pixabay-en-stock-trading-monitor-business-1863880.jpg"
thumbnail: /media/2012/10/pixabay-en-stock-trading-monitor-business-1863880.tn-500x500.jpg
categories:
  - Databases
---
Last night I wrote about [trending data with a moving average](/blog/2012/10/29/trending-data-with-a-moving-average/ "trending data with a moving average"), and then after I went to bed, I realized I made a mistake on the chart I showed. I calculated &alpha; for the exponentially weighted moving average so that the average age of metrics approaches 60 samples as time approaches infinity, and I plotted that on the same chart with a 60-sample simple moving average.

I've made this mistake several times before. The mistake is that the average age of the metrics in the 60-sample simple moving average is 30, not 60.

Here's what the chart looks like if I change the exponential moving average to a 30-second average age:

![](/media/2012/10/moving-averages-2.png) 

If you compare this with yesterday's chart, you'll see that today's red line tracks the trend in the sampled data points more responsively than yesterday's:

![](/media/2012/10/moving-averages.png) 

This illustrates that although the average age of the data is the same in the simple moving average and the exponential moving average, the exponential moving average places much more weight on recent data points. Again, the sampled data here is from a MySQL server (it's queries per second in one-second intervals.)

By the way, Unix load averages are computed similarly, and the labeling is similarly (slightly) misleading. The averages are said to be 1-minute, 5-minute, and 15-minute averages of load, but they aren't really. The average age of the samples of load works out to 1, 5, and 15 minutes over the long run, but that's not the same thing as an average of the load over the last N minutes, because the samples aren't weighted equally. As I wrote this, I thought "didn't I write a blog post about that?" but I see it's just a draft from several years ago, and I never completed it. If I get a chance, I'll try to do that soon.


