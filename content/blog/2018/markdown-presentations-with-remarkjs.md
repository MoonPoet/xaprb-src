---
url: /blog/markdown-presentations-with-remarkjs/
title: 'Markdown Presentations With RemarkJS'
date: "2018-03-30T07:23:36-07:00"
categories:
  - Conferences
author: "Baron Schwartz"
description: "RemarkJS makes it easier and more fun to build and present slideshows."
image: "/media/2018/03/card-1868267_1280.jpg"
---

I switched from traditional presentation programs to
[RemarkJS](https://remarkjs.com), and I'm glad I did. RemarkJS (or Remark) is a
free, open-source presentation system that lets you write slideshows in Markdown
and present with your web browser. It strikes a great balance: it is simple and
has just enough functionality to make the most important things delightfully
easy---but it's not limiting. It's powerful enough to build advanced
presentations.  Most of all, it makes me happy, because it gives me control and
makes me more effective.

<!--more-->

Remark is simple to use: it's a JavaScript library that converts a single
Markdown document into slides. It supports normal Markdown syntax, which is a
simple plaintext format that makes it easy to write headings, lists, and pretty
much anything else you need for moderately complex documents and slideshows.
RemarkJS adds a few slideshow-specific extensions that give you a lot of
flexibility and power. If you already know Markdown, the RemarkJS learning curve
will take you 30 seconds; if you don't, it'll take you 5 minutes.

You use RemarkJS by putting a script tag and a text area into a web page. Remark reads
the text from the text area, and builds a presentation. You just load the page
in your browser and it turns into a presentation. There's a ready-to-use
boilerplate template that just works, so even if the first part of this
paragraph sounds complicated, you'll have no problem because you don't actually
need to do it yourself.

Remark converts the slides into normal HTML and CSS with default styling that
works well for presentations. As an author, you don't need to fiddle with HTML
and CSS, but you can if you want: you're not locked out, and the browser's full
capabilities are just an angle-bracket away. It's easy to add SVG vector images,
animations, beautiful math equations, movies, code syntax highlighting, and much
more. You can also customize the visual styling of the slideshow easily, adding
your own flair with images, web fonts, and anything else that you could do in a
website.

RemarkJS supports all of the most important semi-advanced features you need for
slideshows, again making them *easy* out-of-the-box:

- It's easy to build slides with different styles, like title slides and section
  dividers. You can add full-coverage background images with a single line of
  Markdown, if you like building image-heavy slides. If you like text-heavy
  slides, that's just as easy. And RemarkJS has default functionality for things
  like centering text and making bulleted lists.
- You can create slides that reveal text or images progressively. It's actually
  *much easier* to do this in RemarkJS than in PowerPoint or Keynote!
- There's a simple way to do slide "layouts" (a.k.a. "slide masters"). These let
  you easily customize things like the structure and content of any slide.
  Unlike slideshow programs that make you dig through menus to edit the "slide
  masters," RemarkJS implements them as slides that don't get displayed in the
  slideshow. It's easy to apply these template slides.
- The default aspect ratio is 4:3, but Remark also supports 16:9 aspect ratio
  slides.

RemarkJS works really well as a presentation tool, too---it's not just for
*building* slideshows, it's also "just right" for *presenting* them as a
speaker. Among the things it supports:

- It lets you "clone" a presentation into two browser windows that stay
  synchronized with each other. You can put one on your laptop and one on an
  external display.
- You can add speaker notes to your presentation, and view them in one window
  while the other one is in presentation mode. The speaker view is simple and
  complete: it has a picture of the current and next slides, notes for the
  current and next slides, and a timer.
- There are keyboard shortcuts for controlling the slideshow. You can view the
  shortcuts with the `?` key. You can use the keyboard to control how the slides
  are displayed, and navigate to slides by next, previous, start, end, or slide
  number. If you're on a mobile device like an iPad, Remark works great too: you
  just swipe to navigate slides.
- It's easy to use RemarkJS offline; you don't need to have an Internet
  connection. And you can export slides to PDF[^1] by simply printing the
  slideshow and saving as a PDF.

RemarkJS isn't the only browser-based slideshow program, but it's the only one I
know of that is simple and uses Markdown, which makes it a winner for me. Here
are a few other open-source and free alternatives I looked at:

- [RevealJS](https://revealjs.com/) is a sophisticated browser-based
  presentation tool that is the open-source basis of a commercial slideshow
  service. It's powerful, but lacks the simplicity and speed of Markdown.
- [ImpressJS](https://impress.js.org) is an open-source clone of Prezi. That
  flashy style isn't for me; it's also more complicated than RemarkJS.
- RevealJS and ImpressJS seem to be the most popular, but I found some others that I
  didn't take a lot of time to look into:
  [Bespoke](http://markdalgleish.com/projects/bespoke.js),
  [DZSlides](http://paulrouget.com/dzslides), [Shower](http://shwr.me/),
  [CSSS](http://leaverou.github.io/csss),
  [Flowtime](http://flowtime-js.marcolago.com/),
  [Slidy](http://www.w3.org/Talks/Tools/Slidy/),
  [Deck.js](http://imakewebthings.com/deck.js),
  [RISE](https://github.com/damianavila/RISE), and
  [WebSlides](https://github.com/jlantunez/webslides).

In conclusion, RemarkJS has solved the hassle of dealing with complex
traditional slideshow software for me. It gives me simplicity and control and
makes me look good on stage. It allows me to put my presentations [on this
website](/talks/), eliminating the need to deal with file formats,
synchronizing presentations, and converting across all the devices I use. I
spend a lot of time and effort building and presenting slideshows, and RemarkJS
has improved my quality of life and enjoyment.

[^1]: There's a bug in PDF export, but the [fix](https://github.com/gnab/remark/issues/50#issuecomment-223887379) is easy to apply.
