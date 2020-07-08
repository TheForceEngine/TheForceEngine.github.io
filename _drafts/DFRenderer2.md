---
layout: post
title: Dark Forces (DOS) Rendering, Part II
---

Dark Forces (DOS) Rendering, Part I
Dark Forces (DOS) Rendering, Part II

`Note: many images in this post were generated using Desmos, an online graphing calculator.`

This post is the second in a series of posts that take a deep dive into the Jedi renderer as implemented in Dark Forces (DOS). This will continue where [part 1](https://theforceengine.github.io/2020/05/16/DFRender1.html) left off. At the end of the last post, we had transformed our sector vertices into viewspace, determined which walls were potentially visible and clipped them to the view frustum and finally projected them to screenspace building "WallSegments" that were ready for rendering.

As review from the last post, each Wall Segment has been clipped to camera frustum and projected. These Wall Segments are facing the camera and at least partially inside the frustum. See the image below

<img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/images/WallSegments.png?raw=true" alt="Wall Segments" class="inline"/>

## Wall Draw Flags
During level load or whenever a sector is updated, some extra setup occurs that determines how the walls will be drawn later. We consider a wall as made up of three parts - top, bottom and middle (top, bot, mid in the code). A solid wall will consist of only the mid part. If the wall is adjoined (connected) to another sector, then it may have a top and/or bottom part.

`WallDrawFlags`<br>
`  WDF_MID = 0`<br>
`  WDF_TOP = 1`<br>
`  WDF_BOT = 2`<br>

Simply put if the next sector floor height is higher than the current sector, then WDF_BOT is set. If the next sector ceiling is lower than the current sector the WDF_TOP flag is set. If both are true than WDF_TOP and WDF_BOT are set and if neither are true than draw flags will be WDF_MID - either a solid wall or the floor and ceilings both match between sectors. It is possible to render top and/or bottom and middle parts, but in that case it is a transparent wall which is handled seperately.

In addition to setting up draw flags, the texel height of each part is calculated:<br>
`Sector* next = wall->nextSector;`<br>
`Sector* cur  = wall->sector;`<br>
`if (wall->drawFlags & WDF_TOP)`<br>
`{`<br>
`  wall->topTexelHeight = (next->ceilingHeight - cur->ceilingHeight) * worldToTexelScale;`<br>
`}`<br>
`if (wall->drawFlags & WDF_BOT)`<br>
`{`<br>
`  wall->botTexelHeight = (cur->floorHeight - next->floorHeight) * worldToTexelScale;`<br>
`}`<br>
`if (wall->midTex)`<br>
`{`<br>
`  if (!(wall->drawFlags & WDF_BOT) && !(wall->drawFlags & WDF_TOP))`<br>
`    wall->midTexelHeight = (cur->floorHeight - cur->ceilingHeight) * worldToTexelScale;`<br>
`  else if (!(wall->drawFlags & WDF_BOT))`<br>
`    wall->midTexelHeight = (cur->floorHeight - next->ceilingHeight) * worldToTexelScale;`<br>
`  else if (!(wall->drawFlags & WDF_TOP))`<br>
`    wall->midTexelHeight = (next->floorHeight - cur->ceilingHeight) * worldToTexelScale;`<br>
`  else`<br>
`    wall->midTexelHeight = (next->floorHeight - next->ceilingHeight) * worldToTexelScale;`<br>
`}`<br>

In the original code the multiplication with worldToTexelScale is really a left shift by 3 since `worldToTexelScale = 8` but I modified it for clarity. This means that there are 8 texture pixels (texels) per world unit (DFU).

** Insert Image of wall with top and bottom parts **

## The Window
I will often refer to the "current window" - so what does that mean exactly? Jedi is a portal engine at heart (portals are called "adjoins" by the engine), so the window is the clipped portal that we are currently looking through. Portals are clipped by their parent portals, becoming smaller and smaller as we look through more of them. Portals consist of a bounds in screenspace (`s_windowMinX` and `s_windowMaxX` in the code), a minimum depth value (`s_windowMinZ`), a screenspace Y range per X value (`s_windowTop[]` and `s_windowBot[]`). An overall minimum and maximum Y is stored as well (`s_windowMinY` and `s_windowMaxY`). When starting at the camera, these values are set to cover the entire view.

** Insert Image of Window **

## Segment / Line Crossing
The core "work horse" function used to determine which wall is in front of another in Jedi is `segmentCrossesLine()` - so I will explain the concept before delving into the merge/sort algorithm. The function determines if a 2D line segment `A` crosses an infinite line `B` - i.e. is the line segment A disjoint from the line formed by B or does it intersect? The function returns one of the following:

`0: the line segment A intersects line B`<br>
`1: the line segment A does NOT intersect line B`<br>

The math is fairly straight forward (as seen in the original code):
`segCross = ((A1.x - B0.x)*(B1.y - B0.y) - (A1.y - B0.y)*(B1.x - B0.x)) * ((A0.x - B0.x)*(B1.y-B0.y) - (A0.y - B0.y)*(B1.x - B0.x))`
`return segCross > 0 ? 1 : 0;`

Which is: `(A1-B0)x(B1-B0) * (A0-B0)x(B1-B0)` where x = perp product (aka "2D cross product" - even though that isn't quite accurate mathematically).

** Insert diagram **

## Wall Merge Sort
The next step is to sort the sector Wall Segments and clip them to each other and the current window. Really this is the core of the sector rendering engine, it allows for rendering complex sectors without precomputation. Unlike BUILD, however, each sector is independent and so the sorting and clipping occurs per sector as we go.


