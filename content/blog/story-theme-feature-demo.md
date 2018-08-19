---
draft: true
title: 'Story Theme Feature Demo'
date: "2018-08-19T13:36:21-04:00"
url: "/blog/story-theme-feature-demo"
description: "This is a feature demo for the Story Hugo theme."
credit: "https://unsplash.com/photos/vHnVtLK8rCc"
image: "/media/2018/08/unsplash-photos-vHnVtLK8rCc.jpg"
thumbnail: /media/2018/08/unsplash-photos-vHnVtLK8rCc.tn-500x500.jpg
classes:
- feature-figlink
- feature-fignum
categories:
- Web
---
This blog post is a demo (and test) of many of the features I've built into the [Story](https://github.com/xaprb/story) Hugo theme I use.

### Feature Flags

Feature flags control many of Story's features.
You can enable and disable them using CSS classes defined in your site config or in an individual post's front matter.
The syntax in YAML looks like this in the site config (this isn't a complete list):

```yaml
params:
   classes:
   - feature-math
   - feature-figcaption
   - feature-figcaption-hidden
   - feature-3dbook-covers
   - feature-hyphenate
   - feature-justify
```

In an individual page's front matter you can insert the same values. The
contents of both lists are combined and put into the `<body>` tag's `class`
attribute, verbatim:

```html
<body class="feature-math feature-figcaption...
```

Some features can be negated, so if they're defined in the site config they can
be turned off in an individual page's front matter, e.g.:

```yaml
---
title: My Blog Post
classes:
- feature-nohyphenate
```

### Image Captions and Figures

Story can automatically convert your images into figures with captions. 
There are several ways this can be done. In order of
precedence, here is what Story tries to do:

An image with an `<em>` _immediately following it in the same paragraph_ treats
the content of the `<em>` as the image caption. To enable this, the image and
the text must not have a blank line between them. Example:

```md
![Water Lily](/media/2018/08/unsplash-photos-vHnVtLK8rCc.jpg)
_Water lily photo by Zoltan Tasi on Unsplash_
```

This markup results in a `<p><img...><em...></p>` markup that Story converts into a captioned figure.
Hover your mouse over the picture to see the caption:

![Water Lily](/media/2018/08/unsplash-photos-vHnVtLK8rCc.jpg)
_Water lily photo by Zoltan Tasi on Unsplash_


If there's no `<em>` to use, Story uses the image's `title` attribute as a fallback:

```md
![Water Lily](/media/2018/08/unsplash-photos-vHnVtLK8rCc.jpg "A water lily")
```

![Water Lily](/media/2018/08/unsplash-photos-vHnVtLK8rCc.jpg "A water lily")

Finally, Story falls back to the `alt` attribute:

```md
![Water Lily](/media/2018/08/unsplash-photos-vHnVtLK8rCc.jpg)
```

![Water Lily](/media/2018/08/unsplash-photos-vHnVtLK8rCc.jpg)

Additional image caption and figure features:

- Figures get sequentially numbered `ID` attributes of `#fig-1` and so on, so
  you can link to them.
- The `feature-figlink` feature flag searches the article for text such as
  Figure 1 and automatically links it to the appropriate figure.
- If the `feature-fignum` feature is enabled, the text of the caption is
  prepended with the figure number. Click here to <a id="fignum">toggle this
  feature</a>, then inspect the captions again to see the effect.
- The `feature-figcaption-hidden` feature makes the captions hidden until you
  move the mouse over them. The `feature-figcaption-visible` feature flag
  overrides this and makes the captions visible immediately below the image.
  Click here to <a id="figvisible">toggle this feature</a>.

### Image Formatting Controls

![Small Lily](/media/2018/08/lily.jpg# fr ph1)

Images are automatically shrunk to fit into the width of the article.  You can
control image floats and padding with pseudo-classes in the URL fragment, e.g.

```md
![Small Lily](/media/2018/08/lily.jpg# fr ph1)
```

There's a limited selection of these pseudo-classes, whose names are inspired by
the [Tachyons](http://tachyons.io/docs/) CSS library; check Story's CSS for
what's supported. Images that use this
[technique](/blog/how-to-style-images-with-markdown/) don't get converted into
figures with captions.

[![Small Lily](/media/2018/08/lily.jpg# 3dbook)](https://unsplash.com/photos/vHnVtLK8rCc)

A book cover that's inside an `<a>` link can be floated right and given a 3d
look with the `3dbook` URL fragment pseudo-class. If floated images interfere
with content, it's usually headings, so the `h3-cl`, `h3-cr`, and `h3-cb`
feature flags will add CSS clears to `<h3>` elements. Story assumes you'll use
H3 in your content and reserve H2 and H1 for the article's title and subtitle.

### Mathematical Equation Typesetting

Story uses the [KaTeX](https://khan.github.io/KaTeX/) library to typeset
mathematical formulae in {{< math >}}\LaTeX{{< /math >}} notation. KaTeX is
similar to MathJax, but simpler and faster. Story provides a `math` Hugo
shortcode to help avoid problems that result from Markdown processing, both for
inline code like {{< math >}}x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}{{< /math >}}
and in block form:

{{< math >}}
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
{{< /math >}}

Math typesetting is controlled with the `feature-[no]math` flag.

### Table Captions

Hello | There
-----:| ------
A table | of stuff
that I like | a lot

*A table of important things*

<style type="text/css">
table + p em { border: 1px solid red }
</style>

### Typography Controls

Story is designed for long-form content such as essays and technical blog posts.
It is built for readability and grace in screen and print media. (Try opening
your print dialog and saving this page as a PDF). As such, it supports text
justification and hyphenation. Click here to toggle <a id="hyph">hyphenation</a>
and <a id="just">justification</a>. These features can be enabled or disabled
with the `feature-[no]hyphenate` and `feature-[no]justify` feature flags.

Call me Ishmael. Some years ago---never mind how long precisely---having little or no money in my purse, and nothing particular to interest me on shore, I thought I would sail about a little and see the watery part of the world. It is a way I have of driving off the spleen and regulating the circulation. Whenever I find myself growing grim about the mouth; whenever it is a damp, drizzly November in my soul; whenever I find myself involuntarily pausing before coffin warehouses, and bringing up the rear of every funeral I meet; and especially whenever my hypos get such an upper hand of me, that it requires a strong moral principle to prevent me from deliberately stepping into the street, and methodically knocking people’s hats off---then, I account it high time to get to sea as soon as I can. This is my substitute for pistol and ball. With a philosophical flourish Cato throws himself upon his sword; I quietly take to the ship. There is nothing surprising in this. If they but knew it, almost all men in their degree, some time or other, cherish very nearly the same feelings towards the ocean with me.

### Typography Demo

This section demonstrates typography of a variety of elements not otherwise used
in this article. Here is text with
_emphasis_ and **boldness**; ~~strikethrough~~.^[A footnote]

> This is a blockquote. I thought I would sail about the unimaginative incomprehensibilities of the watery part of the world. It is a way I have of driving off the spleen and regulating the circulation. (This quote is a demo of justification and hyphenation.)
>
>> Blockquotes can nest.

Here is an unordered list:

- Item one
- Item two
- Item three is longer. I thought I would sail about a little and see the unimaginative incomprehensibilities of the watery part of the world. It is a way I have of driving off the spleen and regulating the circulation. (This is a justification and hyphenation demo.)

And an ordered list:

1. Item one
1. Item two
1. Item three is longer. I thought I would sail about a little and see the unimaginative incomprehensibilities of the watery part of the world. It is a way I have of driving off the spleen and regulating the circulation. (This is a justification and hyphenation demo.)


<script type="text/javascript">
$( "#fignum" ).click(function() {
	$("body").toggleClass("feature-fignum");
});
$( "#figvisible" ).click(function() {
   $("body").toggleClass("feature-figcaption-visible");
});
$( "#hyph" ).click(function() {
   $("body").toggleClass("feature-hyphenate");
});
$( "#just" ).click(function() {
   $("body").toggleClass("feature-justify");
});
</script>
