---
title: How to install innotop on Microsoft Windows
date: "2006-11-11"
url: /blog/2006/11/11/how-to-install-innotop-on-microsoft-windows/
categories:
  - Databases
  - Open Source
---
I recently tested innotop on Microsoft Windows. There was one slight glitch, but I changed a couple lines of code, and now it runs out of the box under ActivePerl. Version 0.1.156 contains those changes for Windows compatibility.

### How to install

I installed it under ActivePerl 5.8.8 build 819:

1.  Download and install [ActivePerl](http://www.activestate.com/)
2.  After installation, open the Perl Package Manager from Start/Programs/ActivePerl 5.8.8 Build 819. Select Time-HiRes, DBD-mysql, and install them.
3.  Download and extract innotop and run it.

I also watched another person run it under ActivePerl 5.8.7.

That's it.

### Differences under Windows

If you have term-ansicolor , it is disabled because Windows terminals don't like the formatting characters. That makes the display a bit less compact, but such is life.

If you have any experience with other ways to run innotop under Windows (cygwin?), please let me know.

My next project is to take a number of samples of `SHOW INNODB STATUS `from MySQL running under Windows and make sure they're parsed correctly. I've read the source, but reading the source doesn't mean I've done it right. (Update: yep, I did it right).

**Update**: version 0.1.159 has additional fixes. A new Windows-specific configuration variable, `max_height`, defines how high the viewable window area is. Otherwise innotop can't figure out how much space it has to work with. I also fixed the code to work with MySQL 5.1's new `SHOW ENGINE` output (there is an extra column in the output).

**Update 2006-11-14**: version 0.1.160 has more Windows compatibility. An astute Perl hacker showed me how to get ANSI formatting codes to work in a Windows console, which allows bold and highlighted text and a more compact display (so you can get more on the screen). To get this to work, just install Win32::Console::ANSI. Yay!


