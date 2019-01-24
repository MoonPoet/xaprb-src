---
title: 'Math Equation Typesetting With Latex'
date: "2019-01-23T19:35:03-05:00"
url: "/blog/math-equation-typesetting-with-latex"
description: "I love LaTeX for typesetting math equations. It's a simple, plaintext markup language that produces beautiful results."
tldr: "I love LaTeX for typesetting math equations. It's a simple, plaintext markup language that produces beautiful results. In this article I give a quick introduction to LaTeX and some starting points for learning more, such as books, tools, and examples."
credit: "https://unsplash.com/photos/aIYFR0vbADk"
image: "/media/2019/01/unsplash-photos-aIYFR0vbADk.jpg"
thumbnail: "/media/2019/01/unsplash-photos-aIYFR0vbADk.tn-500x500.jpg"
categories:
- Markup
---
For nearly two decades, I've routinely needed to enter math equations into computer programs for display.
I've used a lot of markup languages to describe these equations, but I've found nothing is as easy, beautiful, reliable, or comprehensive as LaTeX.
And even though you might not know LaTeX yourself, I'm pretty sure that nothing approaches its ubiquity either.
This article is a love poem to LaTeX, and a collection of resources to help you learn more about it.
If you don't know LaTeX, and you ever put math equations into documents on a computer, I encourage you to indulge your curiosity!
<!--more-->

### What is LaTeX?

LaTeX (I pronounce it lay-tek) LaTeX is free software for computer typesetting.
It is also a syntax---a plain-text markup language.
It's based on the TeX typesetting language.
It can produce beautiful mathematical equations, but it's also great at many other things, including typesetting books.
For decades it has been the standard for publishing most scientific papers, books, and so forth.

Here's a simple equation---the quadratic equation---typeset in LaTeX.

{{<math>}}
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
{{</math>}}

The code that's used to typeset that is as follows:

```tex
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
```

It's a mixture of literals and backslashed commands, such as the `frac` command to create a fraction.

In this article I want to focus on some of the variety of math typesetting tools and resources related to LaTeX.

### Learning LaTeX

The LaTeX language is sophisticated but it's not hard to learn.
If you want to learn LaTeX, either for general typesetting or for math equation typesetting, my favorite resources are:

- The [not so short guide to LaTeX](https://www.ctan.org/tex-archive/info/lshort/english/), by Tobi Oetiker.
- [A Guide To LaTeX]({{< amz 0321173856 >}}) by Kopka and Daly, which I own and like.

### Programs That Understand LaTeX

The LaTeX syntax for mathematical equations is supported by lots of other programs beyond LaTeX itself.
For example, there's [MathJax][mathjax] and [KaTeX][katex], JavaScript libraries for rendering equations in websites.
(This website uses KaTeX.)
And there's Google Docs, which lets you input equations in LaTeX both natively and through mechanisms like Google Docs add-ons and Chrome extensions.
The list goes on, and on.
Even Apple's Keynote presentation program added LaTeX support in 2018!

![Release notes showing Keynote adding LaTeX support](/media/2019/01/keynote-latex.png)

### Programs That Can Create LaTeX

Sometimes the easiest way to create the right LaTeX code is to use a visual editor and export the resulting code.
A few ways to do this are:

- Use [Mathpix](https://mathpix.com/), which is frankly mindblowing---you can handwrite your equation and scan it, or scan anything on the screen of your computer. I've used it to generate LaTeX code for extremely complicated equations and it's worked flawlessly. A huge time saver!
- Use [Desmos](https://www.desmos.com/) and after entering your equation, reveal or copy it as LaTeX.
- Use the Grapher program that comes with a Mac. You can right-click and copy your equation as LaTeX.

### Online LaTeX Editors

I usually use LaTeX by installing a distribution of the software, such as the TeX Live distribution.
This installs commandline and GUI programs to write TeX and LaTeX documents.
But I appreciate the modern era of web-based software, with no need to install and maintain it.
A couple of the most popular options are [ShareLaTeX](https://www.sharelatex.com/) and [Overleaf](https://www.overleaf.com/).
Both make it convenient and easy to collaborate on sophisticated LaTeX documents online.

### Just For Fun

Math equation typesetting is immensely complex, but I think it's also very beautiful.

![A Diagram from The Printing of Mathematics](/media/2019/01/printing-of-mathematics.jpg)

([Source](http://ultrasparky.org/school/pdf/Rhatigan_Monotype_4-line_math.pdf))

Hanno Rein created a [LaTeX package that will add a coffee stain](http://hanno-rein.de/archives/349) to your documents, saving a lot of time compared to printing the document and then adding the stain with a coffee cup!

![Coffee Stain LaTeX Package](/media/2019/01/coffee.png)

[mathjax]: https://www.mathjax.org/
[katex]: https://katex.org/
