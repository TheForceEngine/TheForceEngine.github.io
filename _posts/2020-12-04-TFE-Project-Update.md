---
layout: post
title: TFE Project Update
---

It is time for another, long overdue, project update. The project went through a "slow period" of about a month after a flurry of work on the Classic Renderer but progress resumed about a week ago in earnest. This post will go over some of the work done so far, the current state of the project, and the next steps.

# Progress
The majority of the work since the last build has been on the "Classic Renderer" - consistenting of three main phases, though of course work bounces between them.

## Reverse-Engineering
The first stage is reverse-engineering the original DOS code in order to figure out how the original renderer works. This stage consists of decompiling the code, stepping through the code in a debugger to test values and see the results of calculations, and then figuring out what the code is trying to accomplish. This requires figuring out structures, global variables, decompiling functions and going through the program flow. The raw code goes into an internal project called "Dark Forces DOS" which, for a variety of reasons, is kept private.

As blocks of code is figured out, it gets turned into nice "C" code, which leads to phase 2.

## Porting into TFE
The code gets "ported" into the main project (The Force Engine). By this I mean building systems to contain the code in a way that can interact with the other low level systems, such as the file system, OS layer and graphics backend. During this process I attempt to clean up the code and test it in the working build to verify its accuracy to the original. Sometimes there are issues requiring me to bounce between phases 1 and 2.

