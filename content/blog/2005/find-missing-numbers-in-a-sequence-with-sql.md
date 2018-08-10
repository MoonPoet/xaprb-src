---
title: How to find missing values in a sequence with SQL
date: "2005-12-06"
url: /blog/2005/12/06/find-missing-numbers-in-a-sequence-with-sql/
categories:
  - Databases
---
Sometimes it is important to know which values in a sequence are missing, either to find unused values so they can be used, or to find "holes" in the data. In this article I'll show you how to find missing values, how to find the start and end of ranges of missing values, and how to optimize the queries for best performance.

### Exclusion joins

Possibly the most efficient technique, depending upon the application, is to use an [exclusion join](/blog/2005/09/23/how-to-write-a-sql-exclusion-join/) against a list of all legal values (for example, an [integers table](/blog/2005/12/07/the-integers-table/)). For instance, at my current employer we assign a unique tracking ID to certain bits of data. For reasons lost in the mist of time, we use three-character combinations of letters and numbers. It's effectively a base-36 number system. It is not the most efficient thing to work with in SQL! Since there is no magical built-in way to get the database to assign the next unused value in the sequence, we keep a table with all {{< math >}} 36^3 {{< /math >}} legal values, and do an exclusion join against the list of legal values. This is an acceptable way to find the next values, but of course it's nowhere near optimal; when transactional consistency is needed, we have to lock tables up and do an expensive query. An identity (`auto_increment`) column would be preferable.

Putting three-character codes behind and assuming you want to analyze some existing data for holes without creating lists of legal values, it is possible to find missing values in a sequence by matching it against itself. For example, I am helping someone design a database to store information about gravestones. The original data was hand-entered into a spreadsheet, with a single column to keep track of gravestone numbers. There are duplicate and missing values in the sequence, both of which can indicate data problems, so it's highly desirable to find and fix them. After importing the spreadsheets verbatim into a staging table, I ran a number of analyses to find data problems before transforming the data into the final tables.

### The setup

If you want to follow along with the examples, you can run the following queries to create some sample data in MySQL:

```sql
create table sequence (
    id int not null primary key
);

insert into sequence(id) values
    (1), (2), (3), (4), (6), (7), (8), (9),
    (10), (15), (16), (17), (18), (19), (20);
```

Notice the values 5, 11, 12, 13, and 14 are missing from the sequence. If you are using Microsoft SQL Server, change `sequence` to `#sequence` from here on:

```sql`
create table #sequence (id int not null primary key);

insert into #sequence(id)
    select 1
    union all select 2
    union all select 3
    union all select 4
    union all select 6
    union all select 7
    union all select 8
    union all select 9
    union all select 10
    union all select 15
    union all select 16
    union all select 17
    union all select 18
    union all select 19
    union all select 20
```

### Finding duplicate and missing numbers

Finding duplicate numbers is easy:

```sql
select id, count(*) from sequence
group by id
having count(*) > 1;
```

In this case there are no duplicates, since I'm not concentrating on that in this post (finding duplicates is straightforward enough that I hope you can see how it's done). I had to scratch my head for a second to find missing numbers in the sequence, though. Here is my first shot at it:

```sql
select l.id + 1 as start
from sequence as l
  left outer join sequence as r on l.id + 1 = r.id
where r.id is null;
```

The idea is to exclusion join against the same sequence, but shifted by one position. Any number with an adjacent number will join successfully, and the `WHERE` clause will eliminate successful matches, leaving the missing numbers. Here is the result:

| start |
|------:|
| 5     |
| 11    |
| 21    |

### Find ranges of missing values with subqueries

The above query identifies the start of ranges of missing numbers, but not the end. It also gives a false positive for 21, which is a missing number because it's off the end of the whole sequence. I wanted to solve both problems. After squinting at it a while, I realized I could solve this problem with a correlated subquery, as follows:

```sql
select start, stop from (
  select m.id + 1 as start,
    (select min(id) - 1 from sequence as x where x.id > m.id) as stop
  from sequence as m
    left outer join sequence as r on m.id = r.id - 1
  where r.id is null
) as x
where stop is not null;
```

The final `WHERE` clause makes sure the upper end of the sequence isn't counted as a hole. This can be written several ways, some of them without wrapping the whole thing in a subquery (for example, `where r.id is null and r < (select max(id) from sequence)`), but it suits me fine as it is. Here is the result:

| start | stop |
|------:|-----:|
| 5     | 5    |
| 11    | 14   |

If the sequence is a another data type, such as dates or letters of the alphabet, it is often possible to use some other functions to get the "next" value in the sequence in the join condition. For example, if the `id` column is `CHAR(1)`, here is a query for MySQL:

```sql
insert into sequence(id) values
    ('a'), ('b'), ('c'), ('e'),
    ('f'), ('g'), ('l'), ('m'), ('n');

select start, stop from (
    select char(ascii(m.id) + 1) as start,
        (select char(min(ascii(id)) - 1) from sequence as x where x.id > m.id) as stop
    from sequence as m
        left outer join sequence as r on ascii(m.id) = ascii(r.id) - 1
    where r.id is null
) as x
where stop <> '';
```

It's necessary to change the final `WHERE` clause to `stop <> ''` because `CHAR()` skips `NULL`s, converting `CHAR(NULL)` to the empty string. Here is the result:

| start | stop |
|-------|------|
| d     | d    |
| h     | k    |

### Performance analysis: rewriting without subqueries

I don't like correlated subqueries. In fact, I avoid subqueries if at all possible. Correlated subqueries are especially bad because, depending on the query optimizer, they may force the RDBMS to build a temporary table and probe into it for *each value* in the left-most table, which is {{< math >}} O(n^2) {{< /math >}}. It dawned on me that the query could be written as [left joins](/blog/2005/09/23/how-to-write-a-sql-exclusion-join/):

```sql
select l.id + 1 as start, min(fr.id) - 1 as stop
from sequence as l
    left outer join sequence as r on l.id = r.id - 1
    left outer join sequence as fr on l.id < fr.id
where r.id is null and fr.id is not null
group by l.id, r.id;
```

Of course, this is hardly, if at all, better. The `<` in the join condition makes the join essentially a `CROSS JOIN`, which is still an {{< math >}} O(n^2) {{< /math >}} join. Just to see how the query optimizer handles this, I ran it through both MySQL and Microsoft SQL server, and looked at the query plans. I filled the table with values up to 5000 (large enough that the DBMSs would create statistics on the index) and then made holes in the sequence as follows:

| start | stop |
|------:|-----:|
|     5 |    5 |
|    11 |   14 |
|   100 |  100 |
|   855 |  855 |
|  1230 | 1230 |
|  2400 | 2500 |

SQL Server actually optimized the first query significantly better, which highlights one of my favorite principles: **always measure performance**, and never try to "optimize by eye!" Here are the numbers:[^1]

```
-- query one --
Scans:                  9
Logical reads:         35
Physical reads:         0
Read-ahead reads:       0
CPU time:              10 ms
Elapsed time:          49 ms

 -- query two --
Scans:                  9
Logical reads:         77
Physical reads:         0
Read-ahead reads:       0
CPU time:              60 ms
Elapsed time:         148 ms
```

MySQL's results did not vary as much; the execution time was .8% faster on the first query, and the `EXPLAIN` result showed that the second query caused 'Range checked for each record'. The two query plans were actually very different, according to `EXPLAIN`.


[^1]: see my article about [using awk to sum up query statistics](/blog/2005/11/30/quickly-compile-query-statistics-from-sql-query-analyzer/)
