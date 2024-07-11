+++
title = 'Simple IKFK Switch in blender'
summary = 'A tutorial on creating IKFK switches in blender without addons or scripting'
languageCode = 'en-us'
date = 2024-07-09T21:00:00+02:00
draft = true
tags = ['notes', 'maya', 'blender', "reflections"]
showRecent = true
showTableOfContents = true
+++
## 0. Foreword

In this article you'll learn: 
- Importance of using IKFK switch
- How to create an IKFK switch
- How does it work under the hood

## 1. Why does one need IKFK switch?
### What actually IK and FK means?

For those who don't know it yet, let's start with a quick explanation what **FK** and **IK** actually are. *Forward Kinematics* and *Inverted Kinematics* are both terms that are related
to the bone chain and their order of transform. Let's start with *Forward Kinematics*, considering a simple chain of bones:

```
boneA
    boneB
        boneC
``` 

### Forward Kinematics

FK is something that I consider a "standard" way of how a bone in a chain react. As they are parented, if you translate *boneA*, it'll change the space of the children, making them rotate alongsite it. That means,
the order of transforms is created from boneA to boneC - or from up to down in the hierarchy. What might differentiate them, most of the time FK chains are transformed by rotation only, there are setups where one
might want to translate them (that needs additional scaling setups), but rotation is 98% of the use cases I can think of. 

Besides that, FK is a great way to create a consistent, good looking arcs, as you have perfect control over every bone of the limb you're using! As you have to keyframe every bone in a chain for a pose, that means 
that you can also create better overlaps by moving offsetting the keyframes so their end-pose don't end in the same time. 

### Inverted Kinematics


While animating, there are many different techniques that animators might want to use to accomplish their shot. For most of them, you might want to stay in one
mode for the whole time - like when you're animating a walk cycle, your legs will stay on IK meaning that your bone chain - in this case the leg -
consisting of three bones (thigh, shin and a foot) would be driven by moving the end of the chain (foot). It's an extremely useful

## 2. How to create IKFK switch in blender?
## 3. Theory behind
## 4. Closing thoughts