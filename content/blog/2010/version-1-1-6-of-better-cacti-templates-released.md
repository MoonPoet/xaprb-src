---
title: Version 1.1.6 of Better Cacti Templates released
date: "2010-01-10"
url: /blog/2010/01/10/version-1-1-6-of-better-cacti-templates-released/
categories:
  - Monitoring
  - Databases
  - Operations
  - Programming
tags:
  - PostgreSQL
---
I've released version 1.1.6 of the [Better Cacti Templates](http://code.google.com/p/mysql-cacti-templates/) project. This release includes a bunch of bug fixes (but not all of them!) and two new sets of graphs. One set is for disk I/O on GNU/Linux, and the other is a new set of templates for OpenVZ. I'm looking for feedback on both of those. This release also has a bunch of code-level features: much better test coverage (hooray!), and a refactored `ss_get_by_ssh.php` that makes it much easier to create new graphs and templates. The SSH-based templates also take advantage of the same caching as the MySQL templates, which makes them a lot more efficient.

There are [upgrade instructions](http://code.google.com/p/mysql-cacti-templates/wiki/UpgradingTemplates) on the project wiki for this and all releases. There is also a comprehensive tutorial on [how to create your own graphs and templates](http://code.google.com/p/mysql-cacti-templates/wiki/CreatingGraphs) with this project. Use the [project issue tracker](http://code.google.com/p/mysql-cacti-templates/issues/list) to view and report issues, and use the [project mailing list](http://groups.google.com/group/better-cacti-templates) to discuss the templates and scripts.

The full changelog follows.

```
2010-01-10: version 1.1.6

  * Added OpenVZ graphs (--type openvz) (issue 95).
  * Added IO usage graphs (--type diskstats) (issue 97).
  * Added extra error-reporting (issue 110).
  * The $debug $debug_log options couldn't be set in the .cnf file (issue 110).
  * Added a --use-ssh option to ss_get_by_ssh.php (issue 66).
  * Added a debugging log to ss_get_by_ssh.php (issue 54).
  * Enabled caching of results in ss_get_by_ssh.php (issue 46).
  * Added a test suite for ss_get_by_ssh.php (issue 110).
  * The 'free' stats suffered from PHP's issues with big numbers (issue 102).
  * There was ambiguity (but no error) in SHOW STATUS overrides (issue 106).
  * It was hard to debug failures caused by missing ext/mysql (issue 105).
  * Code to make ss_get_mysql_stats.php testable was broken (issue 108).
```


