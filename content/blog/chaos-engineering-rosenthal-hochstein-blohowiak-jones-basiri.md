---
title: "Book Review: Chaos Engineering"
date: "2018-10-05"
url: "/blog/chaos-engineering-rosenthal-hochstein-blohowiak-jones-basiri"
description: "Chaos Engineering, from Rosenthal et al, is a succinct introduction to the what, why, and how of Chaos Engineering, with a bias towards how Netflix uses it."
tldr: "Chaos Engineering, from Rosenthal et al, is a succinct introduction to the what, why, and how of Chaos Engineering, with a bias towards how Netflix uses it. The book advocates for Chaos Engineering as an essential way to surface new information about complex systems, which otherwise defy attempts to reason about their workings."
credit: "https://unsplash.com/photos/e3dY8laAQtA"
image: "/media/2018/10/unsplash-photos-e3dY8laAQtA.jpg"
thumbnail: "/media/2018/10/unsplash-photos-e3dY8laAQtA.tn-500x500.jpg"
categories:
- Reviews
---
[Chaos Engineering: Building Confidence in System Behavior through Experiments](https://www.oreilly.com/webops-perf/free/chaos-engineering.csp). O'Reilly Media, 2017. Casey Rosenthal, Lorin Hochstein, Aaron Blohowiak, Nora Jones, and Ali Basiri.
<!--more-->

[![Chaos Engineering Cover](/media/book-covers/chaos-engineering.jpg# 3dbook)](https://www.oreilly.com/webops-perf/free/chaos-engineering.csp)

This brief book should be required reading for anyone building a system complex enough to make it hard to understand the full scope of its behaviors under varying circumstances, which describes most most software. It's a brief but effective overview of Chaos Engineering, at a medium level of detail. In print, it's about 60 pages and reads quickly. It's a free download from O'Reilly. The authors are all at Netflix.

Chaos Engineering isn't about breaking things in production, it's about learning new things about systems. And as the authors point out, these are often things you cannot deduce or even imagine. Chaos Engineering is the discipline of inducing controlled failure and observing how your systems respond.

One of my favorite parts is the example of systemic complexity on page 13, where a set of well-designed and rational systems with sensible behaviors interacts in a gloriously destructive way that few (if any---certainly not me) people would be able to predict, no matter how well they knew the systems.

Another favorite (and a great recruiting tactic) is the discussion of Netflix's motivations and priorities on page 9:

> Software engineers typically optimize for... performance, availability, and fault tolerance... An experienced team will optimize for all three of these qualities simultaneously. At Netflix, engineers also consider a fourth property: Velocity of feature development.

The book links the discipline of Chaos Engineering to feature velocity in a clear and compelling way.

Part 1 is an introduction and motivation, Part 2 delineates principles of Chaos Engineering, and Part 3 delves into the practice. A nice bonus is the included maturity model and map, and a helpful explanation of how to interpret the scorings on the map and what to do about them.

The level of detail is enough to understand why Netflix does Chaos Engineering, a high-level idea of how, and why it's a Good Thing in general. It should be pretty persuasive, and includes enough outreach and appeal to different disciplines to neutralize most of the reasons a reader might imagine their industry can't use Chaos Engineering safely and profitably. (I could be wrong about that, but I'm left with the feeling that few of us would have valid excuses for not at least trying!)

Really, there's little to no reason that all of us can't use Chaos Engineering, even if we don't add all the trappings of method and science and so on. With just a little imagination, there are so many simple ways we can safely induce behaviors that are hard or impossible to test otherwise, and which will surface valuable new information. As an example, a super-basic way I added some lightweight chaos to a system I built a while ago is some ad-hoc [fault injection](blog/2013/03/14/crash-injection-for-writing-resilient-software/), which allowed me to make a Go program panic deep inside of systems that weren't possible to test in integration tests. This is a good illustration; and I don't think I even knew much about Chaos Engineering at the time. We all can do easy, valuable things like this.

My only complaints about the book are stylistic. I think it would be easier to understand its lessons if it had more unbroken prose and less frequent headings/structure, and if it used plainer words. Nitpicks aside, I think it's the perfect introduction to Chaos Engineering: short enough that nobody can justify not reading it, just the right level of depth and breadth, and just enough information and guidance to get oriented and started, with clear next steps. Let's all introduce Chaos Engineering to make our systems faster, better, and safer!
