---
layout: default
title: Jedi Overview
permalink: TD_Jedi_Overview.html
---
# Jedi Overview

### Contents
* [Creation](#creation)
* [Design and Consequences](#design-and-consequences)
* [Features](#features)
* [Source Code](#source-code)

Prev: [Mods](TD_Mods.md) ... Next: [Task_System](TD_Task_System.md)

---

# Creation
The **Jedi Engine** was created by *Lucas Arts* to power **Dark Forces** and **Outlaws**. It seems probable that Dark Forces was originally going to be created as a full 3D game, you can see remnants of this in the source code - such as the player "lean" functionality still in the code - even though it doesn't do much because of the final renderer doesn't support camera roll. However it is very likely that the team could not meet their performance goals and were inspired by the Doom alpha to take a different approach better suited to the computer hardware of the time.

# Design and Consequences
The result, however, has more in common to the later Build engine than it's Doom inspiration. Each sector is distinct and connected to other sectors using portals, called "adjoins" in the engine. This is the primary visibility system used in the game, rather than the static BSP-based system used by Doom. This has a number of consequences:
* Dynamic sectors - sectors can move and rotate which is used to great effect in almost every level.
* The ability to dynamically change connections at runtime - allowing long elevator shafts connecting multiple floors like a real building, used in Detention Center.
* Sectors could overlap in XZ space since connections were defined using portals, leading to sectors being assigned *layers* to make dealing with mapping easier.
* It was easier to mix in different rendering technologies, helped along by the 1d depth-buffer (see [Renderer](TD_Renderer.md)). This allowed for 3D models to be rendered, similar to *X-Wing* and *Tie-Fighter*.
* While overall level size scales well, with later mods having thousands of sectors, detail density does not scale as well as Doom. This is due to the dynamic nature of the portal culling compared to the overall faster sorting using a static BSP-tree. The result is levels that are large, more interactive, but overall less detailed than Doom.

# Features
In order to make the best use of this technology, LA decided to add pseudo-scripting to handle level interactivity, in the form of **INF**. This allowed much more flexibility in the ways the player could interact with the levels compared to previous FPS games.

To give the games more of a cinematic feel, in-game 3D model animations were added using the **Vue** system. This allowed the Mouldy Crow to land and take off, Tie Fighters to fly around, and other cinematic in-game moments.

To complement the visuals, dynamic music was implemented using the iMuse system - which transitions between tracks based on what is happening in-game. In Dark Forces, this system is pretty simple, transitioning based on whether the player is in combat or just exploring, but it is clear it was meant for more with Boss themes and perhaps other ideas.

The lighting system is also pretty interesting. 3D objects are lit using 3 directional lights and then adjusted based on the sector ambient. These values were hardcoded, but it is likely that they were meant to be set per-level. In addition, each level could have its own palette and color table - this allowed for per-level texture sets and even fog like effects, such as seen in Gromas Mines. The player could use a headlamp, which created a camera light source using table-based attenuation. Light diminshing was used but was very muted compared to Doom or Build games (due to artistic rather than technical considerations).

Objects are controlled by small bits of functionality, called *Logics*, which can be chained together. For example, you can make a sprite animate and be a health pickup. Unfortunately all of the Logics are hardcoded, but TFE will add mod support to edit or add new Logics in the future.

Due to the rendering capabilities of the engine, projectiles can either be 3D objects, such as blaster bolts, or sprites. This gave the blaster bolts in Dark Forces a much more authentic look than sprites could have accomplished. Later, support for hitscan weapons was added for Outlaws. Specific details will be covered in the game sections.

# Source Code
The various components of the Jedi Engine were extracted and recreated by reverse-engineering Dark Forces (DOS) and later Outlaws. The source specifically related to the Jedi Engine can be found under the `TFE_Jedi_*` folders in the source tree, where the wildcard is replaced by the system.

Note that all TFE_Jedi systems have been derived by reverse-engineering the original games, meaning the original copyright still belongs to *LucasArts* and *Disney*. The code has been refactored and some systems, such as the floating point sub-renderer used to support resolutions higher than 320x200, have been derived from the original system. Ultimately this means that while the code is Open Source, it is not directly usable in other programs without concern of these copyrights.

Systems include:
* TFE_Jedi_TaskSystem
* TFE_Jedi_Level
* TFE_Jedi_InfSystem
* TFE_Jedi_Renderer
* TFE_Jedi_Collision
* TFE_Jedi_Sound
* TFE_Jedi_iMuse
