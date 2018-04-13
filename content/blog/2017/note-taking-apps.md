---
url: /blog/note-taking-apps/
title: 'Digital Note-Taking Apps'
date: "2017-12-02T18:50:50-05:00"
categories:
  - Desktop
  - Reviews
  - Gear
author: "Baron Schwartz"
description: "I migrated from the Apple Notes app to Evernote. Here's the research I did and the results."
image: "media/2017/12/background-2846221_1280.jpg"
---

I used to use [paper notebooks][notebooks] extensively. When I didn't have paper
and pen, I emailed myself a quick note from my iPhone.  This led gradually to me
keeping all of my notes on my iPhone, using the [Notes app][mobile_apps]. In the
last few months, I've moved from Notes to Evernote. This process took some time
and research, which I'm sharing in case it's useful to you.

![Notebook][background]

<!--more-->

I used to love the iPhone's Notes app for its simplicity and speed. It had
problems---sometimes links would appear where they didn't belong, and sync was
flaky---but it got better over time. And its design was [just
enough][just_enough] of the right things: the note's title wasn't a separate
piece of data, it was simply the first line of the note; starting a line with an
asterisk turned it into a bulleted list. Small touches like that made it great,
but unfortunately a couple of months ago it became pretty unusable for me. The
upgrade to iOS 11 and MacOS High Sierra made it so slow that it was nearly
unresponsive. I was forced to search for a lightweight replacement.

### Alternatives I Considered

I was strongly biased towards something that was little more than plaintext with
a WYSIWYG interface and sync between devices. One ideal choice would be a Markdown
editor that stores its data in Dropbox or similar. But I need it to work on my
phone, iPad, and laptop. With that in mind, I first searched for barebones,
minimalistic note-taking and research apps. One option I considered briefly was
using plaintext and GitHub, and letting Git be my syncing strategy. This would
be more complex across mobile devices than I was willing to contemplate,
however.

I found and seriously considered the following options:

* [IA Writer][ia_writer]. This is more of a writing tool than a note-taking
  tool, with features for readability analysis and the like. It's also
  plaintext-only, and doesn't support images. I have owned it for a while, but
  it's really not for storing and organizing one's digital life; it's for
  becoming the modern Hemingway.
* [Ulysses][ulysses] is similar: it's a writer's tool, not for an information
  packrat like myself.
* [Byword][byword] was more along the lines of what I was looking for at first.
  It's a Markdown editor with cross-device support. But it's more of an
  authoring tool than an organizational tool, although it has support for some
  organizational tools such as tagging. It's essentially a very thin theme on
  top of Markdown, though; it isn't really WYSIWYG and the Markdown formatting
  is visible.
* [Write][write] looked at first like what I needed: a Markdown editor that
  would work with files in Dropbox or any other cloud sync provider. But when I
  investigated it, it didn't seem to be very reliable or well-implemented.
* [Dropbox Paper][paper] is kind of like a lightweight Google Docs that works on
  Dropbox, but it doesn't work offline and the data isn't stored *inside* of
  your Dropbox account. The data is separate, and the relationship with Dropbox
  seems to be only a high level of integration with your account, not your data
  per se.
* [Simplenote][simplenote] is a very simple, free, and opensource app that
  supports Markdown. It's cross-platform, and the data is stored in their SaaS
  service. The product is provided by the makers of Wordpress. I found it to be
  a little too barebones, although it's simple and lightweight. For example,
  some of the client applications displayed Markdown in plaintext, although the
  web app showed it formatted. All-in-all, I found it to be most similar to Bear
  Notes, but Bear was slightly better.
* [Bear Notes][bearnotes] is the option I eventually used for a while.

### Bear Notes

Bear Notes is a note-taking app that is essentially a thin veneer on top of
Markdown. It uses iCloud for syncing content between devices. It's not too
different from the Mac/iOS Notes app in some regards, but is definitely lighter
and less bloated.

I stopped using Notes, and used Bear exclusively for a few weeks, migrating
notes over from the Notes app as I found I needed to update them.

I found myself liking Bear a lot. Its interface has a lovely aesthetic, and it
feels pleasant and unobtrusive to use. Its search works very well, and it
doesn't have a lot of features, so it is very simple to use. It has a web
browser plugin to help clip web content into notes, which I do a lot.

