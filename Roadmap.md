---
layout: page
title: Roadmap
---

# Version 1.0 Release
### Release: December 19, 2022
With this release, TFE will be a complete replacement for DosBox. This release will also include the perspective-correct GPU renderer.

# Tools
### Estimated Release: Early 2023
The focus of this release is to get the tools working again with the reverse-engineered code. This will include basic functionality like importing and exporting assets, viewing them, etc. and the first release of the full level editor. It might still be missing some planned features, but as of this release it should be fully usable for building real levels and mods.

# Mac and Linux Support
### Estimated Release: Early 2023
With this release, TFE will gain initial support on Mac and Linux. While the code more or less compiles on Linux (or is pretty close), there is more work to make sure it works well. And the Mac requires its own treatment and testing.

# Voxels
### Estimated Release: Early 2023
Quite some time ago now, I implemented an experimental voxel renderer that integrated seamlessly with the Jedi classic renderer. However, there were some loose ends to deal with, such as not supporting the full VOX format and dealing with some palette issues. This release will integrate that code with the main branch and add support for replacing objects with their voxel counterpart.

# Towards Version 2.0
Once version 1.0 is released, I plan on beginning the process of adding Outlaws support to TFE. I don’t yet have any real way of making any time estimates beyond this point, but I expect the reverse-engineering process to proceed at a much quicker rate for Outlaws for several reasons:

* I have become a lot faster at the process by going through the process of reverse-engineering Dark Forces.
* Outlaws was built from the Dark Forces code base, and shares the same engine. This means a lot of the structures will be the same or substaintally similar.
* I have a better sense of how to organize the process and reduce re-work and refactoring time.
