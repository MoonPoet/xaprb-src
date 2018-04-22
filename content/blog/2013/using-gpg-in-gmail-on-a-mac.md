---
title: Using GPG in Gmail on a Mac
date: "2013-10-24"
url: /blog/2013/10/24/using-gpg-in-gmail-on-a-mac/
description: "It's not seamless, but GPG is doable with right-click options."
credit: "https://unsplash.com/photos/BppxrV1fo4s"
image: "/media/2013/10/unsplash-photos-BppxrV1fo4s.jpg"
categories:
  - Desktop
  - Security
---

I used to use the FireGPG extension to encrypt and decrypt text in a browser -- including wikis, for example, where sensitive client information could be stored. It's been a while since I had that need, but recently I wanted to send a GPG-encrypted message to a coworker, and FireGPG has been discontinued for years.

<!--more-->

I also use a Mac now, and Chrome is my primary browser. 
What to do? I looked around at a few Chrome extensions, but didn't really like them. 

Then [someone](https://twitter.com/mnxsolutions/status/393178369543520256) kindly pointed out on Twitter that the GPG suite from [gpgtools.org](https://gpgtools.org/) adds "services" to the right-click menu on a Mac, which enable all sorts of GPG actions on selected text, files, and so on. I had an earlier version of the GPG suite installed, so I upgraded it. (I got an error message about the pin entry application, so I uninstalled and reinstalled, which fixed it.) 

Et voila. Here I'm composing a message:

![image](/media/2013/10/compose.png)

Then I encrypt it:

![image](/media/2013/10/encrypt.png)

Here's the result:

![image](/media/2013/10/encrypted.png)

And here I've decrypted it on the receiving end:

![image](/media/2013/10/decrypted.png)

It's not quite as seamless as a plugin would make it, but for occasional use it's more than acceptable.



