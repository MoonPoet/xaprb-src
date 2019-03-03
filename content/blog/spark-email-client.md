---
title: 'The Spark Email Client'
date: "2019-03-01T19:16:22-05:00"
url: "/blog/spark-email-client"
description: "Spark is a fresh, smart email client for iOS and Mac with lots of great features, but it still has a couple of rough edges."
tldr: "Spark is a fresh, smart email client for iOS and Mac with lots of great features, but it still has a couple of rough edges. Nonetheless it's still a top contender in my list to replace Inbox, which is being discontinued."
image: "/media/2019/03/airplane-backlit-clouds-1262304.jpg"
credit: "https://www.pexels.com/photo/silhouette-photo-of-man-throw-paper-plane-1262304/"
thumbnail: "/media/2019/03/airplane-backlit-clouds-1262304.tn-500x500.jpg"
categories:
- Email
---
As I [wrote](/blog/inbox-by-google-email-client) yesterday, I'm sad that Inbox is going away, and it's hard to bear the thought of using GMail again.
Thus, I've been evaluating a few different email clients to see what's available.
One that I tried recently is [Spark](https://sparkmailapp.com/), an email client for iPhone, iPad, and Mac.
Spark feels not-quite-mature, yet still pretty impressive.
In this article I'll summarize what I see as its main attributes and areas for improvement.
<!--more-->

### The Spark Difference

Spark is a fresh, modern, well-designed email client, but it's more than just that.
It combines a lot of the best innovations of apps like Inbox (snooze, smart inbox, etc) with Spark's own extensions to email.
You might not be interested in these: I didn't find them compelling myself, but some might.
They include a kind of team-chat feature where a chat thread is associated with an email, for example.
The idea is to enable teams to collaborate around emails without sending them back-and-forth constantly.

Spark also does a lot of non-innovative things very well.
It has a rich suite of app integrations, for example.

### What's Great

I really like Spark's design!
It feels fresh, clean, lightweight, but also has a crisp feeling.
This is the biggest standout: it feels like an email client should feel.
It doesn't feel oversimplified, but doesn't feel cluttered or bloated either.

It's also "just right" across devices.
The iPhone design is just right for iPhone, the iPad is different in ways that make sense for iPad, and the Mac client is customized for the desktop too.

Spark has a bunch of smart features that I love:

- Unified inbox across several accounts. No more switching amongst accounts! I love this.
- Snooze emails for later.
- Swipe to archive, making it really easy to get to Inbox Zero (or at least see what needs to be done).
- Integrated calendaring; you can replace your calendar *and* email app with one. The calendar integrates well with other tools like Zoom.
- Virtual "smart folders" can be created from searches.
- Notifications work well on my [Withings Steel HR](/blog/best-fitness-activity-sleep-tracking-watch/) hybrid smartwatch.
- Integrates with Google Contacts and Calendar really well.
- Syncs settings very nicely across devices, in most cases.
- Lets me disable external images in emails to protect my privacy.

In general, Spark often seems built to anticipate relatively minor things that I do a lot, and make them a lot easier.
The unified inbox is one good example.

### What Still Needs Work

Spark actually has a *lot* of features, and that means there are a lot of rough edges that need a little more polish.
Many of them didn't work well enough for me so I ended up not using them.
So the following list might be a little bit long, but don't take that to mean that I dislike Spark.
The fact that it does a great job at the core things I want, and does really well at the little niceties, should be considered as a significant offset against the below list.

**Quick Replies**. Spark has quick-replies you can tap to instantly send a response, somewhat like a reaction in Slack.
The concept is smart: I so often send simple "okay" or "looks good" or "not interested" responses.
Spark's quick-replies should work well for that.
But it's a relatively fixed list without a lot of flexibility, and the resulting emails are a bit weird, and use a different font and have an image/icon, and go only to the sender instead of the whole list, and in general it doesn't end up working as well as I wanted it to.

**Calendar**. The calendar often shows me useless times.
When I go to it, it's often showing something like 12:00 am through 11:00am, when the current time is 2:30pm.
On mobile, the calendar also doesn't show a line to visually demarcate the current time of day, so it's disconcerting to scroll and figure out what's next on the agenda and how far away it is.
I also wish it would show events differently if I've accepted, rejected, or not taken action; they all look the same.
I wish there were a few more features in the calendar, or a bit more flexibility: ability to schedule a room or other resource; "speedy" meetings that leave gaps for restroom breaks and so forth; ability to customize alert times (I prefer 2 minutes, which isn't an option in Spark).

**Formatting**. Email formatting doesn't quite work right.
Bulleted list formatting looks right when composing, looks unindented when reading the resulting sent mail, and when viewed in GMail has empty bullets between bullets.
Quoted content is hard to display, and can be hidden---for example, when someone forwards me an email or adds me into an email, quoted content I haven't seen is hidden.
Sometimes there are strange letter M's in front of contact names, and other oddities I never was able to understand or find in the documentation.

**Performance**. I noticed a lot of performance problems and freezes, some of them quite long (20 seconds or so).
Search performance seems really slow compared to using Inbox or GMail directly.
Loading threads can be slow, and long threads in particular often show stacked lists of not-yet-loaded messages with spinners in them.

![Spark Loading a Thread](/media/2019/03/spark-spinners.png)

Inline images such as embedded or attached images for signatures often showed the same issues, failing to render even though they did not need to be loaded from an external source.

![Spark Loading an Inline Image](/media/2019/03/spark-inline.png)

I noticed these performance problems on my laptop and on mobile; on mobile often it wouldn't respond to touches for a while.
Sometimes the app would freeze and I'd try again, and then I'd end up with duplicate actions when it unfroze, like several new blank compose windows.

I also found that the Mac app always seemed to want to sync something when I closed the app, even when I had taken no actions in a long time.
It's as if it doesn't sync periodically in the background.
It deals with this in a slightly alarming way: it waits a couple seconds, then pops up a dialog asking if you want to wait or close without syncing.
But the dialog times out, and often I wasn't able to get my mouse to the "wait and keep syncing" button in time, leaving me nervous that some work was lost.

My biggest concern with performance was reliability.
In some cases I sent emails---I *know* I actually clicked Send and watched the UI confirm that they were sent---and they didn't actually get sent.
Instead, they were saved as drafts, and when I checked with the recipient, they never had gotten them.
In some cases, I sent emails that *did* get sent, but there were *also* unsent draft copies of them in the Draft folder, which was very confusing and unnerving.

**Keyboard Shortcuts**. Keyboard shortcuts seem to be only partially implemented, and seem highly dependent on what part of the UI is selected or in focus.
There aren't shortcuts for a lot of things I want, such as combining actions like archiving the current message and going to the next/previous---or at least I couldn't find them.
When I'm viewing a thread, I couldn't find a way to use the keyboard to navigate amongst messages in the thread.
I'm not sure if keyboard shortcuts don't work right, if there aren't shortcuts, or if I was simply seeing slowness from the performance problems I mentioned.
A lot of times I'd press a key that was supposed to work, like C to compose, and nothing would happen.
So I'd switch to using the mouse, and start composing.
In general, though, the app has a lot of quirks that keep it from being consistently usable with keyboard shortcuts.

**Smart Features**. A lot of the "smart" features were slightly too-smart, or perhaps not-smart-enough, for me.
For example, signatures.
I don't use signatures, but I couldn't disable the space in the compose UI for a signature.
And after a while, Spark added a "smart" feature to auto-create signatures, which seemed to be learning from my terse three-word emails without a signature.
It started proposing "sounds good to me" and "I'm not interested" as signatures it had magically learned.

There are other examples where either the concept or the implementation is lacking a little something, it's hard to say which.
For example, the Smart Inbox.
I found myself not really trusting it: what if it misclassified an email I wanted to see?
So I'd read my Smart Inbox, and then go read all the rest of the low-priority stuff too, which kind of defeats the point.
I just switched that off---I don't think I'm the target user population anyway, given that I tend to keep very few emails in my inbox.

I also wanted to enable calendar notifications, disable email push notifications, and badge the inbox to show unread counts.
That combination of settings didn't seem possible, and I definitely don't want to be notified when an email arrives.
So I disabled email notifications and left calendar notifications enabled, without any badge for the unread count.
As a result, I ended up opening the email app a lot to check for new email, when there wasn't any.

### Wish List

I really wish I could mute threads.
This isn't something Inbox provides either (although, you can use M as a keyboard shortcut on the web app---an undocumented feature).
I really love being able to mute threads, and aside from GMail and Inbox, I don't know of another email client that provides it.
This feature is just as useful as archiving and snoozing!

### Conclusions

I haven't yet chosen the email client I want to use longterm, but Spark is a top contender.
Its great design, helpful "grace note" features for the little things I do so often, and the fact that it's available on Mac and iOS, make it attractive.
I'd like to see it mature just a bit more, and see if some of the concerns that I had are addressed as they iron out the creases.
In the meantime, I'm giving Outlook another try too, and I'll write about that soon.
