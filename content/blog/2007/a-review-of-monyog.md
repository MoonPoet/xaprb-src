---
title: A review of MONyog
date: "2007-05-25"
url: /blog/2007/05/25/a-review-of-monyog/
categories:
  - Databases
---
This is a review of Webyog's [MONyog](http://www.webyog.com/) MySQL monitoring tool.  The product is still in beta and has some rough edges, but holds promise.  Its design includes some interesting architectural decisions I think will help distinguish it from MySQL's own Monitoring and Advisory Service.

### MONyog overview

MONyog starts an HTTP listener on your machine.  After you start the program, you point your Web browser at localhost:9999.  Your browser talks to MONyog, which talks to one or many MySQL servers.  My impression is that MONyog is meant to be a nearly zero-footprint desktop install you'll put on your own desktop machine, and monitor remote servers.  In other words, you don't install it on the servers you'll monitor.

It initially prompts you for connection information, which it saves for the future.  After you create and select a connection, MONyog starts watching the MySQL instance.  As far as I can see, it just retrieves `SHOW STATUS` and `SHOW VARIABLES`, though I believe there are plans for more in the future.

Your web browser, in turn, communicates with MONyog via AJAX.  You view the data in a dashboard through Flash graphs.  If you have more than one server on your screen, you see the graphs side by side in multiple columns.  Here's a screenshot of the dashboard (nothing's really happening because this is just watching my wife's laptop, which is idle).

![The MONyog dashboard](/media/2007/05/monyog-dashboard.png)

You can also navigate through a hierarchical display of counter data that isn't Flash-graphed, by clicking on the "Show All" in the navigation bar.  For example, if you select "InnoDB Cache," it renders each server side by side in a table, with a bar graph if the value is a percentage.  The built-in rules specify warning thresholds for values, and the top-level knows when something underneath it has a warning.  In the screenshot below, you can see my InnoDB cache hit ratio is only in the 92% range, which would be worrisome if this laptop were really doing any work.  Notice the red dots next to the graph, and also on the far left-hand side of the screen, indicating a problem:

![MONyog all counters](/media/2007/05/monyog-all.png)

The counters are generated from ordinary JavaScript expressions.  Anyone who can write JavaScript can customize the built-in counters or write their own code to generate the desired data.

If you're monitoring Linux servers, you can specify SSH login information and MONyog will also display system stats like CPU usage.

### Rough edges and drawbacks

As I said, things are a bit rough around the edges in places.  There is no documentation at all, despite the fact that MONyog is featured on the Webyog homepage.  (In fact, this article has more information than I have seen anywhere else on the web).  As of yet it doesn't fetch or expose much variety of data from MySQL.  The Linux version is RPM-only; there's not even a .tar.gz to download, and I wasn't able to get it working on my Linux machine.  The Linux version is also very out of date compared to the Windows version, which I tried to use under Wine but couldn't.

As far as I can tell, it is based on some open-source software such as the Netscape Portable Runtime, but is not Free Software itself.  This is a definite drawback for me.

### Zero-install on servers

There's no need to install anything on the servers you're going to monitor, which is refreshing.  From what I've heard, the MySQL Monitoring and Advisory Service (formerly code-named Merlin) actually requires you to install an agent on each server you're watching, as well as another server which is dedicated to collecting data from the agents.

In contrast, MONyog is zero-install on your MySQL servers.  It simply opens a connection and requests status and other information.  I think this is really appealing from a simplicity and maintenance point of view.  It means you can start monitoring an unlimited number of servers without touching the configuration on any of them.  All your MONyog configuration is in a single place.

I'm not picking on the MySQL folks with my comments about installing an agent.  It is one of my favorite gripes.  Nagios and Munin want to install agents, too.  I really dislike this.  In the age of SSH, there should be more agent-less monitoring systems.

### JavaScript object model

MONyog populates a JavaScript object hierarchy with the data it fetches.  I think people will find it easy to customize the interface, especially since you can do it from within your web browser.  You just click on the file you want to edit---including any of the built-in ones---and you see the code.  It's all there; there is nothing hidden from you.  If you don't know where to get started, just take a look at the built-in counters and copy/paste to make your own.

### MONyog compared to innotop

If you're wondering how MONyog compares to [innotop](http://code.google.com/p/innotop), I think they're quite different.  MONyog seems much more counter-oriented to me; sort of like a Flash-based version of an RRD tool.  I am not sure what the future will hold for it, but in my opinion it's a little more narrowly focused at the moment.

Disregarding the different approaches, innotop's feature set is much larger, of course; I haven't seen any tool that even approaches innotop's capabilities, so that should be no surprise.

### Conclusion

I continue to be interested in all sorts of monitoring systems, both for MySQL and in general, and I'm trying to learn as much about them as I can.  MONyog looks like the beginnings of a nice offering, though ultimately I am unlikely to use it since it's not Free Software.  The most important advantages over other monitoring systems, in my opinion, are the simplicity and ease of use, the agent-less installation, and customizability.


