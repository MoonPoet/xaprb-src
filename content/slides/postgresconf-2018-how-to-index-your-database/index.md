---
title: How to Index Your Database
date: "2018-10-15"
url: "slides/postgresconf-2018-how-to-index-your-database/"
image: "slides/postgresconf-2018-how-to-index-your-database/unsplash-photos-4op9_2Bt2Eg.jpg"
description: "Do you know what database indexes are and how they work? Do they seem hard to understand? They don't have to be."
ratio: "16:9"
themes:
- apron
- adirondack
- descartes
---
class: title, shelf, smokescreen, no-footer
background-image: url(unsplash-photos-4op9_2Bt2Eg.jpg)

![Logo](vividcortex-horizontal-white-rgb.svg# smokescreen pa-2 br-3)

# How To Index Your Database
## Baron Schwartz &bullet; PostgresConf SV 2018 

---
layout: true
name: footer

.footer[
- @xaprb
- ![logo](vividcortex-horizontal-web.svg)
]

---
class: img-right-full
# Logistics and Stuff

![Baron Schwartz](headshot.jpg)

- Ask questions anytime
- Write me baron@vividcortex.com
- Tweet me at @xaprb
- Slides at [xaprb.com/talks/](https://www.xaprb.com/talks/)

---
# Introduction and Agenda

The purpose of this talk is to organize and understand the principles
of database indexing.

- What are indexes?
- What kinds are there?
- How do they work?
- What are the three purposes of an index?
- What are the six ways to best design and use indexes?

---
class: title, smokescreen
background-image: url(sanwal-deen-93466-unsplash.jpg)

# What Are Indexes?

---
class: compact, col-2
# Literally Everything You Need To Know About Indexes

Best-case B-Tree Height:

\\[
\left\lceil \log _ { m } ( n + 1 ) \right\rceil - 1
\\]

Worst-case B-Tree Height:

\\[
h \leq \left\lfloor \log _ { d } \left( \frac { n + 1 } { 2 } \right) \right\rfloor
\\]

Where:

\\[
f(x) = \int_{-\infty}^\infty \hat f(\xi)e^{2 \pi i \xi x} \,d\xi
\\]

And:

\\[
\left( \sum \_ { k = 1 } ^ { n } a \_ { k } b \_ { k } \right) ^ { 2 } \leq \left( \sum \_ { k = 1 } ^ { n } a \_ { k } ^ { 2 } \right) \left( \sum \_ { k = 1 } ^ { n } b \_ { k } ^ { 2 } \right)
\\]

---
# Just Kidding!

You don't need to know any of that nonsense.

---
# Indexes Help Find Data

Indexes are fast-lookup structures for the data in a table.

They essentially do two things with the data:

1. Maintain a **search-optimized copy** of the data.
--

2. Point to the data's **original location**.

---
class: img-right-full
![Table](table.png)

# How A Query Finds Rows In A Table

`SELECT c FROM t WHERE b < 70;`

This query must **examine every row** to find the right ones.

---
class: img-right-full
![Table and Index](table-and-index.png)

# How A Query Finds Rows With An Index

Indexes **help find rows** without full-scans.

* This is an index of columns (b, d).

--
* The index is a **sorted copy of those columns**.

--
* The query scans the index until `b >= 70`.

---
class: img-right-full

![Table and Index](table-and-index-pointers.png)

# How A Query Finds Rows With An Index

Indexes **help find rows** without full-scans.

* This is an index of columns (b, d).
* The index is a **sorted copy of those columns**.
* The query scans the index until `b >= 70`.
* The index has **pointers to the rows.**

---
class: roomy
# What About Starting From 70?

The index is more than a plain copy. It's organized in **seekable
ranges.**

--

That lets the database **seek to a starting point** in the
index.

---
class: roomy
# That's All You Need To Know

Just remember an index is a **sorted, searchable** copy of data.

--

* You don't need to know about **B-Tree Algorithms**.
* You don't need to know **data structures**.
* You don't need to understand \\( O(\log_{\frac{b}{k}}(n)) \\).

---
class: img-right-full

![Dragons Blood Tree](dragons-blood.jpg)

# B-Trees For The Curious

Most databases default to B-tree indexes.  
B-trees have sorted leaf nodes. They let the database:

* Find single rows
* Find ranges of rows
* Retrieve rows in sort order.

---
class: img-right-full

![Tool Bits](matt-artz-385667-unsplash.jpg)

# Other Kinds Of Indexes

There are special-purpose indexes for special purposes. Study them when you need
them.

* Hash indexes
* Log-Structured Merge indexes
* Full-text search (inverted) indexes
* Geospatial indexes
* Block-range indexes
* Bitmap indexes

---
class: title, smokescreen
background-image: url(dariusz-sankowski-46479-unsplash.jpg)

# Three Data Access Rules

---
class: img-right-full

![Table and Index](table-and-index-pointers.png)

# Three Data Access Rules

1. Reading a range of data in order is fast.
   * Scanning the index for `b < 70` is a range.

--
2. Reading a range out of order is slow.

--
3. A single-row retrieval or lookup is slow.
   * Finding each row in the table is a lookup.

---
class: title, smokescreen
background-image: url(elena-taranenko-541565-unsplash.jpg)

# Three Purposes Of An Index

---
class: img-right-full

![Colors](rawpixel-com-632461-unsplash.jpg)

# How Do Indexes Help?

1. Read less data.
2. Read data in bulk.
3. Read data presorted.

---
class: img-right-full

![Table Scan](table-scan.png)

# 1. Read Less Data

`SELECT c FROM t WHERE b < 70;`

--

Without an index, this is a full table scan that reads **all rows and all
columns**.

The red cells are the data we read needlessly.

---
class: img-right-full

![Index Scan](index-scan.png)

# 1. Read Less Data

`SELECT c FROM t WHERE b < 70;`

With an index, it reads **only matching rows**.

--

**Three inefficiencies remain**:

- It reads extra columns
- It reads from the table in random order
- It reads from the table row-by-row

---
class: img-right-full

![Covering Index](covering-index.png)

# 1. Read Less Data

Create an index with **all columns mentioned**: `index(b,c)`

`SELECT c FROM t WHERE b < 70;`

--

Now the index "covers" the query and it **doesn't access** the table at all!

- No extra columns
- No randomly ordered access
- No row-by-row lookups

---
class: img-right-full

![Starlings](james-wainscoat-521741-unsplash.jpg)

# 2. Read Data In Bulk

Indexes are sorted, so logically nearby rows are physically nearby.

Range queries will read pages that are **densely packed** with desired rows.

Densely packed pages let the database:
- Read fewer pages (goal #1)
- Read pages in sequential order, avoiding random reads

---
class: img-right-full

![Clustered Index](clustered-index.png)

# 2. Read Data In Bulk

To achieve this you can use *index-organized tables* or *clustered indexes*.

- The table itself is **sorted** in physical order
- The search-and-seek structures are built on the table, not separately

---
class: img-right-full

![Clustered Index](clustered-index-scan.png)

# 2. Read Data In Bulk

`SELECT c FROM t WHERE b < 70;`

The query scans a range from the table only.

- Bulk access
- Ordered access
- Some superfluous columns

---
class: img-right-full

![Balanced Stones](jeremy-thomas-75753-unsplash.jpg)

# 3. Read Data Presorted

Indexes are sorted, so the database doesn't need to sort.

This helps optimize queries such as:

- `ORDER BY`
- `GROUP BY`
- `DISTINCT`
- `MIN` and `MAX`

---
class: img-right-full

![Bowls](tom-crew-625205-unsplash.jpg)

# The Three-Star System

Grade an index with three stars, one for each:

- A star if the rows are densely packed.
- A star if the rows are sorted.
- A star if the query doesn't access the table.

The **third star** is often much more important!

---
class: title, smokescreen
background-image: url(denisse-leon-395932-unsplash.jpg)

# Six Ways To Optimize Index Usage

---
class: img-right-full

![Foliage](aaron-burden-151465-unsplash.jpg)

# 1. Don't Defeat Indexes

This query **defeats** an index on column `a`:

`... WHERE NOW() > a + INTERVAL 30 DAY;`

This query **can use** the index:

`... WHERE a < NOW() - INTERVAL 30 DAY;`

You can seek/search for a **value** in an index, but not for an **expression**.

---
class: img-right-full

![Right Suffix](right-suffix.png)

# 2. The Left-Prefix Rule

Multi-column indexes are sorted by column 1, then column 2, etc.

- Queries can use a **prefix of an index**.
- They generally **can't use a suffix**.

`WHERE c < 70` won't work, it will be a full index scan.

---
class: img-right-full

![Left Prefix](left-prefix.png)

# 2. The Left-Prefix Rule

A prefix specifies a range up to and including the **first inequality**.

`WHERE b < 70 AND c < 50`

Anything past the first inequality is sub-filtering the range: no longer bulk access.

* Place equalities first, ranges last
* Try supplying missing equalities or converting ranges to lists of values

---
# 3. Exploit Index-Only Queries

Create *covering indexes* for important queries (index-only queries).

Remember: it works only if the index has **all** the columns the query mentions.

It's often possible to union the indexes needed by several important queries.

---
# 4. Exploit Clustered Indexes

The benefit of a clustered index is the table is physically organized in PK order.

* Supported in Oracle, MySQL, SQL Server, IBM DB2 LUW
* Not supported in PostgreSQL, despite `CLUSTER` command (~ `DEFRAG`)

There can be **only one** clustered index per table.

---
# 5. Consider Column Selectivity And Order

Column order in compound indexes matters a lot!

* For queries:
	* The leftmost prefix rule applies
	* Makes indexes useful for queries, or not
* For data characteristics:
	* Organize by most-selective or least-selective
   * The best order depends on use-case: least for bulk reads, most for single-rows.

---
class: img-right-full

![Key](duplicate.jpg)

# 6. Avoid Over-Indexing...

Indexes add cost to writes and complicate the planner's job

* Avoid duplicates
* Analyze redundant indexes with a common prefix
* Analyze unused indexes 

---
class: img-right-full

![Spider Web](aaron-burden-27662-unsplash.jpg)

# 6. But Don't Fear Indexes

Caution: "unused" indexes often really aren't!

Indexes are a lot less expensive than you'd guess. Cost/benefit tradeoffs
usually weigh in favor of indexes.

For a rigorous analysis, see Lahdenmaki and Leach's book.

---
class: col-3
# Resources

[![Practical Query Optimization](practical-query-optimization.png)](https://www.vividcortex.com/resources/practical-query-optimization)

[![SQL Performance Explained](sql-performance.png)](http://sql-performance-explained.com/)

<br>

[![Lahdenmaki and Leach](lahdenmaki-leach.jpg)](https://www.amazon.com/Relational-Database-Index-Design-Optimizers-ebook/dp/B000PY48KE/)

---
# Slides and Contact Information

.qrcode.db.fr.w-40pct.ml-4[]

Slides are at https://www.xaprb.com/talks/ or you can scan the QR code.

License: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

Contact: @xaprb and baron@vividcortex.com

---
# Photo Credits

* [Dragon's Blood Tree](https://www.flickr.com/photos/rod_waddington/10941931846/)
* [Keys](https://www.flickr.com/photos/popilop/331357312/)
