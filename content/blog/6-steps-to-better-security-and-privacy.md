---
title: 6 Steps to Better Security and Privacy
date: '2016-11-24T10:52:46-05:00'
author: Baron Schwartz
categories:
- Life Hacking
- Security
- Gear
tags:
- Encryption
- Privacy
- Passwords
- Authentication
- Backups
- Mobile
description: 'VPN, Keybase, Signal, and more: take these 6 steps to improve your digital
  security.'
image: ''
draft: false

---
I wrote [previously](/blog/2013/12/18/secure-your-accounts-and-devices/) about securing your digital life. Technology and digital threats are advancing so fast that we're almost inevitably all going to be attacked in some way. Here are a few more steps I've taken recently.

![Blue Marbles](/media/2016/11/blue-abstract-glass-balls.jpg)

<!--more-->

To repeat some of the recommendations from my previous post, you should absolutely use the following:

* 2-factor authentication everywhere possible (email, social media, etc)
* a password safe like 1Password so you never try to remember a password
* long, strong, randomly generated, unique, never-reused passwords
* full-device/full-disk encryption on hard drives, laptops, tablets, phones etc

Although I don't think it is realistic to think we can avert a catastrophic attack forever on a personal or global scale (think "digital 9-11"), I think mass attacks against easily identifiable vulnerable populations are much more common and damaging, so here are some additional steps to avoid being the "tallest poppy."

### 1. Use a VPN (It's Easy)

When you access the internet or use an app, you're opening a series of data connections between your device and another computer somewhere. Many common vulnerabilities are at or near the start of this chain: from your device to the WiFi router, from the router to the DSL device down the street, etc. A virtual private network (VPN) creates an encrypted tunnel between your device and at least part of the chain.

A VPN is a *big* step up in security and privacy. For example:

* A VPN can prevent people snooping on what you're doing if you're connected to an insecure WiFi point at the airport or coffee shop.
* A VPN can prevent your internet service provider from logging and inspecting your browsing or other usage---some internet service providers even modify what you browse, injecting ads, tracking, and other stuff into websites!
* If someone hacks into your home router or cable modem, they won't be able to intercept VPN-tunneled traffic before it leaves the house.

These are really legitimate things to worry about: millions of cheap, old, unsecured, underscrutinized devices such as routers and modems are sitting exposed to the internet, and tons of them have known security holes.

VPNs sound obscure and hard to set up, but they're not. You can get a subscription to a VPN service easily and cheaply. I use [Cloak](https://www.getcloak.com/), [Private Internet Access](https://www.privateinternetaccess.com/) and there are many others. Just search and read ratings from a few objective review sites.

A VPN service is also flexible. You can use a standard VPN client to connect; you don't have to use the one they probably provide for you. I use Tunnelblick to connect to Private Internet Access, for example, because Tunnelblick is open source so I trust it more, and I already use it for other VPNs I connect to.

### 2. Create a Family Password

I've become increasingly convinced that we're on the brink of widespread sophisticated automated telephone phishing attacks. Consider the following entirely realistic attack against your family's personal information and finances:

1. A robot telephones your parents and listens to the sound of their voice, then hangs up.
1. The robot calls you and imitates the sound of your parent's voice, engaging you in a simple conversation. "Baron, it's mom. I am at the hospital. I need your social security number, quick."

What would you do? Most people would blurt their SSN and ask questions later. You need a previously-agreed way to validate that it's really your mother on the phone. There are a lot of other scenarios you can imagine where you'd give the robot some really sensitive information.

Does this attack sound far-fetched? It's not. In the last year I've gotten amazingly sophisticated robot calls. They've been for relatively innocuous purposes ("can I count on you to donate to the veterans fund?") but they illustrate how adept computers are at carrying on pretty convincing conversations with humans. I've been fascinated at how quickly they've gotten good at this. And a sophisticated attacker could easily ask me for some information that seems harmless, call someone else and ask for more, put the pieces together quickly to form the whole puzzle, then a human could use the information to call the bank and convince the agent that they're me.

