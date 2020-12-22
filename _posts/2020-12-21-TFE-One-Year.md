---
layout: post
title: TFE One Year Anniversary
---

__The Force Engine__ started out life as __DarkXL 2__ on December 21, 2019. Two months later, the project was renamed to The Force Engine, in order to encapsulate the intent of the engine, and put up on GitHub. After another month of work, about 3 months from the beginning, The Force Engine was announced on DoomWorld.

After reflecting on what went well and what could have gone better with DarkXL, the project was started from scratch. In order to build a framework and get things working, basic tools were written, including a level viewer (which is becoming the full level editor) and viewers for most asset types. I wrote a software sector renderer based on my understanding of the Jedi Engine, a sound system and midi engine, and an INF system, and finally released a test build.

While it has been nice to have a working build and to be able to "play" through the levels, these initial systems are not accurate enough to meet the project goals. Thus, once the test build was released and after getting some initial feedback, fixing and improving a few things along the way, the real meat of the project began.

Most of the remaining year has been spent reverse-engineering the original DOS renderer, integrating it into the TFE framework, and extending it to support higher resolutions and widescreen. The DOS fixed-point renderer is still there and that is what you will see when running at the original resolution of 320x200. Because TFE is currently the only source of reverse-engineered Dark Forces/Jedi Engine code, the DOS-derived renderer will never go away. The renderer has the same features, techniques and bugs as the DOS renderer. At higher resolutions, the floating-point variant of the renderer is used in order to handle much higher resolutions and in some cases fix bugs (though most of these fixes will be optional). The "Classic Renderer" is finally days away from completion.

Once the Classic Renderer is finished, the next task is to properly reverse-engineer the original INF system which, once integrated, will complete the visuals since things like texture offsets and other features will be handled correctly. Once complete, the long overdue "Classic Renderer" release will finally be done.

Death Star (Classic Renderer)
![Death Star](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/tfe_gif_Mon-Dec-21-21_14_39-2020_0.gif?raw=true)

Color Correction
![Color Correction](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/ColorCorrection.gif?raw=true)

## Foundation
The Classic Renderer and fully accurate INF system will lay a strong foundation upon which to rebuild the rest of the game and engine. And, of course, working through the rendering and INF code has and will continue to reveal more about the inner workings of the original systems, the layout of the code and over all program flow. As a result, I expect that the difficulty and complexity of the remaining reverse-engineering work to decrease, meaning we are nearly at the top of the hill.

## The Future
Once the Classic Renderer release finally comes out there will be a period of testing to verify that The Force Engine renders everything correctly in the base levels and in mods and that the INF functionality is fully accurate (which handles things like level progress, doors, switches, elevators, 3D model animations, changing light levels, scrolling textures, and more).

The following test release will focus on realizing the cross platform support promised since the beginning. This means setting up a CMake-based build system and adding support for Linux and OS X (including new ARM based Macs).

After that the focus will shift to gameplay, starting with reverse-engineering the original collision, movement and physics code. And then moving on to Logics and weapons. This will finally lead to a fully playable version of Dark Forces through TFE. Once gameplay is complete, the next steps will be cutscenes, mission briefings, finishing the in-game UI, and finishing the iMuse system.

And finally, this will leave the project in a good place to start diving into the Outlaws code to figure out the engine differences and finally getting that game up and running using The Force Engine.
