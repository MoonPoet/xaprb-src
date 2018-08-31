---
title: 'Excel and Google Sheets Spreadsheet Productivity Tips'
date: "2018-08-30T20:33:03-04:00"
url: "/blog/spreadsheet-productivity-tips"
description: "Here are some of my favorite pro-tip secrets for working with spreadsheets."
credit: "https://unsplash.com/photos/Bd7gNnWJBkU"
image: "/media/2018/08/unsplash-photos-Bd7gNnWJBkU.jpg"
thumbnail: /media/2018/08/unsplash-photos-Bd7gNnWJBkU.tn-500x500.jpg
categories:
- Spreadsheets
---
This post is a collection of some things I've done to help me create and maintain complicated spreadsheets.
Spreadsheets can be enormously powerful, and it's probably not an exaggeration to say the world runs on spreadsheets.
But with that power comes complexity, and it's pretty hard to maintain a complicated spreadsheet.
Errors and inconsistencies can creep in quickly and can be really hard to find.
<!--more-->

Here's a few of my favorite ways to help manage that complexity.

### Use `OFFSET`

The `OFFSET` function introduces a level of indirection into a spreadsheet.
Instead of typing a cell or range by naming it directly, you can indicate the position and size of a range relative to a reference cell.
Using a parameter, which can come from another cell or from a formula, lets you change what cells a formula refers to, which can be really powerful.
For example, here's the simple way to calculate the sum of cells:

![Summing cells directly](/media/2018/08/sum-without-offset.png)

The following does exactly the same thing, but it's parameterized so you can control it:

![Summing cells with OFFSET](/media/2018/08/sum-with-offset.png)

Why on earth would you want to do that!?
The answer isn't obvious until you want to write formulas with ranges that automatically expand and adapt to the data you enter.
I'll show you some ways to do that later. But first, named ranges.

### Use Named Ranges

Naming ranges of cells makes it a lot easier to reference them in formulas.
This also helps avoid problems.
Would you notice if you meant to reference an entire range of cells in a formula, but you were off by one row or column?

In Excel you can give a range of cells a name and then reference it from a formula.
Select the cells, then right-click and define a name:

![Naming a range of cells in Excel](/media/2018/08/excel-define-name.png)

Then you can just use that name instead of a range in a formula:

![Referencing a named range of cells in Excel](/media/2018/08/excel-reference-name.png)

You can [name cells in Google Sheets](https://support.google.com/docs/answer/63175), too.

### Use Tables

Named ranges are pretty cool, but you can also use tables.
A table is a range of cells that not only is defined as such, but has extra meaning and behavior.
The default behavior is for each column to be named by its header, and automatically fill down the formulas of the first non-header row.
Use Insert -> Table to define a table:

![Creating a table in Excel](/media/2018/08/excel-define-table.png)

Then fill in the first row with formulas.
For example, you can square and cube the columns:

![Table formulas in Excel](/media/2018/08/excel-table-formula.png)

Now when you into the blank row under the bottom of the first column, the table autofills and the formula is copied into the other columns:

![Table autofills in Excel](/media/2018/08/excel-table-autofill.png)

Now your tables will be filled with the formulas you define just once in the first row, and you can reference columns by their headers in formulas, instead of using row:col coordinates.

This is a little more complicated to do in Google Sheets, but you can do it with combinations of things like array formulas and offsets.
To create an autofilling formula, enter your values.
Then use `OFFSET` and `COUNTA` to calculate how many values there are.
Wrap all of this with `ARRAYFORMULA` and square or cube the result, and you get exactly the same behavior as Excel:

![Creating a table in Excel](/media/2018/08/table-google-sheet-offset.png)

### Other Neat Tricks

Here's a few other things I've done occasionally:

- Use `COLUMNS` and `ROWS` to measure the distance between cells, and use those as parameters to `OFFSET`, thus making ranges expand to encompass the cells you want instead of needing to type in the size of the range you want.
- Use `UNIQUE` together with array formulas to define your own pivot tables with formulas, instead of using the pivot table builder. (It sometimes is overkill and has too much magic that you need to undo to get a simpler result, so sometimes it's best not to use built-in pivot tables.)
- Use `FILTER` to make a copy of data. You can either filter the copy to exclude some values, or you can make an unfiltered copy by providing a filtering expression that's always true.

These would require a lot of work to create examples to show you, so I'll leave these to your imagination.
Hopefully this post has stimulated your creative juices and you now see a few more things you didn't know you could do with spreadsheets!
Overall, if you are resourceful and know a few of the less-obvious spreadsheet functions, you can build complicated spreadsheets without repetition and mistakes.
Now go conquer the world with your choice of spreadsheet programs!
