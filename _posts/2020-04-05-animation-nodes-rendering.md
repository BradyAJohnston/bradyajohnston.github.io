---
title: Rendering around crashes with Animation Nodes.
subtitle: Figuring out how to render using animation nodes when experiencing lots of crashes.
tags: blender, animation nodes
---

# Working around the crashes

![Pixel art RNA polymerase moving along DNA. Created from the same scene described below, rendered in the same method using cmd.](/img/pixel_rna_pol.gif "Pixel art RNA polymerase")

_Some pixel art of the results._

Wanting to test out a nucleic-acid generator I created in Animation nodes, I spent a bit of time putting together a test scene (bacterial RNA polymerase synthesising some RNA from DNA template).

Having set up a scene, done the math and gotten things working I was ready to try out rendering the scene. Unfortunately there are a few problems with rendering using Animation Nodes, and after rendering 1-3 frames Blender would crash.

Frustrated, I looked for solutions. One potential was to bake all calculations to key frames and render without executing the node tree. While it worked for the instanced cylinders, the backbones of my nucleic acids didn’t keyframe so I just had floating nucleotides in my scene.

The final working solution ended up being rendering from the `terminal` / `command line`. Blender has some useful documentation on how to do this *here*.

I still had trouble when trying to render a batch of frames using `-s 1 -e 250` to specify rendering frames  1-250, so instead the solution was to render single frames and restart Blender every time using a `for` loop in `Command Line`.

This results in:
1. Booting Blender
2. Loading the Scene
3. Render the specified frame
4. Save image and quit blender

The final solution worked like this for rendering on my windows machine:

``` cmd
FOR /L %G IN (1,1,250) DO C:\pathto\blender.exe -b C:\pathto\blendfile.blend -o C:\pathto\frames_ -f %G
```
Which wrote frames_0001.png, frames_0002.png _etc_ up to frame 250.

Seemed to work without trouble, yielding this final animation once composited.

_I can't embed html5 image so this gif will have to do, sorry for slow load times._

![Bacterial RNA polymerase at work](/img/rnapol.gif "Bacterial RNA polymerase at work")
