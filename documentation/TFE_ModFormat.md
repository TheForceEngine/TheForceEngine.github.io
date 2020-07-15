---
layout: default
title: TFE Mod "Meta-Format"
permalink: documentation/TFE_ModFormat.html
---

## TFE Mod "Meta-Format"
Zip file or directory containing the following files:

### Recommended for all mod types
 * CoverPic[.png;.jpg] - either a PNG or JPG, this will be shown as the mod "cover" during selection.
 * Info.txt - summary shown during mod selection, with the option to view the whole description (below). This includes the display name, summary and link.
 * ModName.txt - full mod description
 
### Required for Vanilla compatible mods
 * *.GOB / *.LAB - archive file(s) if using a "classic" mod - contains all assets except for LFD.
 * *.LFD - equivalent of dfbrief.lfd, used for briefings.
 
### Alternative format for TFE mods, using the ZIP directly as the archive
Mods may be run directly from folders but it is recommended to run the zip files directly when released and using a plain directory during development. The following sub-directories must be used, though only new content is required. Sub-directories with no content may be omitted. If a file is not found in the mod, then the next mod in the list or base game data will be used.

Each main directory may have sub-directories, though assets will have to include those sub-directories. For example under Textures/ you may have a sub-directory named Wood/ with Oak.bm inside. To reference Oak.bm, you would use "Wood/Oak.bm".

 * Game/* - files that control overall gameplay such as Cutmuse.txt, Text.msg, Cutscene.lst, Jedi.lvl
 * LFD/* - custom LFD files that will be referenced by cutscenes, may include dfbrief.lfd.
 * Video/* - custom videos for cutscenes, may be in "SAN" format (https://wiki.multimedia.cx/index.php/SAN) or a more modern format (once support has been implemented).
 * Graphics/* - images and fonts not used as textures, sprites/frames or for cutscenes.
 * Textures/* - level textures. (BM, PCX)
 * Sprites/* - sprites and frames. (WAX, FME, NWX)
 * Models/* - 3D models. (3DO)
 * Levels/* - level files. (geometry, objects, INF)
 * Palettes/* - palettes and colormaps, referenced by Levels/
 * Sounds/* - sound effects files (VOC, WAV).
 * Music/* - midi and OGG music files.
