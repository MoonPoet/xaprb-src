---
title: 'Engineering The Application/Database Boundary'
date: "2018-04-24T04:54:46-07:00"
url: "/slides/engineering-application-database-boundary/"
image: "/slides/engineering-application-database-boundary/da-vinci.jpg"
description: "What's so special about the interactions between applications and databases?"
ratio: "16:9"
theme: "monobloc"
---
class: title, no-number
background-image: url(da-vinci.jpg)
background-size: cover

.smokescreen[
# Engineering The Application/Database Boundary 
## Baron Schwartz &bullet; Percona Live 2018
]

<div style="position: absolute; right: 10px; top: 10px; width: 250px;
background-color: rgba(0,0,0,.7); padding: 10px; border-radius: 10px">
<img src=vividcortex-horizontal-white-rgb.svg>
</div>

---
layout: true
<div class="remark-slide-number" style="left: 20px; right: unset">@xaprb</div>

---
class: img-right
# Logistics and Stuff
.col[
- Ask questions anytime
- Write me baron@vividcortex.com
- Tweet me at @xaprb
- Slides at [xaprb.com/talks/](https://www.xaprb.com/talks/)
]
.rc[
![Baron Schwartz](headshot.jpg)
]

---
class: img-right
.col[
# Introduction and Agenda
* Why this talk?
* The boundary region
* Ephemeral vs persistent
* Atoms and molecules
* Who builds that code?
* The declarative zone
* Specialization
* Challenges and solutions
]
.rc[
![Agenda](agenda.jpg)
]

---
class: title
background-image: url(velazquez.jpg)
background-size: cover
.smokescreen[
# Motivations
]

---
class: img-right
.col[
# Who Are You And Whatcha Want?
* You probably aren’t appreciated fully
* Do people even know what you do??
]
.rc[
![Assumption](assumption.jpg)
]
???
* I used to have a neighbor who answered the phone this way
* A step back to gain perspective
* As Kenny Chesney says, "I've been there, that's why I'm here"

---
class: title
background-image: url(schloss.jpg)
background-size: cover
<div class="smokescreen" style="top:20px">
<h1>You Tend The Gardens and Courts</h1>
</div>
???
* You don’t guard the moat
* You help people find their way through the thorns they don’t see
---
class: title
background-image: url(sabine.jpg)
background-size: cover
<div class="smokescreen" style="top:67%">
<h1>The Application/Database Boundary</h1>
</div>
---
class: img-right
.col[
# A Region, Not A Crisp Line
* More like a zone than a boundary
* Permits adaptation and coupling
* Sort of like a demilitarized zone, but not
]
.rc[
![Joseph Interpreter of Dreams](joseph-potiphar-wife.jpg)
]
???
* Where impedance mismatches crossfade
* Where dreams have to be interpreted
* Opposite of DMZ: it’s where we agree to put the bad stuff
---
class: img-right
.col[
# Ephemeral vs Persistent
* Stateless above, stateful below
* Statefulness is contained
* Stateless systems are more manageable
]
.rc[
![Archangel Michael](michael-rebel-angels.jpg)
]
???
* The DMZ lets us build stateless tiers
* The web and services tiers are two good examples
---
class: img-right
.col[
# Atoms And Molecules
* Below the boundary is hardened primitives
* Databases, filesystems, drivers, kernels...
]
.rc[
![Adam Names Animals](f5r.jpg)
]
???
* These simple primitives enable rich business logic
* Below: atoms. Boundary: molecules. Above: algae.
---
class: img-right
.col[
# Who Builds That Code?
* Above the boundary is mostly custom code
* Above is Turing-complete
* Below is sealed boxes: voids the warranty
* The area in between is kind of hybrid
]
.rc[
![Cobbler](cobbler.jpg)
]
???
* We don’t run much custom code for bits-on-disk
* Above we build, below we configure
* Above is art, below is science
---
class: img-right
.col[
# The Zone of Declarative
* This is where iptables config lives
* This is where schema and indexes live
* This is where SQL runs
]
.rc[
![Nightmare](nightmare.jpg)
]
???
* The boundary zone is partially sealed, partially customizable
* This is where we design, model, and structure
* Where we give simple instructions to systems that interpret them in complex ways
---
class: img-right
.col[
# Why We Specialize
* Enables expertise and productivity
* Limits the problem/solution space
* Creates coupling and dependency
* A tradeoff best made intentionally
]
.rc[
![Blacksmith](The-Blacksmith.jpg)
]
???
* For as long as we’ve had hard jobs, we’ve specialized
* We specialize both our tools and our skills
* Specialized work is hard work: consistency, durability, persistence, performance
* But it helps us make our problems more tractable
* Divide and conquer
---
class: title
background-image: url(damned.jpg)
background-size: cover
.smokescreen[
# Challenges
]
---
class: img-right
.col[
# Performance
* Database performance problems are common
* And often hard to diagnose and solve
]
.rc[
![School of Athens](school-of-athens.jpg)
]
???
* The other tradeoffs naturally lead to database performance issues
---
class: img-right
.col[
# Specialization
* Dependency for flow of work
* Gatekeeper for knowledge and expertise
* Data inertia
* Single points of failure
]
.rc[
![Supplicant](jerome-supplicant.jpg)
]
???
* We end up createing bottlenecks in systems
* and in teams
* and in mutating our systems
* and in fixing them
---
class: img-right
.col[
# Rigidity
* It’s hard to fine-tune something without making it inflexible
* *Why* is that config option set to a nondefault value?
]
.rc[
![Look behind you but don't make it obvious](bending-backwards.jpg)
]
---
class: img-right
.col[
# Observability
* Highly optimized systems are built for speed, not observability
* Paradoxically, observability is the single best optimization
]
.rc[
![Astronomer](gerrit-dou-astronomer.jpg)
]
---
class: img-right
.col[
# Absorption In The System
* You can focus on the system until you forget who it’s for
* It’s a slippery slope from there to superstition and vanity metrics
]
.rc[
![Vanity](melancholy.jpg)
]
???
* If you want to know about the commute measure the traffic, not the road
---
class: title
background-image: url(cabrera.jpg)
background-size: cover
.smokescreen[
# Conclusions
]
---
class: img-right
.col[
# Keep It Simple
]
.rc[
![Wine](wine.jpg)
]

---
class: img-right
.col[
# Share The Load
]
.rc[
![Fire Brigade](fire-brigade.jpg)
]

???
- Don't let the database problems be just your problems.
- Make everyone responsible for database health and performance
- That requires shared visibility and observability

---
class: img-right
.col[
# Choose Your Battles
]
.rc[
![The Storm](1880_Pierre_Auguste_Cot_-_The_Storm.jpg)
]

---
class: img-right
.col[
# You're Awesome
]
.rc[
![DuCreux](ducreux1.jpg)
]

---
class: three-column
# Resources

.col[
[![Database Reliability Engineering](smartmockups_jgdsglb7.jpg)](https://www.amazon.com/Database-Reliability-Engineering-Designing-Operating/dp/1491925949?tag=xaprb-20)
]
.col[
[![Production-Ready Microservices](smartmockups_jgdsp7xk.jpg)](https://www.amazon.com/Production-Ready-Microservices/dp/1491965975?tag=xaprb-20)
]
.col[
[![Principles of Product Development Flow](smartmockups_jgdsudi9.jpg)](https://www.amazon.com/Principles-Product-Development-Flow/dp/B00K7OWG7O?tag=xaprb-20)
]

---
class: two-column
# Slides and Contact Information

.col[
Slides are at https://www.xaprb.com/talks/ or you can scan the QR code. To export as PDF, print with Chrome.

License: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

Contact: @xaprb and baron@vividcortex.com
]

.col[
<div id="qrcode"></div>
]
