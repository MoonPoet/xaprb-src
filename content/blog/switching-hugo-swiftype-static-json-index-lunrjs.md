---
title: Switching From Swiftype to a Static JSON Index and LunrJS
date: 2018-02-17 21:10:41 -0500
categories:
- JavaScript
- Web
author: Baron Schwartz
description: Adding LunrJS search to my website was incredibly easy.
image: media/2018/02/magnifying-glass.jpg

---
I was shocked how easy it was to add a browser-based search engine to this
website using [LunrJS][lunr] and [Hugo's][hugo] new content types. With a few
small changes and less than 30 minutes of work, I had a great search engine up
and running. I moved it under the menu and made it into a separate [search
page][search].

If you're interested to mimic my approach, you can see the [commit][github] that
I used to add the search page. I copy-pasted most of this code from articles
[here][halfelf-1] and [here][halfelf-2].

(Update: I broke my RSS feeds with the commit above, and needed [two][github2] [more][github3] to fix them).

![Magnifying Glass](/media/2018/02/magnifying-glass.jpg)

<!--more-->

I'd like to express my appreciation to [Swiftype][swiftype] for their excellent
search engine, which I have now removed. I've used it for years and always loved
their service. I still use it, and will continue doing so, for cases that
require more robust capabilities.

[Pic Credit](https://pixabay.com/en/philatelist-stamp-collection-stamp-1844080/)

[search]: /search/
[swiftype]: https://swiftype.com/
[hugo]: https://gohugo.io
[lunr]: https://lunrjs.com/
[halfelf-1]: https://halfelf.org/2017/hugos-making-json/
[halfelf-2]: https://halfelf.org/2017/hugos-lunr-search/
[github]: https://github.com/xaprb/xaprb-src/commit/46e70a8af665407413ca46c0b541c018670b65e2
[github2]: https://github.com/xaprb/xaprb-src/commit/64b235469f669871749d720a8ab796d1404b01f1
[github3]: https://github.com/xaprb/xaprb-src/commit/4dc8ba4d5e5c6982f25dca08595a25b0acbc19e0