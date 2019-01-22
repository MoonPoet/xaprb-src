---
title: 'How To Color Spreadsheet Rows Automatically'
date: "2018-08-26T21:13:40-04:00"
url: "/blog/spreadsheet-row-formatting-productivity-tip"
description: "This spreadsheet formatting tip could save you time and make you more productive."
credit: "https://unsplash.com/photos/Ilpf2eUPpUE"
image: "/media/2018/08/unsplash-photos-Ilpf2eUPpUE.jpg"
thumbnail: /media/2018/08/unsplash-photos-Ilpf2eUPpUE.tn-500x500.jpg
categories:
- Spreadsheets
---
Do you use spreadsheets to organize and categorize lists of things?
I do, and using conditional formatting rules helps me stay efficient and accurate.
This saves me time and makes me more productive.
Here's how I do it in Google spreadsheets.
<!--more-->

When I'm maintaining a list of things, and I want to draw attention to specific ones, I use conditional formatting rules to color an entire row based on the value of a single column.
For example, I maintain a spreadsheet of conferences I'm speaking at.
When I'm accepted to speak, I put a 'y' in the `Accepted` column, and unless I also have 'y' in the `Hotel` and `Flights` columns, that row will turn red, reminding me to book my flights and reserve a hotel.
I have a half-dozen other coloring rules in this spreadsheet, drawing my attention to actions taken, hiding ones I won't attend, and so forth.

![Conference planning spreadsheet with row-coloring rules](/media/2018/08/conference-planning-spreadsheet.png)

This technique comes in handy all the time.
My colleagues and I are continually sharing spreadsheets of things to do, and it seems there's always a reason to color-code something based on category or status.
For example, a couple of us went to a conference recently, and the marketing department built us a spreadsheet of everyone we should prioritize meeting there.
We color-coded customers, partners, investors, and other categories of people differently.

To configure row-coloring rules like this, drag your mouse to select the columns or range of cells you want to color.
Then use the "Format > Conditional formatting..." menu item to open the rules editor.
The editor opens a dialog to configure a new rule (or shows existing rules, and an option to add a new one).
The new rule defaults to "Format cells if... Cell is not empty."
You need to change this to "Custom formula is" instead.

Here's an example of some of my formulas:

![Spreadsheet conditional format rules](/media/2018/08/conditional-format-rules.png)

The trick is to enter the formula like this: `=$A:$A="y"` where `$A` and `$A` are the column, and `"y"` is the value you want to match.
Don't forget to start the entire formula with the `=` symbol!

You can also enter more advanced rules.
For example, here's one that color-codes the entire row red if I'm planning to attend a conference, and it's less than 45 days away, and I haven't booked flights or reserved a hotel yet:

```
=AND($M:$M="y", DATEDIF(TODAY(), $O:$O, "D") < 45, OR(ISBLANK($K:$K),ISBLANK($L:$L)))
```

Bonus points: you can use [checkboxes](https://support.google.com/docs/answer/7684717) instead of text values like `"y"` and make your spreadsheets more visual and interactive.
