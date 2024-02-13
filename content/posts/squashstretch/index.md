+++
title = 'Building a ball rig to start animating'
summary = 'A theory behind building a squash & stretch ball'
languageCode = 'en-us'
date = 2024-02-12T15:20:18+01:00
draft = false
tags = ['rigging', 'beginner', 'theory']
showRecent = true
series = ["Rigging for beginner animation"]
series_order = 1
+++


# Our first rig - a squash & stretch ball

## 0. Foreword

In this article you'll learn:

- The importance of ball exercises for learning animation
- Basic idea on what Ball Rig consist of
- Learn common slang for some controller types
- Understand what is happening in the code of "stretch" modifiers in popular programs

## 1. Why is ball important?

Whether you're just starting your journey, study animation or you're a seasoned animation veteran - the basics of everything you know about animation starts with a ball. 
If we take a look at Richard William's *The Animator's Survival Kit*, the first chapter title where he talks about animating is called *IT'S ALL IN THE TIMING AND THE SPACING* - and 
it's all about how do we use these two terms in understanding the basics of any motion. 

>
> I'll never forget the image of this big Norwegian American sitting in the golden twilight, extending his long arms and spatula hands saying... «The bouncing ball says it all» 
> 
> ~R. Williams "The Animators Survival Kit"
>

That's why I want my first post dedicated to **building a proper ball rig**, on which we can build basics of **spacing**, **timing** and **squash & stretch** principles and to look under the hood of rigging
a mesh that can **preserve it's volume** while being scaled.

Of course, in 3D animation there are two main groups of users: **Autodesk Maya** and **blender** ones. I'm going to try to explain the ideas as software agnostic as possible,
but there are going to be chapter for both Maya and blender rigging - so noone feels left out. I am going to use some scripts along the way, but every script/addon is going to look like this:

