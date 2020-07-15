---
layout: default
title: TFE Mod "Meta-Format"
permalink: TFE_ModFormat.html
---

## TFE Mod "Meta-Format" [Draft]
Zip file or directory containing the following files:

### Recommended for all mod types
 * __CoverPic[.png;.jpg]__ - either a PNG or JPG, this will be shown as the mod "cover" during selection.
 * __Info.txt__ - summary shown during mod selection, with the option to view the whole description (below). This includes the display name, summary and link.
 * __ModName.txt__ - full mod description
 
### Required for Vanilla compatible mods
 * __ModName.GOB / ModName.LAB__ - archive file(s) if using a "classic" mod - contains all assets except for LFD.
 * __ModName.LFD__ - equivalent of dfbrief.lfd, used for briefings; only required if custom briefings are needed.
 
### Alternative format for TFE mods, using the ZIP directly as the archive
Mods may be run directly from folders but it is recommended to run the zip files directly when released and using a plain directory during development. The following sub-directories must be used, though only new content is required. Sub-directories with no content may be omitted. If a file is not found in the mod, then the next mod in the list or base game data will be used.

Each main directory may have sub-directories, though assets will have to include those sub-directories. For example under Textures/ you may have a sub-directory named Wood/ with Oak.bm inside. To reference Oak.bm, you would use "Wood/Oak.bm".

 * __Game/*__ - files that control overall gameplay such as Cutmuse.txt, Text.msg, Cutscene.lst, Jedi.lvl
 * __LFD/*__ - custom LFD files that will be referenced by cutscenes, may include dfbrief.lfd.
 * __Video/*__ - custom videos for cutscenes, may be in "SAN" format (https://wiki.multimedia.cx/index.php/SAN) or a more modern format (once support has been implemented).
 * __Graphics/*__ - images and fonts not used as textures, sprites/frames or for cutscenes.
 * __Textures/*__ - level textures. (BM, PCX)
 * __Sprites/*__ - sprites and frames. (WAX, FME, NWX)
 * __Models/*__ - 3D models. (3DO)
 * __Levels/*__ - level files. (geometry, objects, INF)
 * __Palettes/*__ - palettes and colormaps, referenced by Levels/
 * __Sounds/*__ - sound effects files (VOC, WAV).
 * __Music/*__ - midi and OGG music files.
