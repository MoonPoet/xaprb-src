---
title: 'Markdown'
date: "2019-02-03T20:09:35-05:00"
url: "/blog/markdown"
description: "Markdown is a simple plaintext document format that removes complexity and toil from writing, with everything you usually need."
tldr: "Markdown is a simple plaintext document format that removes complexity and toil from writing, with everything you usually need. Its simplicity, expressiveness, and widespread support make it a compelling alternative to complicated word processors and visual editing programs. People who work in Markdown often claim that it helps them focus and be more productive."
credit: "https://unsplash.com/photos/o14nNEbLa-s"
image: "/media/2019/02/unsplash-photos-o14nNEbLa-s.jpg"
thumbnail: "/media/2019/02/unsplash-photos-o14nNEbLa-s.tn-500x500.jpg"
categories:
- Productivity
---
Markdown has steadily become the dominant way I compose most text documents, which is saying a lot.
Its convenience, simplicity, expressiveness, and increasing ubiquity make it a compelling choice for all but a small fraction of the written material I produce.
What is Markdown, and what makes it so great?
And could/should you use it yourself?
<!--more-->

Markdown is a simple plaintext way to write moderately complex text documents---the types of content you might otherwise use a word processor to write.
It's composed of raw, unformatted text, with no images, bold, italic, or anything like that.
But it lets you include extremely simple formatting instructions within the text, which look almost like you want the formatted document to look.

The most obvious example is bulleted lists.
The following code,

```md
* Item one
* Item two
* Item three
```

Creates the following bulleted list:

* Item one
* Item two
* Item three

Markdown really is that simple.
You basically write a code that doesn't look like a code.

This lets you stop writing with WYSIWYG visual editors that somehow manage to mangle your writing and insert annoying invisible code that makes odd, frustrating things happen---like a bulleted list that has extra space between bullets that you can't seem to get rid of.

Many people report that when they write with Markdown, they feel more focused.
Markdown has a way of disappearing and getting out of the writer's way.
This might be why Markdown-based writing tools emphasize things like minimalism and getting into the zone, into a state of flow.

The tradeoff is that Markdown doesn't support *everything* you might want, such as complicated table layouts and image formatting.
But it *does* support nearly everything you probably use on a daily basis: headings, paragraphs, lists, images, links, footnotes, bold, italics, and so on.
Anything not supported in Markdown is still possible as long as HTML supports it, because an explicit part of the Markdown spec is that you can insert HTML tags anywhere you want.
This gives you a lot of richness without a lot of complexity, and makes sure that anything you can do in a browser is possible in Markdown.

Many Markdown editors also add support for extensions such as charts, diagrams, math equations, and so on.
Usually these are implemented with plugins such as MathJax or KaTeX for math equations, Mermaid for diagrams, and Chart.js for charts.

### Online Markdown Editors

There are lots of JavaScript Markdown implementations, and that means it's relatively simple to create a basic Markdown editor in a browser.
As a result, there are lots of online Markdown editors.
Many of them are far beyond the basics, though.
If you're not sure about Markdown, trying one of them is a great way to see what it's all about.

