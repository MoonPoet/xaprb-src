---
title: The Response Time Stretch Factor
url: /blog/response-time-stretch-factor/
date: 2016-10-30T10:00:39-04:00
description: "Is there a simple stretch-factor equation that describes M/M/m queueing delay for m>2?"
credit: "https://unsplash.com/photos/cIcX_aO9LPo"
image: "/media/2016/10/unsplash-photos-cIcX_aO9LPo.jpg"
thumbnail: /media/2016/10/unsplash-photos-cIcX_aO9LPo.tn-500x500.jpg
classes:
- feature-figcaption-visible
- feature-fignum
- feature-figlink
categories:
- Math
- Scalability
---

Computer systems, and for that matter all types of systems that receive requests
and process them, have a response time {{< math >}}R{{< /math >}} that includes some time waiting in queue
if the server is busy when a request arrives. The wait time increases sharply as
the server utilization {{< math >}}\rho{{< /math >}} increases. For M/M/m queueing systems there is a simple equation that
describes this exactly, but for more complicated systems this equation is only
approximate. This has rattled around in my brain for a long time, and rather
than keeping my notes private I'm sharing them here.
<!--more-->

Figure 1 shows the familiar picture of how response time increases as utilization grows:

![Hockey-Stick Curve](/media/2016/10/hockey-stick.svg "The so-called hockey-stick curve illustrates that as the server's utilization increases, wait time increases sharply.")

### The Stretch Factor Heuristic and Exact Formula

The equation describing the curve above is derived as follows. When a request
arrives at the server, it will have to wait time {{< math >}}S{{< /math >}}, the service time, to be
completed. But if the server is busy, which happens with some probability, then
it will be delayed some additional wait time {{< math >}}W{{< /math >}} for the request in process,
and potentially for other requests are already waiting, before it enters
service. The total time is the residence time, {{< math >}}R = W + S{{< /math >}}.

The wait time {{< math >}}W{{< /math >}} is some fraction of the total residence time, which can be
at most 100%, and if this is denoted by {{< math >}}\rho{{< /math >}} then {{< math >}}W = \rho R{{< /math >}}.
Thus,

{{< math >}}
R = W + S = \rho R + S
{{< /math >}}

Which, when rearranged and divided by service time to make it a relative
"stretch factor," becomes

{{< math >}}
R = \frac{1}{1- \rho}
{{< /math >}}

None of this is original; I've basically cribbed this from Neil Gunther's book
*Analyzing Computer Systems Performance with Perl::PDQ*. Later in that same
book, Gunther shows the derivation of a related formula for the stretch factor
in a multiserver queue with {{< math >}}m{{< /math >}} servers,

{{< math >}}
R \approx \frac{1}{1-\rho^m}
{{< /math >}}

Where {{< math >}}\rho{{< /math >}} denotes server utilization. This heuristic approximation does
arise analytically, but is not exact when there are more than 2 servers. It
underestimates wait time when utilization is high, especially with large numbers
of servers (say, 64). The exact solution is given by

{{< math >}}
R = \frac{C(m, \rho) S}{m(1-\rho)} + S
{{< /math >}}

Where the first term is just {{< math >}}W{{< /math >}}, and the function {{< math >}}C(m,\rho){{< /math >}} is the
Erlang C function. If we put it all together and rearrange into "stretch factor" form, the Erlang equation for stretch factor is

{{< math >}}
R(m, \rho) = 1 + \frac{ \frac{(m \rho)^m}{m!} }{ (1-\rho) \sum_{n=0}^{m-1} \frac{(m \rho)^n}{n!} + \frac{(m \rho)^m}{m!} } \frac{1}{m(1-\rho)}
{{< /math >}}

