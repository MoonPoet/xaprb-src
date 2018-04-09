---
title: "Open Tools for MySQL Administrators"
date: "2006-10-19"
categories:
  - Databases
  - Guest Posts
---

*This post originally appeared on [O'Reilly's blog](http://archive.oreilly.com/pub/a/mysql/2006/10/19/mysql-tools.html).*

*This post originally appeared on [O’Reilly’s blog](http://archive.oreilly.com/pub/a/mysql/2006/10/19/mysql-tools.html).*

[MySQL](http://www.mysql.com/) provides some tools to monitor and troubleshoot a MySQL server, but they don't always suit a MySQL developer or administrator's common needs, or may not work in some scenarios, such as remote or over-the-web monitoring. Fortunately, the MySQL community has created a variety of free tools to fill the gaps. On the other hand, many of these are hard to find via web searches. In fact, web searches can be frustrating because they uncover abandoned or special-purpose, not ready-to-use projects. You could spend hours trying to find tools for monitoring and troubleshooting your MySQL servers. What's a tool-seeker to do?

Relax! I've already done the work, so you won't have to. I'll point you to the tools I've actually found useful. At the end of this article I'll also list those I didn't find helpful.

This article is about tools to discover and monitor the state of your server, so I won't discuss programs for writing queries, designing tables, and the like. I'm also going to focus exclusively on free and open source software.

### Tools to Monitor Queries and Transactions

The classic tool for monitoring queries is [Jeremy Zawodny's mytop](http://jeremy.zawodny.com/mysql/mytop/). It is a Perl program that runs in a terminal and displays information about all connections in a tabular layout, similar to the Unix `top` program's process display. Columns include the connection ID, the connection's status, and the text of the current query. From this display you can select a query to `EXPLAIN`, kill a query, and a few other tasks. A header at the top of the display gives information about the server, such as version, uptime, and some statistics like the number of queries per second. The program also has some other functions, but I never found myself using them much.

There are mytop packages for various GNU/Linux distributions, such as Gentoo and Fedora Core, or you can install one from Jeremy's website. It is very small and has minimal dependencies. On the downside, it hasn't been maintained actively for a while and doesn't work correctly with MySQL 5.x.

A similar tool is [mtop](http://mtop.sourceforge.net/). It has a tabular process display much like mytop, and although it lacks some features and adds others, the two programs are very similar. It is also a Perl script and there are installation packages for some operating systems, or you can download it from SourceForge. Unfortunately, it is not actively maintained and does not work correctly on newer versions of MySQL.

Some programmers have also created scripts to output MySQL's process list for easy consumption by other scripts. An example is this [SHOW FULL PROCESSLIST](http://forge.mysql.com/snippets/view.php?id=38) script, available from the always-useful [MySQL Forge](http://forge.mysql.com/).

My own contribution is [innotop](/blog/2006/07/02/innotop-mysql-innodb-monitor/), a MySQL and InnoDB monitor. As MySQL has become increasingly popular, InnoDB has become the most widely used transactional MySQL storage engine. InnoDB has many differences from other MySQL storage engines, so it requires different monitoring methods. It exposes internal status by dumping a potentially huge amount of semi-formatted text in response to the `SHOW INNODB STATUS` command. There's a lot of raw data in this text, but it's unusable for real-time monitoring, so I wrote innotop to format and display it conveniently. It is the main monitoring tool at my current employer.

Innotop is much more capable than the other tools I've mentioned, and can replace them completely. It has a list of processes and status information, and offers the standard functions to kill and explain queries. It also offers many features that are not in any other tool, including being able to list current transactions, lock waits, deadlock information, foreign key errors, I/O and log statistics, InnoDB row operation and semaphore statistics, and information on the InnoDB buffer pool, memory usage, insert buffer, and adaptive hash index. It also displays more standard MySQL information than mytop and its clones, such as compact, tabular displays of current and past status information snapshots. It is very configurable and has interactive help.

Installation is simple, because innotop is a ready-to-run Perl script, but there are no installation packages yet, so you must download it from my website.

There are also some web-based tools. There are two web-based mytop clones, [phpMyTop](http://sourceforge.net/projects/phpmytop/) and [ajaxMyTop](http://sourceforge.net/projects/ajaxmytop/). These are useful when you don't have shell access and can't connect remotely to your database server, but can connect from a web server. ajaxMyTop is more recent and seems to be more actively developed. It also feels more like a traditional GUI program, because thanks to Ajax, the entire page does not constantly refresh itself.

Another web-based tool is the popular [phpMyAdmin](http://www.phpmyadmin.net/home_page/) package. phpMyAdmin is a Swiss Army Knife, with features to design tables, run queries, manage users and more. Its focus isn't on monitoring queries and processes, but it has some of the features I've mentioned earlier, such as showing a process list.

Finally, if you need to monitor what's happening inside a MySQL server and don't care to--or can't--use a third-party tool, MySQL's own `mysqladmin` command-line program works. For example, to watch incremental changes to the query cache, run the command:

    mysqladmin extended -r -i 10 | grep Qcache

Of course, innotop can do that for you too, only better. Take a look at its "V" mode. Still, this can be handy when you don't have any way to run innotop.

### Tools to Monitor a MySQL Server

Sometimes, rather than monitoring the queries running in a MySQL server, you need to analyze other aspects of the system's performance. You could use standard command-line utilities to monitor the resources used by the MySQL process on GNU/Linux, or you could run [Giuseppe Maxia's](http://datacharmer.org/) helpful script to [measure MySQL resource consumption](http://www.perlmonks.org/?node_id=559540). This tool recursively examines the processes associated with the MySQL server's process ID, and prints a report on what it finds. For more information, read [Giuseppe's own article on the O'Reilly Databases blog](http://www.oreillynet.com/databases/blog/2006/07/measuring_resources_for_a_mysq_1.html).

The MySQL Forge website is an excellent place to discover tips, tricks, scripts, and code snippets for daily MySQL administration and programming tasks. For example, there's an entry to help you measure replication speed, a "poor man's query profiler" to capture queries as they fly by on the network interface, and much more.

Another excellent resource is [mysqlreport](http://hackmysql.com/mysqlreport), a well-designed program that turns MySQL status information into knowledge. It prints out a report of relevant variables, sensibly arranged for an experienced MySQL user. I find this tool indispensable when I have to troubleshoot a server without knowing anything about it in advance. For example, if someone asks me to help reduce load on a MySQL server that's running at 100 percent CPU, the first thing I do is to run mysqlreport. I can get more information by glancing at its output than I could in 10 minutes of talking to the customer. It immediately tells me where to focus my efforts. If I see a high key read ratio and a high percentage of index scans, I can immediately look for large indexes and a key buffer that's too small. That intuition could take many minutes to develop just by examining `SHOW STATUS`.

The mysqlreport website has full information on how to install and use the program, but better yet, there are excellent tutorials on how to interpret its output, with real examples. Some of these go into detail on MySQL internals, and I recommend them to any MySQL developer.

Another common task is setting up automated systems to monitor your server and let you know if it's alive. You could write your own monitor, or you could just plug in a ready-made one. According to a [MySQL poll](http://dev.mysql.com/tech-resources/quickpolls/monitoring-software.html), [Nagios](http://www.nagios.org/) is the most popular tool for doing this. There's also a [Watchdog mysql monitor plugin](http://search.cpan.org/~clemensg/Watchdog-0.10/bin/mysql.monitor) for [mon](http://www.kernel.org/software/mon/), the Linux scheduling and alert management tool. We currently use a home-grown system at my employer, but we're looking at using Nagios soon.

### Tools I Didn't Find Useful

The [Quicomm MySQL Monitor](http://www.quicomm.com/mysql_monitor_descript.htm) is a web-based administration tool similar to phpMyAdmin, not a monitor in the same sense as mytop or innotop. It offers relatively few features compared to phpMyAdmin.

Another web-based tool is [MySysop](http://www.fillon.org/mysysop/), which is billed as a "MySQL system optimizer", though it certainly doesn't do anything on its own to optimize a MySQL system. It offers recommendations I would not trust without doing enough investigation to arrive at the same conclusions. By the time I could install and run this system, I'd have long since run mysqlreport.

Finally, I've never understood how to even use the [Google mMaim (MySQL Monitoring And Investigation Module)](http://goog-mmaim.sourceforge.net/). It is part of Google's open source code contributions, and Google probably uses it internally to monitor its servers. However, it's not obvious to the rest of the world how to do this, as evidenced by the mailing list. The mailing list also reveals that Google released the code simply for the sake of releasing it. While I appreciate the gesture, I can't find any use for the code.

### Conclusion

If you're trying to find tools for your own work, I recommend innotop and mysqlreport, and a healthy dose of command-line competence. I used to rely on mytop for my routine monitoring, but now I use innotop, because it shows much more information, including all-important details about transactions. When I need to analyze a server to discover what's wrong with it, it's impossible to match mysqlreport's instant snapshot of server health and activity. When I need to know about MySQL's resource consumption and performance, I augment standard command-line utilities with scripts, such as Giuseppe Maxia's.

There are certainly other tools, but the ones mentioned here are free and open source, have nearly every feature you can find in other tools, and do a lot you can't find elsewhere at all.

### Related Links

1. [innotop](/blog/2006/07/02/innotop-mysql-innodb-monitor/), the most powerful MySQL and InnoDB monitor
2. [mysqlreport](http://hackmysql.com/mysqlreport), a tool to make easy-to-ready MySQL status reports
3. [MySQL Forge](http://forge.mysql.com/), a place where the MySQL community shares code snippets with one another
4. [mytop](http://jeremy.zawodny.com/mysql/mytop/), the classic tool for monitoring MySQL queries and processes