## Extending the Code
The Force Engine supports higher resolutions, up to 4k at the moment in addition to improved controls and mouse look. The original Dark Forces code does not work well at higher resolutions due to the limits of its internal 16.16 fixed point math. In addition the quality of the texture mapping does not hold up very well beyond 320x200, due to its low sub-texel precision. After evaluating and attempting a few different solutions, I landed on [this renderer design](https://theforceengine.github.io/2020/09/06/TFE-Renderer-Design.html). So far the Fixed Point and Floating Point Classic sub-renderers have been implemented. The Floating Point sub-renderer handles very high resolutions gracefully, with plenty of sub-texel precision.

In addition to supporting higher resolutions, the renderer now supports widescreen. This is made trickier by the requirement to support widescreen for 200p and 400p with rectangular pixels as well as normal resolutions. The biggest changes and caveats:
* 200p widescreen automatically switches to the floating point sub-renderer, the original fixed point renderer has not been altered to support widescreen.
* The algorithm to compute the wall/frustum intersection when clipping is different when using widescreen and is slightly more complex. This is unavoidable, however. With widescreen disabled the original algorithm is used.
* There is no direct FOV control, though that may be added in the future.


![Scene 1 - 200p Normal](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene1_normal_200.png?raw=true) ![Scene 1 - 200p Widescreen](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene1_wide_200.png?raw=true)
![Scene 1 - 1080p Normal](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene1_normal_1080.png?raw=true) ![Scene 1 - 1080p Widescreen](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene1_wide_1080.png?raw=true)
![Scene 2 - 200p Normal](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene2_normal_200.png?raw=true) ![Scene 2 - 200p Widescreen](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene2_wide_200.png?raw=true)
![Scene 2 - 1080p Normal](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene2_normal_1080.png?raw=true) ![Scene 2 - 1080p Widescreen](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene2_wide_1080.png?raw=true)
![Scene 3- Normal](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene3_normal.png?raw=true) ![Scene 3 - 1080p Widescreen](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene3_wide.png?raw=true)
![Scene 4- Normal](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene4_normal.png?raw=true) ![Scene 4 - 1080p Widescreen](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene4_wide.png?raw=true)
![Scene 5](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene5_wide_1080.png?raw=true)
![Scene 6 - Wide 200p](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene6_wide_200.png?raw=true) ![Scene 6 - Wide 1080p](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/scene6_wide_1080.png?raw=true)

And don't forget about ultrawide resolutions! I took this by resizing the window, so I don't remember the exact aspect ratio but I think it was about 35:9. Note that this is still the original software renderer with minimal modifications to support widescreen.
![Ultrawide](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/ultrawide.png?raw=true)

## System UI
The "System UI" has been undergoing improvements. This includes:
* New title screen.
* OS (System) File Dialogs instead of the imGUI version I was using. This improves the UI when needing to select paths and files and makes this part of the UI more consistent with other programs used on your OS.
* New Graphics UI.
* Added the ability to bring up the System UI while playing a game using Ctrl + F1.
* Added the ability to adjust resolution and graphical settings and see the results immediately in-game.
* Added optional color correction.

### TitleScreen
![Titlescreen](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/NewTitleScreen.png?raw=true)

### Adjusting Graphics Settings During Gameplay
![Graphics Settings](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/classic_renderer.png?raw=true)

## Optimizations
Running the software renderer at high resolutions was not always performing well - especially beyond 1080p. The main issue was not the rendering itself, however, but the cost of transfering the framebuffer from CPU to GPU memory and to a much lesser degree, the cost of converting the framebuffer from 8-bit to 32-bit color on the CPU. Several methods are employed to fix this situation.

### GPU Palette Conversion
Rather than converting from 8-bit to 32-bit on the CPU - the new default is to perform this conversion on the GPU during the blit of the framebuffer to the window/screen. This has multiple effects:
* Reduces CPU time spend converting from 8-bit to 32-bit.
* Reduces the amount of memory that needs to be transfered from the CPU to GPU by a factor of 4. This is a huge time-saver.

### Asynchronous Framebuffer Transfer
The next big issue was the stall waiting for the framebuffer to be transfered to the GPU so that the screen could be updated. To fix this, the framebuffer was changed from a Texture to a DynamicTexture. The new DynamicTexture uses multiple Pixel Buffer Objects to allow for an asynchronous copy of the framebuffer data to the GPU and then copy from GPU to GPU resources.

### Results
Combining these two reduced the cost of transfering the framebuffer and converting from 8-bit to 32-bit at 1440p by more than an order of magnitude - allowing the original levels to run at over 100fps at 1440p with the conversion and upload taking around 0.2ms instead of 14ms.

## Level Editor
During this period, I also worked on the Level Editor on occassion. It still has a long way to go, but here are some things I worked on:
* Improved the grid rendering in the 3D view.
* Added the ability to actually edit geometry.
* Improved and refined the UI.
* Worked toward being able to properly draw and shape sectors.

### 3D Grid Rendering Improvements
Extended View Distance
![Extended Grid](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/levelEditor_ExtendedGrid.png?raw=true)

Rendering Sub-Grids (similar to the 2D Grid)
![Extended Grid](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/LevelEditorSubGrid.png?raw=true)

### Geometry Editing
![Geometry Editing](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/LevelEditor_GeometryEditing.png?raw=true)

### Object Editing
![Object Editing](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/LevelEditor_ObjectEditing.png?raw=true)


# State of the Project
Now that you have read and seen some of the progress over the last few months, I want to quickly go over the current state of the project.

## Roadmap Changes
The original November release was estimated based on the apparent project scope and development velocity when the [Roadmap](https://theforceengine.github.io/Roadmap.html) was put together. As a result, it was optimistic despite my original thoughts on the matter. The project is still in development, as I hope this post illustrates, but changes have been required to the [Roadmap](https://theforceengine.github.io/Roadmap.html) and time estimates. Please see the new roadmap for details.

## Classic Renderer State
The Classic Renderer is now about 95% complete. 3D object rendering code still needs to be cleaned up and ported from the reverse-engineered code and the sorting algorithm needs to be finished - it doesn't yet handle all of the special cases between sprites and 3D objects. Mainly because that code could not be tested until 3D objects are rendering properly.

# Next Steps
The next steps for the project are to finish the Classic Renderer, which should be done in the next few weeks. Unfortunately I am going to have to put off a release a bit longer because of a issue:

In the original code, a lot of the initial texture offsets are handled when the INF system starts up. What this means is that some of the textures do not have the correct texture offsets when using the Classic Renderer (though most do). The second INF issue is that some adjoins are not correct until after setup is complete. And the final issue, is that many graphical issues in mods are actually caused by incorrect INF execution.

As a result of these issues, I have decided to put off the next test release until the reverse-engineering of the INF system is complete. Once this is finished most MODs will work correctly and it should be possible to properly test the Classic Renderer to find the real bugs. Basically I want to avoid having to worry about bug reports and issues people find (including myself) that are really due to INF issues.

Once the INF system is reverse-engineered and fully accurate, it will be time to make another test release. After that the focus will be on character control, physics and collision - the game needs to **feel** right. And then reverse-engineer and properly implement all of the Logics and weapons.
