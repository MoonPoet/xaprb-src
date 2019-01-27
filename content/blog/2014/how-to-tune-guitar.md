---
title: "How to Tune A Guitar (Or Any Instrument)"
date: "2014-01-18"
description: "Once you hear it, you'll never listen to music the same way again."
url: /blog/2014/01/18/how-to-tune-guitar/
categories:
  - Music
credit: "https://unsplash.com/photos/59wBmsbP1lM"
image: "/media/2014/01/unsplash-photos-59wBmsbP1lM.jpg"
---
Do you know how to tune a guitar?
I mean, do you *really* know how to tune a guitar?
There's a secret to tuning an instrument.
Very few people seem to know it.
<!--more-->

Most people pick some notes, crank the tuners,
play some chords, and endlessly fidget back and forth until they either get
something that doesn't sound awful to their ears, or they give up. I can't
recall ever seeing a professional musician look like a tuning pro on stage,
either.

The secret is surprisingly simple, it isn't at all what you might expect, and it makes it easy and quick to tune an instrument *accurately* without guesswork.
However, even though it's simple and logical, it is difficult and subtle at first, and requires training your ear.
This is a neurological, physical, and mental process that takes some time and practice.
It does not require "perfect pitch," however.

In this blog post I'll explain how it works. There's a surprising amount of
depth to it, which appeals to the nerd in me. If you're looking for "the short
version," you won't find it here, because I find the math, physics, and theory
of tuning to be fascinating, and I want to share that and not just the quick
how-to.

If you practice and train yourself to hear in the correct way, with a little time you'll be able to tune a guitar by just striking the open strings, without using harmonics or frets. You'll be able to do this quickly, and the result will be a guitar that sounds truly active, alive, energetic, amazing---much better results than you'll get with a digital tuner. As a bonus, you'll impress all of your friends.

### My Personal History With Tuning

