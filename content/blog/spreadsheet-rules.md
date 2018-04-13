---
url: /blog/spreadsheet-rules/
author: Baron Schwartz
categories:
- Desktop
- Programming
date: 2017-02-25T14:43:17-05:00
description: "Here are some practices I've found to help keep spreadsheets manageable over the years."
image: "media/2017/02/ledger.jpg"
title: Simple Guidelines For Maintainable Spreadsheets
---

The spreadsheet is one of the most powerful inventions in the history of
computing. But with that power comes responsibility: just as with a programming
language, the spreadsheet itself can become difficult to understand and
maintain. 

![Ledger](/media/2017/02/ledger.jpg)

<!--more-->

The fundamental issues that cause spreadsheets to be difficult to maintain over
time tend to be similar to those in computer programs: intent is obscured and
replaced with implementation; complexity grows nonlinearly; side effects cause
problems you don't foresee in advance; debugging is twice as hard as creating,
so the cleverest spreadsheet you can create is two times more complex than you
can debug. Here are some practices I follow to help make spreadsheets simpler
and easier to use and maintain.

### Create Visual Clarity

Visual clarity and simplicity are important for me to understand a spreadsheet.
Complexity makes my brain and eyes tired and confused more quickly.

Disable gridlines. Gridlines add a lot of clutter, and once you disable them
you'll discover they are not necessary. The content itself is
sufficient to establish rows and columns. Judicious use of borders, such as 
underlining the header row of a table, is easy to add later.

Begin the spreadsheet in row 2 and column B, leaving row 1 and column A blank.
This gives visual margins that add clarity. It also makes it easier to add
columns and rows without causing formatting issues or duplicating formulas in
unexpected ways. For example, it makes it easier to add a column without
including it in a named range or table.

Use "freeze panes" or drag dividers to create fixed rows that don't scroll, so
row and column headers are visible as you scroll through large amounts of
content. This is especially important if you are working on a large screen and
someone with a small screen might view the spreadsheet later.

### Obvious Is Better Than Clever

In some cases, hiding rows or columns can be powerful by removing distraction,
enabling the user to focus on an outcome or result instead of the process used
to achieve it. However, hidden rows and columns usually are a "bad smell,"
because their invisibility creates magical functionality that's difficult to
discover or understand. They're hard to maintain, too, because you'll often need
to examine them to understand the spreadsheet, and you'll have to unhide them
and hide them again to do that. Therefore, generally avoid hidden columns or
rows.

I wrote previously about [hacks to ignore missing
data](/blog/excel-hacks-to-ignore-missing-data/), which has examples of
techniques that need to be weighed carefully for benefits versus potential
drawbacks.

### Respect And Work With Data Flow

Cycles in spreadsheets are perfectly possible, but just like functions with many
exit points or side effects in a
program, they're a mess. But there are less obvious ways to create messy tangles
in your spreadsheets, too.

In general, it's ideal if data flow through equations is

1. Top to bottom
2. Left to right
3. Avoided between tabs/worksheets

This means that ideally, formulas only refer to cells above and to the left, so
as you read naturally you'll see data that's used in subsequent calculations,
not the result of things you haven't yet read (assuming your native language is
left-to-right).

This isn't always possible, and you'll immediately find reasons to disregard
this suggestion: percentages that refer to summaries at the bottom as well as
rows above, for example. But if you have a choice, following the flow will
create simpler spreadsheets. If rows use later rows as part of their formula,
you have to scroll to the bottom and then back up again to trace
what goes into the cell. If you can rearrange the table so the rows appear in
the order they're computed, it might flow more clearly.

When you manipulate large amounts of data to produce intermediate results and
then use them further, it's often a good idea to place those in their own
worksheets (tabs). If you do this, to the extent you can make source data flow
in only one direction, it'll also improve clarity. I usually do this by placing
my source tabs to the right, so data flows right-to-left. You could do it either
way, but the reason I do it "backwards" is so that as people read the tabs from
left to right, they're beginning with the summaries or outcomes, and can explore
the source data if they want. This follows the [McKinsey Pyramid
Principle](https://medium.com/lessons-from-mckinsey/the-pyramid-principle-f0885dd3c5c7),
which advocates beginning with the outcomes and saving the details for later.

Regardless, I try very hard to avoid making tabs depend on each other, i.e. some
columns in Sheet1 refer to columns in Sheet2, which uses columns in Sheet1
again. That's just a mess.

### Avoid Mixing Parameters Throughout

Spreadsheets often use parameters (inputs) to help model different scenarios:
cost per unit sold, sales rep quota, and so on. For maintainability, it's
important to separate out these parameters, ideally into a single place.

First, a rule I regard as a pretty strict one: do not hardcode literals into
formulas. If you think sales rep quota is $750k, don't write that into a
formula! Put it in a separate cell and refer to it. Hidden "magic numbers" are
the source of a lot of problems.

My other preference is to create a table of parameters, ideally in its own
tab/sheet. This way the parameters are isolated, so there's a single place to
find all of them, and you don't need to hunt around. You can also place remarks
next to them, explaining (is sales quota per-quarter or per-year; is it new
business only, or does it include renewals?). If not a separate tab, then in a
separate portion of the spreadsheet; for simple spreadsheets it is a lot less
work to have everything on one tab.

### Separate Charts From Data

I have found that keeping charts and data separate is helpful in many cases.
Placing charts on their own tabs avoids problems such as chart sizes changing
when new columns are created. And on most monitors, charts and data don't both
fit onto the screen unless they overlap, which causes problems.

A worksheet that has charts way at the bottom, where they'll never be discovered
unless you zoom way out or scroll way down, is very frustrating. In general,
too, a worksheet or tab that serves multiple purposes is an invitation to
ballooning complexity. The presence of several kinds of data in a single tab
seems to imply that just one more table or chart wouldn't hurt, and it takes on
a life of its own because it's not clear where it should stop.

### Conclusions

All of the above suggestions are just general guidelines, not hard-and-fast
rules. I break them all the time myself. But having worked on some fairly
complex spreadsheets, which are shared by multiple people and edited over long
periods of time, I've found that spreadsheets can become a lot more work in the
long run than I thought they would initially. I've slowly adopted these
practices to help with that problem. I'm sure there are spreadsheet experts with
more extensive guidelines, but this is what's worked for me so far.

[Pic Credit](https://pixabay.com/en/ledger-accounting-business-money-1428230/)
