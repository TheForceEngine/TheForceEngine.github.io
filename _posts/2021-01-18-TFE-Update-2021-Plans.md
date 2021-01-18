---
layout: post
title: TFE Update and 2021 Plans
---
As the first blog post of 2021, this will cover several topics. First, an update regarding the progress of The Force Engine. That will be followed by TFE plans for 2021 - the year of the first fully playable release (hopefully), and finally the first "experimental" build and what that is all about.

## Progress
The main focus has been reverse-engineering and integrating the original INF-system to replace the code currently available in TFE, which - despite being mostly functional for the  original levels - was basically placeholder until now.

The reverse-engineering progress is still ongoing and will, most likely, be for a few more weeks. My goal is to finish the INF reverse-engineering and integration by the end of Feburary, at which point proper testing of the Classic Renderer and INF can begin across the original levels and Mods. This will form the foundation for the rest of the year as we speed towards Dark Forces completion (though TFE will still have a ways to go after the first full release, with Outlaws, mod tools, and various improvements and enhancements).

### Inf Debugger
In order to visualize and test the INF system at work I have also started the implementation of the INF debugger.

![InfDebugger](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/InfDebugger.jpg?raw=true)

At any point while running a level you will be able to hit Alt+F10 to bring up the INF debugger. The right window contains a list of all the INF items in the level. You will be able to select whether to show all items, active items and other options. In addition you will be able to click on the Name, Class, or Sub-Class buttons to sort by those categories. Clicking on any of the items will select it, and it will be visible in the Inspector window.

The Inspector window, on the bottom left, allows you to see the current state - such as the current stop, speed, key, flags and more. The values of most of these items are editable in real-time, in order to facilitate testing. Not all values will be shown (there are many values) - so you will be able to add and remove variables from the view, though some will likely always be visible. In the breakpoints tab, breakpoints can be set on various events such as reaching a stop, a variable changing, the item being activated, etc..

This is not shown yet but you will be able to pause the game, needed when breakpoints are hit, and single-step through INF commands. Finally, as the INF system operates, messages are sent to the Output window, on the bottom right, so you can see what is happening. There will be some sort of filtering available, though this has not been implemented yet. If you click on a message in the Output window, it will select the INF item so you can inspect it.

This is still a work in progress and will get fleshed out as I work on the INF system. This is great for me to debug the system but should also be useful to level authors and modders trying to figure out why their INF is not working as intended, or just to check correctness.

## 2021 Plans
The goal for The Force Engine project is to release version 1.0 of TFE this year, which means that TFE will be a full replacement for DosBox when playing Dark Forces. At that point the tools will still be mostly in a preview state, though the level editor should be usable, if not feature-complete.

### INF & Classic Renderer
The next main test release will be the finish INF & Classic Renderer release - where levels should **look** correct compared to DOS, including Mods, and the level functionality - except where it relies on Logics or AI, will be fully accurate. The goal is to have that release done around the end of Feburary.

### Cross Platform Release
The next main test release will be focused on setting up a CMake build system and making sure TFE builds and runs on Linux and OS X platforms. The GitHub projects list marks "Metal" support as required, though I may put this off until after the first release.

### Player Control & Physics
The next test release will see Player Control, Physics, Collision detection reverse-engineered and integrated. Some of this work has already been completed. The goal of this release is to make sure Dark Forces plays and **feels** authentic.

### Logics & AI
Finally, this release will get some real gameplay finished. Logics, such as pickups, and AI should be fully functional after this release, including bosses. The Logics will be scriptable and most likely written as scripts (as the placeholders are now).

