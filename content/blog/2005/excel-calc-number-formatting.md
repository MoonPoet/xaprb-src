---
title: Excel vs. OpenOffice.org Calc in number formatting
date: "2005-12-30"
url: /blog/2005/12/30/excel-calc-number-formatting/
categories:
  - Spreadsheets
---
I was playing with custom format strings in Excel recently and noticed something odd. The number of digits to the left of the decimal place seemed to vary bizarrely when using custom format strings for exponential notation, in ways that contradict the documentation. OpenOffice.org doesn't exhibit the same wackiness. Which spreadsheet formats numbers more sanely?

![Excel vs. Calc](/media/2005/12/excel-vs-calc.jpg)

If you're not familiar with custom format strings, it's just a way of making your own format. You can right-click on a cell, choose "Format Cells..." and click Custom at the bottom of the list, then enter a formatting string. The formatting syntax is used throughout Windows, and you rub elbows with it any number of ways when you program the Windows API, but the documentation seems to be only about 90% consistent between, say, Excel and the [.NET Numeric Format Strings documentation](http://msdn.microsoft.com/library/en-us/cpguide/html/cpconNumericFormatStrings.asp).

Back to the data I was seeing with Excel. I wanted to have two digits to the left of the decimal point and two to the right, for a total of four significant figures; the exponent should be zero-padded so it's two digits as well. Here is how you can do that with Excel, according to the documentation: `00.00E+00`. Sounds good, but it doesn't work in practice. Here's some data, the actual results, and what I expected:

|        Number | Actual Result | Expected Result |
|--------------:|--------------:|----------------:|
|       1209384 |    120.94E+04 |       12.09E+05 |
|     192939393 |     01.93E+08 |       19.29E+07 |
|          1293 |   1293.00E+00 |       12.93E+02 |
| 3910102935348 |     03.91E+12 |       39.10E+11 |

Wacky! Why on earth would Excel choose to format these numbers like it does? I played around with it for a while; it seemed to be unpredictable. It would put too many digits to the left of the decimal point, then when the number got one digit larger, suddenly switch to too few with a much larger exponent---what the heck? Then my coworker noticed the exponent Excel chose was always a multiple of four. I played around with more formats and figured out why: the exponent is a multiple of the number of digit placeholders to the left of the decimal point. Here is a table that makes this clear:

|        Number | ##00.00E+00 | #00.00E+00 | 00.00E+00 |
|--------------:|------------:|-----------:|----------:|
|             1 |   01.00E+00 |  01.00E+00 | 01.00E+00 |
|            12 |   12.00E+00 |  12.00E+00 | 12.00E+00 |
|           123 |  123.00E+00 | 123.00E+00 | 01.23E+02 |
|          1234 | 1234.00E+00 |  01.23E+03 | 12.34E+02 |
|         12345 |   01.23E+04 |  12.35E+03 | 01.23E+04 |
|        123456 |   12.35E+04 | 123.46E+03 | 12.35E+04 |
|       1234567 |  123.46E+04 |  01.23E+06 | 01.23E+06 |
|      12345678 | 1234.57E+04 |  12.35E+06 | 12.35E+06 |
|    1234567890 |   12.35E+08 |  01.23E+09 | 12.35E+08 |
|   12345678901 |  123.46E+08 |  12.35E+09 | 01.23E+10 |
|  123456789012 | 1234.57E+08 | 123.46E+09 | 12.35E+10 |
| 1234567890123 |   01.23E+12 |  01.23E+12 | 01.23E+12 |

Notice how the exponent is always a multiple of four in the first column, three in the second and two in the third.

I can't find where this is documented, and it definitely contradicts the existing documentation which says those digits are used to control how the number, not the exponent, is formatted. I searched around the web and found other people agreed with me. OpenOffice.org's Calc, on the other hand, clearly specifies that you control the number of significant digits, and the exponent is dependent on the value and the number format---so you really do have control over how the number itself is formatted. Here is the same data in Calc:

|        Number | ##00.00E+00 | #00.00E+00 | 00.00E+00 |
|--------------:|------------:|-----------:|----------:|
|             1 | 1000.00E-03 | 100.00E-02 | 10.00E-01 |
|            12 | 1200.00E-02 | 120.00E-01 | 12.00E+00 |
|           123 | 1230.00E-01 | 123.00E+00 | 12.30E+01 |
|          1234 | 1234.00E+00 | 123.00E+01 | 12.34E+02 |
|         12345 | 1230.00E+01 | 123.50E+02 | 12.30E+03 |
|        123456 | 1235.00E+02 | 123.46E+03 | 12.35E+04 |
|       1234567 | 1234.60E+03 | 123.00E+04 | 12.30E+05 |
|      12345678 | 1234.57E+04 | 123.50E+05 | 12.35E+06 |
|    1234567890 | 1235.00E+06 | 123.00E+07 | 12.35E+08 |
|   12345678901 | 1234.60E+07 | 123.50E+08 | 12.30E+09 |
|  123456789012 | 1234.57E+08 | 123.46E+09 | 12.35E+10 |
| 1234567890123 | 1230.00E+09 | 123.00E+10 | 12.30E+11 |

Which is better? Well, it depends. I'm categorically in favor of OpenOffice.org because it's [Free Software](http://www.gnu.org/philosophy/free-sw.html), of course. I also think it's a superior product in many ways: openness, standards compliance, price, security, interoperability, and so forth. But in this particular aspect, I can't really say which is "better." The two products have different ways of doing it, that's all. If I want to control how my numbers are formatted, I go with OpenOffice.org. On the other hand, Excel's "feature" seems to lend itself well to engineering notation---a way to write numbers with exponents that are multiples of three, which correspond to Metric unit prefixes such as kilo, nano and so forth. Engineering notation requires control over significant figures though, which Excel throws out the window! (You can choose the "scientific" number format and select a number of decimal places, but that's not exactly the same thing).

Even though OpenOffice.org is better, I'm going to avoid the "which is better" question and ask the questions I've not been able to answer: can I use "engineering notation" in Excel and get it to honor my instructions about significant figures? Can I get OpenOffice.org to do engineering notation? And finally, if anyone knows of some authoritative specification of how Microsoft products do number formatting, I'd be grateful for a link, because I can't find it---the documentation I see is really poor (I have no such problem with Calc, and if I did, I could look at the source code). If I find any answers of my own to these questions, I'll update this post.

And in case you're wondering whether this post is related to my work on [date formatting in JavaScript](/blog/2005/12/12/javascript-closures-for-runtime-efficiency/), yes it is. I'll be finishing up some work on number formatting soon. I just need to write more unit tests.
