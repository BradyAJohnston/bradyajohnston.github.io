---
title: Becoming one with the ETC.
subtitle: Playing around with face filters for science communication.
tags: blender, sparkAR, AR, ATP, filter
---

# We need ChimeraX

Recently a popular hashtag in the structural biology community went around of `#weneedchimeraX` which to be clear, we definitely do.

Funding was not looking good for the team was that was behind the incredibly powerful and importantly free tool ChimeraX. This also marked the start of the [ChimeraX](https://twitter.com/UCSFChimeraX) team's journey into science twitter. One of their early tweets showed off the ability to generate a _very cool_ animation using the morph functionalities and some nice graphical rendering.

All it would take is two lines of code and you have an animation of ATP synthase in action.
```
open 6n2y 6n2z 6n30
morph #1,2,3 wrap true
```

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">To morph between 3 conformations of ATP synthase use ChimeraX commands &quot;open 6n2y 6n2z 6n30&quot; and &quot;morph #1,2,3 wrap true&quot;. <a href="https://twitter.com/hashtag/ChimeraXHowTo?src=hash&amp;ref_src=twsrc%5Etfw">#ChimeraXHowTo</a> <a href="https://t.co/2u4Au6Tvpf">pic.twitter.com/2u4Au6Tvpf</a></p>&mdash; ChimeraX (@UCSFChimeraX) <a href="https://twitter.com/UCSFChimeraX/status/1258888093068701696?ref_src=twsrc%5Etfw">May 8, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## Taking it into Blender.
Something that I have been playing around with a lot is trying to replicate rendering styles of ChimeraX and PyMol inside Blender. When looking at this tweet, it struck me that maybe I was trying to reinvent the wheel. There was already an incredibly powerful morphing and rendering tool available (ChimeraX) so why was I trying to overcomplicate things.

I had the idea of rendering out frames from ChimeraX and just using the _images-as-planes_ plugin for Blender to import an animated sequence. Render it once and theoretically you could replicate it _a lot_ of times inside a scene with very little increase in computation time for the scene.

There was no easy way to render a movie as individual frames, and I needed a format that would preserve the alpha-channel of the frames, the ideal choice being `.png`.

```
save frame001.png transparentBackground true
```

This command gives you a saved `.png` file which a transparent background. Now we just need to iterate through all of the states, saving the relevant frame for each state. I played around with the _API_ a bit, but I'm not skilled enough with python yet to get anything working. Instead I went for a simpler, if uglier solution.

```
coordset #4  7
```

This will set structure number 4 to frame number 7.

All we need is to combine the two, which a simple loop in the language of your choice will be able to create. I just quickly did it in bash.

```bash
for i in {1..10}; do printf "coordset #4 $i\nsave frame$i.png transparentBackground true\n"; done
```

Which will give you this:

```
coordset #4 1
save frame1.png transparentBackground true
coordset #4 2
save frame2.png transparentBackground true
coordset #4 3
save frame3.png transparentBackground true
coordset #4 4
save frame4.png transparentBackground true
coordset #4 5
save frame5.png transparentBackground true
coordset #4 6
save frame6.png transparentBackground true
coordset #4 7
save frame7.png transparentBackground true
coordset #4 8
save frame8.png transparentBackground true
coordset #4 9
save frame9.png transparentBackground true
coordset #4 10
save frame10.png transparentBackground true
```

You can then just copy and paste that entire block (for whatever i range you give it) into the command line for ChimeraX and it will render all of the files for you.

Into blender you can import the images as frame, and I then tested out a quick scene in EEVEE. To make the shadows cast correctly you must ensure _Blend Mode_ and _Shadow Mode_ in the shader properties for the plane are set to `Alpha Blend` and `Alpha Clip` respectively.

![Blende Modes](https://i.imgur.com/wskg5hL.png "Blend Modes")

Resulting in the following, quite interesting (and very quick to render) animation.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Playing around with some 2D-3D fusion art styles inside blender, made infinitely easier thanks to the fantastic <a href="https://twitter.com/UCSFChimeraX?ref_src=twsrc%5Etfw">@UCSFChimeraX</a> <a href="https://twitter.com/hashtag/WeNeedChimeraX?src=hash&amp;ref_src=twsrc%5Etfw">#WeNeedChimeraX</a> <a href="https://twitter.com/hashtag/b3d?src=hash&amp;ref_src=twsrc%5Etfw">#b3d</a> <a href="https://t.co/nXijr6nT1c">pic.twitter.com/nXijr6nT1c</a></p>&mdash; Brady Johnston (@bradyajohnston) <a href="https://twitter.com/bradyajohnston/status/1260207077743448066?ref_src=twsrc%5Etfw">May 12, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Working from this success, you can also use this trick for importing animations into the SparkAR for making face filters for Facebook and Instagram. I will go into detail about how to do this more in the future, but you can view the results (and use the filter yourself) in the tweet below.

## Want to become a part of the ETC?
<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Did you ever want to become part of the electron transport chain? Well now you can! I created this face filter so now you can wear ATP synthase like a hat.<br><br>Facebook filter: <a href="https://t.co/udtIp9IiMV">https://t.co/udtIp9IiMV</a><br>Instagram filter: <a href="https://t.co/NHrDpgIvVh">https://t.co/NHrDpgIvVh</a> <a href="https://t.co/Uy2ETEbUOf">pic.twitter.com/Uy2ETEbUOf</a></p>&mdash; Brady Johnston (@bradyajohnston) <a href="https://twitter.com/bradyajohnston/status/1263039379095740416?ref_src=twsrc%5Etfw">May 20, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
