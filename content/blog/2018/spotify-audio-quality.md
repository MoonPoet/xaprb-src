---
url: /blog/spotify-audio-quality/
title: "How Good Is Spotify's Audio Quality?"
date: '2018-01-21T00:00:00-05:00'
author: Baron Schwartz
categories:
- Music
- Reviews
description: I decided to figure out why Spotify sounds so terrible through a Chromecast Audio, and I was surprised at what I found.
image: /media/2018/01/mobile-616012_1280.jpg

---

I bought a Google [Chromecast
Audio](https://store.google.com/product/chromecast_audio) for my [budget
audiophile system](/blog/my-stereo-system/), due to problems with Apple's
AirPlay. I like the Chromecast, but as I listened to my favorite music on
Spotify Premium, I was disappointed. The audio quality was noticeably worse than
casting Spotify to AirPlay. I decided to figure out what was going on and see if
I could fix the audio quality issues. I think I've learned what's wrong, and
unfortunately I don't think it's fixable. Read on to learn more.

<!--more-->

A while ago I did an experiment to determine the [all-around best lossy music
compression format](/blog/2016/02/21/best-itunes-mp3-format/). There's a lot of
"it depends," but my takeaways were:

- High-quality variable-bitrate MP3 produced with the LAME encoder is the most
  compatible choice if you want broad compatibility, but has low sound quality.
