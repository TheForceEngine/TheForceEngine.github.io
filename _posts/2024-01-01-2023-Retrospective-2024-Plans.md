---
layout: post
title: 2023 Retrospective and 2024 Plans
---
# Table of Contents
1. [2023 Retrospective](#2023)
2. [2024 Plans](#Plans)

## 2023
With the release of The Force Engine (TFE) version 1.0 at the end of 2022, I had big plans for 2023. Unfortunately, as often happens in these cases, the year was pretty busy and development proceeded at a slower pace overall. That said, several key milestones were reached in 2023 that will set up 2024 features and aid in the path to version 2.0 - Outlaws support.

### Version 1.02 - January 16
The version 1.0 release exposed many bugs and issues with TFE, so a few weeks after the version 1.0 milestone, a large bug-fix build was released. It included quality of life features like Alt+Enter for fullscreen, the framerate limiter, and improvements to the audio system. It also featured over two dozen bug fixes.

### Version 1.08 - February 6
Version 1.08 was the first time Linux was officially supported, thanks in large part to the contributions of Manuel Lauss. He also contributed fixes when running Dark Forces using different languages, and did the initial pass at removing 3DO hardcoded limits (which was then further modified later).

This release also saw more bug fixes, such as HOM in Executor using the GPU Renderer, fixed font rendering issues, fixed the Gamorrean Guard so he attacked properly, similar fixes to the Sewer Creatures, more work on the midi system, and more crashes.

### Version 1.09 - February 15
This version added midi synthesis using **Sound Font 2 (SF2)** data. It also added proper **OPL 3 emulation**, which became the new default, making the music sound similar to playing Dark Forces through DosBox.

### Version 1.09.2 - May 26, Version 1.09.3 - July 4
During this time, work on the project was slow, but feature work was happening in the background. These two releases fixed dozens of additional bugs and issues found throughout the year.

### Version 1.09.4 - July 31
Kevin Foley made large contributions to this release with **Smooth Vue Animations**, which interpolated rotation, translation, and scale for Vue animated objects - such as flying ships. This greatly enhances the animation quality. He also added the Beta version of the **Closed Captions** feature.

In addition to contributions by Kevin and Manuel, I implemented a number of improvements to the GPU renderer allowing for up to 65536 visible portals in a frame, properly handling more than 65536 visible sector vertices in a frame (as originally intended), improved debug view modes, added settings templates, added the **8-bit interpolated** color mode, and finally the post processing system and **bloom**.
<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/Bloom1C.jpg?raw=true" alt="Bloom" class="inline"/>
<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/Captions1.gif?raw=true" alt="Captions" class="inline"/>

### Version 1.09.5 - September 21
This release saw the addition of **True Color Rendering**, which included optional texture filtering **Sharp Bilinear** filtering, mipmapping, and approximated true-color to colormap mapping. It also, finally, added the option to adjust the **field of view**.

Kevin was also hard at work, adding support for custom caption files and fonts, UTF-8 support, and generally improving the Accessibility UI and Captions.
<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/TrueColorRendering23.jpg?raw=true" alt="Captions" class="inline"/>

### Version 1.09.52 - September 25 / Version 1.09.53 - 27th
At this point I was mainly focused on bringing back the built-in tools that were removed early on due to large changes in the project. This release saw the return of the Editor option in the main menu, the initial pass on the Asset Browser, and better error handling. Kevin contributed to fixes in the Captions system, and Manuel continued to contribute fixes and to work on the Linux implementation.

Manuel Lauss contributed more improvements to the audio system, replacing RTAudio with SDL Audio - fixing a number of issues and reducing the number of dependencies. Kevin contributed to more accessiblity fixes, and I worked on improving the true color mode - making textures appear closer in coloration to 8-bit mode. This release also saw more progress on the Asset Browser, such as factoring out the Asset system.

*Color Improvements to True Color Rendering*
<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/ColorImprovements.jpg?raw=true" alt="Color Improvements" class="inline"/>

*Asset Browser*
<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/AssetBrowser.png?raw=true" alt="Asset Browser" class="inline"/>
### Version 1.09.54 - Final Release of 2023
In the final release, more work went into the editor - setting up for the Level Editor work that would consume the rest of the year. RtMidi was made optional on Linux thanks to Manuel, now possible with OPL 3 and SF2 support. After discussions, we also replaced DeviL with SDL Image to make future Linux packages easier.

### Level Editor
The rest of the year was spent on the level editor and supporting systems. While not yet useable, a number of features have been completed and, overall, it is shaping up well for a January release.

*Level Editor*
<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/LevelEditor23_1.png?raw=true" alt="LevelEditor23_1" class="inline"/>
<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/LevelEditor23_2.png?raw=true" alt="LevelEditor23_2" class="inline"/>

### Outlaws
Behind the scenes, initial work on Outlaws was started leading to a good understanding of the renderer changes from Dark Forces as well as various other systems. This work will be leveraged in 2024 to both support Outlaws asset types and levels in the editor, but also to port over enhancements to Dark Forces to allow for the features to be used (slopes, dual-adjoins, etc.) but also to implement Outlaws support throughout the year.

### Other
Another feature that was worked on, but not quite ready for prime time, is dynamic lighting. That will be ported from the branch and finished sometime in 2024.
<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/Lighting23.jpg?raw=true" alt="Lighting23" class="inline"/>


## 2024 Plans<a name="Plans"></a>
For 2024 Plans, I have split things up into a few projects.

### Level Editor - Early 2024
Release a useable level editor that can be used to make complete levels with goals, INF support, editable entities, and everything else needed.

### Asset Editor - Early 2024
Along with the level editor, I want to finish the Asset Browser. In addition to the formats currently supported, I want to add formats needed for cutscenes, and UI. And finally new assets - such as HD assets and voxels.

### HD Asset Support - Early 2024
Now that the Asset Browser is available and editors and import/export functionality is available (for will soon be available), it will be possible to add support and easily test HD assets. HD assets include higher resolution / color depth textures, frames, and sprites, but also higher quality sound as well. My goal is to have this done for the Dark Forces Remaster release, so Nightdive's new assets are supported.

### Voxel Replacement Support - Early 2024
It is finally time to port over the experimental voxel code and make it "production ready." The Asset Browser will be used to import voxel data, map hacks, and similar data to build voxel mods for Dark Forces and Outlaws.

### Outlaws - Late 2024
My ultimate goal is Outlaws support in TFE this year, even if it is only single player to start. This will start by adding Outlaws formats and level editing support to the tools. Then there will be a number of releases throughout the year as Outlaws support is implemented - similar to Dark Forces before version 1.0 was released. A number of new features will come with this that can be used with non-vanilla Dark Forces mods, such as digital music playback.
