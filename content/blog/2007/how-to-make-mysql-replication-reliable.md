---
title: How to make MySQL replication reliable
date: "2007-01-20"
url: /blog/2007/01/20/how-to-make-mysql-replication-reliable/
categories:
  - Databases
---
MySQL statement-based replication is widely discussed, but I haven't seen much about how to design a replication setup for low downtime and easy administration. Statement-based replication has inherent shortcomings experienced MySQL users know to avoid, but rarely write about. This article explains how to avoid problems, help your replicas stay in sync with the master, and recover from disasters more quickly.

By the way, I'm fairly new to MySQL replication. Less than two months ago I was asking many of you for advice. I've had to come up to speed on it pretty quickly. So, if I miss something or get something wrong, please leave comments and help me out.

### Context

This article is specifically about mitigating risks in MySQL statement-based replication setups (statement-based replication is the only type of replication available before version 5.1, currently in beta). Once you decide to clone a server from another server, you have automatically added risks: your master will crash, your replica will get out of sync, your replica will crash, you will come to rely on the replica(s) and downtime will become unacceptable, and so forth. My goal is to tell you how to make these problems less likely, and how to make it easier and faster to recover when the inevitable happens.

I assume that you're running something important on your MySQL installation, so high availability and data integrity are important, if not mandatory. And I assume you have a non-trivial amount of data, say 25GB or more. If this doesn't describe your installation, you can be much more casual about the risks of replication, because recovery from problems is either not important or much easier.

