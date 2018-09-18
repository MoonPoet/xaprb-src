---
title: 'Configuring Firefox for Privacy and Convenience'
date: "2018-09-17T20:53:33-04:00"
url: "/blog/configuring-firefox-for-privacy-and-convenience"
description: "Here's the settings I configure to keep my browser from accumulating a lot of history and tracking cookies."
credit: "https://unsplash.com/photos/zv42KBikfrg"
image: "/media/2018/09/unsplash-photos-zv42KBikfrg.jpg"
thumbnail: "/media/2018/09/unsplash-photos-zv42KBikfrg.tn-500x500.jpg"
categories:
- Privacy
---
I wrote [previously](/blog/configuring-chrome-for-privacy-and-convenience/) about configuring Chrome for privacy and convenience, to ensure that cookies and history don't accumulate in the browser.
I recently decided to switch from Chrome to Firefox.
Here's how I've configured it to behave in a similar fashion, which I believe helps protect my privacy.
<!--more-->

### From Chrome To Firefox

In my previous post, I wrote

> Google wants me to sign in to a Google account within the browser itself. That sends my browsing history and activity to Google, which I don’t want. So I don’t sign in.

Unfortunately I found that despite my choice not to sign in, Google made the browser sign me in anyway.
Perhaps I'm not understanding exactly how Chrome works.
Perhaps Google doesn't understand (or care) how I want it to work.
Regardless, I decided that running software from a company whose tracking I explicitly want to refuse, isn't a smart decision on my part.

I've run Firefox off and on, for many years.
I began using it back when it was a pre-release version of a browser called Phoenix.
I find it useful to use because among other things, I sometimes find bugs in VividCortex's software that people using Chrome don't always find.

Initially, Firefox was unusably slow for me, but some kind strangers on Twitter helped me debug it.
The issue was an external 4k monitor with a non-default resolution; apparently this is a known bug and hopefully will be addressed soon.
Meanwhile I know how to work around it, and Firefox got fast again.
Also, during this process, I found some problems with my [Story](https://story.xaprb.com/) Hugo blog theme that might have been noticed only by people on slow connections.
Run software under adverse conditions, learn helpful stuff!
I count it a win overall.

### My Firefox Settings

Most of my Firefox settings are similar to what I chose for Google Chrome:

- Turn off search engine predictions
- Enable "do not track" and tracking protection
- Set DuckDuckGo as default search engine^[Firefox doesn't auto-add search engines willy-nilly, which is great; that is an anti-feature in Chrome in my opinion, so I'm glad to be rid of it.]
- Disable password saving and form filling
- Set new windows and tabs to open with a blank page---heavenly!
- Enable custom settings for history, remember browsing and download history, and clear history at close: but only cache, site preferences, and offline website data (not cookies and browsing/download history)
- Accept cookies until they expire, but no third-party cookies

The rest I configure with extensions.

### My Extensions

Of the extensions I use, the most important for privacy are both by a developer named Kenny Do, to whom I am grateful:

- **History AutoDelete**. Deletes history after 7 days.
- **Cookie AutoDelete**. This deletes cookies when tabs are closed. This is even better than the settings I configured for Chrome! I enable "Automatic Cleaning," and set a "whitelist"^[I dislike this term because of racial connotations, but I don't get to rename what's shown in the extension.] for sites I want to stay logged in.

I also use some general-purpose extensions:

- 1Password
- Bear Writer
- Feedly Subscribe
- uBlock Origin
- Tabliss to put beautiful photos from [Unsplash](https://unsplash.com/) onto my
  new tab pages.^[Unsplash Instant is the corresponding one from Unsplash
  themselves, but it's only available for Chrome at the moment.]

There are a couple of extensions I do not need in Firefox as I did in Chrome:

- I don't need a blank new tab page extension, because Firefox has a setting to do that.
- I don't need a screenshot extension; Firefox takes great screenshots.
- I don't need Mercury Reader because Firefox has a reader-view feature.

With these settings, as with Chrome, I find that I'm not accumulating history, cookies, or site data. In fact, Firefox configured as I've mentioned here is actually cleaner and better than the way I'd configured Chrome!