* [HackMD, collaborative markdown notes](https://hackmd.io/)
* [Showdown Live Editor](http://demo.showdownjs.com/)
* [Dillinger](https://dillinger.io/)
* [StackEdit](https://stackedit.io/)
* [JBT's Markdown Editor](https://jbt.github.io/markdown-editor/)
* [Minimalist Online Markdown Editor](http://markdown.pioul.fr/)
* [Markdown-it Online Demo](https://markdown-it.github.io/)
* [JavaScript Markdown Editor - SimpleMDE](https://simplemde.com/)
* [CommonMark Demo](https://spec.commonmark.org/dingus/)

### Markdown-Compatible Programs

An ever-increasing number of editing programs for computers, phones, and tablets use Markdown as the underlying storage format.
The advantage is that since it's simply plain text files underneath, it avoids lots of problems, and it's interoperable with tools nearly everyone uses.
An example in my own life is the Bear Notes program I use as a simpler replacement of Evernote.

Here's a (very partial) list of programs that support Markdown, in no special order:

* Many static website generators like [Hugo](https://gohugo.io) and Jekyll
* 1Password (in encrypted notes)
* GitHub issues, comments, wikis, and so on
* Stack Exchange posts
* The Airmail email client
* [Markdown Here](https://markdown-here.com/features.html) for writing Markdown in tools like GMail
* Browser-based slideshow programs like [Remark](https://remarkjs.com/) and [Reveal](https://revealjs.com/)
* A huge variety of programs for serious note-taking and writing, many with a specialty or particular purpose, and some of them open source: [Bear Notes](https://bear.app/), [Ulysses](https://ulysses.app/), [Simplenote](https://simplenote.com/), [Byword](https://www.bywordapp.com/), [IA Writer](https://ia.net/writer), [Paper](http://www.papereditorapp.com/), [Editorial](https://omz-software.com/editorial/), [Scrivener](https://www.literatureandlatte.com/scrivener/overview), [Quiver](http://happenapps.com/), [Boostnote](https://boostnote.io/), [Joplin](https://joplin.cozic.net/), [Write](http://writeapp.net/mac/), [Agenda](https://agenda.com/), [Notion](https://www.notion.so/), [Corilla](http://www.corilla.com/index.html), [Inkdrop](https://inkdrop.app/), [Remarkable](https://remarkableapp.github.io/), [TaskPaper](https://www.taskpaper.com/)
* Lots of dedicated Markdown file editors: [Typora](https://typora.io/), [Mou](http://25.io/mou/), [MacDown](https://macdown.uranusjr.com/), [MultiMarkdown Composer](https://multimarkdown.com/), [Marked2](http://marked2app.com/)
* Many newer text editors designed for programmers have Markdown live preview, such as [Atom](https://atom.io/) and [Visual Studio Code](https://code.visualstudio.com/)

### Building Websites with Markdown

It's easy to create websites with Markdown.
When you do this, you avoid having to type all the HTML tags, and your websites are cleaner and easier to maintain.
Most modern blogging platforms now support Markdown, and there are lots and lots of other ways to use Markdown to simplify and eliminate toil.

Here's a sample:

* Most modern blogging platforms like [Ghost](https://ghost.org), [Jekyll](https://jekyllrb.com/), and [Hugo](https://gohugo.io) not only support Markdown, but assume you'll prefer it.
* Most other static website generators support Markdown. There are so many static site generators now that there are at least two listing sites: [one](https://www.staticgen.com/), [two](https://staticsitegenerators.net/).
* You can even host websites entirely in Markdown. Here's [one example](https://github.com/oscarmorrison/md-page).
* This website is built in Markdown with the open-source [Story](https://story.xaprb.com) Hugo theme, which bundles a lot of extended features together such as Markdown slideshows and music notation.

### Markdown References and Tools

There are lots of tools for working with Markdown: quick-start guides, syntax checkers, linters, and so on.
Using these tools can help produce clean, tidy Markdown files and [avoid mistakes](https://circleci.com/blog/markdown-proofer/).
Here's a partial list.

* This [Markdown Reference](https://commonmark.org/help/) is the best quick-start guide for learning the syntax that I know of. Other helpful references include the [Mastering Markdown GitHub Guide](https://guides.github.com/features/mastering-markdown/) and the GitHub 
[Basic Writing and Formatting Documentation](https://help.github.com/articles/basic-writing-and-formatting-syntax/).
* Style guides and syntax checkers that I'm aware of include [markdown-styleguide](https://github.com/slang800/markdown-styleguide),
[vscode-markdownlint for Visual Studio Code](https://github.com/DavidAnson/vscode-markdownlint), [markdownfmt](https://github.com/shurcooL/markdownfmt) and 
[mdfmt](https://github.com/moorereason/mdfmt) for auto-formatting, and
[tidy-markdown](https://github.com/slang800/tidy-markdown) for fixing formatting mistakes and standardizing syntax.
* [Markdown Table generator](http://www.tablesgenerator.com/markdown_tables) for easy table generation.

### Markdown Specifications and Standards

Markdown was originally described in what was essentially a blog post and a Perl program, but since then it has been formalized, and now there are various specs.

* The [CommonMark](http://commonmark.org/) specification has become more or less the canonical reference specification. There's also some extensions to the original Markdown syntax, such as those supported by the [GitHub Flavored Markdown Spec](https://github.github.com/gfm/). Most of these processor-specific extensions are included in the CommonMark syntax specification.
* The [Markdown Wikipedia page](https://en.wikipedia.org/wiki/Markdown) has a lot of additional information and references.

### Markdown Meta-Standards

In addition to standards for Markdown itself, there are related standards that specify things like file naming and organizational conventions, which---when followed---allow tools to add extra functionality like workflows and special-purpose uses.
Many of these are built upon, or compatible with, Markdown.
Here's a list of some I'm aware of:

* [Textbundle](http://textbundle.org/) is simply a folder containing a markdown file, a manifest (in JSON format) and assets, such as images.
* [CriticMarkup](http://criticmarkup.com/) is a plain-text language for proofreading and adding commentary (redlines, corrections, etc) to plain-text documents like Markdown.
* [Markaround](https://github.com/Markaround/markaround) is a file organization convention that lets Markaround-aware editing programs enhance the editing and file management experience.
* [Fountain](https://fountain.io/) is a markup language for screenwriting. It's sort of like Markdown, and it's supported by some apps that also support Markdown.
* [TaskPaper](https://www.taskpaper.com/) is also "sort of Markdown." It's a plain text to-do list app for Mac.


### Markdown Processors

A Markdown processor is a programming library that reads Markdown syntax and translates it to fully formatted output, usually in HTML for web pages, but often for other purposes too, like PDF export.
There are many Markdown processors.
Some of the most common are:

* [marked](https://github.com/markedjs/marked)
* [Showdownjs](http://showdownjs.com/)
* [commonmark.js](https://spec.commonmark.org/dingus/)
* [markdown-it](https://markdown-it.github.io/)
* [blackfriday](https://github.com/russross/blackfriday)
* [madoko](https://www.madoko.net/)
