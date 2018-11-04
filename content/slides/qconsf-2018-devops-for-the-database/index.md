---
title: 'DevOps for the Database '
date: "2018-11-05"
url: "slides/qconsf-2018-devops-for-the-database/"
image: "slides/qconsf-2018-devops-for-the-database/cover.jpg"
description: "Why is it hard to apply DevOps principles and practices to databases, and how can we get better at it? This talk explores real-life stories that answer these two questions, through the perspectives of teams that succeeded---and those who haven't."
ratio: "16:9"
themes:
- apron
- adirondack
- descartes
---
class: title
background-image: url(unsplash-photos-oyXis2kALVg.jpg)

# DevOps for the Database
## Baron Schwartz &bullet; QConSF 2018

???
Why is it hard to apply DevOps principles and practices to databases, and how can we get better at it? This talk explores real-life stories that answer these two questions, through the perspectives of teams that have changed the entrenched culture, processes, and tooling—and those who’ve tried. Along the way, we’ll cover topics including:
* What the research shows about DevOps, databases, and company performance
* Current and emerging trends in how we build and manage data tiers, and implications
* The traditional dedicated DBA role, and what has happened as a result
* What it takes to change from a DBA-centric culture, to one where database-related competencies and responsibilities are more distributed
* Why some teams succeed in this transformation, while others fail
We can apply DevOps principles to the database, and our work will be better for it. This talk will show you how.

---

* Introduction
* Agenda
* Motivating stories:
	* Gawker Media, our first DevOps customer
	* Zenefits
	* Active Campaign, Scaling too fast
	* The “golden motion” we tried to repeat
	* We saw some success, some failure
	* <- survey anecdotes
* What are benefits
	* Look at DORA [2018 State of DevOps Report](https://cloudplatformonline.com/2018-state-of-devops.html)
	* Faster, better, AND cheaper, pick all three
	* speed -> stability -> speed
	* Agile, Design Thinking, Lean
	* We typically see infra-as-code, CI, CD, monitoring; in other words ops is doing dev. Charity: 2nd age is devs doing ops.
* What is DDB?
	* Schema as code; data model is part of the app, versioned and no manual scripting; automated schema migrations
	* Developer ownership of database schema, workload, and performance
	* Pre-prod can be provisioned/refreshed automatically; reproducible
	* Schema and code go through the same pipeline to get to prod and are delivered together
	* Automation of provisioning, backup, restore and testing, auth and access control, upgrade, scaling, etc without SSH; basically DBaaS and self-service
	* Developers can troubleshoot and repair their own database outages, including restoring from backups
* What happens if no DDB?
	* auth/resp mismatch, “run this code you can’t control.”
	* broken feedback loop between dev and prod
	* overwhelmed DBA, a strategic asset wasted
	* unproductive developers, asking someone else to debug their code
* How do companies achieve it?
	* Either redefine DBA, or noDBA; no separate dedicated DBA role
	* Engineers own the database performance; developer autonomy
	* Work on incentives, not culture. Create a new path of least resistance
	* Align teams around services and products, not their work or technology.
	* Tooling. You need automation, especially CI, CD, monitoring (DB-specific dashboards). leverage what devs and ops have already built
	* Database expertise
	* A mandate from leadership, paired with refusal to enable the old way, paired with champions in development, like senior engineers. Burn the boats. YBYO
	* Education. Engineers can learn what databases are and what their metrics mean, if you teach them.
	* Start with new deployments, migrate established systems later
	* Work backwards from “protect production” standpoint on all automation; 
	* Embrace DevOps approach fully, deliver smaller chunks faster
	* Start with the people
	* Strong product team culture; trust; communication
	* Inclusion; share the pain
	* Frequent deploys
	* A plan and roadmap with stages everyone can see and agree/disagree
	* Perseverence
	* 
* What do companies try that leads to failure?
	* creating two routes to prod, one for code and one for DB, where DB has their own shadow DevOps toolchain
	* Clinging to DBA. “In a traditional sense, the job of the DBA means she is the only person with access to the servers that host the data, the go-to person to  create new database cluster for new features, the person to design new schemas, and the only person to contact when anything database related breaks in a production environment.” - Silvia. Change from DBA to DBRE instead. The database “subject matter expert,” rather than the database babysitter.
	* Relying on a vendor to bring in culture with tooling
	* Under-investing to support growth; need experienced, skilled people to execute it well; need good tooling
	* Assuming people will change without incentive
	* Lack of management buy-in
	* Micromanagement
	* Insisting on One True Way and complete adherence to that
	* Fragile automation, or automation that tries to do too much; poor tooling
	* Any friction or hurdle; people will develop workarounds
	* Pushing for velocity over resilience; pushing for too much too fast
	* Specialized roles, silos
	* Manual work / toil
* What are the hardest parts?
	* Schema changes / migrations, especially at scale and without locking
	* Politics and culture; getting DBAs to give up control; getting DBAs to embrace DevOps
	* Scaling challenges
	* High availability / failover
	* Advocating for change; getting buy-in; marketing your ideas
	* Blue/green and canary deploys combined with schema changes
	* Recovery from failures
	* Relational databases weren’t built for cloud-native operations
	* Tooling is much less mature than devops tooling for stateless 
* What’s required?
	* [look at the what works list, some of that goes here]
	* Leadership, culture, communication, trust, autonomy, buy-in
	* Expertise, skill, experience
	* Monitoring
	* Tooling
	* A plan
	* Documentation to share knowledge, it’s not just visibility. Runbooks, notebooks, deploy confidence wiki at GitHub. Linking alerts to runbooks.
	* The DBRE mentality: active measurement of availability and latency, and a strategy to manage them.
	* Psychological safety
* What happens to the DBA?
	* becomes a DBRE
	* focuses on data architecture and building data platform (not running servers)
	* Becomes a DB subject matter expert, supporting the product team with things like optimizations
* What’s unsolved, next steps?
	* Schema changes
		* Page No 57 Database changes are often a major source of risk and delay when performing deployments… integrating database work into the software delivery process positively contributed to continuous delivery… good communication and comprehensive configuration management that includes the database matter. Teams that do well at continuous delivery store database changes as scripts in version control and manage these changes in the same way as production application changes… when changes to the application require database changes, these teams discuss them with the people responsible for the production database 
	* Failovers
	* Better integration with deploy and release practices like canaries, feature flags
* Conclusions / Stories
	* A concluding story of what companies have gotten out of this. DraftKings. At the “end,” but also: the process itself. You get better DB awareness, more tooling for people, as a team. And individually, you get broader skills and ability to be more valuable. As an org, you get flexibility, reduced potholes and bottlenecks.
	* Even small steps are improvements.
	* Common theme of DevOps, Agile etc you don’t have to do all of it, do what parts make sense. “just get started” tone; don’t fear the database


---
class: col-2
# Slides and Contact Information

Slides are at https://www.xaprb.com/talks/ or you can scan the QR code.

Contact:

.qrcode.db.fr.w-40pct.ml-4[]

---
* Survey Results
	* 
* Resources
	* Phoenix Project
	* DBRE book
	* Strategic DBA ebook
	* DORA report
	* Datical, Liquibase, Skeema, Orchestrator, Vitess, gh-ost
	* Silvia’s article https://sendgrid.com/blog/dbas-a-priesthood-no-more/
	* [The DataOps Manifesto](http://dataopsmanifesto.org/)