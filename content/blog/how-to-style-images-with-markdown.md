---
title: 'How to Style Images With Markdown'
date: "2018-08-13T20:38:17-06:00"
url: "/blog/how-to-style-images-with-markdown"
description: "This post presents a variety of ways to format images with Markdown, from brute force to proprietary syntax extensions, unwise hacks, and everything in between."
credit: "https://unsplash.com/photos/jTCLppdwSEc"
image: "/media/2018/08/unsplash-photos-jTCLppdwSEc.jpg"
thumbnail: /media/2018/08/unsplash-photos-jTCLppdwSEc.tn-500x500.jpg
categories:
- Web
---
Markdown is a convenient HTML-focused shorthand syntax for formatting content such as documentation and blog articles, but it lacks basic features for image formatting, such as alignment and sizing.
This post presents a variety of ways to format images with Markdown, from brute force to proprietary syntax extensions, unwise hacks, and everything in between.
<!--more-->

Here's how you insert an image in Markdown:

```md
![alt text](/src/of/image.jpg "title")
```

That is, Markdown allows you to specify an `<img>` tag with `src`, `alt`, and `title` attributes in HTML.
Standard Markdown doesn't offer anything beyond this, but it's very common for websites to need `width`, `height`, and CSS `class` attributes as well.

The rest of this post is dedicated to various solutions to these shortcomings.
To motivate this discussion, I'll use the example of a large image that should be displayed at a smaller size.
I won't show you how to add alignment, floating, or padding---but my sizing example will suffice, because once you know how to change an image's size, you'll know how to do other things too.

I'll show you the best solutions first, and the undesirable ones last.

### Use Standard HTML

Markdown was originally designed for HTML authoring, and permits raw HTML anywhere, anytime.
As such, the most straightforward solution is simply to use HTML with the desired attributes:

```html
<img src="kitten.jpg" alt="Kitten"
	title="A cute kitten" width="150" height="100" />
```

This works, and gives you unrestrained control over the resulting HTML.
But Markdown is appealing for its simplicity, unlike HTML that's cluttered with messy markup.
Thus, many people dislike this solution because it defeats the purpose of Markdown.

### Use CSS And Special URL Parameters

In general, the best way to style images is with CSS.
Modern CSS syntax can [select elements based on the values of their attributes](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Attribute_selectors), so one way to apply CSS rules is to encode extra information into Markdown's standard `src` attribute.
In this section I'll discuss these possibilities.
Later I'll show you some undesirable CSS-related techniques too.

There are two places in a URL that you can overload to carry information that CSS can use: the URL fragment, and URL query parameters.

The URL fragment is the part that comes after the `#` character.
When it's used in a website's URL, it can scroll the page to bring a desired part of the content into view, but you can add it to images, too.
When you do that, it essentially does nothing as far as the browser is concerned, and a typical user will never see it in the browser's address bar either.
But it's useful for our styling needs.
Here we'll add a `thumbnail` fragment to the image's source URL:

```md
![Kitten](kitten.jpg#thumbnail)
```

This information is kept entirely client-side, and browsers don't transmit this part of the URL to the server when they request content.
However, CSS and JavaScript can read the fragment and use it.
Here's how to write a CSS selector that will match images with this "thumbnail" information in the URL:

``` css
img[src*="#thumbnail"] {
   width:150px;
   height:100px;
}
```

The `*=` selector syntax matches if `#thumbnail` appears anywhere in the `src` attribute.
You could also anchor the matching to the _end_ of the URL with `$="#thumbnail"`.

This permits encoding only a single value into the URL, but you can modify this technique to add several.
CSS also has a `~=` selector, which matches if the specified value appears exactly in the attribute's value, as a space-delimited "word," so to speak.
This lets you simulate combining multiple "classes" in the URL fragment:

```md
![Kitten](kitten.jpg# thumbnail bordered)
```

Now you can target these pseudo "class" names from CSS:

``` css
img[src~="thumbnail"] {
   width:150px;
   height:100px;
}
img[src~="bordered"] {
   border: 1px solid black;
}
```

An equivalent way to encode a space into a URL is with the `%20` URL encoding, but I've found that this doesn't work with the technique I showed here.

Naturally, you can pick different ways to structure values, such as using a `key=value` syntax or whatever suits your purposes.
Depending on what you prefer, you can use any of the CSS selector syntaxes that works well for you.

Another alternative is to use ordinary URL query parameters, the part that comes after the question-mark:

```md
![Kitten](kitten.jpg?thumbnail)
```

This will work, and you can use the same types of CSS selectors to apply styling to the resulting image.
However, in my opinion this is slightly less desirable, because query parameters are meant to transmit information to the server.
The browser will include the parameters in the request, and there could be other disadvantages, such as preventing the browser from caching the images for better performance.
Overall I don't see any advantages to query parameters, unless there's some reason you can't use the URL fragment.

### Use CSS's nth-child() Selectors

You can also use CSS selectors that will select images based on their position in the document.
For example, if your blog's main content is wrapped inside an element with an `article` and you want to change the appearance of the image inside the third paragraph, you could write the following CSS:

```css
.article p::nth-child(3) img {
   width:150px;
   height:100px;
}
```

This will work, but it's tedious and requires article-specific `<style>` tags with custom CSS.
And you'll need to change the CSS if you change the article, for example adding another paragraph above the image.
In general this technique will be a burden to maintain, and I don't do it.

