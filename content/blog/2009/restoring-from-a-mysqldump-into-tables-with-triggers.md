---
title: Restoring from a mysqldump into tables with triggers
date: "2009-01-08"
url: /blog/2009/01/08/restoring-from-a-mysqldump-into-tables-with-triggers/
categories:
  - Databases
  - Open Source
---
This is actually old news, but I never thought to file a bug report ([until now](http://bugs.mysql.com/41958)) or say anything to anyone about it. If you use mysqldump to dump and restore a MySQL table that has INSERT triggers, you can get different data in your restored database than you had when you dumped. The problem? The tool dumps the triggers before the data, so they get added back to the table before the rows are inserted.

The fix for this is really trivial. Just move the triggers after the INSERTs. Someone should patch mysqldump, but I've been too lazy... and besides, you know what I say about me and C programming. Unsafe at any speed.

This isn't a problem with mk-parallel-dump, by the way. It puts the triggers in separate files, and mk-parallel-restore adds them back after the data is restored.


