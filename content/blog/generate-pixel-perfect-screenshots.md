---
title: 'How To Generate Pixel Perfect Screenshots'
date: "2018-04-20T19:46:19-04:00"
url: "/blog/generate-pixel-perfect-screenshots"
description: "Use this simple trick to crop sequences of screenshots to exactly the same dimensions and location"
image: "/media/2018/04/dimitri-tyan-232294-unsplash.jpg"
categories:
- Conferences
---
I frequently do things like draw a diagram in a presentation app and take
screenshots of it to include into other programs. I'll create a diagram and then
take screenshots of steps of its evolution to show how I built it, step by step.
Here's how I crop to the same location and size every time, perfectly and
easily.

<!--more-->

Here's the scenario. Suppose I want to take screenshots of something, say, a
diagram for a presentation. I'm going to evolve this diagram as I narrate the
presentation. First I'll show a simple version, then a more complicated version,
on subsequent slides. It'll look like this, slide by slide:

![Three Steps](/media/2018/04/step-N.jpg)

I want the picture to be in the same place and the same
size, not shift around as I flip between slides. How can I do this?

My secret weapon is the `imagemagick` suite of command-line tools and a thick
black border. I'll draw the first version of the diagram, *inside a thick
black box*. Like this:

![With Border](/media/2018/04/with-border.png)

Then I start changing the image. Every time I get it to a state I want to
snapshot, I screenshot it by pressing `Cmd-Shift-4` (I use a Mac) and clicking
and dragging the screenshot region *within the border*. It doesn't matter
exactly where inside the border; I make the border thick to make it easy. All
that matters is that the edge of the resulting screenshot is totally black, that
it doesn't have any margins that are different-colored.

When I'm done, I'll have a series of screenshots of different images, of
slightly different sizes, with irregular black borders around the edges. Now I'm
going to *trim the black borders off* with ImageMagick's `-trim` command,
leaving the images perfectly sized and located within the area inside the
border:

    for f in Screen*; do convert $img -trim $img; done

And *voila*, the border is gone. The `-trim` command works by deleting the color
of the corner pixels, shrinking the image perfectly.

In general, if you wonder whether ImageMagick can do something, the answer is
usually yes. For example, to make this post, I took three images of the diagram
and then created the final product with `convert Screen* +append step-N.jpg`.
You can do pretty much anything with ImageMagick.
