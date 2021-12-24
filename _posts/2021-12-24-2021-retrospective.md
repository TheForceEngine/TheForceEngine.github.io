---
layout: post
title: 2021 Retrospective and 2022 Plans
---
## Version 1.0 Release Delayed
This is obvious by now, but **The Force Engine** version 1.0 will not hit this year. There has been a lot of progress towards completing the iMuse reverse-engineering work for version 0.9, but that will spill into early January.

## 2022 Plans
The iMuse work is roughly 70% complete, which means that version 0.9 is expected to land in the second week of Janurary. At that point, Dark Forces support in TFE will be *feature complete* and the reverse-engineering process for Dark Forces will be finished. The following few weeks will be dedicated to bug and inaccuracy fixing, with version 1.0 planned for late Janurary or early Feburary.

Feburary will be spent finishing the **GPU Renderer**, which will handle looking up and down with proper perspective by default - though the shearing effect will be available. The initial release of the renderer will only allow for palette emulation with true color options and other effects coming later.  I will talk more about the GPU renderer in a future post. In short it will allow for much better performance when running at high resolutions and refresh rates but maintain the proper look, including the way objects sort with the floor and ceiling, the way they sort with walls, the way portals enable "non-euclidean" geometry in some cases. At this point, the voxel code will also make its way into the master branch, finally properly adding voxel support.

March will see the release of an early version of the built-in level editor and other asset tools, including some initial basic support for voxel replacements. These tools will be expanded even further when working on Outlaws, including support for Outlaws engine enhancements and non-vanilla Dark Forces mods using those enhancements. Finally there will be smaller quality of life enhancements, and bug fixes. Early March will also be spent working towards the Mac and Linux release, with the help of **gilmorem560** (Matthew Gilmore) and others.

Finally, once the Mac and Linux ports are working and the initial tools have been released it will be time to focusing on adding Outlaws support to TFE. Like I mentioned previously, this will include adding support for Outlaws Jedi enhancements to the level editor and support for Outlaws formats in the asset tools.

## 2021 Retrospective
I thought it would be interesting to look back at the 2021, in terms of TFE, and see how far we have come.

Early 2021 saw just a few commits to master. There were some improvements to the perspective correct 3DO texturing code. This feature, while it looked great, was not moved into the final code for performance reasons. There were also a few experiments with scripting, though mainly for future work.

The main focus at this point, however, was the reverse-engineering work. At this point I was working in two locations - a branch of the main TFE code base, and the "code document" where the raw reverse-engineered code lived before being refactored and cleaned up for TFE.

### Breaking Everything
TFE had existed in this strange state for some time where things seemed to be working fairly well but most of the code placeholder. I had originally written a sector renderer based on what was known about the Dark Forces formats. I had an INF system built based on my existing understanding. But none of it was "real". It was there so things could be tested, and initial tools could be built.

At this point, it was time for it to become "real" and, so, in early Feburary I ripped out the renderer, the INF system, the previous object system and initial scripting support - breaking everything.

### The INF System
With the old code gone, I had to spend some time to get things compiling again. During this period there was no rendering, but I could test things through the debugger. In mid to late Feburary, I stubbed out the Dark Forces sound system and started integrating the INF code I had previously reverse-engineered. The reverse-engineering process was not yet complete, in terms of INF, but the larger structure was there and I could finally compile and start testing the code.

During this process, I found that the INF system also touched a lot of level data, so I begun stubbing out those interactions. Late Feburary saw those sector functions getting integrated and becoming "real."

### Gap
Between late Feburary and late March, there is a gap of about 1 month. Here I was focused purely on reverse-engineering the code, filling in missing pieces of the INF system, level loading, the renderer, and more.

### Level Loading
The last few days of March was spent porting all of the reverse-engineered Dark Forces level loading code to TFE. This meant moving code to the correct locations, such as moving code out of the INF system involving sector functions. During this phase I split out the "level data" from the renderer, INF system, and collision system. I had previously reverse-engineered the sector renderer, and it had been accessible in TFE using the command line, but making it "real" - hooking it up correctly - meant finding code I missed and correcting past mistakes.

Reverse-engineering the INF system was a massive undertaking. And I wasn't done yet. Early April would show how much work was left digging through the INF code in Dark Forces, merging the new code into TFE and fixing a seemingly never ending stream of INF bugs and issues. 

### Gameplay
By mid-April I had branched out to the game code. Mid-April saw the integration of the player inventory, which originally had pieces in the INF system since it needed them to be stubbed out (keys and the like). April would see the introduction of the logic system, though there was still a lot more to figure out here. The player finally got its own file and the game code started to take shape. At this point the way that Dark Forces handled timing became much more clear and now the game ran at the correct speed. Mid April to mid May were dedicated to reverse-engineering the gameplay code in prepration for what was to come. But there was little activity in the TFE branch.

