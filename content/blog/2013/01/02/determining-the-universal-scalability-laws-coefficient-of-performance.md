---
title: "Determining the Universal Scalability Law's coefficient of performance"
url: /blog/2013/01/02/determining-the-universal-scalability-laws-coefficient-of-performance/
date: "2013-01-02"
description: "The Universal Scalability Law has a hidden coefficient."
image: "media/2013/01/coeff-of-performance.png"
categories:
  - Scalability
  - Math
  - Databases
---

If you're familiar with Neil Gunther's Universal Scalability Law, you may have heard it said that there are two coefficients, variously called alpha and beta or sigma and kappa. There are actually three coefficients, though. See?

\\[
C(N) = \frac{N}{1 + \sigma(N-1) + \kappa N (N-1)}
\\]

No, you don't see it -- but it's actually there, as a hidden 1 multiplied by N in the numerator on the right-hand side. When you're using the USL to model a system's scalability, you need to use the C(1), the "capacity at one," as a multiplier. I call this the coefficient of performance. It's rarely 1; it's usually thousands.

To illustrate why this matters, consider two systems' throughput as load increases:

![coefficient of performance](/media/2013/01/coeff-of-performance.png)

The green line and the blue line are both linearly scalable systems. Add twice the concurrency, get twice the throughput. But the slope of the lines is different. The blue system can do twice as much work as the green system, even though it's no more scalable.

To model the USL, you need to determine C(1) by measuring the system under test. In my experience with real systems running in production, mostly MySQL servers, this is not simple. You can't just say "let's quiet the web app down, I want to load it with exactly one user for a few minutes and measure how fast it runs." Instead, you get a bunch of samples from production traffic, and you [derive](/blog/2013/01/03/determining-the-usls-coefficient-of-performance-part-2/) the throughput at concurrency=1 from that.

The result goes into the numerator as a multiplier of N, although it's usually omitted when the USL formula is shown.

If you're interested in learning more, I wrote an [ebook about the Universal
Scalability Law](https://www.vividcortex.com/resources/universal-scalability-law/).
