---
title: 'Markdown Editors'
date: "2019-02-05T18:39:23-05:00"
url: "/blog/markdown-editors"
description: "Choosing a Markdown editor isn't as simple as it used to be, because there are now many excellent options for different purposes."
tldr: "Choosing a Markdown editor isn't as simple as it used to be, because there are now many excellent options for different purposes. In this article I review editors for note-taking and writing, editing a single Markdown file with a live-updating preview, and Markdown preview panes built into programming code editors."
credit: "https://unsplash.com/photos/-94oJK3PDQw"
image: "/media/2019/02/unsplash-photos--94oJK3PDQw.jpg"
thumbnail: "/media/2019/02/unsplash-photos--94oJK3PDQw.tn-500x500.jpg"
categories:
- Productivity
---
Continuing the recent theme of lightweight markup languages, I thought I'd write about a few Markdown editors I've used or tried.
So many editing programs now support Markdown that it's not simply a matter of choosing the best editor, but the one that's best for the task, and/or the one you prefer.
I'll cover a few popular choices in each of several categories.
For a more extensive list, refer to my previous [Markdown](/blog/markdown/) article.
<!--more-->

I'll focus on apps that have some element of visual editing, rather than plain-text editors with syntax highlighting and the like.
I use a Mac, so I have a bias for editors that work on the Mac, but some of them work on other platforms too.

### Note-Taking and Writing

A crop of lightweight Markdown-based note-taking apps has sprung up in the last few years.
This is a good thing, because programs like Evernote, which are based on rich-text document formats, tend to accumulate hard-to-fix formatting problems in my experience.
I'm a Bear Notes user, but while migrating from Apple Notes to Evernote to Bear Notes, I tried a lot of different note-taking apps.

[Bear Notes](https://bear.app/) is a Mac and iOS app that stores its notes in plain-text format and syncs them with Apple's iCloud.
The default isn't Markdown, but you can change that with a quick toggle in the settings.

![Bear Notes](/media/2019/02/bear-notes.gif)

What I love about Bear is its minimalism and simplicity.
It has a few features that each do specific things really well, and in combination, are more than the sum of their parts.
For example, the tagging-based organization system is genius.
All you have to do is put one or more `#hashtags` into a note's text, and it gets indexed by those tags.
Tags are much easier to use than folders, *and* they're part of the note rather than invisible metadata with separate mechanisms for seeing and changing them, *and* they offer a lot more functionality and flexibility.
The navigation "folders" in the sidebar of Bear are based on tags.

There's very little I don't like about Bear; I wish I could change the indentation on bulleted lists and a couple of other things, and I wish it would reconcile sync conflicts when I edit a file in two different devices at the same time, but on the whole it's an absolute delight, very well suited for the purpose.

[Ulysses](https://ulysses.app/) is the other Mac and iOS app I think is most similar to Bear Notes.
But it doesn't just do notes: it is designed for writing and publishing too, so it offers advanced features like exporting ebooks.
It uses folders for organization, and can sync files through services like Dropbox.

![Ulysses](/media/2019/02/ulysses.gif)

There's a lot to like about Ulysses, but in my opinion it's not visual enough.
The markup is too prominent, and the editing experience has too many disruptions and details as you can see in the gif.
Overall, the feeling I get when I use it is that it doesn't do enough cognitive work for me.
I realize this is subjective, but it's a reflection of how I feel about the product.
Full disclosure, although I'm obviously working with a trial version without any real content in the above gif, I've used Ulysses for a couple of weeks with all of my thousands of notes---then switched to Bear Notes instead.

Other apps in this category are more-or-less similar, with differences that reveal mostly their intended purpose or their level of fit-and-finish-and-polish.

### Markdown File Editors

There are a few dedicated Markdown editors.
Historically, the category leader was Mou, but there was apparently some uncertainty about its destiny, and the open-source [MacDown](https://macdown.uranusjr.com/) sprang up in its place.
MacDown is a basic two-panel editor with source on the left and a live preview on the right.

![MacDown](/media/2019/02/macdown.gif)

I used to use MacDown a few years ago, but these days I just use Visual Studio Code, which offers a similar editing and preview experience.

Another editor that I like a lot, and use sometimes, is [Typora](https://typora.io/).
Rather than making you edit the source code, it has a unique and innovative blended source/rendered editing mode.
I really like this.
As you type formatting commands or place your cursor into some text, the Markdown is revealed, but when you finish working with a chunk of text, it's rendered in its display mode.

![Typora](/media/2019/02/typora.gif)

As you can see in the screenshot, there's a document outline at the left.
There are other features too, which aren't visible in the gif, but there's some pretty nice things about Typora.
I use it sometimes when I want to get into writing mode in longer essays, where a fixed-width font and other subtle cues make me feel like I'm programming, whereas Typora feels more like writing prose.

### Programmer's Text Editors

Many newer text editors designed for programmers have Markdown live preview.
This is pretty much a standard feature these days, in fact.
I'm historically mostly a Vim user, but I have been appreciating [Visual Studio Code](https://code.visualstudio.com/).
With its speed, flexibility, extensibility, and features like built-in terminal and Git client, I can do a lot in VS Code that I used to do in a collection of terminals and Vim, Sublime Text, or the like.

![VS Code](/media/2019/02/vscode.gif)

As you can see in the gif, you can open up a preview pane to the right, which live-renders the Markdown file much like MacDown.
As you can also see, occasionally it goes berserk and starts doing weird things like scrolling as you type.
Plus-or-minus oddities like that (which MacDown can suffer too), it's an excellent text editor with a decent Markdown experience.
Another editor with essentially identical features and editing experience is [Atom](https://atom.io/).
