---
title: "madTools v1.0.0 released"
date: 2026-01-15
draft: true
description: "Released my first set of tools!"
tags: ["reflections", "tools", "maya", "python"]
showHero: false
---
## 1. The reason why

I've always wanted to have my own tools. When I started my animation journey in 2022, I was downloading a lot of tools made by different people - awesome scripts like [Awesome Lights](https://doomsquid.com/tools/2022/6/5/download-awesomelights) - to help with nice looking playblasts, [Universal IK FK Match](https://monikayellow.gumroad.com/l/srTEI) to... match IK-FK or [ml_convertRotationOrder](http://morganloomis.com/tool/ml_convertRotationOrder/). 

I remember learning about the last one from a video and navigating to Morgan Loomis' [website](http://morganloomis.com/). It was so cool that someone had a whole page of their own tools and it really inspired me to go into the technical part of the animation pipeline. 

As I've been attending [Rigging Dojo](/posts/202509-riggingdojoenroll) in the winter, I've went deep in Maya (again), I noticed how much time I spent clicking through multiple nested menus just to freeze transforms, select hierachy or delete history
off the object - which is pretty important in Maya's rigging way.
![Maya's space menu going through Edit -> Delete type -> History](/images/madtoolspost/madtools_maya.jpg "To get here you need to click <kbd>Space</kbd> -> `Edit` -> `Delete by Type` -> `History` or remember a **3 button** combination.")
Sure you can repeat the last action with <kbd>G</kbd> or clicking **MMB** on category, but it still felt slow when juggling different options. Watching RG materials, I saw all these scripts and shelf tools mentors were using - one mentor in particular built almost whole skeleton using Script Editor and MEL only - it looked so amaizing I wanted to be on that level someday too. 

With two free weeks after *New Year*, I decided to dive in: to learn the API, polish my python skills, try out PySide 2, and finally - create my first toolset.

## 2. Learning and Discovery 

One of the first thing I had to tackle with was Maya API itself - the way MEL commands are wrapped is really different from what you might be used to in blender or when learning python in general. For example to get a value of something, instead of using
a proper function, you'd call the main function and use an argument of `q=True`, which turns the function into a query mode. With my limited programming experience - that part was something really new for me. Besides that, I really wanted the tools to
be as modular as possible - so anyone can download even the smallest module if they find it useful. To do that, I had to figure way the **proper** way of structuring the tools and modules, so I can import and export only the things I needed - but it was 
crucial to ensure the toolbox stays organised and reusable. 

![madTools folder structure](/images/madtoolspost/madtools_structure.jpg "Each tool is a located in a `tools` folder, some of them are using `utils`, which hold utility commands like `get_selection`. Recording uses more advanced v1.1")

## 3. Tools

As I am still learning my way around python and tooldev, I wanted to focus on build a toolbox that is going to speed up repetitive actions - for example by wrapping nested commands into a single button click - things like `Freeze Transforms`, `Delete History` or `Toggle Local Rotation Axis`. As I've built the easy ones, I also started to expand on the complexity. `Create Joints` started as a simple tool that created 3-joint chains, but as I got more comfortable I've decided to expand it - user can define the name, affix and if they want to get a *_end* at the end.
![madTools Create Joints tool usage](/gifs/madtoolspost/madtools_createjoints.gif "With the advanced options, the tool can really speed up finger/cloth joint creation")

When I started a rigging project to test the tools - I found a need to redo the ROM keyframes many times, because I've been deleting and changing joint placements. In this case, the skeleton needed around 1000 frames for every bone, making it a tedious task. It was a great time to test how easily can I add a new tool to the toolbox. The idea is simple: select the skeleton, keyframe each ten frames for the whole visible range. It also saves old values and rounds up to the nearest 10 for clean animation.
![madTools Make ROM tool usage](/gifs/madtoolspost/madtools_makerom.gif "This way you can easily setup keys on your whole hierarchy and use <- and -> arrows to add the motion fast")


What I am most proud of, though is the install process. Tools are here to serve the users, and the easier it is to install, the better. That's why I wanted the to be drag&drop install from the start. While it's not uncommon (I'd say it's 
common for any good tool in Maya), the process itself can be a little tricky. Maya does the biggest heavy lifting by itself: it auto executes the script when it's dropped on the viewport, developer just needs to create a button (or a shelf with buttons), 
populate it with proper commands and icons. Icons were the key - I had to find a way to reliably copy the files from */scripts* folder to */prefs* folder, where Maya looks for icons, and it took me some trial and error with *os* module. 

I've also decided to color-code the tools with their functions for the better recognizabilty. I am really happy about the UI too - it's not the pinnacle of UX design, but it's something I really use everyday and it makes my workflow much more smoother.
![madTools shelf representation](/images/madtoolspost/current_toolbox.png "Shelf toolbox for madTools v1.1.0")
![madTools UI representation](/images/madtoolspost/toolbox_ui.png "UI for madTools v1.1.0, the buttons are also sorted by their functions and pairs")

## 4. Takeaways

Even after creating the first set of tools, I know there are more actions that I need to script properly to make it faster - looking at you, `Match Transforms` and `Offset Parent Matrix values`. It was really important that the moment 
I finished the `madTools v1.0.0`, I jumped straight into a rigging project to test them in real scenarios. That led to improvements, like the second input for `Create Joints` or creating the `Make ROM`. It's still an evolving project
that I continue to refine as new needs come up, but I am very happy that it made my workflow faster and more flexible.

## 5. Closing Thoughts

Using a toolbox that you created is an awesome feeling and I am really happy that I decided to dive deep into python, PySide2 and Maya API as it already made my rigging workflow smoother. It has also given me much more confidence in my scripting skills and understandment of what's happening under the Maya's hood. It was also a nice exercise before working on a basic auto-rigger - that is my next big plan.