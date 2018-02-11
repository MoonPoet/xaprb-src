---
title: Heisenberg Decisions
date: 2018-02-10 16:23:48 +0000
author: Baron Schwartz
categories:
- Leadership
description: Hindsight is less often 20/20 and more often a biased narrative about
  a past that never existed.
image: media/2018/02/rain-2422642_1280.jpg
draft: true

---
A couple months ago we had an incident, in which a legacy recovery mechanism proved to be inadequate to our current scale. In our internal post-incident review, we asked if we should improve this seldom-used capability. I decided not to, because the plan is to completely replace the part of the platform that it serves. My judgment was that we were not likely to need it, and it would be a lot of time and effort to improve.

Shortly thereafter, we did need it again, and again experienced the same pains. Was the decision wrong?

![Raindrop Puddle](/media/2018/02/rain-2422642_1280.jpg)

<!--more-->

This story should be familiar if you operate in any domain in which there's uncertainty about the future return on any investment (or risk due to lack of investment). And really, who doesn't---this story should be relevant to most of us!

These decisions are rarely wrong or right at the time they're made. Like Schrödinger's cat, you won't know whether they live or die until subsequent events occur---events whose occurrence, and outcomes, are unknowable at the time.

And yet, it's common to impose right/wrong judgments in hindsight. Assuming the decision hasn't been obsoleted at the point of hindsight judgment, there's only one "good judgment" box in the decision matrix:

![Hindsight 1](/media/2018/02/hindsight-judgment-1.png)

And if the system is decommissioned and the decision is obsolete, the best-case is a 50/50 split:

![Hindsight 2](/media/2018/02/hindsight-judgment-2.png)

Rarely are there clear errors of judgment when the future is uncertain. Equating outcomes with soundness of judgment is a fallacy: "good" decisions don't necessarily produce good outcomes, and "bad" decisions aren't necessarily punished by subsequent events. The decisions themselves aren't good or bad; they are simply a necessary factor in an outcome that had many necessary, but only jointly sufficient, conditions.

Be vigilant against the tendency to ask "why _didn't_ you." It's dangerous: it's a [counterfactual](https://www.amazon.com/Beyond-Blame-Learning-Failure-Success/dp/1491906413/?tag=xaprb-20), a question about decisions not taken in an imaginary, nonexistent path. This puts people on the defensive against the indefensible, leads to finger-pointing, and tempts leadership to "solve" the problem by punishing those to "blame." Worst of all, it is a serious obstacle to learning. And the goal of any post-incident review should be for the organization to learn so it can become more resilient.

Instead of counterfactuals, ask what the person knew, what pressures they were under, what they thought might happen, what types of risk-reward and cost-benefit estimates they were making. And rather than _judging_ those, seek instead to understand why those seemed to be wise at the time. Because no one got up that morning and said, "today I'm going to be lazy and foolish, not caring about the obvious negative consequences of my action or inaction." That's another past that didn't happen. Don't act as if it did.

PS: although I'm telling a story about people suffering because I decided not to prioritize a fix, and they suffered and correctly identified my decision as part of the cause, this story is _not_ a criticism of them. They didn't "blame" me, and I'm not "blaming" them for stating the truth about how we ended up in Groundhog Day.

[Photo Credit](https://pixabay.com/en/rain-drip-circle-water-raindrop-2422642/)