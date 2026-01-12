---
title: "Rigging Dojo Character 101 Postmortem - Thinking like a TD"
date: 2026-01-12
draft: false
description: "My reflections on Rigging Dojo's Character Rigging 101 course and lessons that shaped my TD mindset"
tags: ["Rigging", "Reflections", "Personal", "Course", "TD"]
---
{{< lead >}}
"TD Mindset is all about finding answers to problems, not knowing everything."
{{< /lead >}}

## A Little Recap

Winter 2025 was a really busy season. At work, we were pushing to release a [big update to Forever Skies](https://store.steampowered.com/news/app/1641960?emclan=103582791471296854&emgid=521984509558653240), and in 
October I've attended Game Industry Conference 2025 in Poznań, Poland where I held [first Animatorowisko Animation Meetup](/posts/202510-animatorsmeetup)

Since September, I've [been training](/posts/202509-riggingdojoenroll) at Rigging Dojo in their *Character Rigging 101* course, strengthening my fundamentas as I increasingly
focus on the technical side of the animation pipeline. The course wasn't really about finishing a polished rig from start to finish - it was about experimenting,
testing, and building the problem-solving mindset of a TD.

## Expectation vs Reality

Before the course, I knew I understood what ecloses the rigging pipeline in general, but I felt like there were gaps I wanted to fix - especially when it comes to good, quality skinning.
After spending last two and a half years in Blender, I wasn't so sure I remember the Maya workflows as well as I'd like. Due to that, I was ready to dedicate serious free time - 
I've planned my Rigging Dojo attendance since around May 2025, so - I've had a few months to make plans to slot it to my calendar properly. 

I wasn't sure what to expect. I knew that this was so-called *Animation Mentor for riggers*, I knew I'll learn a lot, but I only had the general outline & the name indicating
we'll start from scratch.

The reality is that this course **is not hand-holdy at all** - and that's a very good thing! Let me copy-paste from my enrolling post what is (IMO) the most important quote from the whole course: 
>
> This course is not only to teach you **how to rig**, it is as much here to teach you **how to learn about rigging**. 
> 
> --<cite> Brad Clark, Rigging Dojo's Character Rigging 101 Mentor </cite>
>
And that's really the truth about ths course. Each week had a topic in regarding to rigging process, theory (both written & video-based) and exercises. During the course,
we were expected to work on our rigs. I've got the mesh lended by talented [Axel Bossard](https://www.artstation.com/axelbossard) of this awesome Geralt, THANK YOU!"
![Geralt of Rivia by Axel Bossard](/images/riggingdojofinish/geralt.png "Geralt of Rivia Fan Art by Axel Bossard, artstation: https://www.artstation.com/artwork/0lVExY")

While this is a beautiful model with a good topology, it still posed a challange. As Brad said - the model itself is good, but there are lots of parts that are going to be
tough to work with, so the entry bar is just set higher. With his guidance, I was able to push through and discover techniques that opened new ways of thinking about rigging.

## Slowing Down & Facing Weak Spots

My biggest weak spot in the rigging process was skinning - I always dreaded it. Before the course I just thought that it makes no sense, is very hard to do and I just suck at it. I thought,
that we'll just do reps on that and it's only about practice. In reality, I've learned that everything that sums up to skinning is much more nuanced:

- Many of the meshes I'd use before werent properly prepared for rigging - and that can make skinning unnecessarily hard.
- The thing I was missing wasn't the "painting" skill - it was techniques like simplifying shapes and weight transfering them.
- I thought I understood anatomy okay-ish, but exercises like drawing skeletons & muscles over references revealed gaps in applied knowledge.
- Not everything is fixable by "better weight painting". You absolutely needs supporting joints & blendshapes to make things look *right*.

![Geralt of Rivia RIG skinning 1st pass](/images/riggingdojofinish/skinning_bend_1stpass.png "1st pass of chest bend")
![Geralt of Rivia RIG skinning last pass](/images/riggingdojofinish/skinning_bend_end.png "What I ended up with")

This course forced me to slow down and confront these issues head-on. I've struggled a lot when it comes to skinning and I still do, but the biggest difference is
that I've started the course with dread of skinning and now I actuallly enjoy the skinning & deformation - I'd say that as of now, it's probably the most interesting
part of rigging for me. It became something meditative: I can put on music or a podcast and focus, layer by layer, refining the deformations with a properly done **ROM** (that was actually very helpful too).

It wasn't just about the result - it was about the process and **thinking like a TD**: testing, iterating and **solving problems - methodically**.

## The A-ha moment & Key Decisions

The last two weeks of the course were the most pivotal. After preparing the mesh, creating the basic skeleton definition & setting up basic FK system - mostly to show how we thing about animator's UX - we had a choice
between two path to focus rest of our time on:

1. Focus on skinning - explore blendshapes, corrective joints, work more with NGSkinTools
2. Focus on IK setups and system blendng

IK setups seem to be relatively standardized. Every tutorial I ever watched seemed to follow the same or very similar practices and that have been consistend for decades. There's a talk about [Character Rigging Best Practices](https://gdcvault.com/play/1022920/Character-Rigging-Best) from **GDC 2006!**, and the same principle still agree. In general, seems like most of the rigging we do - from tools to principles - seem to be relatively consistent across all these years - I wonder if that's because
after all rigging is a support role to animators and when they're comfortable in a workflow, they seem to rarely want to change it.

I felt like the real difference in modern rigs lie in deformation & skinning techniques - that's something that expanded with beefier gaming setups & new engines.

That's why I've choosen skinning deliberately. It was both my weakest area, and the place where I could make the biggest leaps in understanding. I didn't finish my skinning completely during the course, but that's okay - as
far as I understand - it was even expected of us to **never finish** it during the course. What I really gained is clarity. **I now know exactly what steps to take next**, which tools should & techniques should I use and how to reason through
many tricky areas like armpits and shoulders:

I believe this was **the** key TD lesson: it's not really about finishing a rig perfectly in one go, but about developing a **problem-solving mindset** (which from now on I engraved into my brain as TD mindset) - 
knowing how to break down challanges, and understanding where to focus effort for the most impact.

## Growing pains

Not all the difficulty came from skinning alone. One of the toughest weeks for me was the **math-heavy understanding of Maya Nodes** and what is happening under the hood of this software.

Look, I'm not totally clueless when it comes to maths - I'd say I rather enjoy it. I also did my Algebra I at University, but this is probably one of the first experiences where I could "touch" what I was learning back then
(and see how much I forgot due to not using it!).

Matrix-bassed riggign concepts are everywhere now, I feel like all my social media focused on that back when I was reading all the theory - and I believe it's really important to understand how the math works under the hood so
you can make it useful later. It's not about memorizing formulas (thanks, school!), but really internalizing how tranforms propagate, what a hierarchy really is and what a **bone** even is. Those concepts were challenging because
you can't see the progress immediately, but they were crucial to understanding rings (and space switching for example) at a depeer level.

On the skinning side, tricky areas like the shoulder-arm-chest triangle reminded me that some problems are always going to be hard. No amount of shortcutting could bypass these challenges: it's just *patience* -> *iteration* -> *observation* -> *repeat*.

![Geralt of Rivia RIG skinning 1st pass](/images/riggingdojofinish/skinning_armpit_1stpass.png "Clavicle and arm rotation took some layering and helper passes to fix")
![Geralt of Rivia RIG skinning last pass](/images/riggingdojofinish/skinning_armpit_end.png "Proper guidance and techniques make it possible!")

Overall, I felt like the workload was heavy, but motivating rather than discouraging. Every thing that broke, process that failed, tool that I've used incorrectly reinforced the **TD mindset**: *the skill lies not in knowing everything,
but in learning how to solve the unknown*.

## New Respect for Known Rigs

One of the most rewarding outcomes wasn't just the hand-skills I acquired, it is how I now look at rigs - both my old work & all the rigs I've learned how to animate on.

Looking back at my older rigs - I'm gentler on myself. I see that many limitations weren't solely my fault - *meshes*, *pipeline constraints*, *missing contexts* - they all played a role in the effect.

At the same time, my respect for well-crafted rig has only deepened. You can probably think on a few(or more) "known" rigs that everyone uses to learn animation on - talking of all the **AZRI**'s (by the way Sol - I'm a huge fan of the work done here!!!)
that students use. These rigs are all full of tiny, deliberate decisions that made them work s-e-a-m-l-e-s-s-l-y. I always knew these were high quality, but I feel like I never fully grasped **how much though, iteration and problem solving** it takes to
reach that level of polish.

