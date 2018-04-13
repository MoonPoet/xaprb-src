---
url: /blog/switching-mathjax-katex/
title: 'Switching from MathJax to KaTeX'
date: "2018-04-07T20:32:07-04:00"
categories:
  - Writing
author: "Baron Schwartz"
description: "I've used MathJax for LaTeX mathematical typesetting for years; I replaced it with KaTeX, which is smaller and faster"
image: "/media/2018/04/fractal-1405724_1280.jpg"
---

For several years, I've used MathJax on this blog to typeset mathematical
formulae in LaTeX notation. MathJax is fully compatible with LaTeX, and makes it
simple to create beautifully typeset equations such as the following:


\\[
\\rho = \\frac{1}{2} \\left( \\sqrt{2} \\sqrt{\\lambda+2} + \\sqrt{2} \\sqrt{ \\frac{ -2 \\lambda - \\lambda^2 + \\sqrt{2} \\sqrt{\\lambda+2}}{\\lambda+2}} \\right)
\\]

[MathJax](https://www.mathjax.org/) is sophisticated, but is large and has a lot
of dependencies. It's not exactly slow, but it does render after the page loads,
and that's slow enough to be perceptible. I learned about
[KaTeX](https://khan.github.io/KaTeX/), a simpler, lighter alternative, and I've
switched to use it instead.

![Fractal]({{< param image >}})

<!--more-->

MathJax can be loaded from a CDN, but my website is [hosted on a
CDN](https://netlify.com) anyway, and I prefer to "vendor" my dependencies and
avoid too many external dependencies. I found that it was a little bit of a
chore to get MathJax vendored into my website's repository, and in so doing, I
discovered how large the project really is. It has a *lot* of files, fonts, and
so on. KaTeX is *much* smaller.

MathJax is simple to install, despite its size. If you're using it from a CDN,
it's a one-line `<script>` tag in the web page's header. Then you can just write
LaTeX---sorry, that's \\(\LaTeX\\)---in your page's source. MathJax makes the
rest happen magically.

KaTeX is slightly more involved. You have to include a JavaScript file in the
page, as well as a CSS file, and then set up the page to look for LaTeX
typesetting and render it. (MathJax does this automatically). Still, three lines
of setup isn't bad.

When I did this, at first I was disappointed. An equation that should have been
rendered nicely, as MathJax did, wasn't. Here's the MathJax equation:

![MathJax](/media/2018/04/mathjax.png)

Here's how it initially rendered with KaTeX:

![KaTeX font problem](/media/2018/04/katex-fonts-problem.png)

I opened the browser's inspector tools to check, and found that some fonts
hadn't loaded. I quickly realized I needed to vendor in the JS, CSS, and fonts.
After doing this, the results were satisfactory:

![KaTeX](/media/2018/04/katex.png)

If you look closely, you can see some minor differences in aspects such as font
weights and spacing.

My takeaway is this:

- Use MathJax if you need broader compatibility across every conceivable browser
  and output format, more sophisticated features such as the ability to interact
  with the equations in the browser, and absolutely perfect rendering.
- KaTeX might be right for you if you value a more compact and speedy library,
  and you don't mind ever-so-slightly different typography or less support for
  uncommon browsers.

Both libraries are extraordinary works of engineering and I thank the authors
and supporters.
