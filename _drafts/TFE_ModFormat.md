## TFE Mod "Meta-Format"
Zip file containing the following files:

### Recommended for all mod types
 * CoverPic[.PNG;.JPG] - either a PNG or JPG, this will be shown as the mod "cover" during selection.
 * Info.txt - summary shown during mod selection, with the option to view the whole description (below).
 * ModName.TXT - full mod description
 
### Required for Vanilla compatible mods
 * *.GOB / *.LAB - archive file(s) if using a "classic" mod - contains all assets except for LFD.
 * *.LFD - equivalent of dfbrief.lfd, used for briefings.
 
### Alternative format for TFE mods, using the ZIP directly as the archive
Mods may be run directly from folders but it is recommended to run the zip files directly. But using a plain directory may be desirable during development. The following sub-directories must be used, though only new content is required. If a file is not found in the mod, then the next mod in the list or base game data will be used.
 * Game/* - files that control overall gameplay such as Cutmuse.txt, Text.msg, Cutscene.lst, Jedi.lvl
 * LFD/* - custom LFD files that will be referenced by cutscenes, may include dfbrief.lfd.
 * Graphics/* - images and fonts not used as textures, sprites/frames or for cutscenes.
 * Textures/* - textures to include in the mod, can use sub-directories (for example Textures/Wood/Oak.bm would map to "Wood/Oak.bm")
 * Sprites/* - sprites and frames to include in the mod, can use sub-directories
 * Models/* - 3D models to include in the mod.
 * Levels/* - level files to include with the Mod (geometry, objects, INF).
 * Palettes/* - palettes and colormaps, referenced by Levels/
 * Sounds/* - sound effects files.
 * Music/* - midi and OGG music files.