To learn more about this, take a look at the CSS [nth-of-type](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-of-type) and [nth-child](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-child) selectors.

### Use Proprietary Markdown Extensions

The original Markdown spec isn't formal, and implementations vary.
Many Markdown processors extend the syntax to add richness and control to the output.
From Pandoc to Kramdown and [Github-Flavored Markdown (GFM)](https://guides.github.com/features/mastering-markdown/), extra syntaxes abound.
There's very little standardization, except for some consensus towards [CommonMark](https://commonmark.org) and the gravitational pull of very popular libraries and processors.
In this section I'll explore some of these.

Some Markdown editors like Mou (a Mac writing app) have sizing extensions:

```md
![Kitten](kitten.jpg =150x100)
```

This example syntax is limited and isn't widely supported.
More common is the way Kramdown [offers extensions to add attributes to block-level elements](https://kramdown.gettalong.org/quickref.html#block-attributes), including not only the height and width but CSS and other attributes:

```md
![Kitten](kitten.jpg){: width=150 height=100 style="float:right; padding:16px"}
```

Kramdown also supports one or more CSS classes with a shorthand syntax.
Here's an example of how to add `class="thumbnail bordered"` to the HTML after processing with Kramdown:

```md
![Kitten](kitten.jpg){:.thumbnail.bordered}
```

Pandoc offers a [relative width specification](http://pandoc.org/MANUAL.html#extension-link_attributes), which works not only for HTML output, but for other output formats such as {{< math >}}\LaTeX{{< /math >}} as well:

```md
![Kitten](kitten.jpg){ width=50% }
```

Some other Markdown flavors offer similar ways to add attributes, though the syntax may differ slightly.
All of these, however, extend the basic Markdown syntax in ways that may be incompatible.
And some rumored support for extended syntax simply doesn't exist; for example, I've seen references to nonexistent extensions in the blackfriday Markdown processor, which Hugo uses.

### Use Wrapper HTML Tags

Another technique is to put an HTML tag around the `<img>` tag, like this:

```html
<div style="width:150px; height:100px">
![Kitten](kitten.jpg)
</div>
```

Unfortunately, standard Markdown doesn't process and convert the text inside of tags such as the `<div>`; as soon as it sees raw HTML it simply outputs it verbatim until the tags are closed again.
This approach will work only with processors that support Markdown syntax extensions such as [Markdown Extra](https://en.wikipedia.org/wiki/Markdown#Markdown_Extra).

### Use Processor Hacks That Markdown Editors Ignore

Some users like to edit in a WYSIWYG editor such as Mou, but use a system such as Hugo to render the final Markdown into HTML for publication.
Hugo has special processors that can add features to the output, such as brace-delimited _shortcodes_, which Mou doesn't understand.

You can [take advantage of this](https://discourse.gohugo.io/t/add-a-class-to-images/6724/19) to inject content that overflows the `alt` attribute.
The trick is to make the shortcode output an extra closing quote at the beginning of its output, emit the desired HTML attributes but omit the closing quote, and let the Markdown processor supply that.
The benefit is that your editor will ignore the markup it doesn't recognize, so it doesn't disrupt your editing workflow.
I don't think this is better than the alternatives myself, but I mention it for completeness.

### Abuse Image Attributes As CSS Selector Targets

In addition to the URL fragment as discussed previously, modern CSS syntax can select values of the `alt` and `title` attributes that standard Markdown supports.
In this section I'll discuss each of these possibilities, although I discourage their use.

Many Markdown users are only aware of the standard syntax's support for the `alt` attribute, and don't add titles to their images.
In fact, many don't even add alt text:

```md
![](kitten.jpg)
```

This makes it seem as though the alt text is undeveloped real estate that could be repurposed, for example adding the pseudo-equivalent of a "thumbnail" CSS class.
Here's how you might attempt to do that:

```md
![thumbnail](kitten.jpg)
```

The corresponding CSS to select and format this image could be

```css
img[alt=thumbnail] {
   width:150px;
   height:100px;
}
```

Technically, this will work, but it's not good for accessibility.
Users who are using a screen reader or other accessibility aid will gain no benefit, and will suffer due to the lack of helpful information and the presence of misleading data in places it's not intended to be.
I discourage this practice.

A variation I've seen is to append, rather than replace, the alt text, using syntaxes such as the following examples:

```md
![Kitten class=thumbnail](kitten.jpg)
![Kitten -thumbnail](kitten.jpg)
```

Those examples can be paired with a CSS selector that matches the end of the attribute, such as `img[alt$="-thumbnail"]`.
These are perhaps less offensive than replacing the alt text entirely, but I still discourage this because there are better ways.

A variant of this approach, which has a roughly equivalent impact on accessibility, is to overload the `title` attribute with formatting instructions:

```md
![Kitten](kitten.jpg "thumbnail")
```

This can be selected from CSS as follows:

```css
img[title=thumbnail] {...}
```

Again, I want to emphasize that this approach is not better than misusing the `alt` attribute.
You should use URL fragments or URL query parameters as discussed earlier, instead of hijacking the image's alt text or title.

On the other hand, if you want to write custom CSS per-article and use the CSS selector to target the image's _real_ alt text or title, that's perfectly fine.
In fact this is probably easier to maintain than `nth-child` selectors:

```css
img[alt="Kitten"] {
   width: 150px;
   height: 100px;
}
```

