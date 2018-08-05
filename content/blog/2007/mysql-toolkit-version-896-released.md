---
title: MySQL Toolkit version 896 released
date: "2007-09-20"
url: /blog/2007/09/20/mysql-toolkit-version-896-released/
categories:
  - Databases
  - Open Source
---

This release of MySQL Toolkit adds a new tool, fixes some minor bugs, and adds new functionality to several of the tools.

### New tool: MySQL Heartbeat

This tool was contributed by [Proven Scaling](http://provenscaling.com/)'s [Jeremy Cole](http://jcole.us/) and [Six Apart](http://www.sixapart.com/). It measures replication delay on a replica, which can be daisy-chained to any depth. It does not rely on SHOW SLAVE STATUS, and in fact it doesn't even need the replica processes to be running. You could use it to measure replication delay on your own hand-rolled replication, if you wanted.

The most common way to use it is to run one process to update a heartbeat on the master, and another to monitor the lag on a replica (you can run as many as you wish to monitor multiple replicas). By default it prints moving averages of delay over one, five and fifteen-minute time windows:

```
0s [  0.00s,  0.00s,  0.00s ]
   0s [  0.00s,  0.00s,  0.00s ]
   1s [  0.02s,  0.00s,  0.00s ]
   2s [  0.05s,  0.01s,  0.00s ]
   3s [  0.10s,  0.02s,  0.01s ]
   4s [  0.17s,  0.03s,  0.01s ]
   0s [  0.17s,  0.03s,  0.01s ]
   0s [  0.17s,  0.03s,  0.01s ]
   0s [  0.17s,  0.03s,  0.01s ]
```

(of course, I couldn't resist making that configurable, so you can specify your own time windows).

You can also run it as a daemon. Running the update process as a daemon is intuitive. Running the monitoring process isn't quite as obvious, because a daemon should re-open STDOUT to /dev/null. What you can do is give it the `--file` argument and it'll keep a file current with the most recent line of output, which you can check anytime you want to see how your replica has been doing over the last X time windows.

### Changelog

Here's a changelog for the other tools I updated in this release:

```
Changelog for mysql-deadlock-logger:

2007-09-20: version 1.0.4

   * Added --interval, --time, and --daemonize options, and signal handling.
   * --askpass did not allow different passwords on --source and --dest.

Changelog for mysql-duplicate-key-checker:

2007-09-20: version 1.1.1

   * Exit code wasn't always defined.

Changelog for mysql-query-profiler:

2007-09-20: version 1.1.5

   * Documentation didn't specify how queries in FILE are separated.

Changelog for mysql-slave-delay:

2007-09-20: version 1.0.1

   * Added a --daemonize option to detach from the shell and run in the background.

Changelog for mysql-slave-restart:

2007-09-20: version 1.0.1

   * Added a --daemonize option to detach from the shell and run in the background.

Changelog for mysql-table-checksum:

2007-09-20: version 1.1.15

   * The CHECKSUM strategy was always disabled.

Changelog for mysql-visual-explain:

2007-09-20: version 1.0.3

   * filesort wasn't applied to the first non-constant table.
```


