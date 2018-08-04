---
title: How to write a UNION in SQL without using UNION
date: "2005-09-22"
url: /blog/2005/09/22/union-in-mysql/
categories:
  - Databases
---
MySQL does not support UNION prior to version 4.0.0, but it is possible to write a `UNION` with a [mutex table](/blog/2005/09/22/mutex-tables-in-sql/) and `LEFT OUTER JOIN`. As an example, `UNION` these tables together:

```
create table colors (
    title varchar(20)
);
create table flavors(
    title varchar(20)
);
insert into colors values ('blue'), ('green');
insert into flavors values ('vanilla'), ('chocolate');
```

The trick is to `LEFT OUTER` join such that the values from one table do not get included in the same row with values from other tables, then `COALESCE` the values to select the (only) non-NULL value from each row. This is possible by using the mutex table as the leftmost table, then `LEFT OUTER` joining onto the tables which hold the data you really want:

```
select coalesce(c.title, f.title)
from mutex
left outer join colors as c on i = 0
left outer join flavors as f on i = 1
where i in (0, 1);
```

The result is not as efficient as a true `UNION`, but it works. This technique simulates `UNION ALL`; to simulate UNION, use `SELECT DISTINCT` instead.


