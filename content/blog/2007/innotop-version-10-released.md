---
title: innotop version 1.0 released
date: "2007-01-07"
url: /blog/2007/01/07/innotop-version-10-released/
categories:
  - Databases
  - Open Source
---
I've made the 1.0 release I promised yesterday, and it is available for download on the [innotop project homepage](http://code.google.com/p/innotop/).  I'm now working on version 1.3, which will become 1.4, which is on the road to version 2.0.  I've added a project roadmap for versions 1.4, 1.6, 1.8 and 2.0.

Thanks to Sebastien Estienne, who is maintaining the Debian/Ubuntu innotop packages, for helping me decide how to arrange the source repository, branching and tagging practices, and more.  He's right---once I have things set up right, it's not hard.  Go me!

Lenz Grimmer contributed an RPM spec file, which users can use to build an installable RPM directly from the tarball on RPM-based systems.  As soon as I verify that I've gotten it right, I'll make an unstable 1.3 release.  I'll write more about it then.  I hope at least some people will begin using 1.3 so I get feedback on the (many) changes I've made.

### A little bit of history

My baby is getting all grown up!  Many of you probably don't realize how innotop started.  Here's the email to my coworkers:

```
Date: Mon, 05 Jun 2006 09:57:32 -0400
From: Me
To: Greg, John, Alan, Peter
Subject: tool I wrote over the weekend

In my home directory on kenya, in bin/ you will find a little gizmo 
called innodb-tx-monitor, which I wrote over the weekend.  It parses the 
output of SHOW INNODB STATUS.  I am going to maintain and improve this 
and make it available on my website for the world to use, so if you have 
any improvements to suggest or code changes to make... it's definitely a 
rough draft as of this point, but hey.

I use it like this:

watch --interval=20 innodb-tx-monitor -host usa -user baron -db test -pw password

At some point I want to make it interactive-ish, like mytop, and not 
have to run within watch, and have a config file so the password isn't 
there for others to see on the command line, etc etc.  Lots of ideas. 
Send me yours :-)
```

I no longer have the code from that try---it was little more than a shell script at that time.  But the first version of innotop I committed to my CVS repository is 444 lines, *including a sample of the InnoDB monitor output I pasted in for my reference*, and InnoDBParser.pm was 394 lines total.  It looked like this when I ran it from `watch`:

![innotop](/media/2007/01/innotop-blast-from-past.png)

Given the transactions being held open for 23,000 seconds (it still makes me cringe), I'm sure you can see why I was motivated to write this utility.

Today innotop and InnoDBParser.pm are a combined total of over 5,000 lines of code.  If I'd written it in anything but Perl, it'd likely be many times that size.  Wow!

Happy 1.0, innotop!  Here's to a bright and useful future.


