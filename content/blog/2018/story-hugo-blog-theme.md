---
title: 'The Story Hugo Blog Theme'
date: "2018-09-14T07:54:52-04:00"
url: "/blog/story-hugo-blog-theme"
description: "Story is the Hugo theme I developed for my blog. I've published it for others to use too."
credit: "https://unsplash.com/photos/_NNsOxgemgg"
image: "/media/2018/09/unsplash-photos-_NNsOxgemgg.jpg"
thumbnail: /media/2018/09/unsplash-photos-_NNsOxgemgg.tn-500x500.jpg
categories:
- Web
- About
---
I've developed a Hugo theme for this blog, and now I've published it for you to use too.
It offers a fast and responsive layout, beautiful design, built-in search, JavaScript presentations, LaTeX equation typesetting, social and SEO optimizations, and much more.
Many of the theme's features are pretty unique---for example, the extensions to give you control over formatting images, which I wrote about [here](/blog/how-to-style-images-with-markdown/), are built-in natively.
<!--more-->

All of these features are seamlessly integrated for a great user experience.
Just install the theme into your Hugo site and go.
The theme's source code is available on GitHub at https://github.com/xaprb/story/.
You can install it by simply cloning the repo and adding it to your config file:

```
git submodule add https://github.com/xaprb/story.git themes/story;\

# Edit your config.toml configuration file
# and add the Story theme.
echo 'theme = "story"' >> config.toml
```

I've published a demo site that not only showcases the theme's features, but serves as documentation too.
You can see it at [story.xaprb.com](https://story.xaprb.com).

Here are a few screenshots of the theme. First is what your homepage might look like:

![Story has customizable header images.](/media/2018/09/story-theme-1.png)

Here's what a list page, such as a blog, looks like as you scroll through the content:

![Story displays image thumbnails and summary previews of content.](/media/2018/09/story-theme-2.png)

Story showcases your biography at the bottom of the page:

![Story showcases your biography at the bottom of the page.](/media/2018/09/story-theme-3.png)

Story integrates RemarkJS for beautiful, simple Markdown slideshows:

![Story integrates RemarkJS for beautiful, simple Markdown slideshows.](/media/2018/09/story-theme-4.png)

I have a long list of enhancements I'd like to make as time permits, and contributions are welcomed on the GitHub repository.