Once again, let's repeat - TD Mindset: rigs are more than just technical constructions: they are a list of solutions to many complex problems. The difference between *good-enough* and *well-crafted* rig often comes down to thoughtful problem-solving, 
adaptability and knowing where to focus attention to.

## Is this course for you?

Rigging Dojo Character Rigging 101 is **not a course for portfolio pieces**. Period. The course isn't designed for you to be hand-held to create a polished rig from start to finish, like in a factory. Brad, our mentor, often said:
>
> You're going to struggle. It's normal, that's how this course is designed. By struggle, you will learn.
> 
> --<cite> Brad Clark, Rigging Dojo's Character Rigging 101 Mentor </cite>
>
And believe me - you're going to struggle. You'll feel stuck. You'll feel frustrated. You'll feel like it's not doable. I know I did - and I'm grateful a great mentor had my back in these times.


As this course is about **learning how to learn rigging**, you'll going to be experimenting, breaking things safely, testing the ideas and pushing your boundaries. It's ideal for anyone who want's to:
- Build a strong foundation in problem-solving
- Exploe new rigging techniques in a guided environment
- Develop judgement & adaptability in the context of a real pipeline

It's less suitable for those seeking step-by-step instructions - but I'd argue that around 50% or rigging isn't step-by-step at all - after all it's case-by-case basis.

