---
layout: post
title: DF Classic Renderer Progress
---
Work on the reverse-engineering effort has been progressing well. The sector rendering portion is almost complete with some more work in the next few weeks on sprites and 3d objects. The goal of this effort is to finish the Classic Renderer (for Dark Forces) and have all levels and mods render correctly - except for issues caused by missing gameplay elements (caused by INF bugs or lack of AI).

The renderer will continue to support higher resolutions, such as 1080p. However limits will only be accurate at 320x200. To put it simply, resolutions beyond 320x200 have graphical issues with the base DOS limits. In other words 320x200 will produce near identical results to DosBox (same limits, etc) but resolutions beyond that will relax those limits as needed.

The Classic Renderer will also have hardware support, which means faster rendering at higher resolutions and optional texture filtering. I will post more about hardware rendering features once the software renderer is complete. There will also be additional options in order to improve performance and optionally even rendering quality.

The renderer in the current build has issues with low light environments, where the lighting itself doesn't quite match the original. The Classic Renderer fixes this (among other issues) - so I put together a screenshot that shows the Classic Renderer and DosBox side by side. The Force Engine version was resized in Photoshop and cropped so there is some slight distortion and the viewpoints aren't exactly the same but I think you will be able to see that the character of the rendering, lighting and colors match.

<a href="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/ClassicRendererAndDosBox.png?raw=true" class="inline"><img src="https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/ClassicRendererAndDosBox.png?raw=true" alt="Comparison" class="inline"/></a>
