---
title: Review of Pro Nagios 2.0 and Nagios System and Network Monitoring
date: "2007-02-14"
url: /blog/2007/02/14/review-of-pro-nagios-20-and-nagios-system-and-network-monitoring/
categories:
  - Monitoring
  - Reviews
---
Last week I read two books on Nagios. I found one easier to use than the other.

> Note: [VividCortex](https://vividcortex.com/) is the startup I founded in 2012. It's the easiest way to monitor what
> your servers are doing in production. VividCortex offers [MySQL performance
> monitoring](https://vividcortex.com/monitoring/mysql/) and [PostgreSQL
> performance management](https://vividcortex.com/monitoring/postgres/) among many
> other features.

### The books

[![Cover of Nagios System and Network Monitoring](/media/2007/02/nagios_cov.jpg# fr pa1)]({{< amz 1593270704 >}})
[![Cover of Pro Nagios 2.0](/media/2007/02/pro-nagios.gif# fr pa1)]({{< amz 1590596099 >}})

[Nagios System and Network Monitoring (Wolfgang Barth, No Starch Press, 2006)]({{< amz 1593270704 >}}) is a delight. It explained Nagios briefly and clearly, showed me how to get it running, and continues to be a useful reference. [Pro Nagios 2.0 (James Turnbull, Apress, 2006)]({{< amz 1590596099 >}}) has a lot of useful information as well, but is harder to read and understand.

The differences are mainly in organization, style, and clarity; otherwise the books are identical in many ways. Both have chapters on the same topics. They cover exactly the same subject matter in the same level of detail, have the same target audiences, were written about the same time, are about the same size, and so on.

Barth's book lets me do a breadth-first search of the subject matter, and Turnbull's makes me do a depth-first search. Breadth-first is a better way to learn a topic like Nagios.

### Nagios System and Network Monitoring (Wolfgang Barth)

Barth's book succeeds through clarity, organization, detail, and ease of use. His first language is apparently German, so his English is not always elegant, but it is concise and communicates his knowledge of Nagios well.

The best thing about the book is the organization. The first part, "From Source Code to a Running Installation," is three compact chapters on everything you need to get Nagios working. The first chapter is about compiling, installing, and basic web interface configuration. The second is an overview of general Nagios configuration---the stuff you need to actually monitor things. The third is about checking your configuration and starting Nagios.

By page 55 I understood enough about Nagios to get started. When I finished the first three chapters, I had Nagios running and monitoring itself.

The second part is called "In More Detail," and it was very helpful while I configured Nagios to monitor other servers. It was a useful reference when I looked up specific topics, and easy to skim for important instructions and pitfalls. The good introductory sentences make it easy to decide whether I need to read a section, and the uninterrupted text makes it easy to skip if I don't. Large blocks of text make headings stand out, so there's less need to use the table of contents. References have page numbers.

There are few footnotes, and no interruptions in the text. When there are configuration examples, the book shows the whole configuration definition for context, but makes the relevant parts bold, so they're easy to see. There are lots of diagrams, which clearly show concepts that would require hundreds of words to explain. Captions are in the margins so they don't interrupt the text. The only gripe I have is the typeface, which in my subjective opinion is a little hard to speed-read.

### Pro Nagios 2.0 (James Turnbull)

James Turnbull's Pro Nagios 2.0 has valuable information, but it is harder to learn from it for a few reasons:

* It explains difficult concepts abstractly, using metaphors such as object-oriented programming terms, or passive voice.
* It's hard to skim because it's organized depth-first and interrupts itself with a lot of references, side topics, notes, and tips.
* The material isn't always organized in order of importance, and sometimes there's more verbosity than is helpful.

After I was familiar with Nagios I found it useful for reference a few times. If you know what you want to find, it's easy to navigate the book with the table of contents or the index. I remembered seeing something about how to organize configuration files in various ways, and I referred back to that since Barth's book didn't mention it. This discussion, on pages 32-35, helped me think about how to arrange configuration files into subdirectories with the `cfg_dir` directive.

Still, though, I found Barth's book more helpful for getting Nagios working. A good illustration is how the books explain "flapping," a Nagios feature to prevent a flood of notifications. Turnbull introduces this early, on page 47:

> So how does Nagios determine if a host or service is flapping? When you enable flap detection, Nagios keeps a record of the last 21 states of the host or service in an array. It then counts the number of times the states in the array have changed. This is calculated as a percentage. For example, with 21 states recorded we have a possible 20 state changes. For a normal-behaving host or service, it may be that the last recorded 21 states were OK. Hence, the percentage of states change is 0 percent. If, however, during the last 21 recorded states the host or service changed state 9 times, then the percentage of state change is 45 percent. But there is another added layer of complexity in this calculation. The states in this array are weighted---the newest state is considered 50 percent more important than the oldest state. This is because Nagios considers that the newer states are more indicative of the current behavior of the host or service than the older states.

Barth treats flapping as the minor feature it is, and doesn't mention it until page 219, where he sums it up succinctly:

> If a regular test shows that service or computer is changing its data continuously, this is called *flapping* in Nagios.

In the appendix on page 401 there's a nice diagram that illustrates flapping in case people need to know more.

Summary: I like Wolfgang Barth's [Nagios System and Network Monitoring]({{< amz 1593270704 >}}) better than James Turnbull's [Pro Nagios 2.0]({{< amz 1590596099 >}}).
