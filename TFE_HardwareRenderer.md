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

# GPU Renderer Design
TODO
