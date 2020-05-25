---
layout: post
title: Upcoming DF Classic Renderer Release
---

This post concerns the next major **test release**, the DF Classic Renderer Release. There may be smaller releases in the meantime, such as bug fixes or quality of life improvements.

## Classic Renderer
The "Classic Renderer" is the Dos-Dark Forces derived Jedi Engine renderer. This covers the rendering in the 3D view - purely 2D rendering such as UI is basically done except for a few bugs. This renderer involves several key components: walls with overlays (such as switches or signs), flats (floors and ceilings), mask walls (walls with transparent elements such as fences or force fields), sprites and 3D models - with proper light attenuation in different situations.

For a more thorough description of the renderer Dos itself see the work in progress **Dark Forces (DOS) Rendering** series starting with [Dark Forces (DOS) Rendering, Part I](_posts/2020-05-16-DFRender1.md). I will probably post Part 2 within a week or so.

## DF Classic Renderer Release
The current renderer in the test release is not complete and not fully accurate - there are several issues such as sorting issues with sprites versus walls in a few cases and incorrect sorting with 3D objects versus sprites and walls in general. There are also some issues with wall rendering in some mods - such as "Prelude to Harkov`s Defection" (see the tram/subway). Finally the light falloff is not quite correct (though it is close in many levels), which is probably most obvious in Gromas Mines - the fog effect does not match the original very well in some areas.

As the reverse-engineering of the original rendering nears completion, The Force Engine code is being updated and the code refactored. The ultimate goal of this release is to complete the Classic (DF) Renderer and ensure that it is functionally identical to the Dos version in 320x200. As I have been working, when I identify look-up tables I spend the time to make sure I understand how to accurately re-build the tables - with this knowledge I can remove the tables entirely when appropriate in order to support higher resolutions without sacrificing accuracy.

While refactoring the renderer code I plan on implementing a few non-DOS based features:
  * Widescreen support.
  * "Window-Resolution" option that changes the virtual resolution to match window size and aspect ratio.
  * Improved software renderer performance.
  * [Maybe] Classic Hardware Renderer.
  
Note that after the gameplay is more complete there will be another big renderer release before the project beta release in November that will feature the "Perspective Renderer", more hardware support and Outlaws Jedi Engine enhancements (such as slopes, double adjoins, vertical adjoins, etc.). The goal of this release is renderer accuracy so that all levels and mods are rendered correctly and visually match the DOS version at 320x200.

## Next Steps
Once the DF Classic Renderer Release is finalized, the next steps are to focus on gameplay elements - fully accurate collision detection and player movement, AI and weapons. These will be broken down into major test releases, in a similar manner as the DF Classic Renderer. 

<a href="https://the-force-engine.freeforums.net/thread/15/df-classic-renderer-release">Add Comment</a>