When I was a child my mother hired a piano tuner who practiced the "lost art" of
tuning entirely by ear. His name was [Lee Flory](http://www.genealogybuff.com/va/state/webbbs_config.pl/read/298). He was quite a character;
he'd tuned for famous concert pianists all over the world, toured with many of
them, and had endless stories to tell about his involvement with all sorts of
musicians in many genres, including bluegrass and country/western greats. My
mother loved the way the piano sounded when he tuned it. It sang. It was alive.
It was joyous.

For whatever reason, Lee took an interest in me, and not only tolerated but
encouraged my fascination with tuning. I didn't think about it at the time, but
I'm pretty sure he scheduled his visits differently to our house. I think he
allowed extra time so that he could spend an hour or more explaining everything
to me, playing notes, coaching me to hear subtleties.

And thus my love affair with the math, physics, and practice of tuning began.

### Beats

The first great secret is that tuning isn't about listening to the pitch of
notes. While tuning, you don't try to judge whether a note is too high or too
low. You listen to something called *beats* instead.

Beats are fluctuations in volume created by two notes that are almost the same
frequency.

When notes are not quite the same frequency, they'll reinforce each other when
the peaks occur together, and cancel each other out when the peaks are
misaligned. Here's a diagram of two sine waves of slightly different
frequencies, and the sum of the two (in red).

![Beats](/media/2014/01/beats.png)

Your ear will not hear two distinct notes if they're close together. It'll hear
the sum.

Notice how the summed wave (the red wave) fluctuates in magnitude.
To the human ear, this sounds like a note going "wow, wow, wow, wow." The frequency of this fluctuation is the difference between the frequencies of the notes.

Here's what that looks like when you take a mistuned instrument and analyze its FFT (Fast Fourier Transform). This is a G chord played on a harp. The upper G is not perfectly tuned and its amplitude fluctuates because of beats against the lower G.

![Beats FFT](/media/2014/01/fft-beats.png)

This is the foundation of all tuning by ear that isn't based on guesswork.

Before you go on, tune two strings close together on your guitar or other
instrument, and listen until you can hear it. Or, just fret one string so it
plays the same note as an open string, and strike them together. Bend the string
you've fretted, a little less, a little more. Listen until you hear the beats.

![Bending String](/media/2014/01/bending.jpg)

### The Math of Pitch

Musical notes have mathematical relationships to one another. The exact
relationships depend on the tuning. There are many tunings, but in this article
I'll focus on the tuning used for nearly all music in modern Western cultures:
the [12-tone equal temperament](http://en.wikipedia.org/wiki/Equal_temperament) tuning, said to be developed by Bach (this is
[contested](http://www.larips.com), though).

In this tuning, the octave is the fundamental interval of pitch. Notes double in
frequency as they rise an octave, and the ratio of frequencies between each
adjacent pair of notes is constant. Since there are twelve half-steps in an
octave, the frequency increase from one note to the next is the twelfth root of
2, or about 1.059463094359293.

Staying with Western music, where we define the A above middle C to have the
frequency of 440Hz, the scale from A220 to A440 is as follows:

|Note   | Frequency|
|-------| --------:|
|A220    |220.0000|
|A&sharp;|233.0819|
|B       |246.9417|
|C       |261.6256|
|C&sharp;|277.1826|
|D       |293.6648|
|D&sharp;|311.1270|
|E       |329.6276|
|F       |349.2282|
|F&sharp;|369.9944|
|G       |391.9954|
|G&sharp;|415.3047|
|A440    |440.0000|

We'll refer back to this later.

### The Math Of Intervals

If you've ever sung in harmony or played a chord, you've used intervals.
Intervals are named for the relative distance between two notes: a minor third,
a fifth, and so on.  These are a little confusing, because they sound like
fractions. They're not. A fifth doesn't mean that one note is five times the
frequency of another. A fifth means that if you start on the first note and
count upwards five notes on a major scale, you'll reach the second note in the
interval. Here's the C scale, with the intervals between the lowest C and the
given note listed at the right:

| Note | Name | Interval from C                   |
| ---- | ---- |:---------------                   |
| C    | Do   | Unison                            |
| D    | Re   | Major 2nd                         |
| E    | Mi   | Major 3rd                         |
| F    | Fa   | 4th (sometimes called Perfect 4th)|
| G    | So   | 5th (a.k.a. Perfect 5th)          |
| A    | La   | Major 6th                         |
| B    | Ti   | Major 7th                         |
| C    | Do   | Octave (8th)                      |

On the guitar, adjacent strings form intervals of fourths, except for the
interval between the G and B strings, which is a major third.

Some intervals sound "good," "pure," or "harmonious." A major chord, for example, is
composed of the root (first note), major third, fifth, and octave. The chord
sounds good because the intervals between the notes sound good. There's a
variety of intervals at play: between the third and fifth is a minor third,
between the fifth and octave is a fourth, and so on.

It turns out that the intervals that sound the most pure and harmonious are the ones whose
frequencies have the simplest relationships. In order of increasing complexity,
we have:

* Unison: two notes of the same frequency.
* Octave: the higher note is double the frequency.
* Fifth: the higher note is 3/2 the frequency.
* Fourth: the higher note is 4/3 the frequency.
* Third: the higher note is 5/4 the frequency.
* Further intervals (minor thirds, sixths, etc) have various relationships, but
  the pattern of N/(N-1) doesn't hold beyond the third.

These relationships are important for tuning, but beyond here it gets
significantly more complex. This is where things are most interesting!

### Overtones and Intervals

As a guitar player, you no doubt know about "harmonics," also called overtones.
You produce a harmonic by touching a string gently at a specific place (above
the 5th, 7th, or 12th fret, for example) and plucking the string. The note that
results sounds pure, and is higher pitched than the open string.

![Harmonics](/media/2014/01/harmonic.jpg)

Strings vibrate at a base frequency, but these harmonics (they're actually
partials, but I'll cover that later) are always present. In fact, much of the
sound energy of a stringed instrument is in overtones, not in the fundamental
frequency. When you "play a harmonic" you're really just damping out most of the
frequencies and putting more energy into simpler multiples of the fundamental
frequency.

Overtones are basically multiples of the fundamental frequency. The octave, for
example, is twice the frequency of the open string. Touching the string at the
12th fret is touching it at its halfway point. This essentially divides the
string into two strings of half the length. The frequency of the note is
inversely dependent on the string's length, so half the length makes a note
that's twice the frequency. The seventh fret is at 1/3 the length of the
string, so the note is three times the frequency; the 5th fret is 1/4 the
length, so you hear a note two octaves higher, and so on.

The overtones give the instrument its characteristic sound. How many of them
there are, their frequencies, their volumes, and their attack and decay
determines how the instrument sounds. There are usually many overtones, all
mixing together into what you usually think of as a single note.

Tuning depends on overtones, because you can tune an interval by listening to
the beats in its overtones.

Take a fifth, for example. Recall from before that the second note in the fifth
is 3/2 the frequency of the first. Let's use A220 as an example; a fifth up from
A220 is E330.  E330 times two is E660, and A220 times three is E660 also. So by
listening to the first overtone of the E, and the second overtone of the A, you
can "hear a fifth."

You're not really hearing the fifth, of course; you're really hearing the beats
in the overtones of the two notes.

### Practice Hearing Intervals

Practice hearing the overtones in intervals.  Pick up your guitar and de-tune the lowest E string down
to a D. Practice hearing its overtones. Pluck a harmonic at the 12th string and
strike your open D string; listen to the beats between the notes. Now play both
strings open, with no harmonics, at the same time. Listen again to the
overtones, and practice hearing the beats between them. De-tune slightly if you
need to, to make the "wow, wow, wow, wow" effect easier to notice.

Take a break; don't overdo it. Your ear will probably fatigue quickly and you'll
be unable to hear the overtones, especially as you experiment more with complex
intervals. In the beginning, you should not be surprised if you can focus on
these overtones for only a few minutes before it gets hard to pick them out and
things sound jumbled together. Rest for a few hours. I would not suggest doing
this more than a couple of times a day initially.

The fatigue is real, by the way. As I mentioned previously, being able to
hear beats and ignore the richness of the sound to pick out weak overtones is
a complex physical, mental, and neurological skill---and there
are probably other factors too. I'd be interested in seeing brain scans of an
accomplished tuner at work. Lee Flory was not young, and he told me that his
audiologist said his hearing had not decayed with age. This surprised the
doctor, because he spent his life listening to loud sounds. Lee attributed this
to daily training of his hearing, and told me that the ear is like any other
part of the body: it can be exercised. According to Lee, if he took even a
single day's break from tuning, his ear lost some of its acuity.

Back to the topic: When you're ready, pluck a harmonic on the lowest D string
(formerly the E string) at the 7th fret, and the A string at the 12th fret, and
listen to the beats between them. Again, practice hearing the same overtones
(ignoring the base notes) when you strike both open strings at the same time.

When you've heard this, you can move on to a 4th. You can strike the harmonic at
the 5th fret of the A string and th 7th fret of the D string, for example, and
listen to the beats; then practice hearing the same frequencies by just
strumming those two open strings together.

![Soundhole](/media/2014/01/4542297929_49286da35a.jpg)

As you do all of these exercises, try your best to ignore pitch (highness or lowness)
of the notes, and listen only to the fluctuations in volume. In reality you'll be conscious of both pitch and beats, but this practice will help develop your tuning ear.

### Imperfect Intervals and Counting Beats

You may have noticed that intervals in the equal-tempered 12-tone tuning don't
have exactly the simple relationships I listed before. If you look at the table
of frequencies above, for example, you'll see that in steps of the 12th root of
2, E has a frequency of 329.6276Hz, not 330Hz.

Oh no! Was it all a lie? Without these relationships, does tuning fall apart?

![Nautilus](/media/2014/01/8087829115_b2da0e4435.jpg)

Not really. In the equal-tempered tuning, in fact, **there is only one perfect
interval: the octave**. All other intervals are imperfect, or "tempered."

* The 5th is a little "narrow"---the higher note in the interval is slightly
  flat
* The 4th is a little "wide"---the higher note is sharp
* The major 3rd is even wider than the 4th

Other intervals are wide or narrow, just depending on where their frequencies fall
on the equal-tempered tuning. (In practice, you will rarely or never tune
intervals other than octaves, 5ths, 4ths, and 3rds.)

As the pitch of the interval rises, so does the frequency of the beats. The 4th
between A110 and the D above it will beat half as fast as the 4th an octave
higher.

What this means is that not only do you need to hear beats, but you need to
*count* them. Counting is done in beats per second. It sounds insanely hard at
first (how the heck can you count 7.75 beats a second!?) but it will
come with practice.

You will need to know how many beats wide or narrow a given interval will be.
You can calculate it easily enough, and I'll show examples later.

After a while of tuning a given instrument, you'll just memorize how many beats
to count for specific intervals, because as you'll see, there's a system for
tuning any instrument. You generally don't need to have every arbitrary
interval memorized. You will use only a handful of intervals and you'll learn
their beats.

### Why Are Intervals Imperfect?

There's probably some fascinating number theory behind the relationships amongst
intervals, but what I find remarkable is that there are any octave-based scales
that have close-to-perfect intervals at all. It seems to me that it's an
interesting coincidence and nothing more. Look at it this way:

- Octave-based scales are based on powers of two
- Intervals are based on powers of something other than two
- There are subdivisions of the octave-based scales that coincide nearly, but
  not exactly, with the non-power-of-two intervals[^53tet]
- Isn't that cool? How unlikely is that?

In any case, powers of two are easy to compute: 2, 4, 8, 16, 32, 64, 128, 256.
Those are the multiples of frequencies. How do those multiples compare versus
the next-simplest interval, the fifth? A fifth is a 3:2 relationship, and there
are 12 fifths---the "cycle of fifths"---in the evenly tempered scale. If you
keep increasing by fifths you'll end up at the same note after 12 iterations.

That means the frequency is {{< math >}}1.5^{12}{{< /math >}}; what is that multiple?

{{< math >}}
1.5^{12} = 129.74633789
{{< /math >}}

That's pretty close to 128, but slightly "wide," meaning if you tune perfect
fifths 12 times in a row you'll end up overshooting, with a frequency that's
1.36% too high. There are 7 semitones in a 5th, so what's the relationship between 3:2 and {{< math >}}\sqrt[12]{2}{{< /math >}} to the 7th power?

{{< math >}}
\begin{array}{c}
\frac{3}{2} = 1.5 \\
2^{\frac{7}{12}} = 1.498307077
\end{array}
{{< /math >}}


A single (perfect) fifth is 0.1129% too high in frequency. Repeat that 12 times,
and that cycle of perfect fifths will end 1.36% too high in frequency.

What about fourths? They're just the complement of fifths. Thirds? A perfect
major third is a 5:4 frequency ratio. Unlike fifths, the cycle of thirds returns
to the same note after only three steps (for example, C - E - G# - C), so the
number of steps to multiply is only 3; how far off from 2 is the result?

{{< math >}}
\frac{5}{4}^3 = 1.953125
{{< /math >}}

It's close to 2, but not exactly; it's only 97.65625% of a perfect octave.
What's the relationship between a perfect major third and 4 semitones in the evenly tempered scale?

{{< math >}}
\begin{array}{c}
\frac{5}{4} = 1.25 \\
2^{\frac{4}{12}} = 1.25992105
\end{array}
{{< /math >}}

A perfect major third is too narrow; it's only 99.2% of the
frequency it needs to be to align with the evenly tempered scale. If you cube
that to get an octave, the result is 97.65625% again.

Hopefully that explains how fifths and thirds are close to, but not exactly,
perfectly coincident with the frequencies. Again, I think a mathematician who
likes to think in base 2, base 1/12, base 1.5 and base 1.25 would have fun
with this. Or maybe I'm just overthinking it.

### Tuning The Guitar

With all that theory behind us, we can move on to a tuning system for the guitar.

Let's list the strings, their frequencies, and some of their overtones.

String | Freq | Overtone 2 | Overtone 3 | Overtone 4 | Overtone 5
------ | ------: | ------: | ------: | -------: | -------:
E | 82.41 | 164.81 | 247.22 | 329.63 | 412.03
A | 110.00 | 220.00 | 330.00 | 440.00 | 550.00
D | 146.83 | 293.66 | 440.50 | 587.33 | 734.16
G | 196.00 | 392.00 | 587.99 | 783.99 | 979.99
B | 246.94 | 493.88 | 740.82 | 987.77 | 1234.71
E | 329.63 | 659.26 | 988.88 | 1318.51 | 1648.14

Because the open strings of the guitar form 4ths and one 3rd, you can tune the guitar's strings open, without any frets, using just those intervals. There's also a double octave from the lowest E to the highest E, but you don't strictly need to use that except as a check after you're done.

For convenience, here's the same table with only the overtones we'll use.

| String | Freq   | Overtone 2 | Overtone 3 | Overtone 4 | Overtone 5
| ------ | -----: | ---------: | ---------: | ---------: | ---------:
| E      | 82.41  |            | 247.22     | 329.63     |
| A      | 110.00 |            | 330.00     | 440.00     |
| D      | 146.83 |            | 440.50     | 587.33     | 734.16
| G      | 196.00 |            | 587.99     |            | 979.99
| B      | 246.94 |            | 740.82     | 987.77     |
| E      | 329.63 |            | 988.88     |            |

#### Tuning the A String

The first thing to do is tune one of the strings to a reference pitch. After that, you'll tune all of the other strings relative to this first one. On the guitar, the most convenient reference pitch is A440, because the open A string is two octaves below at 110Hz.

You'll need a good-quality [A440 tuning fork]({{< amz B001T21J80 >}}). I prefer a Wittner for guitar tuning; it's a good-quality German brand that is compact, so it fits in your guitar case's pocket, and has a small notch behind the ball at the end of the stem, so it's easy to hold in your teeth if you prefer that.

![Wittner A440 Tuning Fork](/media/2014/01/wittner-tuning-fork.jpg)

Strike the tuning fork lightly with your fingernail, or tap it gently against your knee. Don't bang it against anything hard or squeeze the tines, or you might damage it and change its pitch. You can hold the tuning fork against the guitar's soundboard, or let it rest lightly between your teeth so the sound travels through your skull to your ears, and strike the open A string. Tune the A string until the beats disappear completely. Now put away the tuning fork and continue. You won't adjust the A string after this.

If you don't have a tuning fork, you can use any other reference pitch, such as the A on a piano, or a digitally produced A440.

#### Tuning the Low E String

Strike the open low E and A strings together, and tune the E string. Listen to the beating of the overtones at the frequency of the E two octaves higher. If you have trouble hearing it, silence all the strings, then pluck a harmonic on the E string at the 5th fret. Keep that tone in your memory and then sound the two strings together. It's important to play the notes *together, open, simultaneously* so that you don't get confused by pitches. Remember, you're trying to ignore pitch completely, and get your ear to isolate the sound of the overtone, ignoring everything but its beating.

When correctly tuned, the A string's overtone will be at 330Hz and the E string's will be at 329.63Hz, so the interval is **1/3 of a beat per second wide**. That is, you can tune the E string until the beats disappear, and then **flatten the low E string very slightly** until you hear one beat every three seconds. The result will be a very slow "wwwoooooowww, wwwwoooooowww" beating.

#### Tuning the D String

Now that the low E and A strings are tuned, strike the open A and D strings together. You're listening for beats in the high A440 overtone. The A string's overtone will be at 440Hz, and the D string's will be at 440.50Hz, so the interval should be **1/2 beat wide.** Tune the D string until the beats disappear, then **sharpen the D string slightly** until you hear one beat every 2 seconds.

#### Tuning the G String

Continue by striking the open D and G strings, and listen for the high D overtone's beating. Again, if you have trouble "finding the note" with your ear, silence everything and strike the D string's harmonic at the 5th fret. You're listening for a high D overtone, two octaves higher than the open D string. The overtones will be at 587.33Hz and 587.99Hz, so the interval needs to be **2/3 of a beat wide.** Counting two beats every three seconds is a little harder than the other intervals we've used thus far, but it will come with practice. In the beginning, feel free to just give it your best wild guess. As we'll discuss a little later, striving for perfection is futile anyway.

#### Tuning the B String

Strike the open G and B strings. The interval between them is a major 3rd, so this one is trickier to hear. A major 3rd's frequency ratio is approximately 5/4ths, so you're listening for the 5th overtone of the G string and the 4th overtone of the B string. Because these are higher overtones, they're not as loud as the ones you've been using thus far, and it's harder to hear.

To isolate the note you need to hear, mute all the strings and then pluck a harmonic on the B string at the 5th fret. The overtone is a B two octaves higher. Search around on the G string near the 4th fret and you'll find the same note.

The overtones are 979.99Hz and 987.77Hz, so the interval is **seven and three-quarters beats wide.** This will be tough to count at first, so just aim for something about 8 beats and call it good enough. With time you'll be able to actually count this, but it will be very helpful at first to use some rules of thumb. For example, you can compare the rhythm of the beating to the syllables in the word "mississippi" spoken twice per second, which is probably about as fast as you can say it back-to-back without pause.

Tune the B string until the beats disappear, then **sharpen it 8 beats, more or less**.

#### Tuning the High E String

You're almost done! Strike the open B and E strings, and listen for the same overtone you just used to tune the G and B strings: a high B. The frequencies are 987.77Hz and 988.88Hz, so the interval is **1.1 beats wide.** Sharpen the E string until the high B note beats a little more than once a second.

#### Testing The Results

Run a couple of quick checks to see whether you got things right. First, check your high E against your low E. They are two octaves apart, so listen to the beating of the high E string. It should be very slow or nonexistent. If there's a little beating, don't worry about it. You'll get better with time, and it'll never be perfect anyway, for reasons we'll discuss later.

You can also check the low E against the open B string, and listen for beating at the B note, which is the 3rd overtone of the E string. The B should be very slightly narrow (flat)---theoretically, you should hear about 1/4th of a beat.

Also theoretically, you could tune the high B and E strings against the low open E using the same overtones. However, due to imperfections in strings and the slowness of the beating, this is usually much harder to do. As a result, you'll end up with high strings that don't sound good together. A general rule of thumb is that it's easier to hear out-of-tune-ness in notes that are a) closer in pitch and b) higher pitched, so you should generally "tune locally" rather than "tuning at a distance." If you don't get the high strings tuned well together, you'll get really ugly-sounding intervals such as the following:

* the 5th between your open G string and the D on the 3rd fret of the B string
* the 5th between the A on the second fret of the G string and the open high E string
* the octave between your open G string and the G on the 3rd fret of the high E string
* the octave between your open D string and the D on the 3rd fret of the B string
* the 5th between the E on the second fret of the D string and the open B string

If those intervals are messed up, things will sound badly discordant. Remember that the 5ths *should* be slightly narrow, not perfect. But the octaves should be perfect, or very nearly so.

Play a few quick chords to test the results, too. An E Major, G major, and B minor are favorites of mine. They have combinations of open and fretted notes that helps make it obvious if anything's a little skewed.

![Chord](/media/2014/01/31859506_7e481da3e7.jpg)

#### You're Done!

With time, you'll be able to run through this tuning system very quickly, and you'll end up with a guitar that sounds joyously alive in all keys, no matter what chord you play. No more fussing with "this chord sounds good, but that one is awful!" No more trial and error. No more guessing which string is out of tune when something sounds bad. No more game of "tuning whack-a-mole."

To summarize:

* Tune the A string with a tuning fork.
* Tune the low E string 1/3 of a beat wide relative to the A.
* Tune the D string 1/2 of a beat wide relative to the A.
* Tune the G string 2/3 of a beat wide relative to the D.
* Tune the B string 7 3/4 beats wide relative to the G.
* Tune the high E string just over 1 beat wide relative to the B.
* Cross-check the low and high E strings, and play a few chords.

This can be done in a few seconds per string.

If you compare your results to what you'll get from a digital tuner, you'll find
that with practice, your ear is *much* better. It's very hard to tune within a
Hz or so with a digital tuner, in part because the indicators are hard to read.
What you'll get with a digital tuner is most strings are pretty close to their
correct frequency. This is a lot better than the ad-hoc tuning by
trial-and-error you might have been accustomed to doing, because that method
results in some intervals being tuned to sound good but others badly discordant.
The usual scenario I see is someone's B string is in good shape, but the G and
the E are out of tune. The guitar player then tunes the B string relative to the
out-of-tune E and G, and then everything sounds awful. This is because the
guitarist had no frame of reference for understanding which strings were out of
tune in which directions.

But when you tune by listening to beats, and get good at it, you'll be able to
tune strings to within a fraction of a cycle per second of what they should be.
Your results will absolutely be better than a digital tuner.

I don't mean to dismiss digital tuners. They're very useful when you're in a
noisy place, or when you're tuning things like electric guitars, which have
distortion that buries overtones in noise. But if you learn to tune by
hearing beats, you'll be the better for it, and you'll never regret it, I
promise. By the way, if you have an Android smartphone, I've had pretty good
results with the gStrings app.

![Tune-o-phone](/media/2014/01/tune-o-phone.jpg)

#### Advanced Magic

If you do the math on higher overtones, you'll notice a few other interesting intervals between open strings. As your ear sharpens, you'll be able to hear these, and use them to cross-check various combinations of strings. This can be useful because as you get better at hearing overtones and beats, you'll probably start to become a bit of a perfectionist, and you won't be happy unless particular intervals (such as the 5ths and octaves mentioned just above) sound good. Here they are:

* **Open A String to Open B String.** The 9th overtone of the open A string is a high B note at 990Hz, and the 4th overtone of the open B is a high B at 987.77HZ. If you can hear this high note, you should hear it beating just over twice per second. The interval between the A and B strings is a minor 7th, which should be slightly narrow. Thus, if you tune the B until the beating disappears, you should then flatten it two beats.
* **Open D String to Open E String.** This is also a minor 7th interval. You're listening for a very high E note, at 1321.5Hz on the D string, and 1318.5 on the E string, which is 3 beats narrow.
* **Open D String to Open B String.** The 5th overtone of the D string is similar to the 3rd overtone of the B string. This interval is about 6 and 2/3 beats wide. This is a bit hard to hear at first, but you're listening for a high F&sharp;.

### Systems for Tuning Arbitrary Instruments

The guitar is a fairly simple instrument to tune, because it has only 6 strings,
and 4ths are an easy interval to tune. The inclusion of a major 3rd makes it a
little harder, but not much.

It is more complicated, and requires more practice, to tune instruments with
more strings. The most general approach is to choose an octave, and to tune all the
notes within it. Then you extend the tuning up and down the range as needed.
For example, to tune the piano you first tune all the notes within a C-to-C
octave (piano tuners typically use a large middle-C tuning fork).

Once you have your first octave tuned, the rest is simple. Each
note is tuned to the octave below it or above it. But getting that first octave
is a bit tricky.

There are two very common systems of tuning: fourths and fifths, and thirds and
fifths. As you may know, the cycle of fifths will cycle you through every note
in the 12-note scale. You can cycle through the notes in various ways, however.

Fun tangent: this [old book from 1821
explains](https://play.google.com/store/books/details?id=jotFAQAAMAAJ), in a
roundabout way, the system of fifths and thirds as well as a system based on
advancing by major and minor thirds.

![tuning](/media/2014/01/old-tuning-book.jpg)

The system of thirds and fifths proceeds from middle C up a fifth to G, down a
third to E-flat, up a fifth to B-flat, and so on.  The system of fourths and
fifths goes from C up a fifth to G, down a fourth to D, and so on.

All you need to do is calculate the beats in the various intervals and be able
to count them. The piano tuners I've known prefer thirds and fifths because if
there are imperfections in the thirds, especially if they're not as wide as they
should be, it sounds truly awful. Lively-sounding thirds are important; fourths
and fifths are nearly perfect, and should sound quite pure, but a third is a
complex interval with a lot of different things going on. Fourths and fifths
also beat slowly enough that it's easy to misjudge and get an error that
accumulates as you go through the 12 notes. Checking the tuning with thirds
helps avoid this.

### Tuning a Hammered Dulcimer

I've built several many-stringed instruments, including a couple of hammered
dulcimers. My first was a home woodworking project with some two-by-four lumber,
based on plans from a book by Phillip Mason I found at the library and decided
to pick up on a whim. For a homebuilt instrument, it sounded great, and building
an instrument like this is something I highly recommend.

Later I designed and built a second one, pictured below. Pardon the dust!

![Dulcimer](/media/2014/01/dulcimer.jpg)

Tuning this dulcimer takes a while. I start with an octave on the bass course.
Dulcimers can have many different tunings; this
one follows the typical tuning of traditional dulcimers, which is essentially a
set of changing keys that cycle backwards by fifths as you climb the scale.
Starting at G, for example, you have a C major scale up to the next G, centered
around middle C. But the next B is B-flat instead of B-natural, so there's an F
major scale overlapping with the top of the C major, and so on:

> G, A, B, C, D, E, F, G, A, B&flat;, C, D...

It's easy to tune this instrument in fourths and fifths because of the way its
scales are laid out. If I do that, however, I find that I have ugly-sounding
thirds more often than not. So I'll tune by combinations of fifths, fourths, and
thirds:

```
G A B C D E F G A B♭ C D...
^-------------^                 (up an octave)
      ^-------^                 (down a fifth)
      ^---^                     (up a third)
  ^-------^                     (down a fifth)
```

And so on. In addition to using thirds where I can (G-B, C-E), I'll check my
fifths and fourths against each other. If you do the math, you'll notice that
the fourth from G to C is exactly as wide as the fifth from C to G again is
narrow. (This is a general rule of fourths and fifths. Another rule is that the
fourth at the top of the octave beats twice as fast as the fifth at the bottom;
so G-D beats half as fast as D-G.)

When I'm done with this reference octave, I'll extend it up the entire bass
course, adjusting for B-flat by tuning it relative to F, and checking any new
thirds that I encounter as I climb the scale. And then I'll extend that over to
the right-hand side of the treble course. I do not use the left-hand (high) side
of the treble course to tune, because its notes are inaccurate depending on the
placement of the bridge.

With a little math (spreadsheets are nice), and some practice, you can find a
quick way to tune almost any instrument, along with cross-checks to help prevent
skew as you go.

### Tuning a Harp

Another instrument I built (this time with my grandfather) is a simplified
replica of the [Scottish wire-strung Queen Mary harp](http://en.wikipedia.org/wiki/Queen_Mary_Harp). This historical
instrument might have been designed for some golden and silver strings,
according to [Ann Heyman's research](http://www.annheymann.com/gold.htm). In any case, it is quite difficult to
tune with bronze or brass strings.  It is "low-headed" and would need a much
higher head to work well with bronze or brass.

![Harp](/media/2014/01/harp.jpg)

Tuning this harp is quite similar to the hammered dulcimer, although it is in a
single key, so there's no need to adjust to key changes as you climb the scale.
A simple reference octave is all you need, and then it's just a matter of
extending it. I have never tuned a concert harp, but I imagine it's more
involved.

Tangent: I first discovered the wire-strung harp in 1988, when I heard Patrick
Ball's [first volume]({{< amz B0000007SD >}}) of [Turlough O'Carolan's music](http://en.wikipedia.org/wiki/Turlough_O'Carolan). If you have not
listened to these recordings, do yourself a favor and at least preview them on
Amazon. All these years later, I still listen to Patrick Ball's music often.
His newest recording, [The Wood of Morois]({{< amz B004FA20T0 >}}), is just stunning.
I corresponded with Patrick while planning to build my harp, and he put me in
touch with master harpmaker [Jay Witcher](http://www.witcherharps.com/), and his own role model, Ann
Heymann, who was responsible for reinventing the lost techniques of playing
wire-strung harps. Her recordings are a little hard to find in music stores, but
are worth it. You can buy them from her websites
http://www.clairseach.com/, http://www.annheymann.com/, and
http://www.harpofgold.net/. If you're interested in learning to play wire-strung
harp, her book is one of the main written sources.
There are a variety of magazines covering the harp renaissance in the latter
part of the 20th century, and they contain much valuable additional material.

### Systems For Tuning Diatonic Instruments

So how do you tune the harp, in practice? Here's how I do it for a harp in C:

- Use an A440 tuning fork to tune the A3 string. Its frequency is 220Hz but it's
  easy to tune by listening to its first partial.
- Down a 5th to D; 1/2 beat narrow.
- Return to the A440.
- Down a 3rd to F; 7 beats wide.
- Up a 5th to C; .6 beat narrow.
- Down an octave to the lower C; perfect.
- Up a 5th to G; .4 beat narrow.
- Up a 3rd to B; 7.75 beats wide.
- Down a 5th to E; .55 beat narrow.
- Cross-check between the E and lower C; both already tuned. Should be just over
  5 beats wide.
- Cross-check all the 4ths and ensure they are neither lifeless nor beating
  rapidly. In particular, the interval D-G is quite important, and there are 5
  steps in the tuning sequence between these notes, so it's a pretty sensitive
  indicator of whether you've been getting the beats right.
- Expand the octave to the rest of the instrument by octaves. At each note, cross-check
  against any already-tuned notes and ensure 5ths, 4ths, and 3rds are not
  drifting and becoming cat-fights.

A diagram might help. The arrows indicate which note to tune from the current
note and in what order. The 'n' and 'w' notation indicates how narrow or wide
the intervals should be.

![Tuning the Diatonic C Scale](/media/2014/01/tuning-c-scale.png)

If your diatonic instrument is tuned in the key of G, you can use this sequence
instead:

![Tuning the Diatonic G Scale](/media/2014/01/tuning-g-scale.png)

Note that in both cases, you are essentially tuning successive major and minor
chords, although when you stay within the confines of a single octave you
sometimes only have an inversion tuned unless you include a note outside the
octave. Of course, you can include more notes, but if you're having a hard time
getting things to sound good together then you probably have some imprecision
(trouble counting beats?) and adding more notes might make it harder for you to
close the loop, so to speak.

### Beyond Tuning Theory: The Real World

Although simple math can compute the theoretically correct frequencies of notes
and their overtones, and thus the beats of various intervals, in practice a
number of factors make things more complicated and interesting. In fact, the
math up until now has been of the "frictionless plane" variety. For those who
are interested, I'll dig deeper into these nuances.

The nuances and deviations from perfect theory are the main reasons why a) it's
impossible to tune anything perfectly and b) an instrument that's tuned
skillfully by ear sounds glorious, whereas an instrument tuned digitally can
sound lifeless.

(In many cases it's really convenient to use a digital tuner to bring things
pretty close, then go through one of the sequences explained above to
cross-check. This can save a lot of time when an instrument is very out-of-tune
and shifts a lot during tuning, in which case it'll be out again when you're
done. If you need to make multiple passes to bring things close to tune, digital
tuners are great time savers.)

#### Harmonics, Overtones, and Partials

I was careful to use the term "overtone" most of the time previously. In theory,
a string vibrates at its fundamental frequency, and then it has harmonic overtones at
twice that frequency, three times, and so on.

However, that's not what happens in practice, because theory only applies to
strings that have no stiffness. The stiffness of the string causes its overtones
to vibrate at slightly higher frequencies than you'd expect. For this reason,
these overtones aren't true harmonics. This is called inharmonicity, and
inharmonic overtones are called *partials* to distinguish them from the purely
harmonic overtones of an instrument like a flute, which doesn't exhibit the same
effect.

You might think that this inharmonicity is a bad thing, but it's not.
Common tones with a great deal of inharmonicity are bells (which often have so much inharmonicity that you can hear the pitches of their partials are too high) and various types of chimes. I keep a little "zenergy" chime near my morning meditation table because its bright tones focus my attention. I haven't analyzed its spectrum, but because it is made with thick bars of aluminum, I'm willing to bet that it has partials that are wildly inharmonic. Yet it sounds pure and clear.

[![Woodstock Percussion ZENERGY3 Zenergy Chime](/media/2014/01/zenergy.jpg)]({{< amz B0000775FZ >}})

Much of the richness and liveliness of a string's sound is precisely because of the
"stretched" overtones. Many people compare Patrick Ball's brass-strung wire harp to the sound of bells, and say it's "pure." It may sound pure, but pure-sounding is not simple-sounding. Its tones are complex and highly inharmonic, which is why it sounds like a bell.

In fact, if you digitally alter a piano's overtones to correct the stretching, you get something that sounds like an organ, not a piano. This is one of the reasons that pianos tuned with digital tuners often sound like something scraped from the bottom of a pond.

Some digital tuners claim to compensate for inharmonicity, but in reality each instrument and its strings are unique and will be inharmonic in different ways.

Some practical consequences when tuning by listening to beats:

* Don't listen to higher partials while tuning. When tuning an octave, for example, you should ignore the beating of partials 2 octaves up. This is actually quite difficult to do and requires a well-developed ear. The reason is that higher partials will beat even when the octave is perfect, and they beat more rapidly and more obviously than the octave. Tuning a perfect octave requires the ability to hear very subtle, very gradual beats while blocking out distractions. This is also why I said not to worry if your low E string and high E string beat slightly. When tuned as well as possible, there will probably be a little bit of beating.
* You might need to ignore higher partials in other intervals as well.
* You might need to adjust your tuning for stretching caused by inharmonicity. In practice, for example, most guitars need to be tuned to slightly faster beats than you'd expect from pure theory.
* Cross-checking your results with more complex intervals (especially thirds) can help balance the stretching better, and make a more pleasing-sounding tuning.
* You might find that when using the "advanced tricks" I mentioned for the guitar, the open intervals such as minor 7ths will beat at different rates than you'd predict mathematically. However, once you are comfortable tuning your guitar so it sounds good, you'll learn how fast those intervals should beat and it'll be a great cross-reference for you.

#### Sympathetic and False Beats

It's often very helpful to mute strings while you're tuning other strings. The reason is that the strings you're tuning will set up sympathetic vibrations in other strings that have similar overtones, and this can distract you.

When tuning the guitar, this generally isn't much of a problem. However, be careful that when you tune the low E and A strings you don't get distracted by vibrations from the high E string.

When tuning other instruments such as a hammered dulcimer or harp, [small felt or rubber wedges]({{< amz B006RE74WA >}}) (with wire handles if possible) are invaluable. If you don't have these, you can use small loops of cloth.

In addition to distraction from sympathetic vibrations, strings can beat alone, when no other note is sounding. This is called a false beat. It's usually caused by a flaw in the string itself, such as an imperfection in the wire or a spot of rust. This is a more difficult problem, because you can't just make it go away. Instead, you will often have to nudge the tuning around a little here, a little there, to make it sound the best you can overall, given that there will be spurious beats no matter what. False beats will challenge your ear greatly, too.

In a guitar, false beats might signal that it's time for a new set of strings. In a piano or other instrument, strings can be expensive to replace, and new strings take a while to settle in, so it's often better to just leave it alone.

#### Imperfect Frets, Strings, Bridges and Nuts

I've never played a guitar with perfect frets. The reality is that every note you fret will be slightly out of tune, and one goal of tuning is to avoid any particular combination of bad intervals that sounds particularly horrible.

This is why it's helpful to play at least a few chords after tuning. If you tune a particular instrument often you'll learn the slight adjustments needed to make things sound as good as possible. On my main guitar, for example, the B string needs to be slightly sharp so that a D sounds better.

It's not only the frets, but the nut (the zeroth fret) and the bridge (under the right hand) that matter. Sometimes the neck needs to be adjusted as well. A competent guitar repairman should be able to adjust the action if needed.

Finally, the weight and manufacture of the strings makes a difference. My main guitar and its frets and bridge sound better and more accurate with medium-weight Martin bronze-wound strings than other strings I've tried. As your ear improves, you'll notice subtleties like this.

![Fretting](/media/2014/01/2516054483_876aa398c5.jpg)

#### New Strings

New strings (or wires) will take some time to stretch and settle in so they stay in tune. You can shorten this time by playing vigorously and stretching the strings, bending them gently. Be careful, however, not to be rough with the strings. If you kink them or strain them past their elastic point, you'll end up with strings that have false beats, exaggerated inharmonicity, or different densities along some lengths of the string, which will make it seem like your frets are wrong in strange ways.

#### The Instrument Flexes and Changes

If an instrument is especially out of tune, the first strings you tune will become slightly out of tune as you change the tension on the rest of the instrument. The best remedy I can offer for this is to do a quick approximate tuning without caring much about accuracy. Follow this up with a second, more careful tuning.

This was especially a problem with my first hammered dulcimer, and is very noticeable with my harp, which flexes and changes a lot as it is tuned. My second hammered dulcimer has a 3/4 inch birch plywood back and internal reinforcements, so it's very stable. On the downside, it's heavy!

Temperature and humidity play a large role, too. All of the materials in an instrument respond in different ways to changes in temperature and humidity. If you have a piano, you're well advised to keep it in a climate-controlled room. If you're a serious pianist you already know much more than I do about this topic.

#### Friction and Torque in Tuning Pin and Bridges

For guitarists, it's important to make sure that your nut (the zeroth fret) doesn't pinch the string and cause it to move in jerks and starts, or to have extra tension built up between the nut and the tuning peg itself. If this happens, you can rub a pencil in the groove where the string rides. The graphite in the pencil is a natural lubricant that can help avoid this problem.

Of course, you should also make sure that your tuning pegs and their machinery are smooth and well lubricated. If there's excessive slop due to wear-and-tear or cheap machinery, that will be an endless source of frustration for you.

![Tuning Pegs](/media/2014/01/8193104904_2c29a6b372.jpg)

On instruments such as pianos, hammered dulcimers, and harps, it's important to know how to "set" the tuning pin. While tuning the string upwards, you'll create torque on the pin, twisting it in the hole. The wood fibers holding it in place will also be braced in a position that can "flip" downwards. If you just leave the pin like this, it will soon wiggle itself back to its normal state, and even beyond that due to the tension the wire places on the pin. As a result, you need to practice tuning the note slightly higher than needed, and then de-tuning it, knocking it down to the desired pitch with a light jerk and leaving it in a state of equilibrium.

This technique is also useful in guitars and other stringed instruments, but each type of tuning machine has its own particularities. The main point to remember is that if you don't leave things in a state of equilibrium and stability, they'll find one soon enough, de-tuning the instrument in the process.

### References and Further Reading

I tried to find the book from which I studied tuning as a child, but I can't anymore. I thought it was an old Dover edition. The Dover book on tuning that I can find is not the one I remember.

You can find a little bit of information at various places online. One site with interesting information is [Historical Tuning of Keyboard Instruments](http://historicaltuning.com/) by Robert Chuckrow. I looked around on Wikipedia but didn't find much of use.

In this post I discussed the equally-tempered tuning, but there are many others. The study of them and their math, and the cultures and musical histories related to them, is fascinating. Next time you hear bagpipes, or a non-Western instrument, pay attention to the tuning. Is it tempered? Are there perfect intervals other than the octave? Which ones?

Listening to windchimes is another interesting exercise. Are the chimes harmonic or do they have inharmonicity? What scales and tunings do they use? What are the effects? [Woodstock]({{< amz B00BD8EM48 >}}) chimes use many unique scales and tunings. Many of their chimes combine notes in complex ways that result in no beating between some or all of the tones. [Music of the Spheres]({{< amz B0007QS6YO >}}) also makes stunning chimes in a variety of [scales and tunings](https://musicofspheres.com/products/music_chart.php).

As I mentioned, spreadsheets can be very helpful in computing the relationships between various notes and their overtones. I've made a small [online spreadsheet](https://docs.google.com/spreadsheet/ccc?key=0AqLZaBImC-JLdFp0RnNpY2JPcWlPdnNQXzkyQ2hyb1E&usp=sharing) that contains some of the computations I used to produce this blog post.

Let me know if you suggest any other references or related books, music, or links.

Enjoy your beautifully tuned guitar or other instrument, and most of all, enjoy
the process of learning to tune and listen! I hope it enriches your appreciation
and pleasure in listening to music.

![Guitar Soundhole](/media/2014/01/8075445_c8b558d3a8.jpg)

Suggested links from various sources:

* http://demonstrations.wolfram.com/TheVibratingString/
* http://www.truetemperament.com/
* (PDF) [Everything You Ever Wanted to Know About String Tension](http://www.daddariostrings.com/Resources/JDCDAD/images/tension_chart.pdf)
* http://www.sksmithmusic.com/virtual_classroom/string_choice.html

### Picture Credits

* http://www.flickr.com/photos/angelocesare/249168890/
* http://www.flickr.com/photos/locomosquito/5540678403/
* http://www.flickr.com/photos/cobalt/7788898528/
* http://www.flickr.com/photos/doug88888/4542297929/
* http://www.flickr.com/photos/spindlewest/8087829115/
* http://www.flickr.com/photos/toniblay/31859506/
* http://www.flickr.com/photos/heandfi/2516054483/
* http://www.flickr.com/photos/rayseinefotos/8193104904/
* http://www.flickr.com/photos/keela84/8075445/


[^53tet]: I remember reading once when I was a child about an avant-garde composer who created a scale with 53 divisions, which had nearly perfect intervals and very small gradations between adjacent notes. This is the [53 equal temperament](https://en.wikipedia.org/wiki/53_equal_temperament) scale.  See also [equal temperaments](https://en.wikipedia.org/wiki/Equal_temperament#Other_equal_temperaments).