I liked that it uses Markdown under the hood, although by default it uses a
variant on Markdown and has to be configured to use standard Markdown. In fact,
the Markdown is only about half-hidden; it feels like only a slight step up from
writing Markdown with good syntax highlighting.

That turned out to be one of its flaws, to tell the truth. Some things about it
bothered me a lot, especially some of the design and typography choices. For
example, headings and bulleted lists didn't indent as I'm accustomed. They
outdent the formatting symbols past the left margin of the text, which makes it
feel like the formatting is distracting from the content. When I create a
bulleted list, I really want the list to be set off with indentation to help
emphasize the cohesiveness of the list in contrast to the surrounding content.

Here's a couple of screenshots to help illustrate. First, here's the Bear
interface without any notes, to show how simple it is.

![Bear Notes 1][bear_1]

The simplicity you feel in that screenshot is borne out in the user experience
in the app. Here's what it looks like with a simple note and some common
formatting options I use:

![Bear Notes 2][bear_2]

Notice how the list isn't indented, and the bullets are outdented? Notice how
the cursor is off the left edge of the document in the heading? Little things
like that add surprising cognitive load to using the app.

Here's an example of a task I do a lot: I put my cursor at the end of a line and
hit Cmd-Shift-Left to select the text to the beginning. In Bear, this copies
more than the text, it copies the formatting too. It surprised me every time I
did it, and never stopped being surprising and slightly jarring. Another example
is the extra space between the title and first line, which you can't put the
cursor into. It feels like groping for something in the dark.

The app's copy/paste behavior is actually one of the biggest issues I had with
it. Although it looks like it's formatted text, it isn't: when you copy and
paste into another app, all you get is plaintext with asterisks and other
formatting codes. I copy and paste between apps a lot, and I want things I copy
from my notes into my emails to have the right formatting. In Bear, I'd have to
export the content to get it into HTML, open that in a browser, and then copy
from the browser. I know copy/paste is probably messy under the hood, but the
experience with Bear was jarring compared to other apps I've used.

Finally, syncing was frustrating. There's no support for conflict resolution. If
I edit a note on two devices offline and then bring them online, I get two notes
with conflicts, and now I have to resolve the differences between them. Most
other note-taking apps I've used have figured out how to merge updates. Even if
there ends up being some amount of conflict or messiness in the text, that's a
lot better than having two notes with slight differences I need to resolve. Bear
isn't up to par here.

In the end, I gave Bear a few weeks and then canceled my subscription. The
less-is-more aesthetic of the app was appealing, but it felt like I was coming
up short on some features I needed to work better, and I had problems that felt
similar in complexity and effort to more complex note-taking apps, which kind of
negated the point.  It looked like I was going to have to use something a bit
less minimalistic.

### Evaluating More Traditional Options

I turned my attention towards more fully-featured products like Evernote. After
giving up on minimalist Markdown-with-a-GUI, I was willing to introduce other
variables into the mix. It'd be great to have the following:

* Ability to replace [Pocket][mobile_apps]. I have a premium subscription but
  have never been fully satisfied. I've used it for years and saved thousands of
  articles, and reported bugs tens of times, and they just don't seem to fix the
  bugs that mangle the content I'm trying to save. I'd like to be able to
  consolidate my "read it later" list with my notes and keep my whole digital
  memory in one place.
* Platform independence, so I don't get stuck in a dilemma if I decide to use an
  Android phone or tablet in the future.
* Good integration with other tools I use, such as a browser extension and
  Feedly integration.

I investigated a few and discarded them:

* Google Docs: I love Google Docs, but they don't work well offline, and they're
  a word processing app, too heavyweight. And, a notes app should be in a single
  UI, with an information hierarchy and navigation between notes in a menu or
  sidebar; Google Docs are standalone and aren't contained within a single good
  UI in that way.
* Google Keep: I tried it but found it very poorly done. Saving an article into
  it, for example, doesn't save the article's text. It just saves the link. If I
  wanted bookmarks, I'd use my browser. It also doesn't work offline.
