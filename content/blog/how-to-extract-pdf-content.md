---
title: 'How to Extract Content From a PDF'
date: "2018-04-07T16:52:49-04:00"
categories:
  - Writing
author: "Baron Schwartz"
description: "Here are easy, free ways to extract text and images from PDFs on Mac OS."
image: "/media/2018/04/extrude-1606468_1280.jpg"
---

I've occasionally needed to extract text and/or images from a PDF. I've found a
couple of easy, free ways to do this on MacOS.

![Extrude]({{< param image >}})

<!--more-->

There's commercial software such as Adobe Acrobat that will extract images from
a PDF, of course, but there's an easier way: a free application called [The
Unarchiver][unarchiver] that treats a PDF file as if it were a zip file and
extracts everything into a folder. Just install the app, then right-click on
a PDF file and select *Open With*.

Related pro-tip: if you want to extract all the images from a Keynote
presentation, you can simply unzip the presentation using the commandline
`unzip` application. It'll expand into a folder that contains all the images and
other assets. (Or you can right-click and open with the Archive Utility app.)

That'll do the trick for the images. For the text, you can just open the PDF in
Mac's default PDF viewer, the Preview app. Use Cmd-A to select all of the text
and other content, and then you can simply paste it into any plaintext
destination. If you don't have a favorite text editor such as Atom or Sublime
Text, you can use Mac's default TextEdit app. Just use *Format > Make Plain
Text* to set it to plaintext mode.

[unarchiver]: https://theunarchiver.com
