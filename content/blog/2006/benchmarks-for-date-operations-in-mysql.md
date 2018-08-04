---
title: Benchmarks for DATE operations in MySQL
date: "2006-06-12"
url: /blog/2006/06/12/benchmarks-for-date-operations-in-mysql/
categories:
  - Databases
---
This article compares the relative speed of extracting the date part of a value in MySQL with `LEFT()` and with the `DATE()` function.

`LEFT()` is faster than `DATE()`. To prove this, I inserted two million un-indexed sequential values into a table and selected the minimum and maximum values. Both queries are table scans, so it does read through all the records. The table below lists the time in seconds for `MAX()` on my computer. I tested with three data types: `DATE`, `TIMESTAMP` and `DATETIME`.

| Type      | Time for `DATE(col)` | Time for `LEFT(col, 10)` |
|-----------|-------------------:|-----------------------:|
| TIMESTAMP |               2.69 |                   1.28 |
| DATETIME  |               1.67 |                   0.48 |
| DATE      |               1.63 |                   0.39 |


I don't know why it's faster to use `LEFT()` than `DATE()`. I would assume the reverse to be true, but clearly it's not, at least on the systems I've tested.

The time for `MIN()` is one or two milliseconds faster than `MAX()`, probably because the values are sequential and only one assignment is performed, whereas the `MAX()` query must perform two million assignments.
