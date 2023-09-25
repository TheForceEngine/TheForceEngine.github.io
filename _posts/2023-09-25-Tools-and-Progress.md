---
layout: post
title: Tools and Progress
---

## Version 1.09.5
Recently, the True Color build was released. With it, several features were added such as the True Color mode, texture filtering - including sharp bilinear, the ability to adjust the field of view, enhancements to the captions/subtitles system - such as choosing between fonts and UTF8 support, as well as a variety of bug fixes.

## Upcoming Bug-Fix Release
Since then, a number of bugs are been addressed. One large issue people found with the true color mode is that some textures did not have the correct hue and saturation at low light values (roughly half and lower). So I have been working on a new experimental automatic "per-texture" adjustment, which works well in most cases though there are some textures in some mods that still have issues.

*Left is adjusted, and right is without the per-texture adjustment*
<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/TextureAdjustments.jpg?raw=true" alt="TextureAdjustments" class="inline"/>
<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/TextureAdjustments2.jpg?raw=true" alt="TextureAdjustments2" class="inline"/>

## Moving Forward
Moving forward, I plan on taking a break from feature work to instead focus on restoring and improving on the built-in tools. There are multiple reasons for this:
* Having tools will make it easier to implement new features such as voxel support and Outlaws engine enhancements.
* I can start getting the Outlaws assets loading, including levels, in preparation for Outlaws support.
* To improve forward momentum in terms of modding and Outlaws support.
* I can change up the work I am doing to help keep the project fresh.

## Current Progress
I have restored the **Editor** option in the menu and have a first-pass implementation of the Asset Browser working, though only for textures and palettes at the moment.
* All textures in the base game can be viewed.
* Textures are automatically assigned a useful palette.
* The palette on textures can be visually changed.
* Textures can be viewed at different light levels to see how the colormap affects them.
* You can scrub through frames of animated textures.
* Palettes and colormaps can be viewed.
* Assets shown can be limited to those that are used in specific levels.

<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/AssetBrowser1.jpg?raw=true" alt="AssetBrowser1" class="inline"/>
<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/AssetBrowser2.jpg?raw=true" alt="AssetBrowser2" class="inline"/>
<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/AssetBrowser3.jpg?raw=true" alt="AssetBrowser3" class="inline"/>

## Current Plans
Rough editor plans going forward. This isn't *all* of the work needed, but instead captures the initial chunk of
work to make the editors useable. Planning will continue once a decent amount of this has been done.

There are two main "work streams" listed here - the Asset Browser and Level Editor. However it is not intended that
the Asset Browser stream is finished before the Level Editor work begins. Most likely I will be jumping between
them as it makes sense for the work.

Note also that work already done for the Asset Browser is not listed here.

## Asset Browser / Core
I. Core Systems
* Add Editor Config
  * Editor Data Path
    * Path to store editor settings, thumbnails, and other editor specific data.
  * Export Path
    * For generic, non-project based file exports and conversions.
  * UI Font Scale
  * UI Thumbnail Scale
    * Compute default UI scaling based on monitor resolution.
	* UI scaling should be adjustable.
* Separate thumbnails from Asset Info image(s).
* Generate thumbnails and store to disk.
* Load generated thumbnails if they exist, else generate.
* Do NOT preload textures, images, and other data except for thumbmails. Lazy loading.
* Handle font scale, set default based on monitor resolution.
* Handle thumbnail scale, set default based on monitor resolution.
* Add Export option for textures and palettes.

II. Resources
* Add the ability to add and remove resources (zips, gobs, folders).
* Add the ability to ignore or hide core game resources.

III. Functionality
* Frame browser.
* Refactor code based on having three different asset types working.
  * Split into shared and unique parts.
  * Factor out common UI patterns.
* Sprite browser.
* 3D Object browser.
* Level browser.
* Final refactor step.

### Projects
I. Core
* Project system.
  * Name, Description, Path, Type (Level, Resources), Game (Dark Forces, Outlaws), Feature Set (Vanilla, TFE).
* Menu options - New, Open, Close, Recent.
* Create project from existing GOB/Zip/Folder.

II. Import/Edit
* Add Import features for each asset type.
  * Convert from true-color, etc.
* Create complex types - such as Wax data.
* Create voxel model editor to handle import, settings, and setting up animations.
  * Port software voxel renderer over from the branch.
  * Add GPU-based voxel renderer.
  * Add "map hacks" equivalent for adjusting voxel models
  (though it might be good to add support for this to the level editor, so it can be done visually).

III. Object Templates
* Auto-generate object/logic templates based on the original game.
* Add the ability to edit and create new object templates.
  
### Outlaws
I. Initial Work
* Add support for Outlaws formats - (PCX, LVT/LVB, NWX, etc.).

## Level Editor
Plans here are a little more unclear, the plan is to get the basics working again and then plan from there.

I. Restoration / Refactor
* Basic UI - ported to new UI patterns and supporting UI scaling.
* Add support for bindable level editor hotkeys (similar to the game).
* Restore level editor rendering.
* Implement new triangulation based on constrained delaunary triangulation
(much more robust then the library I was using, removes any dependencies for triangulation since I will just write it myself).
* Use Project system to allow for creating new levels and editing existing levels.
* Restore basic editing.
* Basic Outlaws level loading / support.
