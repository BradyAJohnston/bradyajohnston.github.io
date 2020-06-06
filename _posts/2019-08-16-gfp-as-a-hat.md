---
title: GFP As a Hat
subtitle: The latest in fluorescent fashion.
tags: GFP, filter, AR, ARkit
---

As I was drifting off to sleep one night, the thought hit me:
>"_People love face filters, people love GFP, what if we combined the two?_"  
> My brain, late at night.


The next morning I had a quick look around and wasn’t able to find any evidence of anyone doing anything before. There has been a bit of effort into making AR protein apps and experiences, but we have all of these 3D models from all of the structural information that biology gathers, but nobody has put it into an instagram filter yet?

I cranked out the old Blender, imported some models from PyMOL and quickly had a nice looking model of eGFP glowing bright green.

To skip the technical details, this was the rather successful result:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Have you ever wanted to wear GFP as a hat? Well now you can. Playing around in blender and apple’s ARkit on iOS13<a href="https://twitter.com/hashtag/b3d?src=hash&amp;ref_src=twsrc%5Etfw">#b3d</a> <a href="https://t.co/08XwyXW9e2">pic.twitter.com/08XwyXW9e2</a></p>&mdash; Brady Johnston (@bradyajohnston) <a href="https://twitter.com/bradyajohnston/status/1177755074853924864?ref_src=twsrc%5Etfw">September 28, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

As for how it was done, I won’t go into too much detail but the basics was this:

* Export .obj file from Pymol, using the structure [4EUL](https://www.rcsb.org/structure/4EUL).
* Import into [Blender](https://blender.org) to clean up the geometry (remove overlapping vertices) and combine to single .obj object.
* Create green .png file to act as the colour texture, save next to .obj file.
* Use the apple `usdzconvert` supplied with xcode11 to do the following
```
usdzconvert gfp.obj gfp.usdz -color_map green.png

```
* With the gfp.usdz file you can now preview it on macOS
* Create a new Reality Composer project for facial recognition
* Import the .usdz file into reality composer
* Compose the scene, press run and play around with the results.

I want to do a lot more with this. There is more potential for using a cross-platform approach using [SparkAR](https://sparkar.facebook.com/ar-studio/) to compose Instagram face filters rather than having to build a whole app. We’ll see where that goes in the future.
