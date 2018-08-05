---
title: Get Maatkit fast from the command line
date: "2008-05-21"
url: /blog/2008/05/21/get-maatkit-fast-command-line/
categories:
  - Databases
  - Open Source
---
I have been using Maatkit in a different way since I joined [Percona](http://www.percona.com/) as a consultant. When I'm working on a system now, it's a new, unfamiliar system---not one where I have already installed my favorite programs. And that means I want to grab my favorite productivity tools fast.

I intentionally wrote the [Maatkit](http://www.maatkit.org) tools so they don't need to be "installed." You just run them, that's all. But I never made them easy to download.

I fixed that. Now, at the command line, you can just run this:

```
wget http://www.maatkit.org/get/mk-table-sync
```

Now it's ready to run. Behind the scenes are some Apache mod_rewrite rules, a Perl script or two, and Subversion. When you do this, you're getting the latest code from Subversion's trunk.\[1][2\] (I like to run on the bleeding edge. Releases are for people who want to install stuff.)

Because there's some Perl magic behind it, I made it even easier---it does pattern-matching on partial names and Does The Right Thing:

```
baron@kanga:~$ wget http://www.maatkit.org/get/sync
--21:38:50--  http://www.maatkit.org/get/sync
           => `sync'
Resolving www.maatkit.org... 64.130.10.15
Connecting to www.maatkit.org|64.130.10.15|:80... connected.
HTTP request sent, awaiting response... 302 Moved
Location: http://www.maatkit.org/get/mk-table-sync [following]
--21:38:50--  http://www.maatkit.org/get/mk-table-sync
           => `mk-table-sync'
Connecting to www.maatkit.org|64.130.10.15|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [application/x-perl]

    [      <=>                            ] 163,259      136.51K/s             

21:38:51 (136.13 KB/s) - `mk-table-sync' saved [163259]
```

The redirection is there because otherwise wget will save the file under the name 'sync' instead of 'mk-table-sync'.

And if you've forgotten which tools exist, you can just click on over to <http://www.maatkit.org/get/> and see.

A quick poll: instead of getting the latest trunk, should this give you the code from the last release? I can do that, if you want.

[1] OK, it's only refreshed every hour. So you're getting code that's up to an hour old.

[2] **update:** now /get/foo gets the latest release, and /trunk/foo gets the latest trunk code.


