---
url: /blog/what-is-moving-average-convergence-divergence-macd/
title: "What is Moving Average Convergence-Divergence (MACD)?"
date: 2017-10-25T21:35:56-04:00
categories:
  - Math
author: Baron Schwartz
description: "MACD is a terrible name for a simple concept. It's an efficient way to compare two moving averages and calculate trend in a metric."
image: "/media/2017/10/macd.png"
---

Moving Average Convergence-Divergence (MACD) is an efficient, compact way to compare averages of a metric over two different intervals, and determine if the metric is trending upwards or downwards. It is widely used in finance and several other fields.

MACD is a terrible name for a simple concept. It simply subtracts the long-term (distant) average from the short-term (recent) average. If the short-term average is larger, the result is positive and the metric is trending upwards.

<!--more-->

MACD is usually implemented with a pair of exponentially weighted moving averages (EWMAs or EMAs). These encode a set of data into a *single number* very efficiently, a property that makes them convenient and widely used in areas where compactness and efficiency are important. But, EWMAs don't retain the full detail of the original history, so you can't use them alone to figure out whether the metric they're averaging is trending up or down.

Above is a picture of some data (the blue columns) and two exponentially weighted moving averages of them. The red line is a shorter-term average, so it reacts to changes in the blue data faster and tracks it more closely. The yellow line is a longer-term average. Time goes from left to right.

At *any point* on this chart, say, the point I've marked with a red arrow, you can subtract the yellow line from the red line and see what the trend of the data is. At this point, red is smaller than yellow, so the trend is negative.

A common misunderstanding is to believe that the MACD shows the trend at the point of time in question. It doesn't. It shows the trend *during the time interval captured by the moving averages.* The average therefore *lags* the real data (and you can see that the longer-term, slower, yellow average lags the data more, as it must).

So a MACD doesn't show that the metric is trending upwards or downwards *now*. It shows the trend from the longer average's centerpoint to the shorter average's centerpoint.

Here's a picture of how that works, using EWMAs. EWMAs give greater weight to more recent measurements, and exponentially less weight to past measurements. If you chart these weights, you'll see a picture like the below. The average influence of these curves is some length of time, whose value and derivation I'll skip here, but conceptually they have a “center of gravity” which is some distance in the past. The MACD effectively calculates the slope between averages centered around those points in the past.

![EWMA](/media/2017/10/ewmas.png)

Hopefully this is an easy-to-understand explanation.
If you want a longer explanation that's more complete, see [Wikipedia](https://en.wikipedia.org/wiki/MACD).
