---
title: How to group data in SQL with a catch-all bucket
date: "2005-09-28"
url: /blog/2005/09/28/grouping-data-with-catch-all-ranks/
credit: "https://unsplash.com/photos/dMeEJRE18VI"
image: "/media/2005/09/unsplash-photos-dMeEJRE18VI.jpg"
categories:
  - Databases
---
In this article I'll show you how to group data into defined buckets, putting everything that doesn't fit into the defined buckets into a catch-all bucket.

For example, suppose my data is online ads, and I store each ad's current position in an integer column. The ads compete against ads from other advertisers, and the top bidder gets position 1. I want to count how many ads are in positions 1 through 5, with 6 through infinity lumped together. The results should look something like the following:

| rank | num |
|-----:|----:|
| 1    | 6   |
| 2    | 8   |
| 3    | 13  |
| 4    | 18  |
| 5    | 11  |
| 6    | 90  |

### Setup and sample data

Here are some queries to create 1000 rows of sample data, with ranks from 1 to 20. First, for Microsoft SQL Server:

```sql
create table #ad (
    rank int not null
)

insert into #ad(rank)
   select top 1000 cast(rand() * 19 + 1 as int)
   from number;
```

And for MySQL:

```sql
create table ad (rank int not null);
insert into ad (rank)
   select rand() * 19 + 1
   from number limit 1000;
```

### The queries

Here's a query for Microsoft SQL Server:

```sql
select
    case when rank &lt;= 5 then rank
        else 6
    end as rank,
    count(*) as num
from #ad
group by
    case when rank &lt;= 5 then rank
        else 6
    end
order by
    case when rank &lt;= 5 then rank
        else 6
    end;
```

And for MySQL:

```sql
select
    case when rank &lt;= 5 then rank
        else 6
    end as rank,
    count(*) as num
from ad
group by
    case when rank &lt;= 5 then rank
        else 6
    end
order by
    case when rank &lt;= 5 then rank
        else 6
    end;
```

The results on my data set are as follows:

| rank | num |
|-----:|----:|
|    1 |  28 |
|    2 |  56 |
|    3 |  59 |
|    4 |  64 |
|    5 |  53 |
|    6 | 740 |

Your results will vary because of the `RAND()` function.

### Shortening the code for readability

In MySQL, it's possible to make the query a bit shorter by referring to the result's `rank` column in the `GROUP BY` and `ORDER BY` clauses. This only works if the column is aliased to a different name than it has in the table. Aliasing a column in the result set to the same name as a column in the base table will confuse MySQL. For example, this works fine:

```sql
select
    case when rank &lt;= 5 then rank
        else 6
    end as bucket,
    count(*) as num
from ad
group by bucket
order by bucket
```

This, however, doesn't:

```sql
select
    case when rank &lt;= 5 then rank
        else 6
    end as rank,
    count(*) as num
from ad
group by rank
order by rank;
```

This query works fine on earlier versions of MySQL such as 3.23, but in later versions such as 5.x, it groups and orders by the *table's* `rank` column, not the *result's*. The result set changes to the following:

| rank | num |
|-----:|----:|
|    1 |  28 |
|    2 |  56 |
|    3 |  59 |
|    4 |  64 |
|    5 |  53 |
|    6 |  53 |
|    6 |  55 |
|    6 |  52 |
|    6 |  46 |
|    6 |  49 |
|    6 |  54 |
|    6 |  46 |
|    6 |  48 |
|    6 |  52 |
|    6 |  48 |
|    6 |  45 |
|    6 |  55 |
|    6 |  60 |
|    6 |  48 |
|    6 |  29 |
