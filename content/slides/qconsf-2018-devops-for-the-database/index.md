---
title: 'DevOps for the Database '
date: "2018-11-05"
url: "slides/qconsf-2018-devops-for-the-database/"
image: "slides/qconsf-2018-devops-for-the-database/thumbnail.jpg"
description: "Why is it hard to apply DevOps principles and practices to databases, and how can we get better at it? This talk explores real-life stories that answer these two questions, through the perspectives of teams that succeeded---and those who haven't."
ratio: "16:9"
themes:
- apron
- adirondack
- descartes
---
class: title, fogscreen, shelf, no-footer
background-image: url(unsplash-photos-oyXis2kALVg.jpg)

# DevOps for the Database
## Baron Schwartz &bullet; QConSF 2018

![Logo](vividcortex-horizontal-white-rgb.svg# absolute smokescreen pa-2 br-3 maxw-2-12th r-1-12th)

???
Why is it hard to apply DevOps principles and practices to databases, and how can we get better at it? This talk explores real-life stories that answer these two questions, through the perspectives of teams that have changed the entrenched culture, processes, and tooling---and those who've tried. Along the way, we'll cover topics including:
* What the research shows about DevOps, databases, and company performance
* Current and emerging trends in how we build and manage data tiers, and implications
* The traditional dedicated DBA role, and what has happened as a result
* What it takes to change from a DBA-centric culture, to one where database-related competencies and responsibilities are more distributed
* Why some teams succeed in this transformation, while others fail

We can apply DevOps principles to the database, and our work will be better for it. This talk will show you how.

---
layout: true
name: footer

.footer[
- @xaprb
- ![logo](vividcortex-horizontal-web.svg)
]

---
class: img-right-full
# Introduction

![Baron Schwartz](headshot.jpg)

I've been focused on databases for about two decades, first as a developer, then
a consultant, and now a startup founder.

I've written several books (High Performance MySQL)... and created a lot of open source software, mostly focused around database monitoring, database operations, and database performance: innotop, Percona Toolkit, Percona Monitoring Plugins among others.

???


---
class: roomy
# Agenda

* Overview of database DevOps
* How companies succeed
	* Tooling, culture, process, people
* How companies fail
* Challenges to database DevOps
* Resources, etc

Slides are online at xaprb.com.

My Twitter is @xaprb, my email is baron@vividcortex.com

???

* This is opinion, not research
* This is my personal experience
* I haven't gotten all this right yet

---
class: img-right-full, roomy
![Pots](elena-taranenko-541565-unsplash.jpg)

# Three Database DevOps Stories

1. One DBA, hundreds of developers, growing the DBA team

???

A.C.

--
2. One DBA, from 20 to 100 developers

???

Zen

--
3. Two database ops folks, seventeen developers

???
The Golden Motion

---
class: img-right-full
![Image](unsplash-photos-6q6qRY2LQJQ.jpg)

# Benefits of Database DevOps

DevOps brings the same benefits to the database as everywhere else.

--

For software delivery performance in particular:

* Faster, better, cheaper---pick all three
* stability -> speed -> stability -> speed

(See the 2018 State of DevOps Report!)

???

Ultimately this lets you work _on_ the system, not _in_ the system.

---
class: img-left-full

![Image](unsplash-photos-6q6qRY2LQJQ.jpg)

# Detriments of Lacking DevOps

Without DevOps, speed and quality suffer:

* Mismatched responsibility and authority
* Overburdened database operations personnel
* Broken feedback loops from production
* Reduced developer productivity

???

* The DBA is responsible for code they can't control
* That leads to them trying to control it, which creates a dependency for devs
* This offloads developer work to the DBA, diverting them from more strategic activities
* That's a shame, because DBAs are often highly skilled and knowledgeable
* So engineering doesn't get the benefit of their input into design, architecture, etc
* Ultimately there's a human in the feedback loop from production to development
* That limits how fast we can learn, fix, and improve
* Developer productivity declines; dependent on DBA to debug

---
# What Is Database DevOps?

Attributes I've seen in companies that apply DevOps to their database:

* Developers own database schema, workload, and performance
* Developers debug, troubleshoot, and repair their own outages
* Schema and data model as code
* A single fully-automated deployment pipeline
* App deployment includes automated schema migrations
* Automated pre-production refresh from production
* Automation of database operations, to an RDS-like level

???

* DBaaS-like automation: provision, backup/restore/test, auth and access, upgrade, scaling...
* Pick any of these. Not all companies do all of these.
* Developers owning database behavior in prod is a big one.
* Charity Majors: the first age of DevOps vs the 2nd age.

---
# From the 2018 State of DevOps Report

> Database changes are often a major source of risk and delay when performing
> deployments... **integrating database work into the software delivery
> process** positively contributed to continuous delivery... good communication
> and comprehensive configuration management that includes the database matter.
> Teams that do well at continuous delivery **store database changes as scripts
> in version control and manage these changes in the same way as production
> application changes**... when changes to the application require database
> changes, **these teams discuss them** with the people responsible for the
> production database

Emphasis mine. See p. 57

---
class: title, smokescreen, no-footer, top
background-image: url(unsplash-photos-C7B-ExXpOIE.jpg)

# Bringing DevOps to the Database

---
class: roomy, img-right-full
![Image](pixabay-en-wood-tree-spruce-picea-conifer-3212803.jpg)

# Core Elements

1. People
2. Culture
3. Structure and Process
4. Tooling

???

* You actually need to start with the people.
* But to understand what that should look like, let's first talk about how their work needs to change.

---
class: roomy
# Tooling: Deploy/Release

* You need frequent, automated deploys
* Eliminate manual work (toil)
* Continuous integration and deployment

???

---
class: roomy
# Tooling: Monitoring and Observability

* Instrumentation, telemetry, analytics, monitoring, observability
* Monitoring: the Seven Golden Signals (CELT + USE)
* Observability is built on these foundations

???

---
class: roomy, img-right
# Tooling: Shared Knowledge and Process

![Deployinator](deployinator.png# minw-100pct)

* DBRE processes, mentality, rubrics
* Deploy confidence procedures
* Documentation to share SME experience & skill
* Notifications should link to runbooks

???
* The DBRE mentality: active measurement of availability and latency, and a strategy to manage them.
* Documentation to share knowledge, it's not just visibility. Runbooks, notebooks, deploy confidence wiki (e.g. GitHub, Etsy). Linking alerts to runbooks.

---
class: roomy
# Structure: Team Orientation

Teams work best when they:

* Are service- or product-oriented
* Are loosely coupled, autonomous
* Are highly aligned and trusted
* Own what they build

My personal experience: Conway's Law is true.

???
* Align teams around services and products, not their work or technology.

---
class: roomy, img-right
# Process: First, Do No Harm

![Image](unsplash-photos-FYrmeWYmR1M.jpg)

* Stabilize the patient, _then_ transport
* Protect production (no holes below the waterline)

???

* Don't automate outages; automation can be weaponized

---
class: roomy, img-right-full

![Image](unsplash-photos-LOHVrTsdvzY.jpg)

# Process: Plan And Roadmap

* Work is work---maintain a single backlog
* Embrace DevOps in small chunks and build on success
* Lay out the progression in stages
* Emphasize what's not changing, too

???

* Present the transformation as small, iterative, prudent
* Have a clear long-term direction to go, to build credibility and buy-in
* This will help get leadership on board too
* Change is stressful; emphasize continuity not just change

---
class: roomy
# Process: Getting Started

Pick a place to start.

* One team
* One app, service, or product
* First new, then established/legacy

???

* Remember, you can start small and add more good over time
* This is key to getting buy-in and continuation

---
class: roomy, img-right-full

![Succulents](edgar-castrejon-459812-unsplash.jpg)

# Culture: Change

* Culture is emergent; you can't operate on it directly
* Create a new path of least resistance
* Include everyone in consequences and benefits

???
* Work on incentives, not culture.

---
class: roomy
# Culture: Leadership Support

* Exec mandate sometimes works; so does attraction
* Starve the old way
* Leadership isn't just top of org chart

???

* Leadership support is required: behavior, not just words.
* "Burn the boats" can work
* Refuse to enable regression to old habits
* Make nonparticipation low-status
* You need champions at all levels

---
class: img-right-full

![Compass](aaron-burden-523450-unsplash.jpg)

# Culture: Communication and Trust

* Align around a North Star: a simple, compelling _why_
* Customer-centric culture, customer empathy
* Psychological safety enables risk-taking

???

* Trust is earned over time by keeping promises
* Strong product team culture; trust; communication
* Inclusion; share the pain

---
class: roomy
# People: You Need Experts

* You do need database expertise
* You do not need a database caretaker
* Engineers can learn database competency

???

* Redefine DBA, or NoDBA
* Education is important, your people are smart but that's not sufficient

---
class: title, fogscreen, no-footer, bottom
background-image: url(pixabay-en-pond-water-shield-dead-end-yellow-3776437.jpg)

# Pathways To Failure

---
class: roomy
# Tooling FAIL

* Fragile or too-ambitious automation
* Lack of automation / accepting manual toil
* Two routes to production---code vs DB

???

* You do need good tooling
* Poor tooling just causes more problems

---
class: roomy
# Culture FAIL

* Any friction in the way of change
* Failure to create incentives to change
* Relying on a vendor to bring culture
* Insisting on adherence to One True Way
* Clinging to legacy DBA roles and duties

---
class: img-right
# Aside: Legacy DBA Roles

![Silvia](silvia.jpg# br-100pct center ba)

> In a traditional sense, the job of the DBA means she is the only person with access to the servers that host the data, the go-to person to create new database cluster for new features, the person to design new schemas, and the only person to contact when anything database related breaks in a production environment.

--- [Silvia Botros, SendGrid](https://sendgrid.com/blog/dbas-a-priesthood-no-more/)

???
Change from DBA to DBRE instead. The database "subject matter expert," rather than the database babysitter.

---
class: roomy
# Leadership FAIL

* Underinvesting in experience and skill
* Lack of management support
* Micromanagement, failure to manage up

See also my [Kafka Summit talk](/talks/kafka-summit-2018-advocate-technical-decisions-to-manager/) on advocating technical decisions.

---
class: roomy, img-right-full

![Speed](alessio-lin-236486-unsplash.jpg)

# Planning FAIL

* All-or-nothing
* Too much too fast
* Velocity over resilience

---
class: title, fogscreen, no-footer
background-image: url(pixabay-en-maze-graphic-render-labyrinth-design-puz-2264.jpg)
# What's The Hardest Part?

---
class: roomy
# Challenge: Politics

* Selling DevOps to the DBA
* Selling DevOps to leadership
* Creating culture change

---
class: roomy
# Challenge: Tooling

* Legacy databases aren't cloud-native
* Data tier ops tooling isn't as mature
* Schema changes
* Integration with e.g. canary deploys, feature flags

---
class: roomy
# Challenge: HA, Scale, Performance

* Failover and recovery
* Locking/blocking
* Nonblocking schema changes at scale

---
class: roomy
# Whither The DBA?

* Become a DBRE instead of a DBA
* Focus on data platform and architecture
* Be the subject matter expert supporting product teams

---
class: roomy, img-right-full

![Image](cassidy-phillips-695625-unsplash.jpg)

# The Rewards

* The outcomes
* The process itself
* Individual benefits

???

* DraftKings.
* At the "end," but also: the process itself
* As a team: better DB awareness, more tooling
* Individuals get broader skills and ability to be more valuable
* As an org, you get flexibility, reduced potholes and bottlenecks.
* Even small steps are improvements.
* Common theme of DevOps, Agile etc you don't have to do all of it, do what parts make sense. "just get started" tone; don't fear the database

---
class: roomy
# Acknowledgments

Many people contributed to this talk. Thank you.

(When I get their OK I will add their names.)

???

Jessica Kerr, Silvia Botros, Charity Majors, Laine Campbell, Nicole Forsgren PhD, too many VividCortex customers and friends to mention, and the 50+ survey respondents.

---
class: roomy
# Slides and Contact Information

.qrcode.db.fr.w-40pct.ml-4[]

Slides are at https://www.xaprb.com/talks/ or you can scan the QR code.

Contact: baron@vividcortex.com, @xaprb

---
class: roomy
# Appendix: Survey

I asked my Twitter followers to respond to an informal, nonscientific survey.
The following two slides summarize some of the quantitative feedback.

---
class: compact
# Survey Results

How important are each of the following in your view of "Database DevOps"?

![Survey 2](DevOps-Survey-2.svg# maxw-70pct center)

---
class: compact
# Survey Results Cont'd
How do you rate the importance of these factors in making progress?

![Survey 1](DevOps-Survey-1.svg# maxw-70pct center)

---
# Resources

* [The Phoenix Project](https://www.amazon.com/dp/1942788290/)
* [Database Reliability Engineering](https://www.amazon.com/dp/1491925949/)
* The [2018 DORA State of DevOps Report](https://cloudplatformonline.com/2018-state-of-devops.html)
* [Three Steps To Psychological Safety](/blog/three-steps-to-psychological-safety/)
* My [Kafka Summit talk](/talks/kafka-summit-2018-advocate-technical-decisions-to-manager/) on advocating technical decisions
