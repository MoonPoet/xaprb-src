---
title: 'Lightweight Markup Languages'
date: "2019-02-04T20:13:12-05:00"
url: "/blog/lightweight-markup-languages"
description: "I've developed a preference for lightweight markup languages whenever I can use them, which turns out to be most of the time."
tldr: "I've developed a preference for lightweight markup languages whenever I can use them, which turns out to be most of the time. In this article I explore the tradeoffs of ABC music notation, diagramming languages, YAML, org-mode, and math equation typesetting."
credit: "https://unsplash.com/photos/czDvRp5V2b0"
image: "/media/2019/02/unsplash-photos-czDvRp5V2b0.jpg"
thumbnail: "/media/2019/02/unsplash-photos-czDvRp5V2b0.tn-500x500.jpg"
classes:
- feature-music
categories:
- Productivity
---
I wrote yesterday about [Markdown](/blog/markdown/), a lightweight document markup language that I use heavily.
Today I want to analyze what some of the best lightweight markup languages have in common, and when it makes sense to use a more heavyweight language instead.
<!--more-->

I define lightweight markup languages this way: the markup in some way resembles, or helps the author visualize, the rendered output.
A good lightweight markup language is readable in the markup source as well as the final document.
Markdown is a good example because the markup is so minimal it nearly disappears.
But there are other examples too.

One I've used recently is the [ABC music notation](http://abcnotation.com/).
From what I've learned of ABC, it didn't start out as a markup language, per se.
Instead, it was an *alternative music notation* that was basically a music shorthand.
You can literally read and play the source markup of ABC, and as far as I know, that is how it was originally used, to "write music notation in plain text files."

Here's an example of ABC source code:

```
X:1
T:Dark Island
M:3/4
L:1/8
K:C
E2|:A3B A2|G3A G2|E3D C2|D4GA|B3A G2|B d3DD|B3d B2|A3DE|
  |A3B A2|G3A G2|E3D C2|D4GA|B3D dB|A3D BA|G4G2|G4Bc|
  |d3e d2|B3A G2|E3G E2|D4GA|B3A G2|B d3B2|B4dB|A4DE|
  |A3B A2|G3A G2|E3D C2|D4GA|B3D dB|A3D BA|G4G2|G6:|
```

Notice how the music is formatted in a way that you could sight-read and play with a little practice.
It uses familiar symbols to emulate traditional music notation, such as a vertical pipe `|` for a bar line.
This very same notation can be transformed^[I used the [abcjs](https://abcjs.net/) JavaScript plugin to do that. It's part of [Story](https://story.xaprb.com), this blog's theme.] into traditional sheet music notation with an ABC program:

```abc
X:1
T:Dark Island
M:3/4
L:1/8
K:C
E2|:A3B A2|G3A G2|E3D C2|D4GA|B3A G2|B d3DD|B3d B2|A3DE|
  |A3B A2|G3A G2|E3D C2|D4GA|B3D dB|A3D BA|G4G2|G4Bc|
  |d3e d2|B3A G2|E3G E2|D4GA|B3A G2|B d3B2|B4dB|A4DE|
  |A3B A2|G3A G2|E3D C2|D4GA|B3D dB|A3D BA|G4G2|G6:|
```

I've written a lot of music notation over the years, and I've used notation formats such as XML, [Mup](http://arkkra.com/), and others to do it.
ABC notation is the easiest and most intuitive.
The tune I rendered there is simple, but ABC is surprisingly capable!
You can produce quite sophisticated sheet music with it, and the markup to produce it doesn't get infuriatingly complicated.
Of the notation markup formats I've used, ABC has the most music and the least markup.
In that way, it's similar to Markdown.

Other lightweight markup languages exist for lots of different purposes.
Examples that come to mind right now include the following:

* The diagram languages (flowchart, sequence, Gantt, etc) supported by [Mermaid](https://mermaidjs.github.io/)
* The [DOT graph description language](https://en.wikipedia.org/wiki/DOT_%28graph_description_language%29)
* [YAML](https://yaml.org/) for encoding data structures and metadata
* [Org Mode](https://orgmode.org) for structuring notes, plans, TODO lists, and much more

Many of these formats are capable of making the common things easy and the harder, more unusual things, at least possible.
This is a great virtue.
Some of them simply can't support the more advanced use cases, and that's okay.
If you're engraving the score for an orchestral work, you're probably not going to use ABC.
You'll use a markup language that makes a different set of tradeoffs: in return for an increased initial complexity, you get unlimited power, control, and sophistication.

A good example of this is [using LaTeX for math equation typesetting](/blog/math-equation-typesetting-with-latex).
It's complicated, but in return you get the ability to beautifully render the most complicated equations, and I'm not aware of a simpler format that doesn't run into limitations quickly.
Similarly, if you wanted to, you could use [LilyPond](https://en.wikipedia.org/wiki/LilyPond) for music notation: unlimited power, higher bar to entry.
(There are many other music engraving programs---I mention LilyPond because it is LaTeX-like).

Having done a whole lot of a bunch of these different types of tasks over the years, I've developed a preference for lightweight markup languages whenever I can use them.
For tasks where they seem to run into limitations quickly---such as math equations---I've learned to just use the more capable tool all the time, so that I only have to learn a single tool.
But most of the time I'm able to get away with the simpler, easier tool that gets most of the job done most of the time.
A nice benefit is that it forces me to keep things simple, instead of tempting me to take advantage of more complicated capabilities I just don't need.
