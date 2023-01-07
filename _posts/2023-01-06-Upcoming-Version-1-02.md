---
layout: post
title: Upcoming Plans
---
# Version 1.02
I am currently working towards version 1.02 - this post will cover what has already been done and what I am still planning to do. Players have found a number of issues, especially with mods, in the release version. So version 1.02 will be another bug-fix release with some minor quality-of-life improvements as well.

## Improvements Already Completed
* Alt+Enter to toggle fullscreen (in addition to F11).
* Secret Percentage update after loading from a save, fixed LADATA save percentage issue.
* Fixed layer keys swapped in PDA.
* Frame rate limiter (still needs the UI).
* Fixed a crash when playing Evacuation of Hoth due to a frame scenery object being destroyed.
* Fixed a bug where sprites didn't always light up correctly when attacking.
* Fixed a bug where the Probe Droid would stay fullbright after firing.

## Improvements Still In Progress
- [ ] Custom Mission Issues
	- [ ] Nearly impossible to crouch-jump out of the Kell Dragon area. In Dos it is nearly instant. Some kind of collision issue?
	- [ ] Exterior Adjoin GPU render issue. Works fine in Software.
	- [ ] Destroy Imperial Supply Depot - door does not open when switch door is pressed. Works in DOS - breaks TFE.
	- [ ] Dark Tide 3-3 static doesn't load for some reason.
- [ ] TFE still not autodetecting Steam installs on different drives.
- [ ] Music and Audio output issues.
	- [ ] UI to select audio output.
	- [ ] UI to select midi output.
- [ ] Issues getting TFE to start.
- [ ] Assassination on Nar Shaddaa Weapon Pallette bug.
- [ ] Agent Menu keyboard scrolling bug.
- [ ] "Back to Yavin" map mod (Bugged switch)
- [ ] PLANE shading in 3D objects being affected by planar scrolling when it shouldn't be.
- [ ] Gas Mask disappearing or when it appears ends up not being fullbright.
- [ ] Player does not "climb" 2nd altitudes properly while jumping.
- [ ] Dark Forces - PDA Map viewer input problems when moused over clickable arrows.
- [ ] Pressing the console key fast prints character in console.
- [ ] Player cannot move while holding leftAlt.

# Version 1.10 - Linux Support
The main goal of version 1.1 is to add official Linux support and clean support for the Steam Deck. Mac support is planned but will probably happen a bit later.
* Integrate Linux PRs already submitted.
* Fix sound issues on Linux.
* Add support for midi synthesis and sound fonts.
* Add support for higher audio processing frequencies, to support midi synthesis. This will enable high quality audio support later this year.

# Version 1.11 - True Color Support
* DirectX 10/11 render backend to better support GPUs with poor or non-existant OpenGL drivers on Windows, such as some integrated Intel GPUs.
* Vulkan render backend support for better GPU support on Linux.
* True color render support - with options for texture filtering and antialiasing. This will also include support for 8-bit color lighting + color map interpolation.
* Bloom post-fx (optional).
* Better low-end support for the software renderer.
* I might add dynamic light support as well, or maybe wait until a later release. This will depend on how long it takes to get this release out.

# Version 1.12 - Voxel Support
* Integrate the experimental voxel loading and rendering code.
* Add GPU voxel rendering support.
* Improve "vox" asset loading.
* Add metadata support for voxel WAX/Frame/3DO replacements.
* Add metadata support for voxel texture replacements (for switches).
* Add "maphacks" equivalent to TFE for fine-tune voxel object positioning.

# Version 1.20 - Editor
* Bring back the asset visualization tools (with the idea of making them more fully featured in future versions).
* Bring back the level editor.
* Initial level editor release.