One unexpected takeaway was inspiration to **push my coding skills & create my own tools**. My whole idea of becoming a Technical Animator developed back when I was still studying animation - I was looking for some tools to help me with 
gimbal locks and I've found [Morgan Loomis](http://morganloomis.com/tools/)'s page with his **awesome** *ml_convertRotationOrder*. I was super hyped by someone (Come on, a Rigging Supervisor at this point) having their own set of tools
they've let everyone else used. I wanted to have something like this too and I planned that one day I'll have my own tool at my personal page... (that's actually a reason why you can read this post!). 

Some of the course materials had awesome TDs either creating basic things on the fly with MEL and PyMEL in Script Editor or straight up launching their own tools that they've built - not as optional extras, but as a natural
extensions of problem-solving. With so many things I was doing taking many (2-3+) clicks in Maya, I've actually started noting everything that was uncomfortable to use so in the future I can start building my own shelf of tools and workflows.
This is yet another aspect of TD mindset: identifying opportunities to **improve efficiency and control through smart tooling**, not just learning techniques. 

Basically: if you do something more than 3 times a day, automate it somehow - that's going to be my next goal.

## TD Mindset & Closing Reflections

If there's one thing Rigging Dojo Character Rigging 101 taught me, it'd be this:

>
> "TD mindset is all about finding answers to problems, not knowing everything"
>

The course wasn't about memorizing workflows or finishing with a perfect rig. It was about **thinking critically, experimenting, failing and solving problems - efficiently**. Every challange - from tricky skinning areas, through 
controller mirroring with proper LRAs, to matrix-based riggign concepts - pushed me to approach the unknowns with curiosity, persistence and adaptability.

For me, the biggest shift isn't just in technical skill. It's in **how I approach rigging now**:
- I' much more patient with myself
- I have a deep respect for every tiny, deliberate decisions on rigs I adore
- I actively think about how tools and workflows can extend my problem-solving muscle
- I approach challenges as opportunities to learn -> iterate -> improve

Rigging Dojo didn't just strengthen my fundamentals - it changed the way *I think* - as a **TD**. That mindset is something I'll carry forward int oevery rig, tool and problem I'll tackle in the future.

![Gif of Geralt RIG shoulderpad moving with arm](/gifs/riggingdojofinish/skinning_shoulderpad.gif "And there are always new stuff to work on and test!")