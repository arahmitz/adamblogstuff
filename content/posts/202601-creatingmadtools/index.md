---
title: "madTools v1.0.0 released"
date: 2026-01-15
draft: false
description: "Released my first set of tools!"
tags: ["reflections", "tools", "maya", "python"]
showHero: false
---

## The Why

I've always wanted to have my own tools.

When I startd my animation journey back in 2022, I was downloading a lot of scripts made by different people - awesome tools like [Awesome Lights](https://doomsquid.com/tools/2022/6/5/download-awesomelights) for better looking playblasts,
[Universal IK FK Match](https://monikayellow.gumroad.com/l/srTEI) to... match IK/FK chains, or [ml_convertRotationOrder](http://morganloomis.com/tool/ml_convertRotationOrder/) to help with gimbal locks.

I remember discovering that last one through a video and navigating to Morgan Loomis' [website](http://morganloomis.com/). It was so cool to see someone with a whole page dedicating to their own tool package. It really inspired me to lean more
into the technical side of the animation pipeline.

This winter, while attending [Rigging Dojo](/posts/202509-riggingdojoenroll), I went deep into Maya again - and quickly onticed how much time I wasted clicking through nested menus just to freeze transforms, select hierarchy or delete history - the
essential parts of Maya's rigging workflow.
![Maya's space menu going through Edit -> Delete type -> History](/images/madtoolspost/madtools_maya.jpg "To get here you need to click <kbd>Space</kbd> -> `Edit` -> `Delete by Type` -> `History` or remember a **3 button** combination.")

Sure, you can repeat the last action wth <kbd>G</kbd> or click **MMB** on the category, but when juggling different operations - these options no longer work. Watching the course materials, I saw mentors using custom scripts and shelf tools constantly.
I was amazed by one skeleton-building material, where the teacher built an entire skeleton working with viewport and Script Editor only - pure awesomeness. I knew I wanted to reach that level someday.

With two free weeks after New Year, I decided to commit: learn the Maya APi properly, polish my python skills, try out PySide2, and finally build my first toolbox.

##  The Process

One of the first things I had to wrestle with was the Maya API itself. The way MEL commands are wrapped feels very different from what one migh've been used to in blender or when using python in general.

For example, instead of calling a dedicated function to retrieve a value, you call the main command and pass a query argument: `q=True`. With my limited programming experience, that approach felt very strange at first. I can't say that it's wrong - but it amde me rethink how I undestand function design in general.

At the same time, I knew I didn't just want a pile of scripts. I wanted my first toolbox to be modular, ideally, someone could download even the smallest module if they found it useful.

That meant learning how to properly structure files - separating tools, utilities, what parts can adn cannot share logic, so I could import and export only what was needed. It took some experimentation to get right, but I feel that it was crucial if I
wanted this toolbox to stay clean and maintainable in the future.

![madTools folder structure](/images/madtoolspost/madtools_structure.jpg "Each tool is a located in a `tools` folder, some of them are using `utils`, which hold utility commands like `get_selection`. Recording uses more advanced v1.1")

## The Tools

Since I'm still learning my way around Python and tool development in general, I decided to start with something practical: macroing up repetitive nested actions.

The first batch of tools were simple wrappers around Maya commands - so the user can one-click `Freeze Transforms`, `Delete History` or `Toggle Local Rotation Axis` - functions that you can easily achieve, but need more clicks. This gave me
small wins, but immediate workflow improvements.

As I gained Confidence, I started expanding the complexity. `Create Joints` began as a very simple script that generated a 3 joint chain. Over time, I expanded it: first, you could change the joint name, later you could also add *_end* at the end joint
and finally - you could customize the affix to help with left/right setups. What started as a tiny helper became something really usefull for building fingers and cloth chains quickly.

![madTools Create Joints tool usage](/gifs/madtoolspost/madtools_createjoints.gif "With the advanced options, the tool can really speed up finger/cloth joint creation")

When I moved into an actually project to test the toolbox, new needs appeared. I had to rebuild and adjust skeleton placements a few times, which meant recreating keyframes for the ROM animation again and again. In this specific skeleton, with a 10f between keyframes, I had to cover around 1000 frames! Is it difficult? Of course not. Did it take time? **YES**. 

That's when I built first version of `Make ROM`.

The idea was simple: set the time start and end, select the hierarchy and hit the button. The tool adds a keyframe each 10f on every bone in the hierarchy for the visible range. As I started testing it, I've quickly found out that I need to also save previous
values and floor/ceil the values to the nearest 10-increment - it was great. More importantly tho, it proved that adding a new functionality to the toolbox was fast & manageable.

![madTools Make ROM tool usage](/gifs/madtoolspost/madtools_makerom.gif "This way you can easily setup keys on your whole hierarchy and use <- and -> arrows to add the motion fast")


What I am most proud of is the **installation process**.

Tools exist to serve users, so installation has to be effortless. From the beginning, I wanted it to be **drag & drop**. It's common for more advanced tools you can find over the internet, so the users are probably expecting it at that point - at least I did.
Implementing it correctly took some experimentation - Maya does the heavy lifting by executing python files dropped into viewport automatically, but proper setting up shelves, commands, and especially icons required extra work.

Icons were probably the trickiest part there. The idea was that user downloads the `madtools` folder and put it in `/scripts` folder and everything happens from there. The problem is that Maya don't want to look for icons in there: it prefers to use the
pre-created folder in `/prefs`. Getting that to work consistently required some trial and error with `os` module and string operations to properly create and maintain new file paths.

To help with the UX of the shelf tools I decided to color-code the icons by functions for better visual recognition. The UI isn't the pinnacle of UX design (yet), but it's something I use every single day - proving it's not using antipatterns (as I'd
probably be frustrated enough to change it at this point).

![madTools shelf representation](/images/madtoolspost/current_toolbox.png "Shelf toolbox for madTools v1.1.0")
![madTools UI representation](/images/madtoolspost/toolbox_ui.png "UI for madTools v1.1.0, the buttons are also sorted by their functions and pairs")

## Takeaways

Even after finishing the first version of the toolbox, I quickly realized there are still actions I need to script out properly to make my life easier - looking at you `Match Transforms` and `Move Values to Offset Parent Matrix`.

What mattered the most to me was testing `madTools v1.0.0` immedietly in a real rigging project. That decision really made all the difference - and as you can see on github it quickly turned it onto `v1.1.0`. Using the tools in production-like conditions
exposed all weak spots and new needs. That's how features for `Create Joints` expanded and how `Make ROM` came to life. Before this project, I just pushed through tedious actions, now I know **I can** automate them and make my
(and my artists and animators) life easier.

`madTools` are still evolving. I keep refining it as new problems appear. But even in its current state, it has already make my workflow smoother, faster, and more intentional.

## Closing Thoughts

Using a toolbox that I built myself is a deeply satisfying feeling. I'm glad I decided to dive into python last year and that I've finally tried creating something in PySide2 myself. It already helps me in my daily work and I hope it can help other people too.

More importantly, it gave me confidence. Not just in scripting, but in understanding what's happening under Maya's hood and how much control is actually possible once you start building your own solutions. This is yet another case 
of [having a TD mindset](/posts/202601-riggingdojofinish).

It also turned out to be a perfect stepping stone before tackling my next goal: building a basic auto-rigger from scratch.