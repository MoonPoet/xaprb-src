---
title: "WordPress and MySQL's strict mode"
date: "2013-03-15"
url: /blog/2013/03/15/wordpress-and-mysqls-strict-mode/
categories:
  - Databases
credit: "https://unsplash.com/photos/Dm974WDaErc/download"
image: "/media/2013/03/unsplash-photos-Dm974WDaErc.jpg"
---
I really don't like [running my database in "I Love Garbage" mode](/blog/2012/12/23/handling-mysqls-warnings-in-go-code/), so I set the following `SQL_MODE`:

```
STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER,NO_AUTO_VALUE_ON_ZERO, NO_ENGINE_SUBSTITUTION,NO_ZERO_DATE, NO_ZERO_IN_DATE,ONLY_FULL_GROUP_BY
```

Guess what WordPress does with that? It doesn't install. If you set the `SQL_MODE` to empty and install WordPress, then restore the `SQL_MODE`, WordPress will run, but if you try to create a post you'll see an error page that says "You are not allowed to edit this post."

This problem was [reported to WordPress at least 7 years ago](http://wordpress.org/support/topic/posts-not-saving-to-database). Lessons learned:

*   There is a huge amount of software that was built to work with MySQL 3.23&#8242;s irritating habit of inserting different data than you told it to, with nothing but a warning most people will never see.
*   That software will break in unlovely ways when you try to make MySQL behave more correctly.
*   Those who gripe about MySQL's bugs (as I sometimes do) should remember that MySQL is probably better quality than most of the software that is built to use it. This is probably a universal truth---the Linux kernel is probably better quality than most software that runs in Linux, for example.
*   MySQL's bugs often get fixed faster than aforementioned software's bugs, too.
