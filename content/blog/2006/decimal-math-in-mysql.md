---
title: How to avoid imprecise DECIMAL math in MySQL
date: "2006-03-08"
url: /blog/2006/03/08/decimal-math-in-mysql/
categories:
  - Databases
---
MySQL versions 4.1 and below use imprecise math in operations with `DECIMAL` data, which is supposed to be precise (that's the whole point). There is no real solution to the problem, though there are workarounds. There is also at least one genuine bug in MySQL related to this problem. In this article I'll explain the problems, demonstrate them in action, and show you how to work around them.

### The problem

Many fractional values cannot be represented exactly as a [floating-point number](http://en.wikipedia.org/wiki/Floating_point) in computers. For example, the value one-tenth, which we represent as 0.1 in base ten, is impossible to represent exactly in base two. SQL databases provide fixed-point data types to support precision math where it is needed. Currency values are a typical use.

MySQL supports `DECIMAL` data types, which store numbers as strings instead of as numbers so there are no issues representing them exactly, but versions prior to 5.0 perform operations on the values with floating-point math. For example, the `SUM` function converts the string representation to floats before operating on them. This is documented in the [MySQL manual](http://dev.mysql.com/doc/refman/5.0/en/problems-with-float.html).

### Demonstration

I first encountered this problem while building a system to import my financial data into a database so I could query the transactions with SQL. I ran a query to find unbalanced transactions caused by splits that had been deleted:

```sql
select transaction, sum(amount) as amount
from split
group by transaction
having sum(amount) <> 0;
```

Here's the result:

| transaction                     |   amount |
|---------------------------------|---------:|
| 1198d02fd0d69f117f4617ba964b69f | -2103.00 |
| 182fedf6bf740de209da658362307d6 |     0.00 |
| 2054cd0a4ce9ef8c7c61625b8c8fe1d | -4288.60 |
| 3c6cb1aa8df451e0d2a234bea919edd |     0.00 |
| 559a3896c86610d860c37cd2ddd9d11 | -2977.52 |
| 81487469bdbc9e862ddaf068086aabe |    -0.00 |
| 8b35ecf20129dae97ba08cd75b6eb69 |  -875.70 |
| 96779b5478b7b4cda07e639729ac4ff |    -0.00 |
| 9906d1f5e2c30208f6c922db4c6eea0 | -2884.80 |
| a05aeca558816b7ed8e86b06cce1a60 |    -0.00 |
| a482d3416841b6870e22aeb7bc1e65b |    -0.00 |
| b1ae92ed169b21d7495b41c8980ae59 |  -886.82 |
| d96ac1878cbbc0b25324acf1304c5ec | -4792.32 |
| e8e1fcd15fc82ae2cdc057341efe4af |     0.00 |
| f5bfdeb0a7e93f501ca530663fa7ef9 | -3241.28 |

The comparison `sum(amount) <> 0` should have eliminated about half those tuples. The fact that it didn't, combined with the presence of -0.00 (negative zero), made me suspect floating-point values were being used behind the scenes. The numbers were being displayed as fixed-point, but if I could display them as floating-point, I could verify my theory. It's not possible to use `CAST` to cast a value to floating-point in MySQL 4.1, but I accomplished the same thing by multiplying the `amount` column by 1e1. When I did this, I found the numbers weren't exactly zero; they were just close, for example, 3.1086244689504e-13.

After hunting around for a while without luck, [I entered a bug report](http://bugs.mysql.com/bug.php?id=17742), which was changed to not-a-bug status with a friendly pointer to the documentation (oops!).

### The bug

There's still at least one real bug, though. The following query adds an `ORDER BY` clause to the query above:

```sql
select...
order by amount;
```

The results are interesting indeed!

| transaction                     |   amount |
|---------------------------------|---------:|
| d96ac1878cbbc0b25324acf1304c5ec | -4792.32 |
| 2054cd0a4ce9ef8c7c61625b8c8fe1d | -4288.60 |
| f5bfdeb0a7e93f501ca530663fa7ef9 | -3241.28 |
| 559a3896c86610d860c37cd2ddd9d11 | -2977.52 |
| 9906d1f5e2c30208f6c922db4c6eea0 | -2884.80 |
| 1198d02fd0d69f117f4617ba964b69f | -2103.00 |
| b1ae92ed169b21d7495b41c8980ae59 |  -886.82 |
| 8b35ecf20129dae97ba08cd75b6eb69 |  -875.70 |

What happened to the spurious results? They disappeared! An `ORDER BY` clause is never supposed to do anything but order the results; it certainly should not eliminate tuples. I think this is kind of weird, creepy and cool at the same time.

If I had to guess, I'd say the results are being ordered *before* they are filtered by the `HAVING` clause, and in the process, converted back to `DECIMAL` from float, then eliminated by the `HAVING`. That may not be what's really happening, but it seems likely.

This strange behavior raises the possibility of improving the code, too. Ordering may not be as efficient as it could be; it should be the last operation in a `SELECT` so it operates on as few tuples as possible. And an implicit cast forced by the ordering operation doesn't seem right, either; it means the ordering clause changes the values in the tuples as well as changing which tuples are present in the output. Both should be of concern.

### Workarounds

There is *no way to force precision math* in these types of operations. It cannot be done. No amount of casting or rounding will fix the problem reliably on every platform (math is different on every platform, and a "solution" may not work everywhere). There are a couple of workarounds, though.

*   Compare to an acceptable tolerance. For example, instead of `having sum(amount) <> 0`, use `having abs(sum(amount)) < .001`.
*   Add an `ORDER BY` clause! Just kidding.
*   Save the results in temporary tables, then perform further operations on them. Once they're stored in temporary tables, they will be cast back to their string representation and the close-but-not-quite values will become exact again.
*   Upgrade to version 5.0 or above, where exact math is implemented with 64-bit integer operations. Yay!

With a little imagination, it's probably possible to work around most situations. I hope this article helps you avoid possible problems with imprecise math.