* Microsoft OneNote: Other people seem to love it, but I can't fathom why.
* Evernote: this is the option I ended up choosing, and I've been very happy.

### Evernote

I had a prejudice against Evernote: I thought of it as bloated, complex,
slow, and buggy. But my wonderful wife has been using it for a while, and she
was happy with it, so I took another look and found I was mostly wrong.

First of all, it does satisfy my wishlist: I can use it as a Pocket replacement,
I can store my whole digital note-taking and information-hoarding life into it,
and it has a browser extension and article simplifier that's better than
Pocket's. And it's platform-independent and is unlikely to go out of business in
my opinion.

When I tried it out, I was pleasantly surprised. It's not bloated or slow; quite
the opposite. It's much faster and easier to use than Notes. It does have almost
every conceivable feature and interface option, but they are designed well so
they're not intrusive, and the user experience feels clean and pleasant.

Sync worked a lot better than I'd been prepared for, too. I've had an issue with
a note that wouldn't sync, and the user interface errors were confusing, but
when I looked into the activity log I found it was an unreachable URL in that
note. Why this was preventing it from syncing I'm not sure, but fixing the URL
fixed the sync problems.

I converted all of my Notes notes into it after a few weeks, and have been
happily using it (and a Premium subscriber) for a couple of months. Overall,
it's a great experience. Here are the only *bad* experiences I've had:

* Like Bear Notes, it doesn't resolve conflicts very well, which can be tedious.
* There's no keyboard shortcut to add a link to selected text on my iPad. This
  is out of character: there's generally "just the right" functionality I need,
  but the iPad has shortcuts for everything else I don't need, and not this one.
  In fact, I couldn't find how to hyperlink text on the iPad version, with or
  without keyboard shortcuts.
* The Mac desktop version doesn't seem to persist some of my settings after
  restarts and upgrades. It's as though I haven't used the app before: when I
  restart the app, it offers me a feature tour and enables features I'd disabled
  previously, such as Context.
* Importing notes by using copy/paste wasn't very good. Bulleted lists didn't
  come over as multiple bullets, but as line breaks with bullet characters. See
  below for how I imported the notes programmatically with better results.

Careful readers will have observed that I seem to be holding Evernote and Bear
Notes to different standards of excellence. Why was it frustrating for Bear
Notes not to resolve sync conflicts, but acceptable for Evernote? I'm honestly
not sure; there's bound to be some psychological effects at work here, some kind
of bias. I'm valuing things differently, I recognize that. It may be that Bear
Notes has a different feeling and aesthetic, and that sets a different standard
for what feels frustrating to me.

### Importing from Notes to Evernote

After importing a couple of notes into Evernote with copy/paste, I found a
script online to automate the process instead. Perhaps you already know this,
but Apple's user interface is highly scriptable, which is great. It's like UNIX
for the GUI. The following script imported all the remaining notes I had in the
Notes app, which was several hundred:

```
tell application "Notes"
	set theMessages to every note
	repeat with thisMessage in theMessages
		set myTitle to the name of thisMessage
		set myText to the body of thisMessage
		set myCreateDate to the creation date of thisMessage
		set myModDate to the modification date of thisMessage
		tell application "Evernote"
			set myNote to create note with text myTitle title myTitle notebook "Imported Notes"
			set the HTML content of myNote to myText
			set the creation date of myNote to myCreateDate
			set the modification date of myNote to myCreateDate
		end tell
	end repeat
end tell
```

[Image Credit][pixabay]

[bear_1]: /media/2017/12/bear-1.png
[bear_2]: /media/2017/12/bear-2.png
[bearnotes]: http://www.bear-writer.com/
[write]: http://writeapp.net/mac/
[byword]: https://bywordapp.com/
[ulysses]: https://ulyssesapp.com/
[ia_writer]: https://ia.net/writer/
[just_enough]: /blog/just-enough-better/
[background]: /media/2017/12/background-2846221_1280.jpg
[pixabay]: https://pixabay.com/en/background-blank-business-2846221/
[notebooks]: /blog/2013/07/10/ultimate-notebook-and-journal-face-off/
[mobile_apps]: /blog/life-on-mobile-apps-services/
[paper]: https://www.dropbox.com/paper
[simplenote]: https://simplenote.com/
