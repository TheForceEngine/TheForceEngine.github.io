---
layout: default
title: TFE Hardware Renderer
permalink: TFE_HardwareRenderer.html
---

# Steps to Recursively Draw Sectors in Software
This is a summary of the rendering pipeline used by the software renderer now. This is the starting point for thinking about the GPU renderer.

## Per-Frame Processing
* Update the sector cache (for floating point rendering only).
* Transform sector vertices into viewspace (2D).
* Transform object positions into viewspace (3D).
* Process walls
  * Cull walls completely behind the near plane.
  * Cull walls outside the frustum on the left or right.
  * Cull back facing.
  * Clip by the 2D frustum.
  * Project vertices, including hole filling by the near plane.
  * Build a wall segment for each potentially visible wall.

## Per-View Processing
* Merge-sort wall segments based on view.
  * Skip walls outside the view window.
  * Clip the segment to the window horizontally (x).
  * Find overlapping segments and split segments so that only the closest segments survive.
  * Add split segments into the wall segment list.
* Sort visible wall segments from left to right (in x).
* Loop through walls.
  * Draw Wall parts, writing per-column depth to the 1D depth buffer.
  * Add top and bottom edges for later flat rendering.
  * Add adjoin segments and edges for portals.
* Draw sky and/or floor and ceiling based on edge segments generated in the previous step.
* Setup Window for recursion - this creates our vertical mask.
  * Start with top and bottom column heights.
  * Loop through each adjoin and adjust column heights based on the adjoin edges.
* Loop through adjoin segments - this is the recursion step.
  * Save draw current state
  * Compute window bounds, including depth.
  * Recurse to the next sector.
  * Restore draw state.
  * Draw the mask wall, if the adjoin has one.
* Determine whether to use the current window top/bot columns to clip objects or the previous (parent) - objects are always clipped by the x range.
* Sort objects from back to front (mostly - “bridges” add a wrinkle).
* Draw objects in order, clipping by window and the 1D z-buffer filled in by step 3.

# GPU Renderer Plans
## Goals
* Match the CPU renderer *results* as closely as possible, to preserve the look and mods.
  * Handle sprites correctly versus flats.
  * Preserve the CPU draw order.
  * Adjoin clipping has to match close enough for non-euclidean space tricks to work and mods to look correct.
  * Palette emulation needs to be supported.
* Both “shearing” and “perspective” support.
  * The shearing look preserves the original game look and gameplay the closest and adding GPU acceleration means people can play this way at really high frame-rates and resolutions.
  * Proper perspective when looking up and down is preferred by the majority of players and makes playing with mouse-look more comfortable.
* High performance rendering - which means pushing as much of the work to the GPU as is practical with OpenGL 3.3 features.
  * Exact clipping is not required if the visual results match (allow overdraw).
  * Using the z-buffer is valid if floor and ceiling versus object behavior matches the original (after all the software renderer uses a 1D z-buffer to clip objects to walls).
  * Push clipping/masking to the GPU whenever possible.
  * Allow some overdraw if it means less data to send between the CPU and GPU.
  * Keep required shaders as simple as possible while meeting the goals outlined above. (More complexity can be added later as long as it is optional).

## Non-Goals
* Emulating texture warping with 3DO rendering. This is one area I think the renderer can deviate with little issue and allow for perspective correct texturing everywhere.
* Emulate 3DO sorting errors. This is another case where I have not seen any mods make use of this and always appears as a visual glitch. One idea is to use the z-buffer here by allowing 3DO objects to write and read from the z-buffer. This means that CPU based sorting won’t be necessary, which means that 3DO geometry only has to be transferred to the GPU once.
* Immediate support for additional effects - ambient occlusion, point lights, true color, etc. - these will be tackled in the future and are lower priority than core functionality.

