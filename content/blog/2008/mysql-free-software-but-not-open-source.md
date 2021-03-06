---
title: "MySQL: Free Software but not Open Source"
date: "2008-05-14"
url: /blog/2008/05/14/mysql-free-software-but-not-open-source/
categories:
  - Databases
---
The title of [MySQL's website](http://www.mysql.com/) states that they are the world's most popular open-source database. This is false; MySQL is not an open-source database. That assertion is a fact, not an opinion.

MySQL is [Free Software](http://www.fsf.org/licensing/essays/free-sw.html), licensed under the GNU GPL. People frequently use the two phrases "Free Software" and "Open Source Software" as synonyms, but there are very large, very important differences.

### The difference between Free and Open Source

Open Source is much more of a development methodology than a philosophical standpoint. The first thing on the [Open Source Initiative's website](http://www.opensource.org/) is this introduction:

> Open source is a development method for software that harnesses the power of distributed peer review and transparency of process. The promise of open source is better quality, higher reliability, more flexibility, lower cost, and an end to predatory vendor lock-in.

In contrast, Free Software is not about development practices at all. You can develop Free Software any way you like; what makes it Free is the license. Free Software is about protection of rights and freedoms. It is a moral and ethical platform. The promise of Free Software is quite different from "better quality, higher reliability..." Free Software is not about quality or reliability.

So why is MySQL not Open Source? Simple. Sun/MySQL uses a closed development model. Nobody can get code in from the outside without accepting a [Contributor License Agreement (CLA)](http://forge.mysql.com/contribute/cla.php) which requires surrendering important rights, including ownership of the code. Sun/MySQL controls the code absolutely and maintains ownership of it. And even people who have signed the CLA report their patches stagnating---often for years---and still not being accepted into the source. This is not Open Source.

Open Source software is usually maintained, owned, and controlled by a decentralized network of peers. This is exactly the opposite of MySQL. You cannot get more opposite. The differences are often summarized as [the cathedral versus the bazaar](http://www.catb.org/~esr/writings/cathedral-bazaar/cathedral-bazaar/). I'm not sure this analogy always holds or is always useful and accurate, but it's a helpful piece of common vocabulary.

### Why this matters

This matters because both Freedom and an open development model are necessary to an empowered, enlightened, free society. Licensing isn't the only thing that matters: ownership matters, too. So does control.

[Google's patches to MySQL](http://code.google.com/p/google-mysql-tools/) are a good example of excellent code with many simple, highly useful features that have not been included into the official MySQL distribution. And there are no signs of that changing, as far as I can see.

I'm not the only one who notices this. Here's [another quote](http://blogs.the451group.com/opensource/2008/04/24/finding-the-right-balance-mysql%e2%80%99s-changing-development-model/):

> With all due respect to Marten, there is a significant difference between the captive open source development model for MySQL and the community open source development model for PostgreSQL.

If this interests you, perhaps you would like to join the discussion on the [oursql-sources](http://groups.google.com/group/oursql-sources) Google group.


