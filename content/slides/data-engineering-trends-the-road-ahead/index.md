---
title: "Data Engineering Trends: The Road Ahead"
date: "2018-10-03"
url: "/slides/data-engineering-trends-the-road-ahead/"
image: "/slides/data-engineering-trends-the-road-ahead/cover.jpg"
description: "VividCortex's free event spotlights companies that define state-of-the-art data engineering culture, through their first-hand experience building data platforms that meet today's needs and offer new opportunities for tomorrow."
ratio: "16:9"
themes:
- apron
- adirondack
- descartes
---
class: no-footer, title, shelf, fogscreen
background-image: url(cover.jpg)

# Data Engineering Trends
## The Road Ahead

![Logo](vividcortex-horizontal-white-rgb.svg# absolute r-0 t-0 pa-5 mw-30)

---
layout: true
class: img-right-full, fit-h1

.footer[
- ![logo](vividcortex-horizontal-web.svg)
]

---
# Key Trends in Data Engineering

![Image](serhat-beyazkaya-670060-unsplash.jpg)

1. Tomorrow's best business models are data-intensive.
2. Companies are moving databases to the cloud.
3. Databases are evolving for cloud computing.
4. Full-stack engineering is becoming dominant.
5. DBA roles are specializing.
6. Monitoring is facing a dilemma.

???

- Eight slides about what's happening right now.
- We've observed these trends ourselves amongst our customers.
- I've interviewed a number of customers and non-customers to validate.
- These are broad trends; not absolutes, but there's truth to them.

---
# The Data-Intensive Future

![Mesh](pietro-jeng-266017-unsplash.jpg)

Many of tomorrow's best businesses will be data-intensive.

- Data is the business value and the moat.
- Computation is becoming a commodity.
- Polyglot persistence is the norm, and remains important.
- Distributed, cloud-native architectures are emerging.
- Cloud-native culture and engineering practices are too.

???

- Companies used to win via unique abilities or secret knowledge.
- Now they win by having a dataset others don't have.
- Applications used to be compute-intensive. Now they're data-intensive.
- We're seeing more monetization of shared customer data pools to derive insights.

---
# Databases Move to the Cloud

![Angles](anders-jilden-219256-unsplash.jpg)

Cloud migrations are accelerating---including databases, which have lagged
behind.

- Many of today's startups are all-cloud, and this trend is growing.
- Hybrid cloud architectures are emerging quickly.
- The database is a key motivating factor in cloud architectures.

???

- A few years ago you moved databases to the cloud only if compelled.
- Today if you're not using DBaaS, you need to justify why not.
- Hybrid cloud architectures go both ways and we're seeing it already.
- Databases are driving significant complexity and feature richness in clouds.
- Many companies are moving to cloud and off proprietary DBs in one step.

---
# Databases Evolve for Cloud Computing

![Evolving](sebastian-kanczok-199612-unsplash.jpg)

Mature relational technologies have friction in the cloud.

- Databases are being redefined and rearchitected for cloud environments.
- The evolution is roughly: MySQL-on-EC2, RDS, Aurora, Cosmos DB
- There is some technology consolidation, but specialization remains important.
- A significant macro trend is the Kafka "log-first" event-driven architecture.

???

- Most new databases don't make it, but least-common-denominator isn't for
  everyone.
- We can probably expect some consolidation of "Big Data" technologies too.
- The "holy grail" is data lakes with multiple access methods, but this 
  remains elusive for a variety of reasons.

---
# The Rise of the Full-Stack Engineer

![Library](max-langelott-665852-unsplash.jpg)

The dev/ops separation of duties is moving down the stack.

- The first age of DevOps was ops doing dev; the second age is devs doing ops.
- Key DB skills are querying, modeling, and sometimes physical design.
- Developers are gaining enormous purchase authority and influence.
- Rich, integrated development experiences and workflows are emerging.
- Complexity is inescapable.

???

- Heroku still sets the standard for full-stack development, but the world is
  catching up.
- UX and simplicity are major factors in tool choice.
- But at the same time, fluency with things like service meshes and k8s is a
  required skillset for more engineers.

---
# Whither the DBA?

![Castle](yoal-desurmont-90493-unsplash.jpg)

- Database:DBA ratios continue to grow.
- DBA roles are being redefined.
- Many DBAs are becoming data platform engineers.
- The stereotypical DBA-as-gatekeeper is falling out of favor.

???

- When I was a DBA, we had 1:1 ratios, then 5:1, now 5000:1.
- Applying DevOps and SRE principles to the database is becoming mainstream.
- See Charity and Laine's book [Database Reliability
  Engineering](http://shop.oreilly.com/product/0636920039761.do)
- The 2018 [DORA research
  report](https://cloudplatformonline.com/2018-state-of-devops.html) explains key
  reasons why DevOps practices are valuable in the database realm.

---
# The Monitoring Catch-22

![Fragments](erik-eastman-267511-unsplash.jpg)

Companies want to do more monitoring with fewer tools, but that remains an
unsolved problem.

- The monitoring problem space has irreducible complexity.
- The monitoring archetype unifies metrics, APM, tracing, and logs.
- Databases are uniquely important, and uniquely hard to monitor.

???

- One-size-fits-all tools leave critical needs unmet, while adding bloat.
- The increasingly powerful full-stack engineer is growing more frustrated with
  the complexity and shortcomings of all-purpose monitoring tools.
- Our goal at VividCortex is to simplify the user experience and give full-stack
  engineers "data engineering superpowers" vis-a-vis database observability.