### Weapons
In this build, weapons will be finished and fully working. This means using ammo, updating the HUD, proper effects in the levels, proper damage and damage falloff. This test release will also cover auto-aim and System UI options to control how much auto-aim you want while playing (from "Dark Forces" to "None).

### Dark Forces UI
In this test release the Dark Forces UI will be finished, including the PDA and cutscenes.

### Beta 1.0 Release
Finally the TFE 1.0 Beta release.

### Post-Release
Once the initial release is complete and the important bugs worked out, the focus will shift to tools - including the initial support for Outlaws levels in the level editor. During this phase features that were added to the Jedi Engine for Outlaws will be ported over - such as slopes and dual adjoins - and made available for Dark Forces mods. Then the focus will shift again to Outlaws. This is about as far ahead as I want to plan, so there will be more updates on Outlaws and tools as we progress through the year and beyond.

## Experimental Builds
The last topic will be experimental builds. I have a variety of possible features and enhancements in mind for The Force Engine, many of which are rendering related. The idea behind experimental builds (and the associated experimental branch) is to be able to take a break from the current work, such as INF reverse-engineering, to implement one of these experimental features and then release an Experimental build for people to play with.

Experimental Features may not make it into master, depending on the results, performance and reactions - though I suspect most will. Experimental Features won't be "production ready" - meaning they may have bugs, low performance or missing features. It is meant as proof of concept, fun breaks from the main work. The features that make the cut will eventually be moved into master and finished, when the engine is ready for the feature.

The first experimental feature is . . .

### Voxels
I couldn't resist implementing voxel support as the first experimental feature. As mentioned above, it isn't ready for production - and won't be for some time, definitely not until after the Classic Renderer / INF test release is out, if not longer - but is a nice proof of concept that you can try out yourself. For this Experimental Build, I embedded Dzierzan's voxel pack (https://github.com/Dzierzan/Dark-Forces-Voxel-Pack) and a patch to Secbase to show some of the voxels.

### How to Get the Build
You can get the current experimental build from Downloads on [The Force Engine site](https://theforceengine.github.io/downloads.html). Scroll to the bottom, under experimental builds.

### How to Run
The setup is the same as normal, unzip the build into a new directory and then run **TheForceEngine.exe**. You will need to setup your Dark Forces data, if it is not auto-detected. If you have run TFE before, it should just work. Next startup the first level, Secbase. **Make sure to either run in widescreen or at higher than 320x200 - otherwise the voxels won't render.**

Once in Secbase, open the console (~ on US keyboards) and type **EnableExperiment**. Hit the same key again to raise the console.

### What is implemented
* Conversion between VOX and the internal format. Proper conversion and saving of the TFE format will happen once the feature is moved to master.
* Rendering of opaque voxel objects.
* Basic console commands to place voxels and to save and load placements.
* Some debugging console commands.

### What is missing (things that need to be finished once I get back to the feature to make it "real")?
As you can see from the list, this is definitely still in the experimental/not production ready phase.
* Proper conversion into the TFE format.
* Animation support.
* LOD support.
* Translucency support (obviously this needs this feature to be added to the engine first).
* Editor to import frames, set scale values, etc.
* Support for arbitrary pitch and roll, needed to support software voxels in the perspective renderer.
* Better handling of palettes (MagicaVoxel mangles the order - meaning the colors have to be remapped).
* Performance improvements (the techique is not fully optimized and may be slow on some machines).
* Quality improvements, the texturing/edge quality leaves something to be desired at lower resolutions due to incorrect sub-pixel precision.
* A few minor bugs, such as sorting breaking if standing inside or over the top of the object.

There are several console commands available to test things out:
### raddVoxel
**raddVoxel filename base offset upVector** Add a new voxel object. This pulls the object from Mods/voxels.zip. If you want to add or change voxels, edit the zip file. There are several options:
 * filename: the path to the voxel, starting from the zip file. For example, decorations/table.vox
 * base: **ceil** or **floor**, default **floor**. This determines if the voxel is floor or ceiling aligned. Use ceiling alignment for things like hanging lights and chains.
 * offset: offset in units from base, negative values go up.
 * upVector: **y** or **z**, default **y**. This is the up vector of the original asset. For some reason a few of the voxel models use Z up instead of Y, such as table.vox. In those cases specify Z to get the correct look.
 
 **Examples**
 * **raddVoxel decorations/table.vox z**  - the voxel is decorations/table.vox, the up vector is Z.
 * **raddVoxel enemies/intdroid.vox -4**  - the Interrogation Droid, moved 4 units from the floor.
 * **raddVoxel decorations/redlit_a.vox ceil** - the redlight voxel aligned to the ceiling.

### rsaveVoxels
**rsaveVoxels filename** Saves a level patch with the voxels you have setup. It will be saved into Mods/filename.

### rloadVoxels
**rloadVoxels filename** Loads a previously saved level patch, assuming you already typed **EnableExperiment**.

### rclearVoxels
There are no arguments, this command simply clears all voxels from the level.

### rvoxel_showDrawOrder
**rvoxel_showDrawOrder enable** - animates the draw order of the voxels if enabled.
* rvoxel_showDrawOrder 1 - enables the debug animation.
* rvoxel_showDrawOrder 0 - disables the debug animation.

### rvoxel_step
**rvoxel_step** - if voxel_showDrawOrder is enabled, this stops the animation and steps forward 1 column. You can specify the number of columns to step.

### rvoxel_continue
**rvoxel_continue** - this resumes the draw order animation.

## Screenshots
![Voxels1](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/Voxels1.jpg?raw=true)
![Voxels2](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/Voxels2.jpg?raw=true)
![Voxels3](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/Voxels3.jpg?raw=true)
![Voxels4](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/Voxels4.jpg?raw=true)
![Voxels5](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/Voxels5.jpg?raw=true)

## Implementation Details
I implemented the voxel rendering code from scratch in order to fullfill some requirements, which I think all new features and improvements in TFE should share:
 * Decent performance in the software renderer - while this feature can certainly be improved in this regard, in general it performs well consuming 1-3 ms per frame on 1080p. This is inline with other features, such as 3D objects.
 * Follows engine patterns - the feature should follow engine patterns, such as favoring column rendering and should mesh well with the engine.
 * Proper sorting - continuing with the integration, the feature should sort properly with sector geometry and other objects. This voxel renderer uses the 1d zbuffer to sort with walls, fits into the same sorting system as other objects, culls and clips against the view window (needed for adjoins), etc.
 * Proper "look" - meaning the results should be consistent with the rest of the game and feel like it belongs.
 
 I will write up more details about the algorithm in the future, but here is the quick overview:
 * Data is organized and rendered as voxel columns, compressed using the same RLE algorithm as WAXes, modified to fit the data.
 * RLE data basically splits voxel columns into transparent runs which are skipped and opaque runs that form "sub-columns."
 * Voxel-column rendering order is determined algorithmically based on the view vector, meaning no sorting is required for back to front rendering.
 * Sub-columns may have vertical caps rendered depending on the camera position, but at most one cap per sub-column will be rendered.
 * Each voxel has a 4-bit adjacency mask, which is used to avoid rendering faces shared by multiple voxels.
 * Sub-columns are further sub-divided based on the adjacency mask and the final contiguous voxel columns are rendered as textured lines using a column renderer very similar to sector walls. No per-pixel transparency testing is required.
 
 Interior voxels are removed, interior faces are skipped using the column sub-division method mentioned above and voxels are rendered as voxel-columns instead of as individual voxels.

## Next Experiment?
I have ideas for future experiments but they will have to wait, the focus has returned to the INF reverse-engineering, integration, and the debugger.
