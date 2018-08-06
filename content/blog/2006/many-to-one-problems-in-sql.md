---
title: How to avoid many-to-one problems in SQL
date: "2006-03-11"
url: /blog/2006/03/11/many-to-one-problems-in-sql/
categories:
  - Databases
---
It's been a while since I've posted an abstract, theoretical article on a fine point of SQL. Today I want to bring your attention to two ways in which an RDBMS can allow you to do something that has no well-defined result. These involve queries where several values are eligible, but only one is chosen---and chosen in an undefined manner. I'll show you the two blunders, tell you when they might occur, and explain how to avoid them.

### Selecting an un-grouped column in a grouped query

As far as I know, this bad behavior only applies to MySQL. As the manual explains, MySQL "[extends the use of `GROUP BY`](http://dev.mysql.com/doc/refman/5.0/en/group-by-hidden-fields.html?ff=nopfpls)" to allow selecting columns that do not appear in the `GROUP BY` clause. What does this mean? Well, suppose I have the following data:

| Fruit   | Price |
|---------|-------|
| Apples  | 5.00  |
| Apples  | 5.00  |
| Oranges | 6.00  |
| Oranges | 4.00  |

MySQL lets me write the following query against the data:

```sql
select Fruit, Price, count(*) as c
from Fruits
group by Fruit;
```

The results will look like this:

| Fruit   | Price | c |
|---------|-------|---|
| Apples  | 5.00  | 2 |
| Oranges | 6.00  | 2 |

Here's the problem: the query groups the tuples (rows) into two groups, one group containing two Apples and one with two Oranges. **I can't logically get "the price" from two tuples in a group, because there is no one "the" price**. In the formal mathematics upon which SQL is based, this query is nonsense. MySQL's documentation admits as much, and tells me not to do this unless all the tuples in the group have the same value in that column---or I'll risk getting unpredictable behavior. In my example, it's pretty easy to see MySQL chooses the value from the "first" tuple in the group (a funny notion, given that there is no first tuple because *sets are theoretically unordered*).

This is a bad behavior introduced solely for the sake of optimization, and the documentation admits that. Grouping requires sorting, which requires comparing values, so grouping literally by as few columns as possible---even when the logical grouping may be by more columns---is an (ill-gotten) efficiency gain.

As with any other non-standard technique, the benefit is offset by lack of portability. Plus, it might cause evil glares from colleagues ;-).

To avoid this problem on MySQL, use standard SQL (sorry for stating the obvious). To make my query standard SQL, I'd either have to use an aggregate function on that column, such as `SUM`, `MIN`, `AVG`, `MAX` or similar---or, I could add the column to the `GROUP BY` clause, which would separate the results into more groups and change the output. In other words, every column must either be in the grouping clause or an aggregate function.

Some platforms, such as SQL Server 2000, will not allow the query. MySQL can be made to throw an error too, if `ONLY_FULL_GROUP_BY` mode is enabled.