### Collision Detection
Mid to late May was spent integrating the reverse-engineered collision detection code from Dark Forces. So far I have spoken about "moving code" and integrating as if it is a one way process. It is not. As reverse-engineered code is integrated, it needs a place to live. Because I don't have access to the original files, function names, variable names, structure or member names during this process - in my "code document" it all lives together as a mass of code. As I integrate it into TFE, I have to figure out how to organize the files and integrate the code with already existing code. Then I see what I missed, what parts I forgot to reverse-engineer, or mistakes I made. Then I would go back to the "code document" and original game and then work through my mistakes or missing code.

### Hit Effects and Projectiles
During this period the Hit Effects system was also integrated - this is the system that allows projectiles and other systems to spawn animated effects on hit. It handles explosions, "puffs" as projectiles hit, splashes when objects hit water. The other side of this was the projectile system, which responsible for spawning projectiles, updating them, handling collision detection, and then spawning hit effects. Projectiles get an update callback which gets assigned when they are created. This allows thermal detonators to arc, mines to falls, and updates blaster bolts as they move. In late May the Sound System was finally fully stubbed out and the API took shape.

### Logics and Pickups
In April there was some initial work with object logics and this work continued in June. During this period the animation logic was added, which allows objects like the shield pickups to animate. The projectile logic function fully formed, connecting projectiles to the logic system. Mid-June I finally factored out the object/INF messaging system from the INF system. Originally I thought it was an INF feature since a lot of INF interactions are done by passaging messages to sectors, lines, and triggers. But it turns out the system is also used to pass messages to objects.

Late June saw the integrating of the "pickup" update function, which meant it was now possible for the player to pick up objects, such as ammo and shields.

### The Task System and Game Loop
During the previous few months of work, it was becoming increasingly clear that game behavior was too dependent on the original "task system" for me to ignore it. It was, at this point - now July - that I began the *very painful* task of reverse-engineering and integrating the task system. Late July saw the introduction of the main game entry point - "darkForcesMain". This was using the new "game system" that will allow TFE to run different games. This month saw a massive refactoring to use the proper reverse-engineered game loop. By the end of July the core game loop was taking shape.

The two thirds of August was mostly spent reverse-engineering more game code but also saw the file searching abstracted to make file handling simpler and to handle mods. But towards the end, there was a massive amount of code integrated into TFE. This included a lot more refactoring, moving Jedi related code TFE_Jedi/, converting the various engine-level namespaces to TFE_Jedi, cleaning up the Jedi Renderer.

Towards the end of August saw a lot of work integrating HUD code, including off-screen buffers that Dark Forces uses while updating the HUD to avoid redrawing all of the HUD elements every frame, moving over more Jedi memory management code to make porting reverse-engineered code easier, starting to properly load data and startup various systems and finishing up the Dark Forces game startup.

The end of August saw the player controller integrated, as well as initial weapon code. The automap was also integrated. I also spent the time converting many systems back to tasks, which continued to have issues. At this point, level loading was finished, object in sector assignment issues were fixed and the level loading screen was displayed. Some of the AI code was integrated, though there was still a lot of work to do here.

### Core Game Loop
During September the core game loop started really coming together. The code was switched to using the original sin/cos tables, which fixed various rendering issues with the Automap, palette based effects were integrated, the HUD code was fully integrated and displayed properly. The classic renderer, reverse-engineered many months prior, was finally properly hooked up. It was finally "real." I could see again - after almost 7 months of most of the game not displaying, because the data was not in place and the renderer not hooked up - there was light.

![](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/IntegrationWork1.jpg?raw)

With so much reverse-engineering work already done and all of the main systems coming online, things started to move quickly from here on out. 

Early September saw the cheats being mostly finished, the general "mission controls" working, meaning the automap could be properly toggled, the headlamp worked, and various other features. Weapon drawing and animation was integrated. Player controls were then integrated, and then player physics and collision. Finally the rest of the Player controller was finished. On September 12th, I posted the "TFE Core Game Loop Release Preview" video - just days after hooking up the renderer again.

The player weapon system was integrated at this point, but the individual weapon fire functions still needed the be reverse-engineered and brought over. On the 14th the fist was itegrated, which led to fixing various bugs. At this point, I moved everything to using the TFE allocator system, so that levels could be flushed and reloaded. On the 15th the Mortar was integrated. The 16th and 17th saw the other weapons also integrated, as the general patterns became more clear.

On the 17th, after getting through most of the player weapon handling code, I posted the "TFE: Dark Forces Weapons" video.

### AI
At this point I started to focus on the AI, splitting off the basic actor code I already integrated - knowing that the AI code would soon get much bigger. Initial AI work revolved around the **mines** - which are in essence both an AI actor and a projectile. Once mines worked, it was time to move on to barrels and then generalize to *exploders.* Next up was scenery, which is also considered AI because it can animate and reacts to damage, causing it to change states. The mouse bot was partially completed, and then I made a slight detour to prepare for version 0.7.

