---
layout: page
title: Roadmap
---

## Version 1.0 Release [Released]
### Release: December 19, 2022
With this release, TFE is a complete replacement for DosBox for most players. This release includes the perspective-correct GPU renderer. This milestone has been successfully reached.

## Linux Support
*Finished*<br>
Basic Linux support has been completed, though Flatpaks and other distribution methods still need to be done.

## Post Processing and Bloom
*Finished*<br>
The Post-processing pipeline was implemented, including a bloom effect that can be adjusted to taste.

## True Color Support
*Finished*<br>
True-color support was implemented with options for colormap blending, full true-color rendering, and texture filtering.

## Level Editor
### Estimated Release: Early 2024
Built-in **level editor** for Dark Forces that can be used to make complete levels with goals, INF support, editable entities, and everything else needed. Support for **Outlaws** levels will be coming later.

## Asset Editor
### Estimated Release: Early 2024
Finish the Asset Browser, started in 2023. In addition to the formats currently supported, support will be added for formats needed for cutscenes, and UI. And finally new assets - such as HD assets and voxels.

## HD Asset Support
### Estimated Release: Early 2024
With the tools in place, the plan is to support higher resolution and true-color assets. This includes textures, already includes models (3DO limits were removed previously as an option), and 44.1kHz audio (wave files).

## Voxels
### Estimated Release: Early to Mid 2024
Quite some time ago now, I implemented an experimental voxel renderer that integrated seamlessly with the Jedi classic renderer. However, there were some loose ends to deal with, such as not supporting the full VOX format and dealing with some palette issues. This release will integrate that code with the main branch and add support for replacing objects with their voxel counterpart.

## Dynamic Lighting
### Estimated Release: Early to Mid 2024
Dynamic light was implemented in a branch along with true color rendering. But it needs to be cleaned up and some tweaks need to be made for release. This will include shadows, and the ability to attach lights to objects/frames.

## Towards Version 2.0
### Estimated Release: Late 2024
Outlaws support has already begun on the back end and I have a pretty clear understanding of the renderer and other aspects of the game. Once the level editor supports Dark Forces and is useable, I plan on adding support for Outlaws assets and Outlaws levels. From there, I will start implementing proper support with iterative releases throughout the year.