Figure 2 shows the resulting response time curves for various numbers of servers, from 1 to 64. You can explore it on [this Desmos calculator](https://www.desmos.com/calculator/9dr7azq0ot).

![Erlang Curve for 1-64 Servers](/media/2016/10/erlang-1-64.png)

Now here's the part my brain has been trying to connect, almost idly in
shower-thought time, for a while. If intuition led from one direction to the
heuristic approximation {{< math >}}R=\frac{1}{1-\rho^m}{{< /math >}}, and an exact derivation leads to
a formula that in the single- and dual-server case is the same as the
heuristic, then what is the heuristic missing to extend to an exact multiserver
queueing system? Can it be extended, or is it just a coincidence that it's an
exact solution for {{< math >}}m=1, m=2{{< /math >}}?

A few trains of thought have sprung into my mind.

First, I observed that the Erlang C formula includes {{< math >}}m!{{< /math >}}, and it happens to be the
case that 1! = 1, and 2! = 2. A clue, or a distraction? What if I add a term
to the heuristic, multiplied by {{< math >}}m/m!{{< /math >}} or similar, which would just reduce
to the same thing for the single- and dual-server cases? What form would that
term take?

Secondly, what if I work backwards from the Erlang formula and see if it reduces
to a different form of the heuristic?

Thirdly, what if the heuristic's exactness for the base cases is just a
coincidence after all? In that case, perhaps a new, simpler approximation to the
Erlang formula is waiting to be invented. Approximations are highly useful to me
in tools such as spreadsheets and the like, or even in using intuition, which is
workable with the heuristic form. Approximations are easy to think about and a
lot easier to type and troubleshoot. They're also faster to compute, should
performance matter.

I'll take each of these cases in turn.

### A Missing Term

If the heuristic is exact for 1- and 2-server cases because of the coincidence
that the factorial function for these values is the value itself, then what is
the missing term? What shape might it have?

To gain some intuition about this, I wrote a simple [Desmos
calculator](https://www.desmos.com/calculator/qo1n4shf1f) to show
the *value* of the hypothetical "missing term" in the context of the heuristic's
value. In other words, the heuristic's *error function*.  Figure 3 is a graph of
that for several values of {{< math >}}m{{< /math >}}. Red is 1 server, green is 8, purple is 16, orange
is 64.

![Heuristic Error Function](/media/2016/10/heuristic-error.png)
_The heuristic function for queueing delay is inexact at values of m greater
than 1. This image shows the error for m values of 1, 8, 16, and 64._

Note that I showed utilization extending out beyond the value 1 because the
shape of the function is interesting, but that value is impossible---a server can
never be more than 100% utilized. What's interesting, to me anyway, is that the
error function looks kind of like the PDF of a Gamma distribution. I'll leave that thought
there.

I'm not sure what form a term including, say, {{< math >}}m/m!{{< /math >}} would take. This is
something I haven't explored a lot yet. *TODO*.

### Reducing Erlang

<!-- Wolfram Alpha input

1 + ((m p)^m/m!)/((1-p) Sum[(m p)^n/n!, {n, 0, m-1}] + (m p)^m/m!) * 1/(m(1-p)), m=1

-->

What does the Erlang formula reduce to in the {{< math >}}m=1{{< /math >}} case? The Erlang C
formula itself reduces to {{< math >}}\rho{{< /math >}}, and when
decorated with the additional stuff to get it into stretch-factor form, it
reduces to

{{< math >}}
R(1, \rho) = 1 + \frac{\rho}{1-\rho}
{{< /math >}}

Which is just a rearrangement of the heuristic function.
(Interestingly, Wolfram Alpha will simplify it to
include the Gamma function and list the heuristic as an approximation. Gamma
again, though Gamma function and Gamma distribution are different. The Gamma
function is closely related to the factorial function.)

In the {{< math >}}m=2{{< /math >}} case, if I'm doing my algebra right, the Erlang C function
simplifies to

{{< math >}}
C(2, \rho) = \frac{2\rho^2}{ (1-\rho) + (1-\rho)2\rho + 2\rho^2}
{{< /math >}}

Which further simplifies to {{< math >}}\frac{2\rho^2}{\rho+1}{{< /math >}}, which when
rewritten into stretch-factor form, becomes

{{< math >}}
R(2, \rho)=1+\frac{2\rho^2}{\rho+1} \frac{1}{2(1-\rho)}
{{< /math >}}

Which is exactly {{< math >}}\frac{1}{1-\rho^2}{{< /math >}}, the heuristic form.

At {{< math >}}m=3{{< /math >}} and above, the heuristic is only approximate. What does the Erlang
form reduce to for the first of those cases? Does it result in the missing term
that will extend to 4 and beyond too?[^followup]

### Approximations to Erlang, Based on the Heuristic

Approximations to complicated equations are often really useful. You use them
all the time, although you may not know it. For example, a computer uses
approximations to calculate functions such as sine, square root, and logarithm.
The field of numeric methods is dedicated to studying such algorithms and their
errors.

In 1977, Sakasegawa discovered an approximation to the length of a queue, which
is more accurate than the heuristic function, but wasn't derived analytically.
You can find the paper
[here](https://github.com/VividCortex/approx-queueing-theory). In a nutshell,
his method was to begin with a well-known queueing theory formula derived by
[Pollaczek and
Khinchine](https://en.wikipedia.org/wiki/Pollaczek%E2%80%93Khinchine_formula),
which is valid (exact) for M/G/1 systems, that is, single-server queueing
systems in some specific cases. Sakasegawa observed the error curve at various
parameters and essentially did a least-squares sum of errors regression to
arrive at an approximation for the queue length, which in the simplest types of
queueing systems reduces to:

{{< math >}}
L_q \approx \frac{ \rho^{\sqrt{2(m+1)}} }{ 1-\rho} 
{{< /math >}}

In "stretch factor" form, this becomes

{{< math >}}
R(m, \rho) \approx 1+\frac{\rho^{\sqrt{2(m+1)}}}{\rho m(1-\rho)}
{{< /math >}}

This is such an accurate approximation that it's more than good enough for
real-life applications, and I use it all the time. (It's hard to put Erlang's
formula into a spreadsheet, because it has iterative computations.)

Given the usefulness and simplicity of approximations, perhaps an approximation
to the stretch factor can be derived from the heuristic form
{{< math >}}1/(1-\rho^m){{< /math >}}. This idea appeals to me because it might lead to insights
about what's disappeared or simplified out of the exact Erlang formula in the
base case.

One possible way to do this is to approximate the error function of the
heuristic.  I already mentioned that it might be possible to do this with the
Gamma distribution's PDF. Finding an approximation to that, and then adding or
multiplying by it, might result in a usable approximation.

Another idea is a sigmoid such as the classic logistic function. In fact, if I
wanted to approximate the error in the range (0,1) this isn't too bad an
approximation for {{< math >}}m=16{{< /math >}}, for example:

{{< math >}}
\frac{.5}{1+e^{-10(x-1)}}
{{< /math >}}

Finally, instead of adding a term or multiplying the heuristic by a term,
perhaps it's the {{< math >}}\rho^m{{< /math >}} portion in the denominator that needs to be
tweaked. A little analysis led me to the following conclusions.

The error at {{< math >}}m>3{{< /math >}} could be explained by the exponent {{< math >}}m{{< /math >}} being too large. If so,
then the correct value for the exponent could be a function of {{< math >}}\rho{{< /math >}}, and
an adjustment to it would need to be of the form

{{< math >}}
A_{exp} = \frac{log\left( \frac{E(\rho)-1}{E(\rho)} \right)}{log(\rho)}
{{< /math >}}

Where {{< math >}}E(\rho){{< /math >}} is the Erlang formula for the stretch factor. I arrived at
this by solving the error function for {{< math >}}\rho{{< /math >}}. For convenience, this can be
divided by {{< math >}}m{{< /math >}} to normalize it relative to the number of servers. Figure
4 illustrates the shape of this adjustment term for 1, 4, 8, and 16 servers. You
can explore it with this [Desmos calculator](https://www.desmos.com/calculator/7ygut81via) too.

![Heuristic Error as Function of Utilization](/media/2016/10/heuristic-error-as-f-util.png)

One of the challenges with this is that due to the limitations of floating-point
math in computers, the heuristic function appears to have no error at low
utilization. I think it does, but it's just a small value. That's why the shape
of that curve has a discontinuity at low utilization.

An interesting observation: If you zoom out and remove the limits on the range
of values plotted, you get something that looks like a part of the Gamma
function. Is this a coincidence? Could the Gamma function be used as an
approximation to this error? Or is the missing term a Gamma function, which
would result in an exact solution? *TODO*.

Another way to nudge the heuristic to approximate the Erlang residence time
stretch factor would be to examine whether the base, {{< math >}}\rho{{< /math >}}, is too large
or too small. Following a similar train of thought as before and solving the
error function for the number of servers, I found that the error would need to be of the
form

{{< math >}}
A_{base} = \left( \frac{E(\rho)-1}{E(\rho)}\right)^{1/m}
{{< /math >}}

Normalizing this relative to {{< math >}}\rho{{< /math >}} by dividing, I obtained a function that has
similar discontinuities as before; see Figure 5. It looks
like it might be possible to approximate with something like a quadratic from 0
to 1, but if you zoom out further, it looks more like... wait for it... part of
the Gamma function. You can see this on
[Desmos](https://www.desmos.com/calculator/hsidkl4og8).

![Heuristic Error as Function of Servers](/media/2016/10/heuristic-error-as-f-servers.png)

I experimented with this in a different way, by trying to approximate
{{< math >}}A_{base}{{< /math >}} directly. I just guessed at its shape and came up with the
following, which isn't too far off for {{< math >}}2<m<5{{< /math >}}:

{{< math >}}
A_{base} \approx \rho - \frac{2}{15} \sqrt{m} (\rho-1)\rho
{{< /math >}}

Figure 6 shows this function's shape, compared with the actual {{< math >}}A_{base}{{< /math >}}.
You can explore these functions at this [Desmos graph](https://www.desmos.com/calculator/sgwrqdcnzk).

![Square Root Approximation To Heuristic](/media/2016/10/sqrt-approx-to-heuristic.png)

And Figure 7 ([Desmos](https://www.desmos.com/calculator/opa1sfpxfw)) shows what this
looks like when included as a term in the heuristic stretch factor.

![Heuristic Via Skewing Utilization](/media/2016/10/heuristic-via-skewing-utilization.png)

Red is Erlang, blue is my heuristic, and black dashed is Gunther's.
Don't be fooled; mine may look better, but if you examine high utilizations
you'll see it's much worse. Small errors in the approximation to the error
function make big differences in the result. (This is true if the error is
defined as a function of number of servers, too.)

### Conclusions

There's a lot of outright superstition in this blog post, but hopefully some of
the intuition I'm trying to develop comes through as well. Guessing at
approximations (and seeing Gamma-things everywhere, like shapes in the clouds)
is probably more time-wasting than productive, but I find that by playing with
things I learn a lot. There's something still unfinished in my mind, something
unsatisfactory about coming towards an exact solution from two directions,
finding two different forms, and finding that one of them runs aground at a
certain point, even though it's just a simplification of the other under some
circumstances. You might replace "even though" with "because" in the previous
sentence, and be satisfied, but as for me I feel there's still something to be
learned here. And potentially a useful result might come out of it, even if
it's only a fast approximation like Sakasegawa's.

Besides, I just enjoy exploring math and its shapes; this is a great form of
relaxation or stress relief for me when I want to concentrate on something so as
to put other things out of my mind. Hopefully there's a kindred soul out there
who finds this interesting too. If so, hello, and enjoy!

[^followup]: I wrote about this in a [followup post](/blog/erlang-stretch-factor-three-four/).