## Concepts
* Identify all adjoins in the view frustum and current window for recursion - this means we may recurse into more sectors, but it avoids having to handle wall processing on the CPU.
* Push wall quads to the GPU, including quads to project the floor and ceiling onto.
* Draw wall parts - reading and writing to the z-buffer.
* Draw floor and ceiling quads (projecting the texture or sky) - read-write to the z-buffer (writing wall depth, not floor plane depth).
* For each adjoin:
  * Make a list of sectors.
  * Keep adjoin screen-space rect for further clipping, culling, and to extend the floor and ceiling quads.
  * The adjoin plane can be used as a near plane for clipping - this means we can just rely on the z-buffer and near plane for clipping, meaning we can use “oblique” clipping.

## Oblique clipping:
This has the advantage of not needing a mask, of being well supported on AMD and NVidia, and using the depth-buffer to best advantage, including fast z-culling.

* Draw the current sector - walls, floor and ceiling.
  * Floor and ceiling quads are extended to the top of the screenspace clip-rect along the same plane as the portal.
  * Any quads that are outside that clip rect can be culled.
  * Depth is the wall plane depth, not the floor and ceiling depth, in order to properly support object-in-floor rendering.
  * By extending the wall plane with additional quads, tessellation is not required even for perspective rendering and using wall depth is the equivalent of the Jedi 1D depth buffer extended to 2D for perspective.
  * No software clipping is required, clipping is handled through the screenspace clip-rect, the depth buffer and the modified near-plane.
* For each adjoin, set up a near-plane and screenspace clip-rect. By re-purposing the frustum near plane, custom hardware clip planes are not needed - which are generally very buggy on some drivers, work differently on NVidia and AMD, and come at a noticeable performance cost on some hardware.
* This means that we can’t look straight up (I think, this will need to be revisited later)... but something like 80 deg or so should be fine.
* Render the next sector, using the depth buffer + near-plane for clipping.
* Merge adjacent adjoins to look into the same sector if they share planes.
* Objects are rendered last, pre-sorted based on position. Sorting is done on the CPU.
* 3DO objects read and write to the depth buffer to handle sorting, no per-polygon sorting is done. This means 3DO geometry will always have the correct sorting.

* 3DO objects use static vertex and index buffers and only the transforms are updated. Quads are already triangulated in Jedi, so it is still just triangles.
  * Dithering between light levels can be approximated, but this will likely look slightly different than the software renderer.
* Sector geometry and sprites are built from dynamic quads.
  * The index buffer is pre-created and stored on GPU, since all dynamic geometry is made of quads this buffer never needs to be updated but has a maximum size.
  * The dynamic vertex buffer is updated each frame.
  * A sector’s vertex buffer is only updated once per frame, even if it is rendered through multiple views.

## Bandwidth
If we assume 2,000 sectors and 16 walls per sector average, with an average of 2 portals which all require top and bottom parts.

```
2,000 * 14 solid walls = 2,000 * 14 * 3 quads (wall + floor + ceiling) +
2,000 * 2 adjoins = 2,000 * 2 * 4 quads (top + bottom + floor + ceiling) =
100,000 quads * 4 = 400,000 vertices.
```

That is assuming *every* sector is visible. In reality, a small fraction will be potentially visible every frame, even when culling is more loose. So, assuming 10% are potentially visible, though it is highly unlikely to be that high, then:

```
200 * 14 solid walls = 200 * 14 * 3 quads (wall + floor + ceiling) +
200 * 2 adjoins = 200 * 2 * 4 quads (top + bottom + floor + ceiling) =
10,000 quads * 4 = 40,000 vertices.
```

If we assume 32 bytes per vertex, then that requires transferring 1.22MB/frame versus 1.98MB/frame for a 1920x1080 8bpp framebuffer. In other words, the amount of bandwidth scales with visible complexity instead of resolution and already reduces the bandwidth requirements at HD resolutions.

Bandwidth can be further reduced if sector changes are tracked, similar to the caching that already occurs in the floating point software renderer. In addition, vertex data can be quantized to reduce the size down to 24 or even 16 bytes per vertex. This would allow for much larger maps, perhaps even hundreds of thousands of sectors.
