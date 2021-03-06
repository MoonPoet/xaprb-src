---
title: Mutex tables in SQL
date: "2005-09-22"
url: /blog/2005/09/22/mutex-tables-in-sql/
categories:
  - Databases
---
A "mutex" table is a clever trick that allows joining tables while keeping them independent of each other in a query. This property allows interesting queries that are not otherwise possible. It is especially useful in earlier versions of MySQL, where it can be used to simulate some unsupported queries such as UNION and derived tables in the FROM clause.

My standard mutex table is as follows:

```
create table mutex(
    i int not null primary key
);
insert into mutex(i) values (0), (1);
```

I typically use the mutex table as the leftmost table of `LEFT OUTER JOIN` queries. For examples, see my articles about [simulating `UNION`](/blog/2005/09/22/union-in-mysql/), [FULL OUTER JOIN on MySQL](/blog/2006/05/26/how-to-write-full-outer-join-in-mysql/), and [simulating derived tables in the FROM clause](/blog/2005/09/21/subselects-in-mysql/). I add as many values for `i` as needed, usually one per table in the `LEFT JOIN`.

If you insert values 0 through 9, the table can do double duty as an [integers table](/blog/2005/12/07/the-integers-table/), too. Alternatively, an existing integers table can be used as a mutex table.