I will try *not* to cover topics about which more knowledgeable people have written: the [MySQL manual section on replication](http://dev.mysql.com/doc/refman/5.0/en/replication.html), [Giuseppe Maxia's article on advanced replication techniques](http://www.onlamp.com/pub/a/onlamp/2006/04/20/advanced-mysql-replication.html), [how to scale out with application partitioning](http://dev.mysql.com/tech-resources/articles/application_partitioning_wp.pdf), etc.

### 1. Design with snapshots in mind

In my opinion, probably the most important cornerstone of low-downtime, fault-tolerant replication is the ability to *take consistent snapshots quickly*. You need snapshots for two reasons: initializing replicas and taking backups. You can take a snapshot of your master to initialize a replica or take a backup, and a snapshot of your replica to initialize another replica or make a backup. Both types of snapshots are important for different reasons.

For initializing replicas, I strongly prefer binary snapshots of the files as they exist on disk, with the MySQL instance shut down. Binary snapshots are usually larger, and can thus be slower to take than just using `mysqldump`, but there are other advantages to binary snapshots. For example, they're generally faster to restore; you just copy the files into place and start the server---no need to reload dumps and wait hours for indexes to rebuild. I'll explain more reasons I prefer binary snapshots in the following sections.

#### 1.1 Snapshots on the master

Taking a snapshot of the master is necessary to initialize at least the first replica you clone. If you are very lucky, you'll be able to stop the master for as long as you need to dump all the data or copy the files to the replica. I don't know anyone who has that luxury.

Your snapshots for initializing replicas have to be point-in-time atomic, or you won't be assured the replica is an exact copy of the master. If you're snapshotting for a backup, that might be less important, but I personally would strive for atomicity in backups too. You can potentially take snapshots with the server running by locking all the tables, flushing tables to disk, etc etc. This might be quite disruptive, but one way or another you have to stop all modifications to the data long enough to get the snapshot.

My favorite technique is using a filesystem with snapshot capability, such as LVM under GNU/Linux. This lets you take a *read-only snapshot nearly instantaneously*, then take as much time as you need to copy it somewhere, while the MySQL server runs normally. If you want to know more about this, read about [using LVM for backup and replication](http://www.mysqlperformanceblog.com/2006/08/21/using-lvm-for-mysql-backup-and-replication-setup/), and take a look at [mylvmbackup](http://lenz.homelinux.org/mylvmbackup/) for a script that can help you take backups from an LVM snapshot.

One thing I would add to these articles: I never try to take snapshots while MySQL is running in the installations I help manage. Our requirements are such that it is okay for the server to be down for a few seconds, and there's not much overhead in restarting it (I know this isn't always the case for everyone). This gives us the peace of mind of knowing the snapshot is totally consistent, with no risks of InnoDB background threads modifying things, for example. If you can't shut down MySQL, it is a delicate dance, but there's good advice in the article I just linked above.

#### 1.2 Snapshots on the replica

The second place you can take snapshots is on a replica. This is the main way my employer avoids snapshots on the master, which we don't like to do. Replicas are much less critical for us---we run reporting and read-only queries from them, so it's not a big deal to stop MySQL on a replica whenever we need a backup or to initialize another replica.

Cloning replicas from other replicas is easy: you just run `STOP SLAVE`, record the master binlog and log position, shut down the replica, take the filesystem snapshot, then bring the replica up again. This can happen very quickly. Then you copy the snapshot to the new replica and bring the new replica up, point it at the same binlog and position as the first replica (that is, the position where the snapshot was taken), and start the new replica. After it catches up, it should be an exact copy of the master.

However, there are extra things to think about when taking a snapshot on a replica. First, you need to make sure you get *everything you need*. You need the data files of course, and if you're running InnoDB, you need the log files too, but you also need the temporary files if you use `LOAD DATA INFILE`. There's a configuration parameter that tells replicas where to store these temporary files, which are inlined in the binlog and then written out to the filesystem on the replica. If your new replica doesn't get these temporary files, replication may break on `LOAD DATA INFILE`. If you're using a filesystem snapshot, that means your temp files need to be stored on a snapshot-ready filesystem just like the data and log files.

The other thing you have to worry about on a replica is temporary tables. If you need to stop your replica to get a consistent snapshot, you can't do it while there are replica temporary tables open. This is an important topic that I'll discuss in more detail later.

#### 1.3 Beware of relying only on filesystem snapshots

If your data files get corrupted, you may not know it until some query tries to read the bad data. Taking regular text backups with `mysqldump` as well is a very good idea.

On the other hand, if you rely solely on text backups, you could also get corruption---the files might be fine on disk, but your server might have memory corruption (these things happen). If your data is important, I think it's best to be redundant.

### 2. How to keep the replica in sync

Okay, so you've designed your systems so it's very easy to take snapshots. Now you are ready to take nearly instantaneous backups and initialize new replicas quickly and easily. Once your replicas are running, though, you have to worry about keeping them in sync with the master.

There are several things to think about here, too. One is simply making sure the replicas can keep up with the master. You also have to make sure nobody makes any changes to the replica's data and schemas. And finally, you have to avoid problems inherent to MySQL replication that can cause the replica to have different data than the master.

#### 2.1 Make sure the replicas are keeping up

Making sure the replica can keep up with the master is not always easy. Replica hardware typically needs to be at least as powerful as the master, because the replica has to execute all the same DML statements as the master. But replicas have an additional handicap: they can't do these operations in parallel. If you have even a slightly busy master, it probably runs lots of queries at the same time. When a query asks for some data that's not available right away, the server requests the data and then puts the query to sleep until the data is available (for example, the disk finds and returns the data). In the meantime, the master can run other queries. However, these queries are serialized to the binlog in order of transaction commit, so they are run serially on the replica. The replica doesn't read ahead in the binlog and execute multiple queries simultaneously. To keep the updates consistent, the queries must be executed in the order they're in the binlog. This means the replica might spend much more idle time waiting for the disk to respond. Furthermore, presumably you're actually using the replica to take load off the master---analytics queries, reporting, or whatnot. That's additional load on the replica.

Your options are fairly limited. You can monitor how far behind the replica is (the development branch of [innotop](http://code.google.com/p/innotop/) makes this easy) and assign less work to it when it starts to lag the master a lot. We do this with a monitoring script and DNS. You can make the replica's hardware more powerful, especially giving it faster disks and more memory if that makes sense for your workload. You can try not to run near capacity---favorite tactics at Google and Flickr.

If you have the coding kung-fu, you might also try to "pipeline the relay log." To do this, you'd write a program to read ahead in the binlog, convert the statements to `SELECT`s that read the data needed, and thus get the data into cache so the queries don't have to wait for I/O so much. I haven't used this technique myself, but I know of a person at a popular Web 2.0 company who does and found it speeds things up a lot, especially queries that access a very small amount of data. The explanation of it made a lot of sense to me. However, as I said I haven't done it, and I just mention it here for completeness. If you have the skills to do this, I'm sure you can work it out. One caveat: you might consider whether it makes sense for your query workload. You will only get benefit from this in certain types of queries; otherwise you might just spend a lot of time flushing good data from the cache, causing cache misses and extra disk activity.

#### 2.2 Prevent changes to replica data

If you don't keep users and processes from changing data and tables on the replica, you're guaranteed to get out of sync. If someone updates, deletes or inserts rows on the replica, the data is automatically out of sync, and the errors accumulate over time. Likewise, if someone changes a table structure, alters a column's data type, or makes any other schema change, things will break. The most straightforward way to avoid this is revoke all write privileges on replicas. (By the way, your [schema and privileges ought to be in version control](/blog/2006/07/09/so-you-think-your-code-is-in-version-control/)).

Changed data on the replica doesn't just cause it to have different data. It can cause replication to break, if the changed data causes an integrity violation or other error. The binlog contains information about every event, including whether it caused an error on the master, and replication will fail if there's a different error on the replica than on the master.

Finally, if you intend to prevent any writes on replicas but still allow users to create temporary tables on replicas (quite helpful for reporting and the like), you need to be careful about the interaction between temporary table privileges and regular table privileges. Read more about privileges in the MySQL manual. My simple advice is this: create a separate database that only exists on the replica and only grant temporary table privileges in that database. Creating the database only on the replica ensures nobody uses it on the master (if it even exists on the master, you already have potential problems). Revoking temporary table privileges except in that database keeps replicated tables safe from modifications.

### 3. Avoid gotchas that cause different results on replicas

There are several replication gotchas that can cause the replicas to get out of sync with the master. There are non-deterministic queries that won't produce the same result on the replica, there are errors caused by the binlog being serialized on the replica, and there are problems mixing transactional and non-transactional storage engines.

Although this technically falls under "keeping replicas in sync," it's a big enough topic that I want to dedicate a section to it.

#### 3.1 Queries not safe for replication

The queries that won't replicate might surprise you. You might think queries involving the current date and time, `RAND()`, process ID and so forth wouldn't replicate. However, all the information needed to replicate these things properly is included in the binlog. Things that *do not* replicate properly are well-documented in the MySQL Manual section on [replication limitations](http://dev.mysql.com/doc/refman/5.0/en/replication-features.html). Especially if you are living on the bleeding edge (for example, mixing stored procedures and replication in version 5.0), you may run into some of these. You just need to be aware of the things that don't replicate right and avoid them. They're generally easy to avoid because they're not "plain vanilla" things to do.

Even some "plain vanilla" things don't replicate right if you don't take care, however. For example, suppose you have a MyISAM table on the master which has had a lot of deletes and inserts. You take a snapshot of the master with a custom dump script you wrote yourself. For some reason you wrote your dump script to always `ORDER BY` the primary key when dumping a table to disk. Now you initialize the replica from this script and everything looks fine. Then someone runs a `DELETE FROM TBL LIMIT 1` on the master. Which row gets deleted on the replica? Probably not the same one that got deleted on the master, because the rows are probably stored in a different order on the replica. Now your master and replica are out of sync. This is one reason I feel much more comfortable with filesystem snapshots for initializing replicas.

Finally, stored procedures make even more "plain vanilla" queries unsafe for replication. You need to be very careful about this.

#### 3.2 Don't disable InnoDB's locking selects

It's pretty easy to get bitten by binlog serialization and the problems it can cause with InnoDB, if you don't understand how and why it works as it does. As I mentioned, each transaction goes into the binlog in the order in which it commits, not in the order in which it is started, so transactions may execute in a different order on the replica. To prevent inconsistent reads on the replica, InnoDB takes shared locks on all `INSERT INTO ... SELECT FROM` statements. That ensures transaction 2 can't modify any data transaction 1 has just read, so the transactions will not cause inconsistent data on the replica when transaction 2 executes first. I personally know people who are very frustrated by this, and it's been widely discussed (it's well-documented in the manual, among other places).

You might be strongly tempted to disable the behavior so you don't get so much lock contention. Don't do it.

Unless you really know what you are doing, you are pretty much guaranteed to get your replicas out of sync. It is such a bad idea, I'm not even going to tell you what configuration parameter controls this. Instead, I'll show you better ways when you know a particular statement doesn't need to acquire locks.

The first way, if you know you can get away with it, is to simply commit immediately after the `INSERT ... SELECT`. This doesn't prevent locks from being taken, but it does release them as soon as possible. That may solve the problems.

The second way, which doesn't take any locks at all, is `SELECT INTO OUTFILE` followed by `LOAD DATA INFILE`. You will have to have additional privileges for this, and you'll have to consider how to clean up the outfile, but these are relatively easy to solve.

If you're here looking for a solution to this problem and this is the first time you've heard of these two options, I encourage you to read more elsewhere. I won't write any more about this---I just wanted to mention it to you so you can find out more if you want.

#### 3.3 Be careful replicating only some databases

If you want to replicate only certain databases and not others, you need to be very careful. It is possible to make a change to a database that should be replicated to the replica, but will not be because of how you executed the query. Take a look at this introductory paragraph from the [manual](http://dev.mysql.com/doc/refman/5.0/en/replication-rules.html):

> If a master server does not write a statement to its binary log, the statement is not replicated. If the server does log the statement, the statement is sent to all replicas and each replica determines whether to execute it or ignore it.

Notice, you need to pay attention to *both master and replica* configuration. Read more about [replication rules](http://dev.mysql.com/doc/refman/5.0/en/replication-rules.html)---I won't duplicate the manual here. In general, if you are replicating everything except the mysql database, and you never make that your default database, you will probably be okay.

#### 3.4 Don't mix transactional and non-transactional storage engines

Using a mixture of transactional and non-transactional storage engines causes lots of problems. The short and sweet is, don't do it, because you will be exposed to very high risk of creating different data on the master and replica.

Here's one scenario: there's a deadlock on the master in a query that updates two tables, one InnoDB and the other MyISAM. The query has proceeded to a certain point when it tries to get a lock on a row in the InnoDB table and causes a deadlock. At this point it's too late: no matter what happens, the master and replica are going to have different data. The changes to the MyISAM table cannot be rolled back, and the changes to the InnoDB table cannot be committed. If the query doesn't get put into the binlog, the MyISAM changes will not propagate to the replica. If it does get into the binlog, there will probably not be a deadlock on the replica, because the replica's queries are serialized, and both the InnoDB and MyISAM updates will proceed to completion on the replica.

Either way, one or both tables will be different on the replica. MySQL does put the statement into the binlog, for better or for worse. As I said, there's no right choice.

Another scenario is if you have some user running queries on the replica that affect the InnoDB table, such as selecting from that table into a temporary table and acquiring locks on it. In this case, a transaction that caused no deadlock on the master might cause a deadlock on the replica; then the changes that succeeded on the master will not proceed to completion on the replica. Boom, your tables are different on the replica.

In both cases, MySQL will detect a different error on the master and replica, and replication will break. There is no way to recover from this; you will have to re-initialize the replica, unless you happen to know that skipping or retrying the statement on the replica will bring the tables back into synchrony (very unlikely). If you had the first kind of error, you're going to have to re-initialize every replica from the master; if you had the second kind, you might be able to clone the replica from another replica that wasn't affected, which is much less painful.

A note on temporary tables: if your server's default storage engine is MyISAM (often the default) and you don't explicitly specify the storage engine for temporary tables, they will be MyISAM. Temporary tables are not exempt from the transactional/non-transactional problems, so be aware of that. Of course, please read on to find out why temporary tables are inherently bad for replication.

No matter what, mixing transactional and non-transactional storage engines in replication is bad news. There is no workaround.

#### 3.5 Beware of relay log corruption

I sometimes see relay log corruption on the replica. The replica I/O thread fetches the binlog from the master and writes it to the relay log on the replica, which the replica SQL thread then replays. If there's corruption in the relay log that makes a statement un-parsable, the replica SQL thread will throw an error and stop. If you then examine the MySQL error log you'll see the position in the relay log where the error was found, and you can use `mysqlbinlog` to examine the log at that point. I've seen the contents, which should look like a normal SQL statement, have a bunch of apparently misaligned bytes, which look like censored expletives.

Fortunately, this is fairly easy to fix. Just record *the corresponding position in the master's binlog* where the corruption occurred, shut down the server, and delete all the relay logs it has fetched from the master. Then bring it back up, and tell it to begin replication again from that point.

The scarier scenario is when there's invisible corruption that doesn't cause the replica to fail. What if a byte got lost somewhere, for example? Perhaps you inserted "oranges" on the master, but the replica only got "ores"---entirely possible, because [there are no checksums on the binlog](http://bugs.mysql.com/bug.php?id=25737) entries. This is why you need good tools to check whether your replicas have the same data as the master.

I haven't yet seen binlog corruption on the master, and I don't know fully what its effects might be. While I was at MySQL Camp at Google in November I listened to some Google engineers talk about the problems caused by very large numbers of replicas pulling the binlog from a single master. I don't recall exactly what the problems were---I think they were related to the presence of large binlog entries and lots of replication threads using tons of memory on the master---but it's just something to be aware of. MySQL replication has the proven ability to scale very large, but apparently when you get that big there are problems lurking.

I mention binlog corruption not because I can tell you how to avoid it, but because it highlights the need to have good disaster recovery capabilities, and the need to know when your replicas silently get out of sync with the master.

### 4. Monitor whether your replicas are in sync

Preventing your replicas from getting out of sync with the master is hard enough, but it can be even harder to detect when they get out of sync. When I say "out of sync" I don't mean there's replication time lag or delay---that's normal---but that the master and replica really have different data. The problem is, you can easily get a positive "yes, the replica is out of sync," but you can't be very confident about a negative; false negatives are easy to get.

The simplest technique is simply to count rows on the master and replica. You can do this with a short script in your favorite scripting language: iterate through the databases, run `COUNT(*)` on each table, then compare that to the replica. If you see different row counts, you have a problem.

If the row counts are the same, though, you still don't know anything for sure. The contents of some rows could differ (for example, perhaps you got relay log corruption that didn't cause a hard failure). The best way I know to verify the row contents is with a checksum. MySQL doesn't provide a solution themselves. MyISAM tables maintain an internal checksum, but that doesn't help for any other storage engine. For other storage engines, you'll have to write your own checksum. Giuseppe Maxia to the rescue again---he has a very [good article on table checksums in MySQL](http://datacharmer.blogspot.com/2006/03/seeking-alternatives-to-cursors.html), as sort of a tangent to a discussion on cursors.

**Update:** I have improved upon Giuseppe's technique; see my article on [how to calculate table checksums in MySQL](/blog/2007/01/25/how-to-calculate-table-checksums-in-mysql/).

**Update:** I've created a tool that can [verify tables are identical](/blog/2007/02/26/introducing-mysql-table-checksum/) on the master and many replicas.

To take checksums of your master and replica, you'll obviously have to halt the master and let the replica catch up to it. The safest way I know is to stop the master, let all replicas catch up and then stop them, re-initialize one replica directly from a filesystem snapshot of the master, start the master again, and keep all the replicas stopped---thus ensuring that you have all replicas stopped at a single point in time relative to the master. Then you can compare each of the replicas to the brand-new snapshot from the master. If there are any differences, you have a problem, and you should re-initialize all the replicas from the new snapshot.

### 5. Avoid temporary tables like the plague

Temporary tables are very convenient, and they generally work fine in replication, but they make restarting after crashes impossible. If your goal is to have a reliable setup that's easy and quick to recover in case of a problem, you need to completely stay away from temporary tables.

Here's why: temporary tables exist only in memory. They do not persist across server restarts. If a replica crashes---and [MySQL replica crashes can happen even when you're just doing routine work](http://bugs.mysql.com/bug.php?id=25531)---you can only restart it if everything is recoverable from disk. Temporary tables make that impossible, because when the replica starts reading from the binlog and tries to execute a statement that refers to a temporary table created before the server was started, the statement will fail. The temporary table no longer exists, and there's nothing you can do about it. If you're lucky you can tell the replica to skip one or two statements that you know don't really affect any data, but in general you're probably going to have to re-initialize the replica.

You also need to be able to stop and restart your replicas at will, for example to take snapshots for backups or to clone another replica. If you have even a single temporary table open, you can't do that. Temporary tables stay open until they're explicitly dropped on the master, or the connection that created them closes. If you use temporary tables much, you might have lots of them open at any given time, and if you need to stop a replica for a backup, you will probably never get a chance.

I think the best solution is to simply use real tables instead. Real tables persist on disk and will let you stop, start, and recover from crashes. Instead of creating temporary tables, create a real table with a unique name, which no other query will use.

You will need to make allowances for cleaning up these tables, however. If a process dies before it cleans up after itself, the table will stay around. I recommend that you create a separate database for the tables and have a reaper process run every now and then. You can do this several ways; one suggestion I've heard is to run `SHOW TABLE STATUS` and examine the create date, then drop tables after a certain safe amount of time. I don't like this very much, because a "safe" interval is likely to be pretty long depending on your workload, and it's hard to be really sure the table is "safe" to drop.

The way I do it is to name each table with its connection ID as a suffix. For example if my connection ID is 123, I might name the table `client_report_123`. This ensures table names are unique, removing the messiness of trying to find an unused random string. It makes table names meaningful, instead of random garbage whose purpose is unknown. And it makes it easy to know for sure when the table is obsolete, because you can run `SHOW PROCESSLIST` and see whether connection 123 is still open. With this naming convention, the reaper job can be a few lines of code in your favorite scripting language (yay regular expressions!).

### 6. Beware of new features

Sometimes replication gets very unhappy about new features. I remember the first time I tried to use `ON DUPLICATE KEY UPDATE` with a `VALUES()` clause in the `UPDATE` in MySQL 4.1. It ran fine on the master, but when it got to the replica, it core dumped the server. I had similar experiences with views and triggers in the first versions of MySQL 5.0. In general, it's a good idea to test everything against a non-production setup, just as you would any other code. That's just general advice, but I wanted to warn you not to assume things that run fine on the master will be okay on the replica.

### Conclusion

In this article I tried to summarize what I've learned about making replication as reliable and recoverable as possible over the last several months. These are tried-and-true techniques for most experienced MySQL users, but I found a paucity of information on the web about it, so I thought it would be helpful to write it down.

I'm sure this is an incomplete list, and maybe I've even gotten some things wrong, but hopefully this will help you avoid a lot of pain if you're new to MySQL replication. If you have other things to add, please write into the comments.