### Input and UI
TFE needed a system to remap keys to actions, which had been implemented previously. What hadn't been implemented yet is the UI. So the UI was created, though not fully hooked up yet.

![](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/InputMenu1.jpg?raw)

### More AI
Late September saw a lot more AI work, with more reverse-engineering time required as gaps became evident during the integration process. Along with the AI, the Task system was being cleaned up and simplified. Finally the mouse bot was completed, but the AI journey was just getting started.

In Dark Forces, AI agents are split up into a number of actors, which all have little bits of functionality. With the introduction of the "troopers" - more of this functionality needed to be integrated.

On September 30th I posted the "TFE: AI System" video. By this point the "trooper" AI was complete, as well as the mouse bots, land mines, exploding barrels, and scenery (like the red lights in Secbase).

### Flyers and Bosses
In early October I started work on "fliers" - which have yet more "actor" structures and code. At this point the AI code was complete enough that I was able to add several more enemies that had very little custom code. Then came the Sewer creature, which isn't complete unique but shares less code that any other enemy so far.

Next was the Kell Dragon, which is the first "boss" enemy to be integrated. These enemies are different than any so far in that most of the code is custom. Most of the regular enemies share code, with their initial settings determining their behaviors. But the bosses change that.

### Turrets, Generators, and Vues
The Welder and Turrets were integrated, which also use mostly custom code. Fortunately they use fewer states and less code than the bosses.  I also fixed some latent rendering bugs in this period and removed a lot of no longer used code. Finally VUE animations and Generator logic were integrated.

On October 14th, I posted the "TFE: VUE Animations, Enemy Generators, and Fixes" video.

### Level Reloading
So far, you could only load a single level and then restart the program and load another. Mid-October saw that finally fixed with level skip cheats and by fixing level reloading issues. It also saw the ability to add new agents using the in-game UI. Late October saw the integration of player death and respawing. Jabba's ship was now properly handled,  the code for it had been previously reverse-engineered but never integrated until now.

At this point I started uploading "Pre-Core Game Loop" releases, with the idea of updating them regularly for testing until the Core Game Loop release was finally finished. When I had previously ripped out all of the old code, including the reverse-engineered classic renderer until it could be hooked up properly, various problems were fixed and corrections made to the classic renderer. As a result, it was parred back to the original fixed-point renderer - meaning builds were in 320x200 only.

People quickly found numerous bugs, some of which are still waiting to be fixed. Work on the boss AI continued, with new pre-releas builds often coinciding with a new enemy being integrated. The Input Remapping was also finished during this period.

By early November, all of the enemies were finally integrated.

### Towards Version 0.7
With the enemies all in place and the core game loop complete, it was time to re-implement the floating-point version of the Jedi renderer. I was my original version of the floating-point classic renderer as reference, but I re-implemented it directly from the fixed-point renderer. The reason for this is so that all of the fixes and changes were captured.

On November 14th, I posted the "TFE: Widescreen & High Resolution Rendering" video.

Once the floating-point renderer was complete, it was time to finally prepare for the Core Game Loop release. This involved fixing more menu code, fixing crashes due to resolutions not divisible by 4, fixing various 3DO model rendering bugs. But the biggest new feature was the mod loader - so it would be possible to play mods in TFE.

![](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/ModLoader3.jpg?raw) ![](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/tfe_hotel.jpg?raw)

On the November 18th, **version 0.7** was released and the core game loop was complete.

### Version 0.8
With the Core Game Loop complete, it was time to tackle the cutscene system. During this period I also fixed many bugs, cleaned up the renderer code. But most of the time was working through the "Landru" system.

![](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/pdaFinished1.jpg?raw)

The Landru system uses its own "actor" model for handling images and sounds. It also has its own sound and music management code. Even the display code is different then the rest of the game. There were numerous systems, such as the fading system, that needed to be converted from DOS-style while loops to state machines.

And, finally, on December 5th, I posted a video and posted the official 0.8 release.

![](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/cutscenes5.jpg?raw)

### Today
That brings us to today. I have been spending the last few weeks reverse-engineering the iMuse system, and prior to that had successfully integrated the game music module that integrates with iMuse.

It has been a long road and a wild ride. We didn't quite make it to version 1.0, but we came really close. The renderer, AI, INF system, in-game UI, cutscenes, game systems - all of it derived directly from the original executable using reverse-engineering, which is almost complete.

You can now watch the cutscenes, though the music still has issues, create a new agent and play the game from beginning to end. You have all of the relevant in-game UI, the mission briefings, the gameplay. Within mere weeks we will finally reach version 1.0.
