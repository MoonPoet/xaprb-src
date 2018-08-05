---
title: Why is Embarq hijacking my DNS?
date: "2007-11-23"
url: /blog/2007/11/23/why-is-embarq-hijacking-my-dns/
categories:
  - Commentary
---
Isn't this the same thing that happened a few years ago with ICANN or Verisign or one of those big names?  (strangely, I can't find relevant search results about this!).

I clicked on my toolbar shortcut for [Toggl](http://www.toggl.com/) and my Embarq DSL service redirected me to a search-results page instead of telling my browser the truth.  This makes me *mad*.  The core layers of the Internet are designed the way they are **for a reason** and I don't want to "opt out" of a stupid DNS hijacking stunt I never opted into.

Here's a screenshot of what happens when I type in any old non-existent (or, in Toggl's case, timing-out) domain name.

![Embarq screwing with my DNS](/media/2007/11/embarq-sysbench.png)

And here's what happens when I do a DNS lookup:

```
baron@kanga:~$ dig www.toggl.com

; <<>> DiG 9.4.1-P1 <<>> www.toggl.com
;; global options:  printcmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 27795
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;www.toggl.com.                 IN      A

;; ANSWER SECTION:
www.toggl.com.          22      IN      A       66.199.249.106

;; Query time: 72 msec
;; SERVER: 208.33.159.39#53(208.33.159.39)
;; WHEN: Fri Nov 23 15:50:14 2007
;; MSG SIZE  rcvd: 47

baron@kanga:~$ ping www.toggl.com
PING www.toggl.com (66.199.249.106) 56(84) bytes of data.
64 bytes from 66-199-249-106.reverse.ezzi.net (66.199.249.106): icmp_seq=1 ttl=53 time=79.2 ms
```

Did I mention that this makes me mad?  Time to get on the phone.

PS: it looks like [Verizon](http://www.consumeraffairs.com/news04/2007/11/verizon_search.html) is doing it too.