It's important to group the query by the *data*, not by the expressions used to transform the data. Programmers who don't really understand what's going on sometimes just change the code to make the errors stop, often making an even worse mess out of the query. Watch out for this. Here's a good article on [how to group queries properly](http://weblogs.sqlteam.com/jeffs/archive/2005/12/14/8546.aspx).

### Updates from a join

Unlike the first gotcha above, this one can happen systems other than MySQL. The issue is an `UPDATE` in a join with a `FROM`, where tuples from the base table being updated appear multiple times. Here is a query:

```sql
update t1
   inner join t2 on t1.id = t2.id
set t1.col1 = t2.col1;

/* Equivalent syntax for SQL Server 2000
update t1
   set t1.col1 = t2.col1
   from t1 inner join t2 on t1.id = t2.id
*/
```

If you're used to seeing it, it may look like there's nothing wrong with that query. Suppose, though, that my data looks like this:

| Fruit   | Price |
|---------|-------|
| Apples  | NULL  |
| Oranges | NULL  |

(Ignore for a moment that this table has pretty much the same data as the Fruits table...)

I'll re-write the query to show how I might unwittingly update a FruitPrices tuple from multiple Fruits tuples:

```sql
update FruitPrices as fp
   inner join Fruits as f on f.Fruit = fp.Fruit
set fp.Price = f.Price;
```

What does this statement actually do? Well, logically it first [joins the base tables together](/blog/2005/10/03/understanding-sql-joins/):

| Fruit   | Price | Fruit   | Price |
|---------|-------|---------|-------|
| Apples  | NULL  | Apples  | 5.00  |
| Apples  | NULL  | Apples  | 5.00  |
| Oranges | NULL  | Oranges | 6.00  |
| Oranges | NULL  | Oranges | 4.00  |

Next it updates each `Price` value in the left-hand side from the column on the right-hand side. But wait, the value appears twice---that means logically, Apples are being assigned $5.00 twice, and Oranges are being assigned both $4.00 and $6.00 prices. Danger, Will Robinson! Which one wins? As it turns out, in MySQL again the "first" value wins. Not in SQL Server 2000, though---the "last" one wins on that platform, if memory serves. It doesn't really matter the particulars of which value wins; it would be more legitimate if the database server threw an error, in my opinion.

I can think of a few ways to avoid this situation.

#### Method 1: Avoid non-standard syntax

Neither syntax above is standard, and neither makes any sense from a true relational standpoint, which is why they have undefined, vendor-specific behavior. A standard `UPDATE` statement does **not** have a `FROM` clause. Joe Celko has [written](http://groups.google.com/group/microsoft.public.sqlserver.programming/browse_thread/thread/c7bff2f93c2a90e0/e9cb0f92a9361619%23e9cb0f92a9361619?sa=X&oi=groupsr&start=1&num=3) extensively about this, saying that "the correct syntax for a searched update statement is [the below]... The `UPDATE` clause simply gives the name of the base table or updatable view to be changed."


```sql
<update statement> ::=
  UPDATE <table name>
     SET <set clause list>
  [WHERE <search condition>]

<set clause list> ::=
  <set clause> [{ , <set clause> }...]

<set clause> ::= <object column> = <update source>

<update source> ::= <value expression> | NULL | DEFAULT

<object column> ::= <column name>
```

That's not terribly enlightening to most people, especially those not used to reading BNF! Let me try to correct the query:

```sql
update FruitPrices as fp
   set fp.Price =  (
      select f.Price from Fruits as f
      where f.Fruit = fp.Fruit);
ERROR 1242 (21000): Subquery returns more than 1 row
```

Oops! It looks like MySQL is now complaining about me trying to update a single value from a whole set of values! Very good. This shows me that my query is wrong, instead of silently doing something bad. Here's a query that works:

```sql
update FruitPrices as fp
   set fp.Price =  (
      select max(f.Price) from Fruits as f
      where f.Fruit = fp.Fruit);
```

#### Method 2: Join one-to-one

The second way, if you must use non-standard, mathematically invalid syntaxes, is to make sure the join is based on indexes and primary keys in such a way that the many-to-one problem doesn't happen. For example, if the columns used in the join criterion are the primary key in the right-hand base table, it's safe.

#### Method 3: Group the right-hand side

The last is to follow the advice of the article linked above and group the right-hand table appropriately. This is effectively the same thing as my second suggestion.

You can create the tables I'm using with the following scripts:

```sql
create table Fruits(
   Fruit varchar(50),
   Price decimal(3,2));

create table FruitPrices(
   Fruit varchar(50) not null primary key,
   Price decimal(3,2));

insert into Fruits values
   ("Apples", 5.00),
   ("Apples", 5.00),
   ("Oranges", 6),
   ("Oranges", 4);

insert into FruitPrices(Fruit)
   values("Apples"), ("Oranges");
```

### What's really wrong with these queries?

The relational model, which SQL doesn't follow exactly, is all about functions in the mathematical sense. Recall a function is just a mapping from the domain to the range, and one input value from the domain must produce exactly one output in the range. A given input value may not map to two output values. This is why a lot of functions can't be turned around backwards and still be functions. For example, `sin(0)` is 0, but so is `sin(2*pi)`, and `sin` is a function; but the inverse isn't a function. If you turn `sin` around and try to put 0 into the back end, what do you get out? You get 0, and 2*pi, and ... infinitely many other values.

The incorrect statements I've shown above make no sense because they're trying to shove data into a function backwards, and there can be more than one result on the output. I've shown how RDBMSs often just pick one of the outputs, and it's fine to know that's going to happen, but it's also important to know what is really going on.

This really does matter. Two days ago at work, my boss brought up a situation where a production query on our main database server had created a bad situation because of updates in a join. Bogus!
