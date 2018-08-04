---
title: How to use meta-data to sort itself
date: "2006-06-04"
url: /blog/2006/06/04/how-to-use-meta-data-to-sort-itself/
categories:
  - Databases
---
I'm a big fan of meta-data stored in the database. I love having a table that records arbitrary data about data. In fact, such a table can even be used to store meta-data about itself. In this article I'll explain how to use meta-data to define a sort order for both itself and the data to which it's related.

I've mentioned an online cemetery database several times. One of the great things about this project is it doesn't need custom-designed interfaces for every view on the data; the interfaces can be automatically generated. This was simple until the customer wanted the fields to be ordered a certain way. Since the interfaces are automatically generated from the meta-data, I hadn't built that feature in.

After bit of thought, I found a way to do it easily.

### The setup

Here's the table schema for the meta-data:

```sql
create table meta (
   t varchar(50) not null, -- table
   c varchar(50) not null, -- column
   name varchar(50) not null,
   value varchar(50) not null,
   primary key(t, c, name)
)
```

### Defining a sort order

I knew I wanted entries in this table to define a sort order. For the `marker` table, for instance, I'd need entries that looked like this:

| t      | c      | name | value |
|--------|--------|------|-------|
| marker | width  | sort | 1     |
| marker | height | sort | 2     |

... and so on. That data would sort the marker's width first, followed by the height, and so forth.

So far, so good. The only complicating factor was the customer wanted certain fields first, others all the way at the end, and the rest she didn't care about. To ease maintenance, I decided to leave the columns in the middle to fall where they may, so I needed my sorting technique to work correctly when sort order isn't specified.

I decided no table is likely to have more than a couple dozen columns, so I built in a "default" sort value of 50, and allowed pulling fields to the front with low numbers, or pushing them to the end with high numbers (up to 99). The resulting data looks like this:

| t      | c      | name | value |
|--------|--------|------|-------|
| marker | width  | sort | 1     |
| marker | height | sort | 2     |
| marker | notes  | sort | 98    |
| marker | misc   | sort | 99    |

### Getting the data

I wanted my interface-building query to retrieve all meta-data about the desired table, already sorted in the defined order (I don't like to sort things in code; that's what databases are for). The query to fetch the meta-data *without* the ordering is pretty simple:

```sql
select m.*
from meta as m
where m.t = 'marker'
```

To add the ordering, I have to join the meta table to the "sort" subset of itself. To make sure all the meta-data is included in the results even if it has no defined sort order, I use a left join. Since there's a left join, the "default" sort position of 50 is implemented with a `COALESCE`, and to make string data sort as though it's numeric, I left-padded everything with zeroes to a width of 2 characters:

```sql
select m.*
from meta as m
    left outer join meta as s on m.t = s.t
        and m.c = s.c
        and s.name = 'sort'
where m.t = 'marker'
order by lpad(coalesce(s.value, "50"), 2, "0")
```

*Et voila*, meta-data that sorts itself.
