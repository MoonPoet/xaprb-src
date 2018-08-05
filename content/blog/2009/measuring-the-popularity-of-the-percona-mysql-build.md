---
title: Measuring the popularity of the Percona MySQL build
date: "2009-02-19"
url: /blog/2009/02/19/measuring-the-popularity-of-the-percona-mysql-build/
categories:
  - Databases
---
I have a Google Alert on "percona". (And many other things---great way to keep tabs on competitors, what people are saying about you, etc.)

I've been seeing increasing amounts of this type of thing:

```
MySQL server version: 5.0.67-percona-3 CATEGORY QUERY: SELECT wp_term_taxonomy.count as 'count', wp_terms.term_id, wp_terms.name, wp_terms.slug, wp_term_taxonomy.parent, wp_term_taxonomy.description FROM wp_terms, wp_term_taxonomy WHERE ... 
```

Go to the page in question (sorry, I won't link it) and you don't see "percona" anywhere on it. View the source and you do. It's WordPress debugging output.

I'm glad to see the anecdotal evidence of more and more active use of the [Percona server builds](http://www.percona.com/percona-lab.html), but at the same time, it's kind of like finding out that your best friend made it onto the Jerry Springer Show. Sometimes I think WordPress makes things too easy for novices.


