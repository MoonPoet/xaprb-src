---
title: "Approaching the Unacceptable Workload Boundary"
date: 2018-03-29T11:25:00-07:00
event: "USENIX SREcon18 Americas"
location: "Hyatt Regency Santa Clara, 5101 Great America Parkway, Santa Clara, CA 95054, USA"
site: "https://www.usenix.org/conference/srecon18americas/presentation/schwartz"
image: /slides/srecon-approaching-unacceptable-workload-boundary/action-balance-fun-305250.jpg
slides: /slides/srecon-approaching-unacceptable-workload-boundary/
thumbnail: /slides/srecon-approaching-unacceptable-workload-boundary/thumbnail.jpg
video: "https://www.youtube.com/watch?v=8omPFYif3J8"
description: "What happens to systems as they approach saturation? Understanding this highly nonlinear region offers the key to avoiding it and building more scalable, resilient systems."
---
We've all stared in frustration at a system that degraded into nonresponsiveness, to the point that you couldn't even kill-dash-nine whatever was responsible for the problem. A key fact we all recognize, but may not recognize as significant, is that this isn't a sharp boundary. There's a gradient of deteriorating performance where the system becomes less predictable and stable.

<!--more-->

In this talk I'll explain

- what the unacceptable workload boundary is
- how to recognize and predict the signs
- how to measure and model this simply
- what causes nonlinear performance degradation
- how to use this to architect more scalable systems