One way to avoid this is to agree on a family password or other cue. Many families have passwords for unexpected situations such as [sending a coworker to pick up the kids from school](http://www.homesafetyeducation.com/welcome/index.php?option=com_content&view=article&id=55&Itemid=59) when there's an emergency, for example.

I'm not sure I have the right answer for this yet. Please comment if you have a suggestion. We need a technique that works for humans under stressful situations, but doesn't fall prey to robo calls trying to create those situations and trick the humans into bypassing the system or revealing the secret.

### 3. Use Signal or WhatsApp

Encryption provides a host of benefits. We really, really, really need to normalize encryption as a global society. Plaintext communication needs to become weird, and encrypted needs to become easy and expected.

Right now it's the reverse, and people who use encryption for some types of communication are outliers. We need herd immunity.

WhatsApp and several other messenger apps can use end-to-end encryption for text messages and the like. Sometimes by default, sometimes as a configuration option. Signal is a popular option; I like that it's open-source so it's verifiable.

### 4. Use Keybase

One way of normalizing encryption, and making yourself easily and publicly reachable for private communications, is to join [Keybase.io](https://keybase.io). A simplified way to explain what Keybase does:

1. It creates trustworthy identification: I am who you think I am, so you can trust that you're communicating with me, not someone impersonating me.
2. It provides a trustworthy way to encrypt that communication: if you encrypt something meant for me, only I can decrypt it.
3. It ensures that you receive exactly what I communicate to you, without modification.

Keybase is very popular among engineers and techies, but we need more. The more people who join Keybase, the closer we are to critical mass and adoption thresholds; the closer we are to practical herd immunity.

### 5. Use HTTPS On Your Blog

If you have a personal blog or website, please use HTTPS (SSL) for it. There are several ways to do this. I use [Netlify](https://www.netlify.com/) to host this blog, so SSL is provided for me. You can also use [Let's Encrypt](https://letsencrypt.org/). Setting up SSL on a personal site used to be hard. It's now so easy that nobody should use plain-HTTP anymore.

Why? Again, encryption needs to become normalized and expected everywhere. Your website's users deserve it. Even if they're just reading a blog, having an HTTPS connection will prevent someone from snooping or modifying the information that is exchanged between their device and the blog server.

Google has a nice article about [why every site should use HTTPS](https://developers.google.com/web/fundamentals/security/encrypt-in-transit/why-https).

### 6. Don’t Use Fingerprint Unlock

Fingerprint readers on computers, phones, and tablets are useful. But it's risky to unlock the device itself with them. (They are still good for things like unlocking apps that you'd otherwise have to unlock with a long, hard-to-type password.)

The problem is that you can't change your fingerprint. You should never use something unchangeable for a password, especially on a device that has a lot of sensitive data and access to services. And there are validated cases of fingerprint-locked devices being unlocked by law enforcement, malicious people, etc.

The US government's attempted power-grab during the 2016 San Bernadino Shooter case, where they tried to use the fear surrounding the case to expand their powers of search and seizure, should give every thoughtful person serious pause.

Use a passcode, and configure your device to reset itself after 10 failed attempts.

### 7. Bonus: Set Up Automatic Backups

I've added this bonus item a bit later. There were some [ransomware
attacks](https://en.wikipedia.org/wiki/Ransomware) recently where a worm
infected computers, encrypted their data, and then forced people to pay to
decrypt their own files again. If they'd used a backup service, they'd have been
able to get their files without paying the ransom.

I use [Backblaze](https://www.backblaze.com/) and I'm happy with it.

The other thing we should all do is enable automatic updates for our devices.
This is the single most important security measure. A fix for the security flaw
that made the ransomware attack possible was released months before the
ransomware happened; those who were infected were users that didn't update their
software, and remained vulnerable.

### Conclusions

Please share this post with friends and family. And please post comments below and let me know what you think.

[Photo Credit](https://www.pexels.com/photo/blue-abstract-glass-balls-1341/)
