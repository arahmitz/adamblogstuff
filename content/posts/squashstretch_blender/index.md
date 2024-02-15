+++
title = 'Squash & Stretch Ball in blender'
summary = 'A step by step guide to build your first ball rig in blender'
languageCode = 'en-us'
date = 2024-02-12T15:20:15+01:00
draft = false
tags = ['rigging', 'beginner', 'blender']
showRecent = true
series = ["Rigging for beginner animation"]
series_order = 2
+++
## Rigging the squash & stretch ball in blender

## 0. Foreword

In this article you'll learn:

- How to rig a ball in blender
- How to create armatures and move them to snap bones in place
- How to use [Bone Widget](https://blenderdefender.gumroad.com/l/boneWidget) to create controls
- How to make clean layers in rig
- Basics of preparing rig for usage by other people

## 1. Preparation 

As far as rigging in blender goes, we're start by downloading the [project files](https://github.com/arahmitz/am_blender_ball_tutorial) and [Bone Widget](https://blenderdefender.gumroad.com/l/boneWidget).

Attention: due to lack of rigging nodes (as of day of writing this post), we'll need to do little hacking in the controllers hierarchy,
that I'll try to avoid later in the series, I'll let you know where and why it happens.

{{< alert >}}
The files are prepared for version 4.0, I am going to utilise new bone collections, so this part will look different
if you're on the old version of blender. 
{{< /alert >}}                                  

## 2. Armature and Skinning
After you start up your project file, it should look like this:
![A checkerboard ball in an open scene](/images/ballrig_blender_1.png "View after opening the file")                                    

First of all, we are going to create an armature in the proper axis. That's why we'are going to click <kbd>NUM3</kbd> to make our camera allign,
making our left side the front, and our right side the back. We can add the *Armature* by clicking <kbd>SHIFT</kbd> + <kbd>A</kbd> and selecting *Armature* that'll be created in 
the middle of the bar. Of course we can't see it, so we can navigate to the right side, and by selecting *Armature Data*>*Viewport Display*
we are going to enable  
- [x] Names - This option shows bone names, it'll help us in defining bones on screen, without having to look all the time at the outliner.
- [x] Shapes - It'll let us look at controls later
- [x] Bone Colors - It'll let us change controller colors later
- [x] In Front - It'll render bones always in front, super useful for aligning stuff.
- [x] Axes - It's important for understanding our rotations.
![Outliner view of Armature data](/images/ballrig_blender_2.png "Armature Data in outliner") 

With selected armature, we can change the mode to *Edit* by using <kbd>Tab</kbd> (It's not a basic setting, go to *Preferences* > *Keymap* and select Tab for Pie Menu,
it'll make things faster later)
![Tab for Pie Menu](/images/ballrig_blender_3.png    "Mode Select Pie Menu")

While in Edit Mode with the bone selected, I am going to use <kbd>F2</kbd> to fast-change name of the bone to root - as I've explained it before, root always sits at the origin of the world, and thats where our root will sit too.
![Bone rename](/images/ballrig_blender_4.png "Rename tool")

Now, in Edit Mode, we are going to select the *Head* of the bone, and by clicking <kbd>SHIFT</kbd>+<kbd>S</kbd> we're going to choose *Selection to Cursor*. After that, by moving the head with <kbd>G</kbd>, I am going to clikc *Y* to lock axis and hit <kbd>1</kbd> to move it by 1m.
![Changing the root's placement](/gifs/ballrig_blender_1.gif "Changing the root to world transform by using 3D Cursor")

Now that we know how to use 3D cursor, we are going to change the mesh origin point by first moving the *3D Cursor to Active*, but in order to select the mesh, we need to use use <kbd>TAB</kbd> to get back to Object Mode.
![Moving 3D Cursor to Active Element Origin](/gifs/ballrig_blender_2.gif "Changing the 3D Cursor to Ball Origin")

After we've done that, the next step is to create our only *def* bone, that we'll call *def_body*. To do that, we are going to select the armature back, change to Edit Mode,
then select it's *Tail* and Extrude a bone after clicking <kbd>Z</kbd> to lock the axis as height. We are going to extrude it up to around the middle and rename the bone.
![Extruding a bone from root](/gifs/ballrig_blender_3.gif "Extruding a bone from root")

>
> Clean outliner is your friend - rename things as early as possible to de-clutter things!
>

After that, we are going to move the *def_body* bone to start in the middle of the ball by selecting the bone (make sure it's not parented, if yours is, use <kbd>ALT</kbd>+<kbd>P</kbd>>*Clear Parent*)
then by using <kbd>SHIFT</kbd>+<kbd>S</kbd> use *Selection to Cursor*. Your rig should look like this:
![def_body in proper place](/images/ballrig_blender_5.png "Rig with proper deformation bone placed")

One super important thing for later is changing the rotation mode - with your bones selected in Pose mode use <kbd>CTRL</kbd>+<kbd>R</kbd> and select *XYZ* - we'll touch it later!
![Selecting a rotation mode](/images/ballrig_blender_18.png)

After that, we are going to bind the mesh to the bone in a process called **skinning**.

To do that, we are going to start by checking every bone in *Bone Data* tab of Properties to look if [ ] Deform is checked, we want our *root* to be unchecked
while def_body should be checked.

>
> In blender, bones with the prefix DEF are the only ones that should have deform checked, by doing that you'll know which bones influence your mesh
>
![Properties of def_bone with Deform checked](/images/ballrig_blender_6.png "Properties of def_bone with Deform checked")

If all of these are checked (and believe me - it's a good idea to get a habit of checking that before skinning the model), we can start skinning process.
To do that, go back to your Object Mode, select your Mesh, then with <kbd>SHIFT</kbd> select your Armature and by using <kbd>CTRL</kbd>+<kbd>P</kbd>> *Armature Deform - Automatic Weights*.
![Skinnig process with Armature Deform](/gifs/ballrig_blender_4.gif "Skinning process with Automatic Weights")

{{<alert icon="info">}}
You might ask yourself - why using automatic? Is it always the best? The answer is sadly **no** - automatic weights is almost never the answer. Only models consisting of one mesh
(or many single meshes like mechanical stuff) is okay-ish, but I still suggest to use *Empty Groups* and select *Vertex Groups* (information which skin touch what) yourself, but
that's beyond scope of this tutorial.
{{</alert>}}

After that, we're going to check if our skinning worked properly by going to select Armature, then in Pose Mode moving first *root* and then *def_body* and see if ball works properly.
Note: I am resetting transforms fast by hitting <kbd>ALT</kbd>+<kbd>R</kbd> and <kbd>ALT</kbd>+<kbd>G</kbd> for rotation and transformation.
![Checking if skinning is working right](/gifs/ballrig_blender_5.gif "Checking if skinning is working right, we'll do it every time after skinning")

With that, we've done our first phase of making the **ball rig in blender**. Now, to keep you on your toes, please parent the *def_body* to *root* with offset., here's the fast guide in spoiler if you're not sure how to do it.

<details> 
  <summary> Click to reveal </summary>
   Go to edit mode

   Select def_body, then shift-click root
   
   Hit CTRL+P -> Parent With Offset
</details>

## 3. Making Squash & Stretch mechanism

As I've talked about what's the math behind the good squash and stretch ratio, blender comes with a pre-built constraint that is going to do the work for us. There are some advantages
of this, although personally I'd prefer rigging nodes like in Maya. 

The constraint I'm talking about is **Stretch To** that looks like this:
![Stretch To Constraint](/images/ballrig_blender_7.png "Screenshot of Stretch To from blender docs")

As I am not a fan of explaining perfectly created documentation, here's the link to [Stretch To Constraint](https://docs.blender.org/manual/en/latest/animation/constraints/tracking/stretch_to.html).
I am going to touch things, that we're really interested in:
- *Target* - it'll be the the "end" of our squash & stretch target
- *Maintain Volume* - it picks which axes should be affected to preserve the virtual volume stretching along Y axis.

Let's get back to our rig. We'll start by creating our **stretch mechanism*. To do that, we are going to copy our *def_body* bone, then select the tail and by resetting the
3D Cursor to World Origin move the tail to the new cursor position. But to do that, we are going to learn about **Bone Collections**.

![Bone Collection Menu](/images/ballrig_blender_8.png "Bone Collection Menu in Properties Tab")
You can think of *Bone Collections* like layers in any other software - in blender 4.0, developers actually revamped old system (which had 16 normal and 16 protected layers) and made
them actually unlimited. By using + button, we are going to add some layers and make it look like this:

![Filled Bone Collections with layers](/images/ballrig_blender_9.png "I've added five different layers that we're going to use for the whole tutorial")

The most important thing to understand here is that if we click a bone, and it has a dot near the name of the collection, then it's a part of the collection - and we can hide/unhide them. Be careful - you cant parent/unparent to bones that are actively hidden!

We're going to sort the bones we've created with the prefixes they added. 
![Adding bones to the right layers](/gifs/ballrig_blender_6.gif "Sorting out the bones to the right layers")

With that done, we can finally do the *mch_stretch* bone. Lets start with our sequence again: we are going to copy our *def_body* bone, then select the tail and by resetting the
3D Cursor to World Origin move the tail to the new cursor position.
![Stretching mch_stretch bone to it's proper place](/gifs/ballrig_blender_7.gif "Stretching mch_stretch to it's proper position")

Now, looking back to our control list, we need to add something, to control out stretch from both sides - to do that, we're going to need two controls,
but general cleaniness of rigging means that we are going to use **target** bones making our constraits separated between deformation skeleton that will follow our
target skeleton (tgt and sometimes mch), that will follow **control** bones which animators are going to move. You can think of it as something similar to Maya's *offset groups* which are used to make the controllers themselves at transform [0, 0, 0]. As always - we're going to build habits that will make us better riggers in the future.

We are going to extrude two bones on Z axis, one from bottom and one from top of the mch_stretch, we're also going to name them *tgt_stretch-top* and *tgt_stretch-bottom* and *Clear Parent*.
![Creating the tgt bones to control the stretch](/gifs/ballrig_blender_8.gif "Creating target bones for the stretch controlls, notice I am checking if the things separated properly")

Again, I am going to leave you some exercises. In the next step, we are going to assign proper bone collections and create a *tgt_body* and that will control *def_body*. Remember to uncheck deform! Besides that, we are going to copy *tgt_body* once more and call it *tgt_cog*

After we've done that, we should end up with a hierarchy like this:

```
root
    def_body
    mch_stretch
    tgt_stretch-top
    tgt_stretch-bottom
    tgt_cog
    tgt_body
```

Now, to explain how this ball's mechanism will work, we are going to do two things:
- Add stretchTo to *mch_stretch*
- parent things properly

And then we'll talk about **why** does it work like this.

Let's start by adding the constraint. To add them, we need to be in *Pose Mode*. You can add them by using <kbd>SHIFT</kbd>+<kbd>CTRL</kbd>+<kbd>C</kbd> or by going to *Properties*>*Bone Constraints*. We're going to pick *Armature* as our target and *tgt_stretch-top* as our bone target. After that, we can check if it works properly.
![Adding stretchTo constraint](/gifs/ballrig_blender_9.gif "We could also shift-click our target bone > bone we add constraint to to automatically select it")

After that we're going to parent our mechanism the proper way. Think of it that way:
- We want to move everything by tgt_cog, meaning it should be at the top of the hierarchy
- After that, we want our stretchers, to follow the cog, so they should be children of cog
- We want our mch_stretch to stretch in both ways by moving either contoller and not move the other one, which means that stretch needs to be a children of one of them - because our stretch works with tgt_stretch-top we don't need stretch to follow it, so we can freely make it a child of tgt_stretch-bottom
- We want to be able to keep rotation independent of the stretch, so it needs to happen after stretching - basically making the rotation happen AFTER, by making it a children

We end up with a hierarchy like this

```
root
    def_body
    tgt_cog
        tgt_stretch-top
        tgt_stretch-bottom
            mch_stretch
                tgt_body
```
![Making the parenting work](/gifs/ballrig_blender_10.gif "While it might be hard to remember how Parent actually works, think that it's always CHILDREN first being grabbed by PARENT at last")

## 4. Controls

We don't really want animators to touch our rig insides, so for the ease of all we are going to create controls for our rig - remember, we're rigging for somebody else - so we need to make rigs in a way clear enough that other people understand it as well. Because of that, in this sub-section I am going to talk about some conventions. 

To start, we need to make our mesh follow our target bones first. In this case, because we have only one deformation bone, it'll be super easy and I am going to let you do it yourself! 

The goal is to add a *Copy Transforms* constraint to *def_body* and select *tgt_body* as the target.

![def_body bone constraint menu](/images/ballrig_blender_10.png "It should look like this, if you can't select it - unhide def bone collection")

Now, we can look if every control works properly - we can disable all other bone collections

![Checking out if all target bones work properly](/gifs/ballrig_blender_11.gif "A quick look if we can do everything even if we disable other bones than target ones")

After a check, we are ready to create controls! Remember to get [Bone Widget](https://blenderdefender.gumroad.com/l/boneWidget) for this step.

We'll start by looking at different controls first and we are going to start with a **root control**. While in blender armature modifier creates a joint that we can use, 
it's always a good idea to create a control for your root bone, that will let you do some tricks like progressive walks (adding motion to root bone to mimic what game engine
does).

There are different shapes for root bones:

![Vayne Valorant Style Rig](/images/ballrig_blender_11.jpg "Vayne Rig by Matheus Lima @ artstation")
![Azri Style Rig](/images/ballrig_blender_12.jpg "AZRI Rig by popular autor Jonathan Cooper, author of GameAnim: Video Games Explained")
![Uncle Death Rig](/images/ballrig_blender_13.jpg "Uncle Death Rig for blender by Crabnuts (@Kani_Natto_), blender rig controls are generally lighter and less saturated")

As you see, there are few popular shapes and I'm sure that you've encountered even more - but mostly they are circular (sometimes squared) with or without arrows. In Bone Widget, we have an option to add one of two (Root 1, Root 2), and for the Vayne-styled one, we are going to create "Root 1".

To do that, first we need to create a copy bone of *root* and name it *ctrl_root* and add it to a proper bone collection. As controls are going to mimic our target bone hierarchy,
you can leave it unattended under Armature.

![Creating ctrl_root](/gifs/ballrig_blender_12.gif "We can easily leave it in hierarchy as we'll mimic target one")

Next, we are going to do switch to *Pose Mode* and hit <kbd>N</kbd>, to open the sidebar. By picking *Rig Tools*, we open up **Bone Widget** and select *Root 1* as the shape. Then we can click *Create*, to create the shape.
![Creating the shape](/gifs/ballrig_blender_13.gif)

After done that, I am going to give you a simple exercies - your task is to copy all target bones and rename them `ctrl_*` where * is the relative name. Remember, we don't need to copy MCH one. After that, we can parent it to mimic tgt bone hierarchy.

>
>That's also where the hack I've been talking about happens - **do not copy** *tgt_body*, we'll create a control from it (so you can move it to ctrl collection),
>because otherwise the rotation will break.
>

![Creating other ctrl bones](/gifs/ballrig_blender_14.gif "Remember to add them to collections afterwards")

To get more clarity, we are going to add copy transforms from *ctrl* bones to *tgt* ones, this time doing it faster, by shift clicking one after another like this
![Adding copy transform constraints](/gifs/ballrig_blender_15.gif "If you cant click the bone, you can always select it in outliner")

Let's now think about our other controls. We'll start by creating something for the *ctrl_cog* and *tgt_body*. A standad cog (and sometimes called hips) is some kind of a circle, and we'll go with that, we are going to create a smaller circle for the rotation. When you add a shape, you can also change it's shape by clicking *Edit* button, by doing that, I can easily re-size the controls.

![Creating cog and rotation controls](/gifs/ballrig_blender_16.gif "You can notice, that I've forgotten to add tgt_body to the right collection before and it didn't let me create shape because tgt was hidden")

Stretching controls can vary from rig to rig, but for the case of our rig, we are going to consider is as **auxilary controls** - which means that we need to create a shape, that'll
convey the idea behind what it does, so an animator can understand how to work with the rig. You can think of controls building kinda like designing UX for the animator - you want
to use marker - things, that by form, shape or color will subconsciously give an idea on how to work with your designed thing (for more about markers in design, you can check
*The Design of Everyday Things* by Donald Norman). 

For my markers, I've chosen pyramids - they are pointy on one side, so they can lead the eye to the center of the ball naturally making animator think that if he translates
the controller to the inside, something will happen. 

As we've learned how to do it, you can add them yourself, at the end it should like this

![Finished controlls](/images/ballrig_blender_14.png "If you select two bones, you can add the same shape at the same time!")

As you see, my pyramids are smaller and moved up, and you can achieve that either by using *Edit*, or by the menu that appears in the down left corner

![Add shape menu](/images/ballrig_blender_15.png)

When you've experience enough rigs, you start to see that colors in rigging are usually the same no matter who creates them. While I was researching the history of them, I've
established my own control scheme that I am going to pass down for you:

- Left side controls are <span style="color:red"> RED </span>
- Right side controls are <span style="color: #209DFF"> BLUE </span>
- Middle side controls are <span style="color: green"> GREEN </span>
- Auxilary controls are <span style="color:yellow"> YELLOW </span>

We can change our controls colors in *Bone*>*Viewport Display*. I usually change them to a custom color theme and use the button next to it, to copy them to other controlls (the object you are copying from is LAST), let's try it by adding yellow color to rotation and stretch controllers. We're going to select *ctrl_stretch-top* and add a custom color theme under their Viewport Display tab, set them up to YELLOW, and then by selecting rest of the control hit the double arrow button.

![Adding yellow colors to the controllers](/gifs/ballrig_blender_17.gif "Blender uses a specific setup where you give 3 colors -  Regular / Select / Active")

As you know how to add controls, let's wrap this up, by adding colors to the rest of controllers. You should end up with this:

![Finished controlls rig](/images/ballrig_blender_16.png "We've almost done!")

## 5. Clean up & final touches

So, we've finally created everything, we could start animating right away!

<span style="color:red" size ="16"> WRONG! </span>

I've told you at the start that mess is going to be a pain in the ass, so let's do final cleaning up.

We'll start with Armature Tab - we can finally check off *Names*, *In Front* and *Axes* tab - animators don't really need them and if they need to have controls in front, they'll set them up.

![Rig without names](/images/ballrig_blender_17.png "Your rig should look like this")

The last thing we should think about is locking up some transforms - I am generally against limiting animators choices, but there are some things we can do, to help animators
in their work. 

We'll start with stretch controllers - while animator can use Transform (location), adding rotation or scale is only going to rotate the control, without any real consequences - 
we can lock it, so he can work with just pressing <kbd>G</kbd> to control the stretch.
![Locking stretches](/gifs/ballrig_blender_18.gif "You can hold LMB and drag to lock more than one thing at a time")

After that lets think about our rotation control - we don't really need the scale, so it should be locked. Rotation is the main thing so it should be open, but what about location?
I'd say tha there are two schools when it comes to that. First school would lock it out (because the control isn't to do that), but I believe it's better to leave it open - 
animators are going to see if they would add a keyframe to the wrong controller and fix it themselves, but sometimes they might need to detach the translation to two different bones
and this setup will let them. Sadly, it can break our squash & stretch - I'll leave it to your call, but for my example I am not going to lock it.

When it comes to cog, it's the main control which animators are going to move the mesh with, so location and rotation should be open, as far as scale goes - I'm going to lock it to 
avoid bugs.

And lastly the root control - of course location and rotation should be unlocked. As far as scale goes - with our setup (of making the hierarchy the same) user can easily scale the
root to achieve bigger balls - as controls are going to scale too and the rig will work! Of course it's not always the case with rigging and sometimes you'll need to plan if a rig
should be scalable or not and you'll have to create the controls appropriately.

With that we've finally finished our rig! You can start learning animation right away with your own, self-rigged ball! 
Good luck in your animation journey and if you decide to share your ball animation, I'll be happy to be tagged (@arahfx) to see what you created!

## 6. Closing Thoughts

Congratulations on rigging your first, fully working **ball rig**! Now, you can start your animation journey by tackling bouncing ball exercises.
Besides that we've now have idea on how to **plan our controls** and **name them properly**, which will be super handy later.

As you are probably as happy as me, I am not going to hold you any longer - after you master *the ball*, the animation world will be your oyster!
