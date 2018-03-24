---
title: 'Configuring Chrome for Privacy and Convenience'
date: "2018-03-23T22:15:52-04:00"
categories:
  - Privacy
author: "Baron Schwartz"
description: "Here's the settings I configure to keep my browser from accumulating a lot of history and tracking cookies."
image: "media/2018/03/pocket-watch-3156771_1280.jpg"
---

I've recently set up a new MacBook, which helped remind me of some of the
settings I've configured in the Google Chrome browser, to keep it from
accumulating lots of "stuff" over time: history, cookies, and so forth. The
accumulation of this stuff eventually represents a loss of privacy and control
that I dislike. On the other hand, browser features such as history are
convenient, and I don't want to disable them entirely. I just don't want too
much of them. This blog post is about how I've found a balance that I like.

![Watch](/media/2018/03/pocket-watch-3156771_1280.jpg)

<!--more-->

Here's a quick list of what I've done and why:

- Google wants me to sign in to a Google account within the browser itself. That
  sends my browsing history and activity to Google, which I don't want. So I
  don't sign in.
- I turn off search engine prediction services and enable the "do not track"
  setting.
- I visit DuckDuckGo, then open the search engine preferences and set it as my
  default. DuckDuckGo doesn't track you when you do searches and is a very good
  search engine in my opinion.
- I disable automatically adding search engines as a side effect of visiting
  websites. I find it disturbing that this feature exists and isn't possible to
  disable from within Chrome, because it's a form of history in a way. This
  requires a bit of fiddling with internals via SQLite, but isn't otherwise hard
  to do. The solution is described at https://superuser.com/a/688270
- Under content settings and cookies, I configure Chrome to keep local data
  until I quit the browser, and block third-party cookies. This cuts down on
  most cookies, and a quick restart of the browser deletes the ones that do
  accumulate. There's a short list of sites that I want to allow cookies from; I
  add these under the settings to allow specific sites to set cookies that won't
  get cleared when I restart the browser.
- I disable all the features related to filling forms and saving passwords. I
  use 1Password for that and I trust it a lot more than a browser from Google.

I don't install a lot of extensions. The ones that I keep active are:

- uBlock Origin, an ad blocker
- Mercury Reader, which mimics Safari's reader view
- 1Password
- Feedly Subscribe Button
- History AutoDelete, which I set to clear history after 5 days

There's a few others that I install but don't activate unless I need them:

- Awesome Screenshot, although I like Firefox's screenshot features enough that
  I often use it instead of Chrome when I want to take a screenshot of a very
  tall page
- Evernote Web Clipper; it works okay but I rarely use it, preferring to save
  articles through Feedly, which does a better job
- Buffer, which is fine but I rarely use via extension, since I usually compose
  an email to my "email to buffer" address instead
- Super Auto Refresh, which I use rarely

With those settings and extensions installed, I find that my history, cookies,
and similar don't accumulate over time. Restarting my browser a few times a week
is enough to delete the relatively small amount of tracking content that gets
past uBlock Origin.

[Pic Credit](https://pixabay.com/en/pocket-watch-time-of-sand-time-3156771/)
