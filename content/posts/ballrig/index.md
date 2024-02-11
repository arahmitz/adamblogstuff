+++
title = 'The ball says it all'
summary = 'Tutorial for basic squash & stretch ball rig'
languageCode = 'en-us'
date = 2024-02-11T15:20:18+01:00
draft = false
tags = ['ball', 'rigging', 'beginner', 'maya', 'blender']
showRecent = true
+++


# How to build a proper ball rig?

## 1. Why is ball important?

Whether you're just starting your journey, study animation or you're a seasoned veteran - the basics of everything you know about animation starts with a ball. If we take a look at Richard William's *The Animator's Survival Kit*, the first chapter title where he talks about animation is called *IT'S ALL IN THE TIMING AND THE SPACING* - and it's all about how do we use these two terms in understanding the basics of any motion. 

>
> I'll never forget the image of this big Norwegian American sitting in the golden twilight, extending his long arms and spatula hands saying... «The bouncing ball says it all» 
> 
> ~R. Williams "The Animators Survival Kit"
>

That's why I want my first post dedicated to **building a proper ball rig**, on which we can build basics of **spacing**, **timing** and **squash & stretch** principles and to look under the hood of rigging a mesh that can **preserve it's volume** while being scaled.

Of course, in 3D animation there are two main groups of users: **Autodesk Maya** and **blender** ones. I'm going to try to explain the ideas as software agnostic as possible, but there are going to be chapter for both Maya and blender rigging - so noone feels left out. I am going to use some scripts along the way, but every script/addon is going to look like this:

[Example](https://www.example.com) - so you can install it yourself and follow along.

Besides that, I am going to include rigs done in this series (as I want to rig with you all rigs that you'd commonly find in animation exercises) both as fully working rigs and basics to follow the tutorial **totally free of charge** and **licensed under [GPL v3.0](https://www.gnu.org/licenses/gpl-3.0.html#license-text)**. 

If you're interested to hop into the world of animation technicality then let's start!

## 2. How does a ball rig works?

### Mesh

For this example I’m going to use a simple ball mesh with a texture that you can download [here](https://www.example.com).

### Skeleton

A ball skeleton in the easiest form is just one bone which joints (Maya) or head and tail (blender) are touching the start and end of the height line, like this:

IMAGE

The whole mesh is skinned to this one bone only.

### Controls

If we think about a ball rig, there are a few basic things we'll need.

{{< alert >}}
For blender I'm going to use [Bone Widget](https://blenderdefender.gumroad.com/l/boneWidget) to create control shapes.  
For Maya, I'm are going to use [IDR ControllerTools](https://indyrigger.gumroad.com/l/kybSJ?layout=profile) to do the same.
{{< /alert >}}

The list of controls:
- **Root** - if you ever downloaded a rig, you probably know it as some kind of a circle or a variation of circle with arrows - it's going to tell every software we work in what's the **default space** of our object. The easiest way to think about it is to think that if we are going to move the root controller, everything will move along with it. In gameplay animation most of the time it'll stay at default [0, 0, 0] position to mimic the player's capsule.
- **Center of Gravity** - commonly known as cog or c.o.g is usually the control around hips or general center of gravity of your rig. It's one of the main thing animators are going to use to give a sense of weight. For a ball usage, we'll create a **cog** to move the ball in 3D space.
- **Rotor** - while it's not something that you might find in every rig, I am going to add a second controller under the COG that is going to let us rotate the ball - why? To detach the **translation** of our ball from it's **rotation**. It will help us with separating squash and stretch from the rotation.
- **Squash and Stretch Controllers** - as we are going to make our ball not only move and rotate but also to squash and stretch - we'll need some controls to *control* the amount of squash and stretch. We'll make **two** controls: at the **top** and **bottom** of the ball to give animators more flexibility when it comes to to proper animation. Because of the rotor control, we'll be also able to rotate the ball independently of these controllers - in case the ball is going to hit a wall for example!

### How does squash & stretch work under the hood?

#### The mathematical explanation

We'll start by eating the frog. As far as mathematics go, we are going to take a sphere that has dimensions of *x*, *y* and *z* and volume *V1*,  we are going to multiply it by *n* in one direction and multiply it by 1/sqrt(*n*) in the rest to get a *V2* that is the same as *V1*

>
>{{< katex >}}
>\\(\text{Volume} = x \cdot y \cdot z = n \cdot y \cdot \left(\frac{x}{\sqrt{n}}\right) \cdot \left(\frac{z}{\sqrt{n}}\right)\\)
>
>Where: 
>*x*, *y*, *z* - our sphere transform values\
>*n* - the amount of change along we add, in this case along Y axis

#### Techanim Technobabble explanation

In rigging there are multiple ways to achieve a volume preservation effect depending on the usage and outcome. 

In this post I’m going to talk about the most basic one - **joint scaling**. To achieve the stretching in one axis, we are going to take the dimension between** two joints** (for Maya) or the **length of a bone** (for blender) and make it larger for example by increasing it in the height axis. By doing this, we are going to feed rest of the axis (width, depth) with a multiplification of {{< katex >}} \\(\frac{1}{\sqrt{n}}\\), where **n** is the amount of transform we are adding - basically making the width and depth smaller the longer the bone is. Of course it’ll work the opposite when we are going to squash the controllers by making the object wider in other directions. Just like we would stretch or squash a water balloon.

## 3. Rigging the ball in blender

## 4. Rigging the ball in Maya

## 5. Final thoughts

## 6. Useful links
