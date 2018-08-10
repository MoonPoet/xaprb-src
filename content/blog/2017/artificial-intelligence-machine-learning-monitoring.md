---
url: /blog/artificial-intelligence-machine-learning-monitoring/
author: Baron Schwartz
categories:
- Monitoring
date: '2017-05-26T10:42:13-04:00'
description: There are three major use cases for ML and AI in system monitoring.
image: /media/2017/05/artificial-intelligence.jpg
credit: https://pixabay.com/en/brain-cactus-skull-1841528/
title: Monitoring with Artificial Intelligence and Machine Learning

---
Artificial intelligence and machine learning (AI and ML) are so over-hyped today
that I usually don't talk about them.  But there are real and valid uses for
these technologies in monitoring and performance management. Some companies have
already been employing ML and AI with good results for a long time.
VividCortex's own adaptive fault detection uses ML, a fact we don't generally
publicize.

AI and ML [aren't magic](http://www.fast.ai/), and I think we need a broader
understanding of this. And understanding that there are a few _types_ of ML use
cases, especially for monitoring, could be useful to a lot of people.

<!--more-->

I generally think about AI and ML in terms of three high-level _results_ they
can produce, rather than classifying them in terms of how they achieve those
results.

### 1. Predictive Machine Learning

Predictive machine learning is the most familiar use case in
monitoring and performance management today. When used in this fashion, a data
scientist creates algorithms that can learn how systems normally behave. The
result is a model of normal behavior that can predict a range of outcomes for
the next data point to be observed. If the next observation falls outside the
bounds, it's typically considered an anomaly. This is the basis of many types of
anomaly detection.

Preetam Jinka and I wrote the book on using [anomaly detection for
monitoring](http://www.oreilly.com/webops-perf/free/anomaly-detection-monitoring.csp).
Although we didn't write extensively about machine learning, machine learning is just
a better way (in some cases) to do the same techniques. It isn't a fundamentally
different activity.

Who's using machine learning to predict how our systems should behave? There's a
long list of vendors and monitoring projects. Netuitive, DataDog, Netflix,
Facebook, Twitter, and many more. Anomaly detection through machine learning is
par for the course these days.

### 2. Descriptive Machine Learning

Descriptive machine learning examines data and determines what it means, then
describes that in ways that humans or other machines can use. Good examples of
this are fairly widespread. Image recognition, for example, uses descriptive
machine learning and AI to decide what's in a picture and then express it in a
sentence. You can look at [captionbot.ai](https://www.captionbot.ai) to see this
in action.

What would descriptive ML and AI look like in monitoring? Imagine diagnosing a
crash: "I think MySQL got OOM-killed because the InnoDB buffer pool grew larger
than memory." Are any vendors doing this today? I'm not aware of any. I think
it's a hard problem, perhaps not easier than captioning images.

### 3. Generative Machine Learning

Generative machine learning is descriptive in reverse. Google's software
famously performs this technique, the results of which you can see on their
[inceptionism
gallery](https://photos.google.com/share/AF1QipPX0SCl7OzWilt9LnuQliattX4OUCj_8EP65_cTVnBmS1jnYgsGQAieQUc1VQWdgQ?key=aVBxWjhwSzg2RjJWLWRuVFBBZEN1d205bUdEMnhB).

I can think of a very good use for generative machine learning: creating
realistic load tests. Current best practices for evaluating system performance
when we can't observe the systems in production are to run artificial benchmarks
and load tests. These clean-room, sterile tests leave a lot to be desired.
Generating realistic load to test applications might be commercially useful.
Even generating [realistic performance
data](https://www.xaprb.com/blog/2014/01/24/methods-generate-realistic-time-series-data/)
is hard and might be useful.

### 4. Prescriptive

Bonus: prescriptive. (I added this later, after a discussion with someone.) Prescriptive machine learning would produce instructions: _what to do to a system_.

