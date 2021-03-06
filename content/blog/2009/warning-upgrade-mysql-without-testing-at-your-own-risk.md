---
title: "Warning: upgrade MySQL without testing at your own risk"
date: "2009-08-08"
url: /blog/2009/08/08/warning-upgrade-mysql-without-testing-at-your-own-risk/
categories:
  - Databases
  - Open Source
---
Do you test your application systematically when you upgrade or reconfigure your database server? You should! Here's a real (anonymized) story of what happens if you don't.

> When we upgraded to 5.0.62 (from 5.0.27 and 5.0.45), our code broke for queries like this:
> 
> `SELECT SUM(amt) FROM daily_amt
WHERE day = FROM_UNIXTIME(1222889772);`
> 
> The problem here was a [wrong DATE/DATETIME comparison](http://bugs.mysql.com/bug.php?id=27590) and other bug fixes in MySQL 5.0.62; it was stricter in enforcing the comparison.
> 
> This resulted in an outage and revenue loss to the company.

Daniel and I (mostly Daniel) continue to improve [mk-upgrade](http://code.google.com/p/maatkit/wiki/mk_upgrade) to make it easy and inexpensive to find these kinds of scenarios *before* they bite you. Don't get caught with your pants down---next time you make *any* major change to your database server (upgrade, configuration change, switching to InnoDB...) follow at least this bare-minimum process:

*   collect all queries run against the server for a sufficient time
*   get a snapshot of your data
*   use mk-upgrade to validate correctness and performance
*   [submit bug reports](http://code.google.com/p/maatkit/issues/list)---this is a non-trivial tool, and we need your feedback

If you need help with any of the above, I know [someone](http://www.percona.com/services/mysql-database-server-upgrade.html) who can help.