[Example](https://www.example.com) - so you can install it yourself and follow along.

Besides that, I am going to include rigs done in this series (as I want to rig with you all rigs that you'd commonly find in animation exercises) both as fully working rigs and basics to follow the tutorial **totally free of charge** and **licensed under [GPL v3.0](https://www.gnu.org/licenses/gpl-3.0.html#license-text)**. 

If you're interested to hop into the world of animation technicality then let's start!

## 3. What is actually squash & stretch?


You're probably familiar with the idea of squashing and stretching of stuff - it seems super simple. If we *squash* a water balloon, water inside will push the sides making it look like pancake.
If we release it, it'll spring back to the more natural shape and if we throw it - it'll going to *stretch* in air before squashing on somebody's face.

![Squash & Stretch](https://i.gifer.com/IG9T.gif "A balloon squashing on a face, courtesy of gifer.com")

Disney's Nine Old Men found that squashing and stretching of objects is one of the most important principles to create a good looking animation - probably that's why they've made it **the #1 principle** in their **12 Principles of Animation** and
understanding it, is one of the building blocks of a strong animator today - because no matter if you draw your frames or manipulate a super complex humanoid body, you have to account for squash & stretch 
to achieve a real *illusion of life.

#### The mathematical explanation

We'll start by eating the frog. As far as mathematics go, we are going to take a sphere that has dimensions of *x*, *y* and *z* and volume *V1*,  we are going to multiply it by *n* in one direction and multiply it by 1/sqrt(*n*) in the rest to get a *V2* that is the same as *V1*

>
>{{< katex >}}
>\\(\text{Volume} = x \cdot y \cdot z = n \cdot y \cdot \left(\frac{x}{\sqrt{n}}\right) \cdot \left(\frac{z}{\sqrt{n}}\right)\\)
>
>Where: 
>*x*, *y*, *z* - our sphere transform values\
>*n* - the amount of change along we add, in this case along Y axis
>

#### Rigging explanation

In rigging there are multiple ways to achieve a volume preservation effect depending on the usage and outcome. 

If you came to animation from modelling, the first idea that might pop to you mind is **Lattice Deformer*.

![Image of Lattice Deformer](/images/ballrig_theory_1.png "Lattice around the cube object in Object Mode - from blender official docs")

Lattice is a deformer that is found both in <span style="color:#FF3600">blender</span>( that color will mean it's a blende term) and <span style="color:#00ECFF">Maya</span> (that color will mean it's a Maya term) and it's often used for applying deformation. For our purposes, 
**deformation cage** can be constrained and controlled, but while working on ball rigs (and I've saw a lot of Youtube videos using this idea), it's not the most transferable way to create deformations, that's
why I am not going to talk about them in upcoming tutorials.

Second one, more in line with rigging tools themselves would be <span style="color:#FF3600">**Stretch To Constraint**</span>/<span style="color:#00ECFF"> **Squash Deformer** </span>. 
Both of them are off-the-shelf features that are going to streamline building the mechanisms on simpler rigs, but might be limited in some more advanced setups. Because <span style="color:#FF3600">blender</span> as of 4.0 didn't add 
rigging nodes yet, we'll be using <span style="color:#FF3600">Stretch To Constraint</span> in <span style="color:#FF3600">blender</span>-specific tutorial. How does it work under the hood? 

Actually, the basic idea of doing a squash & stretch is **joint scaling**. When the object *stretches*, the joint (or chain of joints) is getting longer and whem it *squashes*, it naturally gets shorter.
As this can be done both uniformly along all axes (thus making the chain bigger) and along specific ones - one might try to imitate what is happening to other axes at the same time.
For that, we can use base math.

Let's do an example. 

We have a bone of transform (x, y, z), where y will be the height. 

As we know the y, we stretch the bone by vector \\(\vec{v}\\) = [0, 1, 0] resulting in new transform of (x, y+1, z). As we know the new transform, 
we know that the new bone is higher from the default one by 1, but to sell the effect of *stretching*, we need to also make the bone smaller in other axes - therefore we can multiply x and z using the Volume formula
I've given you before, looking like this: {{< katex >}} \\(\frac{1}{\sqrt{n}}\\), where **n** is the amount of transform we are adding by translation, in our case **n = 1**. 

In <span style="color:#00ECFF">Maya</span>, we can use a *Rigging Node Editor*, to directly connect the channels of x, y and z with *multiplyDivide node*, to multiply the channels accordingly - 
achieving a good squash & stretch that is going to work on all type of bone chains - it's extremly useful for humanoid skeleton rigs with cartoon features!

#### Squash & Stretch in video games

*Squash & Stretch isn't something that you are going to see in video games a lot.* 
At least... not by default.

Unreal Engine by default do not export scale of deformation bones at all! And while this can make you think - *why bother?* - 
is has a really good reason to do so. A volume-perserving squash & stretch in a *Skeletal Mesh* has to calculate skinning deformations every frame, making it one of the heaviest (or rather the most expansive)
things for your CPU to do. Of course, sometimes whole art style might be broken because of that, but that's why there's a special option to enable bone scaling while importing the mesh to preserve them,
but normally it has to be included in general optimalization or rather - it has to be a game feature, not a default.

Because of heavy optimalization implications there are different ways to sell this principle while animating for video games. You might see some slight translations of skeleton, arms or legs, 
sometimes the legs are becoming longer to stay on ground for a while to give more weight (World of Warcraft's Pandaren jump loop), sometimes you will translate the skeleton a little to give a better pose - 
there are many different tricks to sell scalling and stretching you'll learn while animating. Of course, it won't be a *real*, *calculated volume preservating* squash & stretch, but it'll create the *illusion
of life* - and that's what we aim for.

## 3. How does a ball rig work?

### Mesh

For this example I’m going to use a simple ball mesh with a checker texture that you can download:
- For blender [here](https://www.example.com)
- For Maya [here](https://www.example.com)

### Skeleton

A ball skeleton in the easiest form is just one bone which <span style="color:#00ECFF"> joints </span>or head and tail <span style="color:#FF3600"> joints </span> (that color will mean it's a blender term)
are the only pieces over which we will skin. Because there's no deformation of these, we can use automatic weight painting.

### Controls

If we think about a ball rig, there are a few basic things we'll need.

{{< alert >}}
For blender I'm going to use [Bone Widget](https://blenderdefender.gumroad.com/l/boneWidget) to create control shapes.  
For Maya, I'm are going to use [IDR ControllerTools](https://indyrigger.gumroad.com/l/kybSJ?layout=profile) to do the same.
{{< /alert >}}

The list of controls:
- **Root** - if you ever downloaded a rig, you probably know it as some kind of a circle or a variation of circle with arrows - it's going to tell every software we work in what's the **default space** of our object. 
The easiest way to think about it is to think that if we are going to move the root controller, everything will move along with it. In gameplay animation most of the time it'll stay at default [0, 0, 0] position to mimic the player's capsule.
- **Center of Gravity** - commonly known as cog or c.o.g is usually the control around hips or general center of gravity of your rig. It's one of the main thing animators are going to use to give a sense of weight. 
For a ball usage, we'll create a **cog** to move the ball in 3D space.
- **Rotor** - while it's not something that you might find in every rig, I am going to add a second controller under the COG that is going to let us rotate the ball - why? To detach the **translation** of our ball from it's **rotation**. 
It will help us with separating squash and stretch from the rotation.
- **Squash and Stretch Controllers** - as we are going to make our ball not only move and rotate but also to squash and stretch - we'll need some controls to *control* the amount of squash and stretch. 
We'll make **two** controls: at the **top** and **bottom** of the ball to give animators more flexibility when it comes to to proper animation. Because of the rotor control, 
we'll be also able to rotate the ball independently of these controllers - in case the ball is going to hit a wall for example!

## 4. Closing Thoughts

So we've learned **what is squatch & stretch**, we know **why is this principle important** and we finally **know how does it work**. 

Besides that we have an outline on what do we need, to build a working ball rig, so **let's apply** what we've learned in next articles!