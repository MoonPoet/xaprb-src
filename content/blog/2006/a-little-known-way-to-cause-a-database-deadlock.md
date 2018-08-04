---
title: How To Prevent Database Deadlocks In InnoDB
date: "2006-08-03"
url: /blog/2006/08/03/a-little-known-way-to-cause-a-database-deadlock/
description: "What causes MySQL and InnoDB database deadlocks and how to avoid them."
image: media/2006/03/wrestlers.jpg
categories:
  - Databases
---

In this article I'll introduce deadlocks, analyze and explain a real example, and show how to cause and avoid deadlocks. 
![Wrestlers](/media/2006/03/wrestlers.jpg)

<!--more-->

A deadlock happens when two or more database transactions hold exclusive access to something the other wants. To proceed, one of them has to yield. Since queries are only concerned with what they're doing, and like to imagine they have exclusive access to the entire database, they don't notice when they are deadlocked. Something external must check for deadlocks, choose a victim, and roll one of the transactions back.

A deadlock is a cycle of "I've got this, you have to gimme that before I'll let go of mine" locks. Thinking of it as a cycle is more than just a metaphor; detecting a cycle is how the RDBMS detects a deadlock. And it's useful to visualize, because it helps you anticipate where a deadlock could occur.

Here's a recent example of a deadlock I found at work. Transaction 1 was [aggregating an atomic traffic data table](/blog/2006/07/19/3-ways-to-maintain-rollup-tables-in-sql/) with a query like the following:

```
create temporary table cost as
   select day, client, sum(clicks), sum(cost)
      from ad_data
      where day = '2006-08-01'
      group by day, client;
```

Transaction 2 was inserting into that same table:

```
insert into ad_data(day, ad_id, client, clicks, cost)
   values('2006-08-01', 5, 1, 50, 500);
```

Boom! They deadlocked. Now, why would that happen? Shouldn't one of them just
wait for whoever got there first?  I haven't told you enough to know why, though you
may still be able to guess.  Here's a relevant detail: the table's primary key
is on `(day, ad_id)`. 

The missing information is that in addition to the row it was trying to insert
for `ad_id` 5, transaction 2 had previously inserted a row for `ad_id` 7:

```
insert into ad_data(day, ad_id, client, clicks, cost)
   values('2006-08-01', 7, 1, 70, 700);
```

To help you understand how this situation caused a deadlock, consider the following: both queries were getting locks on the primary key, which in an InnoDB table is the [clustered index](/blog/2006/07/04/how-to-exploit-mysql-index-optimizations/). The two queries were getting the locks very differently. Transaction 1 was *scanning* the index. It had to, in order to get every row for the date specified in the `WHERE` clause. And since it was selecting the data to use elsewhere, it was getting shared locks on each row it encountered, locking an entire range of the table.

By contrast, Transaction 2 was *probing into the index* with a new row, trying to find where to put it. And when it found the spot, between `ad_id` 4 and 6, it tried to insert it in the gap.

Here's the deadlock: Transaction 1 had already *scanned past that point*, locking every row along the way. If it hadn't, Transaction 2 would have been able to insert the new row, and there'd be no deadlock. Additionally, we can deduce that Transaction 1 had scanned all the way to the (newly inserted) row for `ad_id` 7, and stopped there. If it hadn't, it wouldn't be waiting for anything, and again there would be no deadlock.

Transaction 1&#8242;s locks cannot allow Transaction 2 to insert the new row. If that row were inserted, Transaction 1&#8242;s sum of the data would be wrong. That's where the deadlock really comes from.

Here's a picture of the situation. Start reading at the bottom right, then go to the top left, then to the top right:

<img src="/media/2006/08/deadlock.png" width="400" height="102" alt="deadlock" />

A key point is that those transactions are working in opposite directions. Transaction 1 is working downwards through the table. Transaction 2 is working upwards. If you think about it, that's sort of cyclical, right? That's one way to cause a deadlock: get two transactions working in opposite directions.

This brings me to the corollary: **many deadlocks can be avoided by working in primary key order**. If Transaction 2 had done that, Transaction 1 would have had to wait at the lowest `ad_id` for which Transaction 2 had a lock, leaving the higher ranges open for Transaction 2 to work on.

Another solution for avoiding this deadlock is to have Transaction 2 commit after every single insert, but that's not efficient and probably not desirable, if it wants an entire set of data to either succeed or fail.

This deadlock was not obvious for me to debug. It showed up in the output of `SHOW ENGINE INNODB STATUS` and took a little thought to understand, because it wasn't clear that the `INSERT` query had previously done inserts. However, with a little insight into the situation, it's not too bad to debug. It especially helps if you have tools to format the data nicely.

I'll deliberately cause this deadlock so you can see what the InnoDB monitor output looks like. Here's the setup:

```
create table ad_data(
   day date not null,
   ad_id int not null,
   client int not null,
   clicks int not null,
   cost int not null,
   primary key(day, ad_id)
) engine=innodb;

insert into ad_data(day, ad_id, client, clicks, cost)
   values
   ('2006-08-01', 1, 1, 10, 100),
   ('2006-08-01', 2, 1, 20, 200),
   ('2006-08-01', 3, 1, 30, 300),
   ('2006-08-01', 4, 1, 40, 400),
   ('2006-08-01', 6, 1, 60, 600);
```

Now open two connections to this database, and issue the following queries:

```
-- On connection 2
start transaction;
insert into ad_data(day, ad_id, client, clicks, cost)
   values
   ('2006-08-01', 7, 1, 70, 700);

-- On connection 1
start transaction;
create temporary table cost as
   select day, client, sum(clicks), sum(cost)
      from ad_data
      where day = '2006-08-01'
      group by day, client;

-- Connection 1 should have blocked.
-- On connection 2,
insert into ad_data(day, ad_id, client, clicks, cost)
   values
   ('2006-08-01', 5, 1, 50, 500);
```

I just did this, and Transaction 1 was chosen as the victim. Here's the relevant output of `SHOW ENGINE INNODB STATUS`:

```
------------------------
LATEST DETECTED DEADLOCK
------------------------
060803 20:04:04
*** (1) TRANSACTION:
TRANSACTION 0 94732, ACTIVE 8 sec, process no 12585, OS thread id 1141680480 fetching rows
mysql tables in use 1, locked 1
LOCK WAIT 3 lock struct(s), heap size 368
MySQL thread id 4, query id 101 localhost baron Copying to tmp table
create temporary table cost as
   select day, client, sum(clicks), sum(cost)
      from ad_data
      where day = '2006-08-01'
      group by day, client
*** (1) WAITING FOR THIS LOCK TO BE GRANTED:
RECORD LOCKS space id 0 page no 45 n bits 80 index `PRIMARY` of table `test/ad_data` trx id 0 94732 lock mode S waiting
Record lock, heap no 7 PHYSICAL RECORD: n_fields 7; compact format; info bits 0
 0: len 3; hex 8fad01; asc    ;; 1: len 4; hex 80000007; asc     ;; 2: len 6; hex 00000001720b; asc     r ;; 3: len 7; hex 80000000320110; asc     2  ;; 4: len 4; hex 80000001; asc     ;; 5: len 4; hex 80000046; asc    F;; 6: len 4; hex 800002bc; asc     ;;

*** (2) TRANSACTION:
TRANSACTION 0 94731, ACTIVE 24 sec, process no 12585, OS thread id 1141414240 inserting, thread declared inside InnoDB 500
mysql tables in use 1, locked 1
3 lock struct(s), heap size 368, undo log entries 1
MySQL thread id 3, query id 102 localhost baron update
insert into ad_data(day, ad_id, client, clicks, cost)
   values
   ('2006-08-01', 5, 1, 50, 500)
*** (2) HOLDS THE LOCK(S):
RECORD LOCKS space id 0 page no 45 n bits 80 index `PRIMARY` of table `test/ad_data` trx id 0 94731 lock_mode X locks rec but not gap
Record lock, heap no 7 PHYSICAL RECORD: n_fields 7; compact format; info bits 0
 0: len 3; hex 8fad01; asc    ;; 1: len 4; hex 80000007; asc     ;; 2: len 6; hex 00000001720b; asc     r ;; 3: len 7; hex 80000000320110; asc     2  ;; 4: len 4; hex 80000001; asc     ;; 5: len 4; hex 80000046; asc    F;; 6: len 4; hex 800002bc; asc     ;;

*** (2) WAITING FOR THIS LOCK TO BE GRANTED:
RECORD LOCKS space id 0 page no 45 n bits 80 index `PRIMARY` of table `test/ad_data` trx id 0 94731 lock_mode X locks gap before rec insert intention waiting
Record lock, heap no 6 PHYSICAL RECORD: n_fields 7; compact format; info bits 0
 0: len 3; hex 8fad01; asc    ;; 1: len 4; hex 80000006; asc     ;; 2: len 6; hex 00000001720a; asc     r ;; 3: len 7; hex 80000000320154; asc     2 T;; 4: len 4; hex 80000001; asc     ;; 5: len 4; hex 8000003c; asc    &lt;;; 6: len 4; hex 80000258; asc    X;;

*** WE ROLL BACK TRANSACTION (1)
```

That's fairly verbose, because it prints information about the locks it was waiting for and holding, but that's exactly what you need to figure out what was really going on. Notice how you can see Transaction 1 waiting for exactly the same lock Transaction 2 holds. Notice also Transaction 2 locks the "rec but not gap" on that lock. That means it locks the record, as opposed to the [gap before the record](http://dev.mysql.com/doc/refman/5.0/en/innodb-next-key-locking.html). You can read more about this in the MySQL manual -- the entire section on InnoDB transactional model is recommended reading.

Finally, notice how Transaction 2's waited-for lock is trying to lock the gap before the record, with intention to insert. That's what finally caused the deadlock.

[Picture Credit](https://pixabay.com/en/men-wrestling-sports-grappling-mat-83501/)
