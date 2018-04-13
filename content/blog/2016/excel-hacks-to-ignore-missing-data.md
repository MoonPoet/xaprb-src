---
url: /blog/excel-hacks-to-ignore-missing-data/
title: Excel Hacks To Ignore Missing Data
date: '2016-11-20T11:11:14-05:00'
author: Baron Schwartz
categories:
- Desktop
- Math
- Programming
description: Here are two alternatives to straightforward spreadsheet syntax when
  annoying errors seem to make things more difficult than needed.
image: media/2016/11/min-error.png
draft: false

---
I've done quite a bit of work with Excel over the last few years, and I've found a couple of recurring problems when there's missing or error data in ranges. I've had to work around this enough times that I thought it was worth sharing the solutions I've used.

![Beautiful green bird eating orange peels](/media/2016/11/pexels-photo-191757.jpeg)

<!--more-->

### Using AGGREGATE() Instead Of MIN()

Aggregate functions such as `MIN()` and `SUM()` often produce errors when they're defined over a range with missing or bogus data. Although this is good, I often want to create a spreadsheet that operates over a fixed range, with computations based on that range. And I want to avoid complicated `IF()` or error-handling in long formulas, which make them hard to maintain and understand. In some cases, I've found that there's really no way to solve the problems through that approach anyway. For example, if I use `IFERROR()` and output a 0 when there's an error, the next set of cells that are derived from that output will divide-by-zero and it's just turtles all the way down.

With the `AGGREGATE()` function, I have found a way to solve some of these issues. In return for using a function whose meaning and syntax is a little confusing, I can centralize all the mess into one place instead of smearing it all over the entire spreadsheet.

Here's an example. I've entered some numbers in a range, and then filled the rest of the range with `=LOG(0)` to create an error. Then I've tried to take the `MIN()` of B6:B15 in cell C6\. This results in an error, of course.

![min-error](/media/2016/11/min-error.png)

You can solve this with the `AGGREGATE()` function. You have to look up the documentation for the syntax and meaning of each set of options, but in short, you can specify an aggregate operation, extra arguments, and what to do if there are errors. Here's how to get the `MIN()` result I want:

![min-error](/media/2016/11/aggregate.png)

### Using OFFSET() To Create Ranges

Sometimes I haven't been able to work around all the challenges using `AGGREGATE()` and I've needed to specify a variable-sized range. This is possible with the `OFFSET()` function.

For example, suppose I want to do linear regression using the `LINEST()` function, but part of the range might contain errors or non-values. After typing in the formula in cell D6 and using the "array formula" command (Control-Shift-Enter), I get the following:

![linest-error](/media/2016/11/linest-error.png)

`OFFSET()` can help. It defines a range relative to a specified cell. You specify where the range begins, and how many rows and columns it covers. As long as the range contains a contiguous set of values (all the non-values are at the end), `OFFSET()` together with `COUNT()` can define a variable-sized range that adapts to the valid set of cells. `COUNT()` counts the number of valid values in the range, so you can use it as the argument to `OFFSET()` to set the size of the resulting range.

Here's the solution in action on my example spreadsheet. I'm using `OFFSET()` to specify the first two parameters to `LINEST()`, defining the ranges C6:C10 and B6:B10.

![linest-using-offset-count](/media/2016/11/linest-using-offset-count.png)

The caveat with `OFFSET()` is that, unlike explictly setting a range with cell identifiers, Excel won't adjust the range when you do things like deleting rows from the middle of it.

### Conclusion

Both of these workarounds introduce their own complexities: with `AGGREGATE()` you're adding a more obscure syntax, and with `OFFSET()` you're circumventing some of Excel's features to help maintain and adapt your spreadsheet. In both cases, though, I've found that in some circumstances the net outcome is a simpler, more comprehensible spreadsheet overall.

[Pic Credit (which has nothing to do with anything, but it's pretty)](https://www.pexels.com/photo/green-and-lime-bird-on-gray-wood-log-191757/)
