---
title: 'Building Static Sites With Hugo'
date: "2018-06-22T08:59:39-04:00"
url: "/slides/building-static-sites-with-hugo/"
image: "/slides/building-static-sites-with-hugo/cover.jpg"
description: "In this talk I'll explain the basics of Hugo and how it works."
ratio: "16:9"
theme: "monobloc"
---
layout: true
<div class="remark-slide-number" style="left: 20px; right: unset">@xaprb</div>

---
class: title, no-number
background-image: url(cover.jpg)
background-size: cover

.smokescreen[
# Building Static Sites With Hugo 
## Baron Schwartz &bullet; Capital Golang 2018
]

<div style="position: absolute; right: 20px; top: 20px; width: 250px;
background-color: rgba(0,0,0,.7); padding: 10px; border-radius: 10px">
<img src=vividcortex-horizontal-white-rgb.svg>
</div>

---
layout: true
<div class="remark-slide-number" style="left: 20px; right: unset">@xaprb</div>
<div class="remark-slide-number" style="left: 566px; width: 85px; padding: 5px">
<img src=vividcortex-horizontal-web.svg>
</div>

---
class: img-right
# Logistics and Contact Info

.col[
- Ask questions anytime
- Write me baron@vividcortex.com
- Tweet me at @xaprb
- Slides at [xaprb.com/talks/](https://www.xaprb.com/talks/)
]

.rc[<img src=headshot.jpg style="width: 100%; height: 100%; object-fit: cover">]

---
class: img-right
.col[
# Introduction & Agenda

- What is a static site?
- How can you build one?
- What is Hugo?
- How do you use Hugo?
- An overview of my personal site
- Resources
]

.rc[<img src="unsplash-photos-hM14nrcUUic.jpg" style="height: 100%; width: 100%; object-fit: cover">]

---
class: title
background-image: url(unsplash-photos-TyxmMj6Fqs4.jpg)
background-size: cover

.smokescreen[
# What Is A Static Site?
]

---
# Static Websites & Their Benefits

- A static website is plain HTML files

--
- It's simple, clean, fast, secure, flexible

--
- It's convenient, fun, fits your workflow

--
- It's highly available and low-maintenance

--
- It's the reaction to CMSs

---
class: img-right
.col[
# Static Sites Are For You

- Programmers
- Marketers
- Open source maintainers
- Documentation
- Hobbyists
- Bloggers
- Corporate sites
]

.rc[<img src="unsplash-photos-UoehHcoiMB0.jpg" style="height: 100%; width: 100%; object-fit: cover">]

---
# Dreamweaver, Wordpress, Static Sites

- In 1998, Dreamweaver was everywhere
- In 2008, Wordpress was ubiquitous
- In 2018, Jekyll + Hugo + etc are dominant

???
Remember Apache server-side includes?

--
- Why? Control, **separation of content & presentation**

---
class: img-right

.col[
# Why Not Use A CMS?

- Maintenance
- Complexity
- Performance
- Security
]

.rc[<img src="unsplash-photos-lxwCWj-3ig0.jpg" style="height: 100%; width: 100%; object-fit: cover">]

---
class: title
background-image: url(unsplash-photos-gvz9HhGuwIg.jpg)
background-size: cover
.smokescreen[
# How To Build A Static Site
]

---
# How Static Sites Work

1. Write the content, **without presentation**
  1. Typically in Markdown + front-matter
1. Create templates (nav, etc) to hold content
1. Render the content & inject it into the templates
1. Write out HTML files into directories
1. Merge/copy static assets (images, CSS, etc) into the dir

---
class: title
background-image: url(unsplash-photos-lF2MKLI7A1c.jpg)
background-size: cover
.smokescreen[
# What Is Hugo?
]

---
# Static Site Generators

- A SSG renders Markdown to HTML and applies templates
- A SSG has features to make your markdown simple & clean

--
- Examples: shortcodes for YouTube embedding; "include" files

???
These features are like the libraries and reusable snippets of Dreamweaver

--
- Ultimately, *most sites can be built statically*

???
- Example: you can use Swiftype for search, Disqus for comments, form providers
  for forms, Stripe for payments, Optimizely for A/B testing...

---
class: two-column
# Hugo is a Static Site Generator

.col[
- There are hundreds of static site generators
- The major ones are Jekyll, GitHub Pages (Jekyll), Hugo, and a few others
- Hugo is written in Go
]

--

.col[
- Hugo is very fast
- It's mature, powerful, and flexible
- It's popular with a large community
- It's easy to install
- The main downside is learning all its capabilities
]

---
class: title
background-image: url(unsplash-photos-jR4Zf-riEjI.jpg)
background-size: cover
.smokescreen[
# How Do You Use Hugo?
]

---
# Hugo Quick-Start ([Docs](http://gohugo.io/getting-started/quick-start/))

1. Download and install the latest from gohugo.io
1. Create a site: `hugo new site capitalgo`
1. Add a theme such as Ananke...
1. Customize the site's config
1. Create a new page or blog post: `hugo new posts/hello-world.md`
1. Start the Hugo server: `hugo server -D`
1. View your site at http://localhost:1313/
1. Push to GitHub, host with GitHub Pages, Netlify, or S3

The site live-reloads as you edit and save the content.

---
class: title
background-image: url(unsplash-photos-nXt5HtLmlgE.jpg)
background-size: cover
.smokescreen[
# A Tour Of My Site/Blog
]

---
# My Site's Features

- ~1300 pages/posts etc; Hugo renders in ~1s
- Slideshows in [RemarkJS](https://remarkjs.com/)
- [KaTeX](https://khan.github.io/KaTeX/) for math typesetting
- [LunrJS](https://lunrjs.com/) for search

---
# Resources

- [Hugo](https://gohugo.io) and its
  [Quick-Start](http://gohugo.io/getting-started/quick-start/)
- [Hugo Themes](https://themes.gohugo.io/)
- [Netlify](https://www.netlify.com/), [Forestry](https://forestry.io/)
- [GitHub Pages](https://pages.github.com/)
- [Static Site Generators](https://staticsitegenerators.net/)
- [My personal site](https://www.xaprb.com/),
  [source](https://github.com/xaprb/xaprb-src), and
  [theme](https://github.com/xaprb/story)

---
class: two-column
# Slides and Contact Information

.col[
Slides are at https://www.xaprb.com/talks/ or you can scan the QR code.

Contact: @xaprb / baron@vividcortex.com

]

.col[
<div id="qrcode"></div>
]