- If you want the best sound quality, AAC (Apple's native format) or Ogg Vorbis
  are much better than MP3 but aren't as universally supported.

At that time I was actively using both Apple Music and Spotify. Ultimately, I
stopped using Apple Music because I didn't need two services, and I like
Spotify's UI and recommendations better. I stopped my trial of Google Play Music
and haven't thought about it since then, because of the terrible sound it
produces by transcoding everything to MP3 files.

Since then, I've been listening to a lot of music by playing it on Spotify
Premium and using AirPlay to cast it to an Apple Airport Express hooked up to my
stereo system. I have generally been very happy with the audio quality. Despite
what many people claim, even though I'm growing older and I've suffered some
hearing damage, audio compression artifacts are very obvious when listening on a
decent system. But Apple Music and Spotify both use high-enough-quality
compression that it's still pleasant.

AirPlay became frustrating, though. There were so many reliability issues with
it! I needed to reboot the Airport Express on a pretty regular basis to get
audio to stream to it. It was so annoying that I eventually gave up and bought a
[Sonos]({{< amz B00EWCUK1Q >}})
in the kitchen. This has been much more enjoyable than trying to stream to the
boombox I had previously. In my listening room, though, I still used AirPlay.

After a while I decided to try a Chromecast Audio. If you haven't heard about
these, they're a super small, convenient little puck that plugs into power,
connects to WiFi, and streams music. It's brilliant, much better designed than
AirPlay or similar.

But the sound quality was immediately disappointing! One example is the
triangles in the chorus to Jann Arden's *Sleepless*. They don't even sound like
triangles; they sound like someone spitting while whistling. It's not subtle:
it's *horrible*.

So I decided to repeat my experiment to evaluate audio quality in Audacity, and
see what's going on with Spotify. Did I just not notice this before when I was
using AirPlay? Or is something wrong with the Chromecast? I decided to compare
Spotify's audio quality to iTunes's AAC and to the original music.

You may know that Spotify uses Ogg Vorbis. According to the [documentation](https://support.spotify.com/us/article/high-quality-streaming/),

> The desktop app’s standard quality is Ogg Vorbis 160kbit/s.  Premium subscribers can choose to switch on High quality streaming, which uses 320kbit/s

I own the *Blood Red Cherry* CD that has that song, so I ripped it to WAV and
used iTunes to encode it to AAC. Then I used Soundflower to record Spotify, set
to high-quality 320kbps audio.  I tried to see if I could hook the Chromecast up
to my computer and record the audio from its output, but I wasn't successful
with that.

I compared these recordings against each other. What I found reassured me:
Spotify's audio quality is not terrible. If you have Spotify Premium, you should
be getting *very* good quality audio, even though it's not perfect.

For those who are curious, it's not as good as Apple Music's, though. Apple
Music encodes everything in 256kbps AAC files, which are nearly transparent to
most listeners even on audiophile systems. For the records, here's an excerpt of
the chorus to *Sleepless* in several formats. Notice the triangles, mostly lost
in the dense layers of instruments and vocals:

- WAV ripped directly from CD.<br>
    <audio controls>
    <source src="/media/2018/01/sleepless-wav.wav" type="audio/x-wav">
	 Your browser does not support the audio element.
	 </audio>
- 256kbps AAC encoded with iTunes.<br>
    <audio controls>
    <source src="/media/2018/01/sleepless-aac.wav" type="audio/x-wav">
	 Your browser does not support the audio element.
	 </audio>
- Spotify's 320kbps Ogg Vorbis high-quality streaming.<br>
    <audio controls>
    <source src="/media/2018/01/sleepless-spotify.wav" type="audio/x-wav">
	 Your browser does not support the audio element.
	 </audio>

The triangles in this chorus make a good test case because of the complexity of
the music and clarity of the triangles; if they're badly compressed, it's easily
audible.

To put Spotify's audio quality into a different perspective and compare versus
AAC, here's the residual/noise after subtracting the encoded versions from the
original bit-for-bit copy ripped from the CD.

- AAC's noise due to lossy encoding.<br>
    <audio controls>
    <source src="/media/2018/01/sleepless-aac-noise.wav" type="audio/x-wav">
	 Your browser does not support the audio element.
	 </audio>
- Spotify's noise due to lossy encoding.<br>
    <audio controls>
    <source src="/media/2018/01/sleepless-spotify-noise.wav" type="audio/x-wav">
	 Your browser does not support the audio element.
	 </audio>

Less noise is "better," from a purist's point of view, because it means less
musical information was discarded while encoding. But remember the point of
lossy encoding is to throw away *as much signal as possible, inaudibly*. So this
is not necessarily a good measure of how good quality the compression is,
because a perfect algorithm would discard lots of inadible information!

I was a bit stumped. Spotify's audio quality is excellent for lossy-compressed
streaming. What on earth could make Spotify sound so bad through
the Chromecast Audio? I checked the Spotify documentation again, and found the
following:

> What bitrate is used when streaming Spotify with Chromecast?
> Standard quality for streaming Spotify with Chromecast is AAC 128kbit/s, and 256kbit/s for Premium.

Suddenly it made sense. *I think the Chromecast is playing Ogg Vorbis transcoded to
AAC.* That would *absolutely* explain the degraded sound quality I noticed.

Transcoding is a *terrible* idea. This is the very reason that I ran screaming
in terror from Google Play Music. Transcoding a lossy-compressed format to
another lossy-compressed format sounds like garbage. If this is what's happening
with Spotify Connect and Chromecast, I think I'll reconnect my AirPort Express.

I'm spending enough time and effort on this that I'm seriously considering a
music server with all of my CDs in FLAC or ALAC lossless format. My CD
collection is decades old and I can't imagine those CDs will last forever
anyway. I'm starting to learn about [Roon](https://roonlabs.com), which seems
pretty amazing and integrates with [Tidal](http://tidal.com/us), a lossless
streaming service. There's also [Deezer](https://www.deezer.com/us/features),
[Murfie](https://www.murfie.com/), and
[Subsonic](http://www.subsonic.org/pages/index.jsp).

To conclude, I have two wishes for Spotify:

1. Let me upload my own music to the service, the way I can with Google, Apple,
	and Amazon; but use a really high-quality encoding and don't transcode. I
	have hundreds of CDs that aren't available on any streaming or download
	service. I want all my music available in one place.
2. Offer a lossless streaming subscription. (About a year ago they tested this
	out, but there's no word if they'll actually do more than test). I'm highly
	likely to become a Tidal subscriber at some point if Spotify doesn't offer
	lossless.

I want these things because I'm convinced that at some point, perhaps soon, I'm
going to be able to find my wished-for service that combines lossless streaming
of music via subscription, with a subscription to store the music I own and
isn't available through the service itself. It just feels like an absolute
certainty that this will come to pass. Whoever gets there first will likely earn
my business.

A couple of footnotes I didn't want to mention above, to avoid distracting
readers:

1. I connected my Chromecast Audio to my stereo through a headphone-to-RCA
	adapter, not digitally.
2. When I recorded Spotify's output on my Mac, I found that the volume was
	slightly lowered (perhaps normalized). I used an Amplify transform in
	Audacity to raise the peaks to the same level as the raw audio extracted from
	the CD. I suspect the "noise" file for Spotify is noisier than the real audio
	I streamed from them, due to that.
3. Why would Google Chromecast Audio support AAC, when [Google Play Music
	supports only lower-quality MP3](https://support.google.com/googleplay/answer/1100462)?

[Photo Credit](https://pixabay.com/en/mobile-phone-iphone-music-616012/)
