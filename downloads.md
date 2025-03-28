---
layout: page
title: Downloads
---
**Downloads**
* [Version 1.22.2, Windows Build](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.22.200/TheForceEngine-v1.22.200.zip)<br>
* [Version 1.22.2, Source Code](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.22.200.zip)
 
**Editor Documentation**
This is still WIP and incomplete
* [Manual (WIP)](https://df-21.net/wiki/?title=TFE-EDITOR)
* [Tutorials (WIP)](https://youtube.com/playlist?list=PLz1JY7gjEDQQa-IgwVznTOXdjmBqDHSCm&si=BQpxruRilQMC-NxR)

**A purchased copy of the original game is required and is not provided by The Force Engine.** The [documentation](https://theforceengine.github.io/Documentation.html) has information on how to legally purchase Dark Forces.

Generally it is a good idea to download the latest available version. Previous builds are mainly for archival purposes. When downloading a new version, simply copying over an existing install will work fine. Note that there are no automatic downloads and TFE does not currently connect to the internet in any way. However, optional features such as checking for the latest version, directly downloading new versions and mods, and similar features will be added later.

This means that you will need to check for new versions of TFE manually for now.

### Timeline
The release of version 1.0 is a momentus event but it is not the end of the road. Outlaws support will be coming in version 2.0 and before that there will be new features, bug fixes, cross-platform support, and the built-in editors (including the level editor). See the [TFE Roadmap](Roadmap.md) for more information.

### Having Issues Running TFE?
* If TFE does not start, you may need to install the VC++ Redistributable Package. Install the latest version, x64 only.
[https://learn.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170](https://learn.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170)

* If you get a message saying *MFPlat.DLL was not found* you may not have the *Media Feature Pack* installed, which is the default. To fix *Open Settings, Apps & features. On the right side, click Optional features. Install “Media Feature Pack”*.

* If you run into other issues, see [documentation](https://theforceengine.github.io/Documentation.html).

### Version 1.22.200
**Windows Build** [TheForceEngine-v1.22.200.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.22.200/TheForceEngine-v1.22.200.zip) <br>
**Source Code** [v1.22.200.zip](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.22.200.zip)

Another small iterative release with TFE Editor improvements.

## Changes
* Added the ability to invert the Y axis for camera rotation.
* Added shortcuts for edit modes: draw, vertex, wall/surface, sector, and entity.
* Added shortcuts for Resetting and Aligning the grid.
* Added a shortcut to reset texture offsets.
* Added a shortcut for Join Sectors.
* Added a confirmation dialog for Reloading a level.
* Added a confirmation dialog when trying to close the level editor or exit when there are unsaved changes.
* A popup error message is now shown when trying to test a level with no source port set.
* Added an option to make new sectors use the DEFAULT texture (Level menu -> User Preferences -> Editing: New sectors use DEFAULT texture.
* Double-click selection and Auto-align properly respect Group locked and hidden states.
* In the INF editor it is now much easier to select an elevator, trigger, or teleporter - just click on the Class: Type labels.
* In the INF editor, you can now delete selected elevators, triggers and teleporters.
* Fix WAX packing to account for rows not perfectly fitting into the rows - this was causing a crash.
* Fixed a crash in level_unpackSectorAttribSnapshot() when the group ID is not valid, but an error is written instead.

### Version 1.22.100
**Windows Build** [TheForceEngine-v1.22.100.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.22.100/TheForceEngine-v1.22.100.zip) <br>
**Source Code** [v1.22.100.zip](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.22.100.zip)

A small iterative release with early TFE Editor improvements.

## Changes
* Added option to avoid waiting for process completion, this process is not completing correctly for at least one user.
  * If the Level Editor is crashing when you hit play to test, go to the **Level** menu > **User Preferences** > **Editing** > disable **On Play, wait for process completion**.
* Cleans up the curve segment controls, so the number of segments is properly clamped (no more having to hit the key multiple times to see a change).
* Changed the "Lock movement" shortcut text to be more clear.
* Added shortcuts to move the camera up and down in the 3D view (Space, Ctrl+Space by default).
* Fixed a crash trying loading a sprite when an Archive is null.
* Added support for mouse buttons to be used for shortcuts (except for left-mouse).
* Added editable shortcuts for
  * Texture mouse panning.
  * 2D viewport panning.
  * 3D camera rotation.

### Version 1.22.000
**Windows Build** [TheForceEngine-v1.22.000.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.22.000/TheForceEngine-v1.22.000.zip) <br>
**Source Code** [v1.22.000.zip](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.22.000.zip)

With this release the **TFE Editor** finally hits the **Alpha** phase. Documentation and tutorials are still being worked on - but here is what is currently available:
* [Manual (WIP)](https://df-21.net/wiki/?title=TFE-EDITOR)
* [Tutorials (WIP)](https://youtube.com/playlist?list=PLz1JY7gjEDQQa-IgwVznTOXdjmBqDHSCm&si=BQpxruRilQMC-NxR)

**What's Changed**
* TFE Editor Alpha Release @luciusDXL 
* Replay support @ifeldshteyn 
* Fix building on ARM and make CI run on x86 and aarch64 Linux by @fpiesche
* Add GS_Player class by @jerethk
* Fixed JSon/External data pathing on Linux @jerethk 
* Fixed Pickup serialization issue @jerethk 
* Cleaned up Linux build - removed option for scripting (always enabled), fixed related issues. @luciusDXL 
* Various bug fixes, such as weapons not showing fullbright pixels correctly in true color. @luciusDXL 
* Added GS_Player class @jerethk 
* Added more Mod-Conf overrides @jerethk 

### Version 1.15.000
**Windows Build** [TheForceEngine-v1.15.000.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.15.000/TheForceEngine-v1.15.000.zip) <br>
**Source Code** [v1.15.000.zip](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.15.000.zip)

This release improves moddability by externalizing previously hard-coded data into ExternalData/DarkForces/ and allows for many properties of effects, pickups, projectiles, and weapons to be changed. In addition, first pass scripting integration has been implemented in the form of script functions that can be called from INF.

**What's Changed**
* Numerous bug fixes (everyone)
* Many editor changes @luciusDXL
* ForceScript API work @luciusDXL
* ScriptCall functionality in INF (with editor support) @luciusDXL
* Script state serialization for save games @luciusDXL
* CMake: automatically make system midi optional by @mlauss2
* Update Dear ImGUI to 1.90.9 by @mlauss2
* Use external release metadata XML for Flathub info by @fpiesche
* Replace GLEW with built-in GLAD by @mlauss2
* Fixes for GCC LTO (Link Time Optimizations) by @mlauss2
* Enable item ten by @jerethk
* Adding logging timestamps by @ifeldshteyn
* Ading new input buttons such as HD, screenshot and GIF recording. by @ifeldshteyn
* Mod conf overrides by @ifeldshteyn
* Adding Mouse panning to the PDA by @ifeldshteyn
* Custom logic proposal by @jerethk
* Add mod directory to s_searchPaths when loading from a custom GOB by @jerethk
* Adding open folder button for mods. by @ifeldshteyn
* GIF capture feedback messages by @kevinfoley
* actor.cpp, flyers.cpp, sewer.cpp: replace anim.state magic numbers ... by @kevinfoley
* dragon, phaseOne: replace anim.state magic numbers with enum values… by @kevinfoley
* Switch mod conf versioning to 1 by @ifeldshteyn
* Weapon data externalisation by @jerethk
* Fixes for TELEPORTER BASIC by @jerethk
* Make sure we can fly over water sectors. by @ifeldshteyn
* Change to forward slash for paths by @jerethk
* Custom logics fix by @jerethk
* New Dev panel with lighting controls by @kevinfoley
* Fix VUE camera by @jerethk
* Subdirectory related amendments by @jerethk
* Externalise pickups by @jerethk
* Fix custom logics serialisation by @jerethk
* Add svg redraw of app icon following modern icon guidelines by @fpiesche
* Check for FME extension before attempting to load a FME by @jerethk
* Externalise weapons by @jerethk
* Actor code readability amendments by @jerethk
* Fix building on Linux by @sotpapathe
* Fix for fist ammo by @jerethk


### Version 1.10.000
**Windows Build** [TheForceEngine-v1.10.000.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.10.000/TheForceEngine-v1.10.000.zip) <br>
**Source Code** [v1.10.000.zip](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.10.000.zip)

It has been months since the last official release. While most of my work has been directed towards the Level Editor, there still have been a large number of changes and improvements that have accumulated in that time frame, many from contributors.

Below I list the user facing improvements, it is a summary so doesn't go into detail about many GitHub changes, or enumerate every change that went into a feature (such as HD Assets). It also doesn't enumerate the work done on the Level Editor, that will be discussed in the next major release. However you can see all the commits, pull requests and work done on GitHub.

## User Facing Changes (Summarized)
* Added Remaster HD Asset support (textures, sprites, and HUD - cutscenes and briefings coming in the future)
	* Three categories (textures, sprites, HUD)
	* Can be toggled at runtime.
	* Only enabled in "true color" mode.
* Added support for MOD_CONF.txt overrides:
	* TFE option overrides, so mods can enable or disable options as needed.
	* HD Asset opt-out overrides.
* The Dark Forces Remaster is now automatically detected as a valid game data source.
* Mod description text should no longer be cut off in the mod loader.
* Added an option to enable the player to step up onto second altitudes, similar to normal height changes.
* Added a crouch toggle in Game options.
* Cycle next/previous weapon inputs now need to be pressed, making weapon cycling easier using a controller.
* Asset Browser - "resources" can be added (such as gobs/zips).
* Added per-asset editor support.
* Fixed a bug where the weapon muzzle flash would be "stuck" after loading from a save.
* Fixed a true color crash in Imperial Library.
* Fixed a crash in Raid to Ovarid.
* Fixed alpha blending/sorting issues in true color mode.
* Fixed visual issues when using anisotropic filtering.

*Manuel Lauss (mlauss2)*
* Midi fixes
	* Cross platform method for pausing/running midi thread.
	* Introduced "Disabled" device.
	* Fixed midi buffer overrun
* SDL2 fixes on Linux
* Handle Type 2 VOC chunks and avoid spam for unsupported chunk types
* Landru/Music: fixed sequence error in Cutscene Music File parser (mlauss2)
* Fixed numerous clang/gcc warnings, Linux issues, 32-bit issues (though no 32-bit support on Windows is planned), and enabled GCC LTO (Link Time Optimizations).

*Kevin Foley (Kevinfoley)*
* Added one-hit-kill cheat (LAIMDEATH)
* Added one-hit-death cheat (LAHARDCORE)
* "Hardcore" mode cheat: Per request, only projectile and explosive damage will one hit kill the player.
* LAIMDEATH and LAHARDCORE status is now serialized
* Added A11y setting to disable screen flashes (on item pickup and when taking damage)
* Added a slider to System Settings for adjusting GIF recording framerate
* Added Dark Forces cheat menu
* Added new cheat LACAT (gives you 9 lives)
* Added Dark Forces cheat menu (under Game settings)
* Added a new A11y photosensitivity setting to disable player weapon lighting (illumination caused by firing the player's weapons)
* subtitles-en.txt: Add missing end quote to m01reb02 (thanks Doctor Octogonapus)
* A11y: added a "Refresh caption/font files" button to settings menu.
* Added new cheat LABRIGHT; when enabled, renders everything at fullbright.

*Jake Smarter (JakeSmarter)*
* Update AppStream metadata (rename file to match app's component id, drop depracated application element, add more url types, add a number of other elements, add de, en-US, pl translations)
* Desktop Entry updates (rename file to conform to spec, add keywords)
* Improved and updated TFE About text
* Clear color buffers with opaque black instead of transparent black

*Rosalie (Rosalie241)*
* Added workaround for GLEW on Wayland (Linux) (Rosalie241)

*Jerethk*
* New optional setting: observe "solid wall" flag when testing if object overlaps a wall (fixes maps like Harkov and Dark Tide 3 when riding on moving or rotating sectors).
## Other Efforts
Ongoing work not yet publicly facing, GitHub changes, and other backend efforts.

* Level Editor work.
* Work on "Force Script" - which will be used in the editor first to enable custom functionality.
* Integrating Outlaws features into TFE in preparation for Outlaws support (vertical adjoins, dual adjoins, etc.).
* TFE is now on Flathub thanks to contributor efforts.
* Ubuntu Workflow to test compilation on Linux for every diff (Manuel Lauss)
* GitHub Readme updated.



### Version 1.09.540
**Windows Build** [TheForceEngine-v1.09.540.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.09.540/TheForceEngine-v1.09.540.zip) <br>
**Source Code** [v1.09.540.zip](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.09.540.zip)

Another small release that fixes some issues and releases another iteration of the editor (still early WIP).

**Editor**
* Fixed a crash when returning from the Editor the menu, and then selecting editor again.
* Escape now exits the editor, unless a modal dialog is active in which case it closes that dialog instead.
* Levels and 3DOs are listed in the Asset Browser, but functionality is somewhat limited.
* Added multi-select.
* Added the ability to force selected assets to use an alternate palette for testing.
* Added export selected - allowing for assets to be exported and PNGs to be generated where appropriate for viewing.
* Added central error handling and modal message box functionality for errors/warnings.

**General**
* Linux: Make RtMidi optional - this allows for OPL 3 and SF 2 synth but disables system midi.
  * This should make it easier to compile in some cases.
* Replace DeviL with SDL Image to make future Linux packages easier.
* Small PNG issues fixed.


### Version 1.09.530
**Windows Build** [TheForceEngine-v1.09.530.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.09.530/TheForceEngine-v1.09.530.zip) <br>
**Source Code** [v1.09.530.zip](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.09.530.zip)

A bug-fix release, with some improvements to the Accessibility UI, slight improvements to true color texture color accuracy, more work on the TFE editor, and mostly bug fixes.

**TFE Editor**
* Implemented Editor Config with font/UI size and thumbnail size options.
* Improved the Asset Browser UI.
* Added support for Frames and Sprites.
* Factored out Asset system to reduce code and data duplication.

**Game**
* Removed RTAudio and uses SDL audio instead, which fixes a number of audio issues on Linux (@mlauss2).
* Replaced different Windows/Linux Mutex/Thread code with SDL equivalents (@mlauss2).
* Improved German subtitles (@mlauss2).
* Improved Accessibility UI (@kevinfoley).
* Fixed game settings text getting cutoff (@kevinfoley).
* Improved discoloration that can occur to some textures when using the true color mode.

### Version 1.09.521
**Windows Build** [TheForceEngine-v1.09.521.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.09.521/TheForceEngine-v1.09.521.zip) <br>
**Source Code** [v1.09.521.zip](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.09.521.zip)

Bug-fix release, but it includes the per-texture color adjustment when using the true color renderer.

* Removed an extra multiply that was darkening alpha blended edges.
* Disabled alpha blending for sprites when using the true color renderer (fixes fringing artifacts).
* Implemented a per-texture adjustment based on texture hue shift at 50% light level when using the true color renderer.
* Re-enabled the Editor option in the menu (Windows only).
* Initial work on Asset Browser.
* Fixed compile issues on Linux.
* Fixed memory overwrite in audio system.
* Fixed A11y crash on startup.
* Headwave is now a persistent setting in the Accessibility menu.
* Added a better error message when failing to compile a shader.
* If a texture fails to be created, the GL error code is now written.
* Fixed various shader compile issues.

### Version 1.09.500
**Windows Build** [TheForceEngine-v1.09.500.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.09.500/TheForceEngine-v1.09.500.zip) <br>
**Source Code** [v1.09.500.zip](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.09.500.zip)

The "True Color" release.

* Automap is no longer affected by Bloom.
* Fixed several GPU renderer bugs.
* Fixed serialization of Vue state for save games when using Vue smoothing.
* Added the "True color" (non-palettized) colormode, including settings and UI.
* Added support mipmapping and anisotropic filtering.
* Added support for bilinear filtering with sharpness setting.
* Added approximate true-color to colormap mapping.
* FOV is now adjustable with UI slider.
* Three settings templates, instead of two: Vanilla, Retro, Modern.
* Added "LVB" level format loading as work towards future Dark Forces demo support.
* Added support for custom caption files and fonts, with UTF-8 Unicode support. Caption and font files can be added to the program or documents directory in the corresponding folder. This makes it possible to translate * the captions into other languages, even languages that use a non-ASCII character set, as long as a compatible font is used.
* Added Noto Sans as the new default font for captions. It includes Latin, Cyrillic, and Greek character sets, as well as the Devanagari alphabet (most notably used for Hindi).
* Added a section about caption customization to the in-game manual
* Added captions for enemy death sound effects (these help with situational awareness)
* Added missing captions for Kyle's voice-over on M11 Imperial City
* New cheats LAADDLIFE and LASUBLIFE for adding and subtracting lives.

### Version 1.09.410
**Windows Build** [TheForceEngine-v1.09.410.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.09.410/TheForceEngine-v1.09.410.zip) <br>
**Source Code** [v1.09.410.zip](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.09.410.zip)

A quick bug-fix release following up version 1.09.4.

* Fixed the Linux build.
* Fixed a crash on some graphics drivers when creating textures for bloom.
* Color correction and bloom can now be used at the same time.
* Fixed captions and subtitles both showing if you had either one or the other enabled.
* Fixed a timing issue with subtitles when running at very high framerates (the subtitles would never disappear and become "stuck").

### Version 1.09.400
**Windows Build** [TheForceEngine-v1.09.400.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.09.400/TheForceEngine-v1.09.400.zip) <br>
**Source Code** [v1.09.400.tar.gz](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.09.400.zip)

This build introduces several new features as part of the set of releases leading up to version 1.10. Features include Bloom, Colormap Interpolation, Smooth Vue animations, and a Closed Caption system for accessibility.

* Smooth Vue Animations (optional).
* Fixed color flashing when switching between levels.
* Ported over GPU Renderer portal fixes - now supports up to 65536 visible portals as originally intended.
* Fixed GPU Renderer issues when using more than 65536 vertices for sector or sprite geometry in a frame.
* Fixed Wireframe so it works correctly in release mode, and made 3DOs solid color when in wireframe.
* Added a new "Retro" settings template which matches the "Modern" template from previous versions, where "Modern" enables new features, such as Bloom by default.
* Added an "8-bit Interpolated" color mode, which smooths out colormap-based shading and removes most of the banding.
* Added a new console command **exportTexture** that will export the texture on the surface the camera is currently pointing at.
* Added a bloom option, with the ability to adjust its strength and spread.
* Added Accessibility options, starting out with Closed Captions / Subtitles (Beta).

### Version 1.09.300
**Windows Build** [TheForceEngine-v1.09.300.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.09.300/TheForceEngine-v1.09.300.zip) <br>
**Source Code** [v1.09.300.tar.gz](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.09.300.zip)

Another small bug-fix release.

* Fixed a bug when there are too many entries in Jedi.lvl
* Fixed a bug with display bounds when selecting the correct display.
* Fixed a crash if the HUD pieces do not load.
* Added a confirmation for loading a game from the Load Menu.
* Added mod filtering for the Mod Loader, to make finding mods easier.
* Mods are now alphabetically sorted (once the list loading is complete).
* Fixed issues with the "No Game Data" message being incorrectly displayed.
* Separates out errors because files aren't found, versus files are invalid.
* Fixed a memory overwrite bug in Dark Tide 4, level 3 - due to having too few "texture vertices" set.
* Fixed Vue Logic sprite yaw to match vanilla.
* Hopefully fixed Steam path detection when the game is installed on a different drive than Steam itself or the ACF files cannot be found.
* IMuse: clamp priority parameter to 127 (Manuel Lauss)
* Linux: improve crash handler (Manuel Lauss)

### Version 1.09.200
**Windows Build** [TheForceEngine-v1.09.200.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.09.200/TheForceEngine-v1.09.200.zip) <br>
**Source Code** [v1.09.200.tar.gz](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.09.200.zip)

A small bug fix release with fixes backported from the "True Color Renderer" branch, as well as other fixes. The "True Color Renderer" release will be the next major build.

* Fixed a bug where IR Vision state wasn't properly saved and loaded.
* Fixed a bug where IR Goggles would stay active after respawning from death.
* Fixed a bug where the player could pick up items while dead.
* Fixed a bug where the player could use cheats, such as LAPOSTAL, to resurrect from death.
* The "About" tab in the Settings menu now works correctly.
* Added an option, enabled by default, to ignore the INF limit. When enabled, there is no hard coded limit to the number of INF items that a level can have.
* Fixed a "hang" (infinite loop) if an invalid INF sector class is used in a level. This fixed the hang in "STEALTH.GOB".
* Fixed the spelling of the LARAMSHED cheat.
* Fixed a crash that occured in the mod loader if files cannot be loaded from a zip file.
* Fixed a bug in the mod loader where stale text would be shown for a mod without a valid text file or description.
* Fixed bugs with the way mousebots would die, removing the up to 1 second delay that could happen.
* Fixed 3DO lighting bugs in the software renderer.
* Added an option, enabled by default, to fix the normal calculation in 3DOs in some cases.
* Portal traversal optimizations.
* Greatly reduced the number of memory allocations that the GPU renderer would use for 3DOs.
* Fixed a collision bug that kept the player from jump onto some ledges at certain framerates (including 60 fps). This fixes jumping issues in "DeathStr" and "Lara Hotel".

### Version 1.09.100
**Windows Build** [TheForceEngine-v1.09.100.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.09.100/TheForceEngine-v1.09.100.zip) <br>
**Source Code** [v1.09.100.tar.gz](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.09.100.tar.gz) <br>
Hotfix release that addresses critical issues with version 1.09.

#### Note For Linux Users
Linux is now supported but it requires additional setup. For now, you will need to compile from the source in order to run Linux. For more information, see the Linux section of the GitHub [README](https://github.com/luciusDXL/TheForceEngine/blob/master/README.md).

In addition, a Flatpak/snap (or similar) package is planned for version 1.10, alleviating the need to manually compile the project. **If you don't want to compile the code, it might be better to use Windows for now or wait for version 1.10.**

* [GitHub Repository](https://github.com/luciusDXL/TheForceEngine)
* [README](https://github.com/luciusDXL/TheForceEngine/blob/master/README.md)

**Changes**
* System Midi volume bugs, causing notes not to play properly on some midi devices and volume issues with Windows GM synth.
* Linux crashes when not specifying the build type.

### Version 1.09.000
**Windows Build** [TheForceEngine-v1.09.000.zip](https://github.com/luciusDXL/TheForceEngine/releases/download/v1.09.000/TheForceEngine-v1.09.000.zip) <br>
**Source Code** [v1.09.000.tar.gz](https://github.com/luciusDXL/TheForceEngine/archive/refs/tags/v1.09.000.tar.gz) <br>
This build adds both Sound Font (sf2) and OPL3 midi synthesis. External midi is no longer required on Linux. Note that midi settings will be reset with this build, if you want to change from the default (OPL3 emulation) - than use the Sound menu.

**Changes**
* Implemented midi device types to support system midi as well as midi synthesis.
* Implemented support for midi synthesis using Sound Fonts (sf2).
* Implemented support for midi synthesis using OPL3 emulation and the iMuse OPL driver.
* Implemented the ability to change midi devices and outputs during gameplay, the game music is restarted as needed.
* Added Roland SC-55 and AWE64 sound fonts.
* Added support for 800p in the resolution list for the Steam Deck.
* Update the Readme to reflect that external midi is no longer required on Linux.
* The midi device now defaults to OPL3.
* Reduced stack size requirements in the audio system to fix issues on Steam Deck.
* Linux/CMake: also install the Mods and SoundFonts folders.
* Linux/Paths: look for support data in the executable directory too.
* CMake: gitVersion: do nothing if Git is not available.
* Linux: name executable "theforceengine"
* Add comments categorizing keywords and noting those which are not implemented.

### Version 1.08.000
**Windows Build** [TheForceEngine-v1.08.000.zip](archive/TheForceEngine-v1.08.000.zip) <br>
This build contains most of the features slated for version 1.10, with the only major missing feature being internal midi synth support and better Linux packaging. This marks the version "official" TFE version with Linux support.

**Changes**
* Changed "activated" to "toggle" to better match existing cheat messages.
* Fixed a HOM issue in Executor.
* Added a proper FPS counter which can be enabled in the graphics menu.
* Renamed "energy" to "battery power".
* Official Linux support added.
* Updated the README with Linux build and run instructions.
* Removed the unique 3DO model limit.
* Fixed font rendering bugs (lack of language-specific symbols) due to using signed 8-bit characters instead of unsigned.
* Dark Forces menu shortcuts now work correctly for different languages.
* Fixed the Gamorrean Guard attack delay - they were attacking much more often than in vanilla.
* Fixed the Sewer Creature attack and search delays, they were slightly longer than vanilla (meaning it attacked less often than it should have).
* Midi selection in the Sound menu now works correctly.
* The Escape menu now uses the correct palette, fixing issues with some languages and mods.
* Fixed a crash when a WAX did not have the appropriate animation in certain areas of the AI code.

### Version 1.02.000-6-g779b9745
[TheForceEngine-v1.02.000-6-g779b9745-1.zip](archive/TheForceEngine-v1.02.000-6-g779b9745-1.zip) <br>
* Fixed a bug where the mouse buttons wouldn't work if ALT is being held.
* Replaced single dots on the automap when diamonds that scale with resolution when using the GPU Renderer.
* When typing cheats into the console, they no longer need to be prefaced with cheat. So instead of `cheat LAMAXOUT` you can type `LAMAXOUT`.
* Added a new cheat code: `LAFLY` - when active, the player is not affected by gravity and can fly up using jump and down by using crouch.
* Added a new cheat code: `LANOCLIP` - when active, the player will pass through walls and adjoins regardless of collision.
* Added a new cheat code: `LATESTER` - this is short hand for activating `LAREDLITE, LAIMLAME, LAFLY, LANOCLIP`.

### Version 1.02.000-1-g7ec69bb1
[TheForceEngine-v1.02.000-1-g7ec69bb1.zip](archive/TheForceEngine-v1.02.000-1-g7ec69bb1.zip) <br>
* Changes the default audio outputs back to the 1.01 default.
* Adds buttons to the Sound Menu to reset audio outputs.

### Version 1.02
[TheForceEngine-v1.02.000.zip](archive/TheForceEngine-v1.02.000.zip) <br>
**Quality of Life Features**
* Alt+Enter will toggle fullscreen in addition to F11.
* Frame limit options added to the Graphics UI.
* **Load** added to the main menu.
* The Mod Loader will now return to the main menu if escape is hit.
* The Mod Loader will close mod descriptions is escape is hit.
* A System Menu has been added with two options:
  * An option to return to the main menu if you Quit a game.
  * An option to return to the Mod Loader if you Quit, if you loaded a mod (assuming the first option is enabled).
* The Audio system will try multiple sound APIs, including Direct Sound, if the default fails.
* You can now select the output audio and midi devices.

**Bug Fixes**
* Fixed a crash when playing Evacuation of Hoth custom level due to a frame scenery object being destroyed.   
* Fixed a bug where levels wouldn't load if they had spaces in front of certain keywords - such as Mission 2 of Don Sielke's.
* Fixed a bug where items would be despawned in some cases where the sector heights were too small.
* Fixed a bug where briefings could be skipped in some mods due to an order of operations error.
* Fixed a bug where sprites didn't always light up correctly when attacking.
* Fixed a bug where the Probe Droid would stay fullbright after firing.
* Fixed a bug where autoaim wasn't working with 3D objects like turrets and welders.
* Fixed a bug where autoaim targeted farther away items instead of closer items in some cases.
* Fixed a bug where the player could save while dying and then be invulnerable on load until they healed.
* Fixed crashes when INF sectors don't exist in custom maps.
* Fixed a bug where jumping up to sector second heights isn't as forgiving in TFE as DOS, resulting in custom level progression issues.
* 3DO PLANE projection when using the GPU Renderer now matches the software renderer for non-flat polygons.
* Fixed a bug where the top and bottom textures were drawn even with the "no wall" flag set instead of showing the sky when using the GPU Renderer.
* Fixed a bug with crouch jumping that kept the player from fitting into small places, blocking progression in Boba Fett's Revenge and other custom levels.
* Fixed bugs with exterior adjoins that caused walls to be incorrectly drawn where there should only be sky.
* Fixed a bug with INF messages using invalid delay values behaving different in TFE than DOS, making switches in some custom levels work incorrectly.
* Fixed a bug with invalid INF message types (such as "done") being treated different than DOS, breaking different triggers and elevators in custom levels.
* Fixed bugs with Gas Mask rendering when using the GPU Renderer at 320x200 resolution.
* It is now possible to hold ALT and move, and use ALT for crouch and slow actions.
* Improve Mod Loader text file parsing so it can be reliably extract the mod names.
* Improved PDA input and fixed layer keys being swapped.
* Fixed another PDA input issue, where the mouse location could effect hotkey results.
* Fixed a bug with keyboard input on the Agent menu, where scrolling downward would not wrap if all levels are complete.
* Secret Percentage update after loading from a save, fixed LADATA save percentage issue.
* The GPU renderer now properly emulates several stretching mid-texture effects (these worked in the software renderer).
* Fixed a sky texture offset bug using the GPU renderer that caused the incorrect part of the sky to show up in part of Stars End.
* Saved games with no name given are now assigned a default name, so that they can be selected and loaded.

### Version 1.01
[TheForceEngine-v1.01.001.zip](archive/TheForceEngine-v1.01.001.zip) <br>
* Improved robustness against sound system setup errors.
* Added --nosound commandline to disable digital sound (music still plays).
* Draw "no data" message in large red letters so it is obvious.
* Changed the name of the file the the Browse dialog asks you to point to from DARK.EXE to DARK.GOB to reduce confusion.
* Steam path detection is now more robust and should handle libraries on different drives than the base Steam install.
* TFE will now find the game source data if it is in the same directory as TFE.
* TFE now supports putting the game data under the TFE directory, under Games/Dark Forces/* and that case will be autodetected.
* Source data path validation is now more robust.
* Fixed a bug where the 'settings.ini' failed to parse, messing up settings.
* Shows a configuation menu on the first run where you can set either Vanilla or Modern defaults.
* Fixed Escape Menu background stretching when using the GPU Renderer with widescreen disabled.
* Fixed divide by zero crashes in the projectile code.
* The GPU Renderer now honors fullbright and opaque/transparent flags for signs and sign textures.
* Fixed a flags issue in the explosion code, where explosions could effect some things they are not supposed to.
* Fixed the thermal detonator damage the player takes, they were taking too much.
* Added a custom deadzone setting and proper deadzone sensitivity scaling.
* Fixed a lighting bug with the muzzle flash being too dark.
* Fixed sprite culling using the GPU renderer close to the camera.

### Version 1.0
[TheForceEngine-v1.00.000.zip](archive/TheForceEngine-v1.00.000.zip) <br>

### 1-RC-4  Version 1 Release Candidate 4
[TheForceEngine-v1-RC-4.zip](archive/TheForceEngine-v1-RC-4.zip) <br>
* Fixed a bug where enemies didn't always freeze on death - this caused some enemies like Gamorean Guards to slide around excessively.
* Creatures no longer move towards the player after falling to their deaths.
* Fixed missing "air friction" - which wasn't accounted for before due to an error (only affects enemies).
* Fixed a bug where if night vision is enabled when exiting a level, the increased lighting effect is visible in the next level.
* Fixed an endless pause when pressing escape while in a level, then pressing Alt+F1, exiting to the main menu and then starting a new mission.

### 1-RC-3  Version 1 Release Candidate 3
[TheForceEngine-v1-RC-3.zip](archive/TheForceEngine-v1-RC-3.zip) <br>
* Adjusted the point at which rotating sectors run at double rate in order to handle very slow rotations at high framerates. At some point the train in Harkov stopped working but only in release, with vsync enabled.

### 1-RC-2  Version 1 Release Candidate 2
[TheForceEngine-v1-RC-2.zip](archive/TheForceEngine-v1-RC-2.zip) <br>
* Fixes a crash when a cutscene cannot fully load.

### 1-RC-1  Version 1 Release Candidate 1
[TheForceEngine-v1-RC-1.zip](archive/TheForceEngine-v1-RC-1.zip) <br>
* Fixed the "no wall" case so it handles different floor and ceiling textures. This fixes the skybox rendering issues in the *Asteroid* mod.
* The Escape menu buttons should be adjusted based on art changes for different languages.
* Fixed a bug where projectiles would disappear while riding an elevator. This fixes an elevator that "eats projectiles" in the *Assassination on Narshadda* mod.
* Dark Tide AT-ST turrets now shoot more reliably like DOS, which fixes Dark Tide turret issues, such as the AT-ST in Dark Tide 2.
* Added optional autorun as a quality of life feature.

### 0.94.000-38-g1b42c2a9
[TheForceEngine-v0.94.000-38-g1b42c2a9-1.zip](archive/TheForceEngine-v0.94.000-38-g1b42c2a9-1.zip) <br>
* Fixed sky offsets for sky adjoins, they were using the current instead of next sector.
* Fixed an issue where an adjoin is treated as a sky when it shouldn't be.
* Fixed the issue with overlapping/intersecting adjoins causing HOM.
* Renamed the GPU Renderer in the UI so it is more clear.
* It is now possible to use Escape or the System UI combo to close the Input config
like the others, unless the key binding window is open.
* Fixed a crash in a mod due to a bad animated texture asset.

### 0.94.000-35-ge74b3249
[TheForceEngine-v0.94.000-35-ge74b3249.zip](archive/TheForceEngine-v0.94.000-35-ge74b3249.zip) <br>
* Fixed conditionals for corpse removal. This fixes a bug where elevators were rebounding off of pickups incorrectly. This fixes a possible softlock in Ramsees Hed as well as a potential rendering issue in DT 3.
* Nudge transparent mid-textures so they tend to show up in front of objects in the covered sector (fixes z-fighting in DT 1, inside the sandcrawler).
* Fix z-fighting when the floor is higher than the ceiling. This fixes z-fighting in Detention Center (the large door to one of the cell blocks) and DT 3 among other levels.
* Partial fix to the overlapping/intersecting adjoin bug, which fixes the HOM issue on Jabba's Ship.

### 0.94.000-31-gaef577f5
[TheForceEngine-v0.94.000-31-gaef577f5.zip](archive/TheForceEngine-v0.94.000-31-gaef577f5.zip) <br>
* Updated the credits and manual.
* Removed unused documentation.
* Fixed a bug where music doesn’t play correctly when starting a level cutscene for some levels, such as Hoerby level 1.
* When blitting a Delt into a bitmap, skip out-of-range columns. This fixes a bug in the Hoerby Trilogy text crawl.
* Fixed a bug where the camera offset was inverted, which kept the camera height clamping from working correctly - so it could go underground or underwater in some cases.
* Fixed a bug where hitting escape when the console is open did not unpause the game.
* Mods should only be listed once.
* Fixed sky alignment for both vanilla and cylindrical sky projections.
* Fixed a bug where the top or bottom sky adjoin would cover the entire wall, blocking the view of objects outside or causing a wall to look like the sky.
* Fixed custom cutscenes sometimes using the incorrect sounds, such as the final cutscene in the Hoerby Trilogy.

### 0.94.000-13-g119c90c7
[TheForceEngine-v0.94.000-13-g119c90c7.zip](archive/TheForceEngine-v0.94.000-13-g119c90c7.zip) <br>
* Fixed a crash when hitting "escape" while the console is open.
* Fixed a bug where the cursor would disppear if opening and closing the console on the main menu.
* Escape now closes the console, as expected.
* The Escape Menu cannot be opened if the console is open.
* Escape always closes the Escape Menu if it is bound to a different key, though that key will also close it as expected.
* HUD elements now have their own horizontal offset, so it is easier to fine-tune HUD placement.

### 0.94.000-11-g5b56a8a3
[TheForceEngine-v0.94.000-11-g5b56a8a3.zip](archive/TheForceEngine-v0.94.000-11-g5b56a8a3.zip) <br>
* Fixed an issue where cutscenes can play the incorrect sound effect.
* Lowered the priority of the Secret Found message slightly so that important messages, like the revive pickup, show through.
* Cleaned up log and console messages - even low priority messages are captured and iMuse noise has been removed.
* Pausing should work now without hanging notes when using certain midi devices.
* Fixed a GPU Renderer bug where having exactly 8 clip planes caused no clipping to occur.
* Fixed a Software Renderer bug that could incorrectly clip walls in some rare cases.
* HUD text now has the correct aspect ratio when scaling at higher resolutions.

### 0.94.000-1-g2550a4e7
[TheForceEngine-v0.94.000-1-g2550a4e7.zip](archive/TheForceEngine-v0.94.000-1-g2550a4e7.zip) <br>
* Fixed missing sound and crash when disabling sound in menus and then returning exiting to the main menu and starting the game again.
* Fixed Input menu length to show the whole list of weapon bindings again.
* Restored "weapon previous" behavior which was somehow removed at some point.

### 0.94.000
[TheForceEngine-v0.94.000.zip](archive/TheForceEngine-v0.94.000.zip) <br>
* Improves the accuracy of the grayscale filter on the Escape menu when the GPU renderer is being used.
* When saving, the edit box now properly limits the name length when typing instead of cutting it off.
* Added directions to the Input Menu.
* It is now possible to unbind keys/buttons in the Input Menu.
* Fixed HUD scaling options when using the GPU Renderer.
* Community provided endcap graphics are now used when the HUD elements are moved away from the edges of the screen.
* Added edit boxes and +/- buttons to the HUD scale and offset options for easier and more precise control.
* Added a *Game* option that optionally improves Boba Fett's AI by making him try to face the player more often when attacking.
* Fixes a crash that can happen when using the Quick load hotkey during a cutscene or on the Agent Menu.
* Added the ability to disable sound on menus, which will improve the experience for those with certain midi setups.
* The Config settings always show the background, not just when setting up graphics.
* The floor number is properly drawn on the PDA map.
* Fixed a bug where an inaccessible mission can be selected on the agent menu.
* Added the missing confirmation prompts to the Escape Menu, including hotkeys.

### 0.93.000-41-gee470c37
[TheForceEngine-v0.93.000-41-gee470c37.zip](archive/TheForceEngine-v0.93.000-41-gee470c37.zip) <br>
* Escape menu now has a grayscale background when using the GPU renderer.
* Avoid loading MacOS X gob file references, this allows some demos to load that failed before.
* Fixed a crash when an empty WAX cell is encountered in the GPU Renderer.
* Fixes a crash when trying to draw an empty string.
* Fixes a crash when trying to use a NULL palette.
* Fixes a crash when gamePaths are not set in jedi.lvl
* Fixes an issue with reading the '#' character in sector names.
* Fixes a crash when an object gets pushed out of the level by a moving elevator - this fixes a crash seen in DT 3, level 1.

### 0.93.000-38-g4b44e54c
[TheForceEngine-v0.93.000-38-g4b44e54c.zip](archive/TheForceEngine-v0.93.000-38-g4b44e54c.zip) <br>
* Added audio startup logging to help troubleshoot issues.
* Fixes a crash on DT 4 due to invalid data (adjoin commands effecting out of range walls).
* Fixes slow speed caused by dying after using the LABUG cheat.
* Preserve the UI toggle across levels like DOS.
* Fixes weapon rendering when running at 320x200 using the GPU renderer.
* HUD messages now display when running at 320x200 using the GPU renderer.
* Resolution and aspect ratio changes work correctly while using the GPU renderer.
* The player no longer moves when scrolling the map.
* The GPU Renderer cache is now updated when changing renderers on the fly.

### 0.93.000-29-gecb23784
[TheForceEngine-v0.93.000-29-gecb23784.zip](archive/TheForceEngine-v0.93.000-29-gecb23784.zip) <br>
* Fixes incorrect lighting for full bright sectors when using the GPU renderer. Example: outdoor lighting on Robotics Facility.
* Fixes a bug that causes projectiles to disappear incorrectly (seen when trying to hit a switch with the Dark Trooper weapon on the Arc Hammer level).
* Fixes the PDA using the incorrect palette in some cases (such as DT 4).
* Cleans up palette flashes when usin the GPU renderer, when closing the PDA or first loading a level or save.

### 0.93.000-27-gb2c03e72
[TheForceEngine-v0.93.000-27-gb2c03e72.zip](archive/TheForceEngine-v0.93.000-27-gb2c03e72.zip) <br>
* Fixes a GPU Renderer crash when the camera is almost exactly on top of a wall vertex.
* Fixes an ambient sound issue, where ambient sounds would fail to play when loading from a save.


### 0.93.000-25-g31035a60
[TheForceEngine-v0.93.000-25-g31035a60.zip](archive/TheForceEngine-v0.93.000-25-g31035a60.zip) <br>
* Fixes a bug with determining max object size in a sector, which caused an elevator in Dark Tide 1 to fail to move.
* Fixed a few minor general bugs.
* Fixed a minor Phase 3 AI bug with turning radius.
* The Phase 3 homing missiles now move at half speed to match DosBox (the value in TFE was correct according to the code, but during gameplay they move at half that speed).
* Numerous fixes to the Boba Fett AI. It is still "broken" - but it is broken in the same way as DOS. (If you set BOBA_FACE_PLAYER = 1 in the code, the AI feels much better - but that isn't vanilla DOS behavior).
* General AI cleanup.

### 0.93.000-19-g023a90da
[TheForceEngine-v0.93.000-19-g023a90da.zip](archive/TheForceEngine-v0.93.000-19-g023a90da.zip) <br>
* Fixes a bug with duplicate animated textures which would break switches and animated textures, making mods like Dark Tide 1 unplayable.

### 0.93.000-18-gf2459f1a
[TheForceEngine-v0.93.000-18-gf2459f1a.zip](archive/TheForceEngine-v0.93.000-18-gf2459f1a.zip) <br>
* Changed the "offscreen target" to use the system allocator which fixes allocation errors with 4k or high resolutions, which caused Escape menu crashes.
* Fixes a collision bug when dealing with custom "collision functions" - this fixes a bug on Detention Center where both walls blow up instead of just the targeted wall.
* Fixed the PDA timing when running at high framerates.
* Added mouse wheel movement accumulation so that scrolling or zooming using the mouse wheel in the PDA is much smoother.
* Fixed a bug where animated texture references were incorrectly modified when saving - which caused the textures to flash (but could cause worse problems).

### 0.93.000-14-g80f9ca12
[TheForceEngine-v0.93.000-14-g80f9ca12.zip](archive/TheForceEngine-v0.93.000-14-g80f9ca12.zip) <br>
* Fixes a save issue with the INF adjoin command. For saves where adjoin commands have already been executed, the data is "fixed up" to avoid crashes but adjoins may be missing until adjoin commands replace them or the level is restarted.

### 0.93.000-11-gc9beb48b
[TheForceEngine-v0.93.000-11-gc9beb48b.zip](archive/TheForceEngine-v0.93.000-11-gc9beb48b.zip) <br>
* Fixed an INF bug where non-players objects LEAVING a sector did not send an correct INF message.
* Fixed a long standing bug on Jabba's Ship.
* Fixed a crash caused when blowing up a mine with explosives after a load when the mine had multiple logics.

### 0.93.000-10-g19520b50
[TheForceEngine-v0.93.000-10-g19520b50.zip](archive/TheForceEngine-v0.93.000-10-g19520b50.zip) <br>
* Fixed a bug where INF files would not load unless the first uncommented line was the version. This caused the INF in level 3 of the DF 96 mod to fail to load INF.
* Fixed a bug with the LANTFH cheat where the player would not teleport to the correct height.
* Fixed a bug where the Datatape would stay in the player's inventory once acquired.
* No longer plays cutscenes when skipping to a specific level, like DOS.
* The recticle no longer shows up over the in-game UI when first enabled on the main menu.
* Fixed an INF elevator issue, where the move type could be changed at a stop. This made it possible to keep activating elevators and doors even between stops.

### 0.93.000-1-g9b1a71e8 Save System Release
[TheForceEngine-v0.93.000-1-g9b1a71e8.zip](archive/TheForceEngine-v0.93.000-1-g9b1a71e8.zip) <br>
* Save System / Quicksaves
* Fixed a "random" crash caused by invalid addressing in the sound system.
* Fixed an issue with level progress not being preserved if you exited immediately after completing a level.
* Fixed pitch issues with turrets, they should look much more accurate now.
* Fixed mouse speed issues with the in-game menus.
* Improved the responsiveness of the PDA menu.
* And many other minor fixes.

### 0.92.000-3-g9d01b27
[TheForceEngine-v0.92.000-3-g9d01b27.zip](archive/TheForceEngine-v0.92.000-3-g9d01b27.zip) <br>
Fixes several GPU Renderer issues with adjoins. This fixes:
* Incorrect rendering of search lights in Imperial City.
* HOM artifacts when looking out windows in the main building of Imperial City.

### 0.92.000-2-g3156e26
[TheForceEngine-v0.92.000-2-g3156e26.zip](archive/TheForceEngine-v0.92.000-2-g3156e26.zip) <br>
* Fixes a crash on exit.

### 0.92.000-1-ga6fbcac
[TheForceEngine-v0.92.000-1-ga6fbcac.zip](archive/TheForceEngine-v0.92.000-1-ga6fbcac.zip) <br>
* Fixes a crash when exiting the PDA and immediately firing a weapon.

### 0.92 GPU Renderer Beta Release
[TheForceEngine-v0_92_000.zip](archive/TheForceEngine-v0_92_000.zip) <br>
* Beta release of the GPU Renderer.
* Feature to enable or disable autoaim in **Game Settings**.
* Bug fixes.

### 0.91 Bug Fix Release 6
[TheForceEngine-v0_91_000-1-ge1aa3da.zip](archive/TheForceEngine-v0_91_000-1-ge1aa3da.zip) <br>
* Added optional extended adjoin limits - this fixes HOM issues in most mods due to engine limits if enabled (default).
* Added optional crosshair support (defaults to off).
* Fixed 3DO lighting to match DOS.
* Fixed a 3DO gouraud shading clipping bug when using the floating point renderer (which caused streaking artifacts).
* Fixed differences between DOS and TFE 3DO/sector clipping.
* Fixed the pitch offset calculation (it was slightly off before) - this makes shots fired up and and more accurate.
* Improved Escape menu button hover offsets.
* Fixed a bug where it was possible to not have a mission selected on the Agent Menu, causing a crash if beginning the mission.
* Fixed a bug where completion of the final level wasn't shown on the Agent Menu.
* Fixed a bug where level complete status wasn't saved when hitting Quit to DOS instead of Next Level.
* Fixed a bug where land mines were triggering through doors and similar situations.
* Fixed a bug where death effects kept occuring even after reaching 0 health - this fixes the repeating death sounds on damage floors.
* Enemies now die properly if they fall too far.

### 0.9x Bug Fix Release 5
[TheForceEngine-v0_09_000-42-g32a941a-2.zip](archive/TheForceEngine-v0_09_000-42-g32a941a-2.zip) <br>
* Fixes additional sign rendering issues if the base wall texture heght is smaller than the switch texture height.
* Fixed an issue where some switches couldn't be triggered.
* Fixed a crash if warping to an invalid position.
* Fixed crash that could be caused by an elevator with a null sound, which caused a crash when blowing up the lava dam in the Lava Planet mod.
* Fixes bugs with 3DO parsing, which fixes missing 3DOs in mods.
* Fixes display issue with "tall screen" resolutions (i.e. taller than 4:3).
* Fixes bug where elevator should remove corpses and continue instead of hitting them and moving back up.
* Fixes a bug where an elevator thinks there isn't enough room to fits objects incorrect, which fixes the bug in DT 3 where the blue key rises, hits the ceiling and then lowers again.
* No longer sets 0 channels even when requested - fixes music stopping permanently in Imperial Library.
* Verifies proper texture frame sizes and uses frame 0 if bad asset - fixes crash in Imperial Library.
* Fixes a crash that can occur if a mid-texture isn't setup correctly on a solid wall - this fixes the Dark Tide 3 "Droid Deception" level end crash and visuals.
* Fixes looping VUE animations (such as Nar Shaddaa and Executor).
* Fixes incorrect 3DO orientations (mostly noticeable in mods).

### 0.9x Bug Fix Release 4
[TheForceEngine-v0_09_000-34-gdb7a5c0.zip](archive/TheForceEngine-v0_09_000-34-gdb7a5c0.zip) <br>
* Fixes Kyle incorrectly sliding off of moving platforms in some mods, like Dark Tide 1.
* Fixes a bug with animated textures that were not setup correctly - this fixes some switches that did not show up at all in mods, and potentially other animated textures.
* Fixes a bug where transparent animated textures might show up as opaque, this affected some mods and switches.
* Fixes a bug where animated texture frames may have a few incorrect/corrupted colors.
* Fixes a bug where some switches could not be triggered in mods, and other switches were harder to trigger than they should be.
* Added a 'warp' command to the console so you can warp directly to positions reported by the LADATA cheat.

### 0.9x Bug Fix Release 3
[TheForceEngine-v0_09_000-27-g5f123b0.zip](archive/TheForceEngine-v0_09_000-27-g5f123b0.zip) <br>
* Fixes a crash that occurs when a cutscene "film" fails to load.
* Fixes a crash when the top or bottom texture of a wall is null.
* Frees a digital sound if it fails to setup data, which avoids a bug where all of the channels can be consumed.
* Fixes a bug where a teleport can fail to be setup correctly if it has an invalid field - this caused a crash in Dark Tide 2 when going into water.
* For Boba Fett, make double sure the msg is MSG_RUN_TASK before freeing the task after death - which can cause a crash on DT 2.
* Added support for half-step rounding when a rotating elevator delta is too small (due to high framerate combined with low speed).
  - This fixes the train in Harkov when running at higher than 90 fps.
* Fixes a bug where a texture with an blank name wasn't set to default - some mods, like the Dark Tide series, such blank texture names to mane default.bm for some reason. This fixes missing textures and HOM effects.
* Reduces the velocity jitter threshold by half so the player doesn't get stuck on low friction surfaces when the framerate is high.
  - This fixes a bug where I got stuck underwater in DT 2 with vsync off.
* Made time tracking more robust
  - Ensure that time is purely monotonic.
  - Disable vsync interval rounding at 120+ fps since it becomes unreliable.
  - Recheck sync and refresh rate less often to avoid stutters.
* Fixed a bug where some trigger functions were firing even with the trigger master was off.
* Fixed a potential crash when iterating through objects in a sector.
* Reduced external velocity 0 clamping by half to better handle high framerates.
  - This should reduce sliding on some moving platforms at high framerates.
* Cleaned up landing animation code, which is now accurate.
* Cleaned up head/weapon wave code, which is more accurate.
* Fixed the headlamp calculation which was slightly inaccurate.
* The cutscene music repeat bug is fixed when canceling from the mission briefing (previously this bug was fixed when entering a mission, exiting out, and then playing the cutscenes again. This bug handles the case where you cancel from the mission briefing).
* Fixes a crash in DT 1 because sector vertices are NULL.

### 0.9x Bug Fix Release 2
[TheForceEngine-v0_09_000-15-gc28638a.zip](archive/TheForceEngine-v0_09_000-15-gc28638a.zip) <br>
* Fixed OBJ_FLAG_HAS_COLLISION, which should be OBJ_FLAG_MOVABLE. This fixes errors such as corpses not moving with rotating sectors.
* Fixed object collision radii - this fixes a bug where the collision for many objects was too large.
* Fixed a bug where TFE crashes if there is no briefing.
* Fixed a bug with collision where a flag was checked - it should only check the collision radius. This fixes a bug where some props did not have collision when they should have.
* Fixed the default message type for line triggers (which can effect some INF functionality in mods).
* Fixed several areas while loading INF that could cause crashes with malformed data.
* Fixed slave "value" - I thought it was fixed point but it is actually an angle.
* Fixed triggers to accept evt == INF_EVENT_ANY (aka -1), this can also have an effect on INF in mods.
* Fixed collision issues with moving and rotating walls.
* Fixed object default flags - this also could cause some objects to not move correctly with rotating or moving sectors.
* Fixes a bug when decompressing transparent textures (compressed transparent BM) - this fixes bugs such as holograms in Assassination at Nar Shaddaa.

### 0.9x Bug Fix Release 1
[TheForceEngine-v0_90_000-13-g2b1bc8d.zip](archive/TheForceEngine-v0_09_000-13-g2b1bc8d.zip) <br>
* Fixes a sound crash when exiting to the main menu while in a level and then starting up a mod.
* Fixes a Dark Forces bug where music doesn't play in a cutscene on a second viewing in the same session.
* Fixes a bug when an object has an incorrect class or type on load - it should be skipped.
* Clean up differences between TFE level loading and DOS.
* Fixes a bug where the ambient sound index was always 0.
* Correct screen flash fade lengths for shield and health damage, and pickup flashes.
* Fix crash when destructible object has no animation 1 - this resulted in numerous crashes.
* Fix camera sound update.
* Fix issue that could cause textures to fail to load if one line is bad.

### iMuse and Sound - version 0.90.000
[TheForceEngine-v0_90_000.zip](archive/TheForceEngine-v0_90_000.zip) <br>
* Reverse-engineering of Dark Forces complete (with the obvious exception of going over bits of code again for bugs, or if I ever want to port TFE to DOS - and no that is not happening anytime soon if ever).
* iMuse system with proper music cues, transitions, and effects. Features like fades and similar effects work the same for both midi and digital audio.
  * This is where most of the time was spent. iMuse is big and convoluted.
* Game music with fight/stalk transitions.
* Game and Cutscene sound system that uses iMuse to play digital audio; which includes proper sound priorities and accurate sound falloff and panning.
* Level ambient sounds.
* Sound UI will volume control for Cutscene Music, Sound, and Game music and sound.
* The ability to enable 16-channel digital audio support in iMuse (it was basically already there in the code, I just had to make some tweaks so it could be changed at runtime). 16-channels is the default but if you disable the option, it reverts back to 8-channels like DOS.
* The ability to disable fight music if desired.
* Mouse wheel now bindable.
* Mouse wheel works on mission briefings and some PDA screens (mission briefing and map).
* Improved support for System UI scaling for 1440p and 4k.

### Cutscenes and Game UI Bug Fix Build 2 - version 0.80.000-6-g5b663b3
[TheForceEngine-v0_80_000-6-g5b663b3.zip](archive/TheForceEngine-v0_80_000-6-g5b663b3.zip) <br>
* Fixes a cutscene related "infinite loop" with at least one mod.
* Fixes a crash due to missing midi file in at least one mod.

### Cutscenes and Game UI Bug Fix Build - version 0.80.000-4-ga10f68d
[TheForceEngine-v0_80_000-4-ga10f68d.zip](archive/TheForceEngine-v0_80_000-4-ga10f68d.zip) <br>
* Improved the accuracy of the cutscene playback speed.
* Cutscene music plays at full speed.
* Fixed a crash caused by sprites writing past their bounds.
* Fixed issue when hitting Return or Escape to move past cutscenes either immediately launching the next level or returning to the Agent Menu.

### Cutscenes and Game UI Release - version 0.8
[TheForceEngine-v0_80_000.zip](archive/TheForceEngine-v0_80_000.zip) <br>
* The Escape menu now supports keyboard shortcuts.
* The "Configuration" option in the Escape Menu loads the TFE System UI options.
* PDA now works.
* Mission Briefings now work.
* Difficulty level now accurate (no more extra super shields on Medium).
* Cutscenes play.
* Better support for tall windows.
* Fixes a model rotation problem in some mods (like Lava Planet).
* Fixed a memory overwrite that could lead to a crash.

Known Issues:
* Cutscene music is not 100% correct, there are late cues and "dead space." This will be corrected in version 0.9 with full iMuse support.

### Core Game Loop Release - version 0.7
[TheForceEngine-v0_70_000.zip](archive/TheForceEngine-v0_70_000.zip) <br>
* Fixes a bug where opening the System Menu (Alt+F1), and then going to the graphics tab on the Agent Menu would cause the screen to go black.
* Fixes a bug with floor/ceiling rendering when changing from high resolution to 320x200.
* The Force Engine supports dragging and dropping zip files onto the executable to launch mods.
* The Force Engine now supports loading mods directly from zip files.
* The Mod Loader now supports loading direct from Zip Files.
* The Mod Loader now queues up load requests instead of pausing everything to wait.
* The Mod Loader does a better job of extracting the mod names from their text files.
* The Mod Loader now displays the original zip or gob file name.
* The Mod Loader handles longer text files more gracefully.
* The Mod Loader now supports different views - images, a list of mod names, and a list of mod directories/zip files.
* Misc small fixes.
* The version has been changed to 0.7 to better reflect progress towards version 1.0.

### CGL Pre-Release Build Version 0.02.001-134-g22afe3c
[TheForceEngine-v0_02_001-134-g22afe3c.zip](archive/TheForceEngine-v0_02_001-134-g22afe3c.zip) <br>
* Fixes 3DO loading that was broken by the previous fix. Now all models should load.

### CGL Pre-Release Build Version 0.02.001-133-gd444883
[TheForceEngine-v0_02_001-133-gd444883.zip](archive/TheForceEngine-v0_02_001-133-gd444883.zip) <br>
* You can exit from the game using Alt+F1, which takes you back to the main menu.
* Fixes a crash with resolutions with a non-divisible by 4 width; this was causing a crash with Ultra-wide resolutions.
* Fixes the AT-AT model loading (and presumably others).
* Fixes a crash in the floating point renderer when caching sectors due to
a mismatch between sector ID and index. Now the caching system uses the index.
* Early WIP Mod Loader

### CGL Pre-Release Build Version 0.02.001-129-gbc44570
[TheForceEngine-v0_02_001-129-gbc44570.zip](archive/TheForceEngine-v0_02_001-129-gbc44570.zip) <br>
* Fixes "3D Hologram" rendering when running at a higher resolution and/or widescreen.

### CGL Pre-Release Build Version 0.02.001-128-gf987b7c
[TheForceEngine-v0_02_001-128-gf987b7c.zip](archive/TheForceEngine-v0_02_001-128-gf987b7c.zip) <br>
* High resolution and wide screen support.
* HUD adjustments are working again.
* Compressed loading screens now display properly (found in some languages and mods).
* Fixed a rendering error with some models used by mods.

### CGL Pre-Release Build Version 0.02.001-112-gf4c6a81
[TheForceEngine-v0_02_001-112-gf4c6a81.zip](archive/TheForceEngine-v0_02_001-112-gf4c6a81.zip) <br>
* Adds support for detecting which display a window is on and using that for fullscreen and refresh rate.
* Fixes the update when vsync is enabled to detect cases where the refresh rate changed or vsync is not set as expected or changed.
* Resets the window position if it is not on an active display.
* Enables DPI-Awareness, which should allow the correct window scaling even if the desktop scale is changed.

### CGL Pre-Release Build Version 0.02.001-110-gc940ee7
[TheForceEngine-v0_02_001-110-gc940ee7.zip](archive/TheForceEngine-v0_02_001-110-gc940ee7.zip) <br>
* Adds a fix to weapon firing with low delta times (high framerates) - it fixes
an issue where projectiles could pass through near objects in the initial firing frame due
to a misalignment with the projectile speed and initial instantaneous movement.
The most obvious result was the punch constantly missing when the framerate is higher than ~70.
* Fixes a bug where placing landmines was **slightly** too fast.
* Fixes a bug in the parser that wasn't recognizing empty strings ("") as tokens.

### CGL Pre-Release Build Version 0.02.001-107-g5977a8a
[TheForceEngine-v0_02_001-107-g5977a8a.zip](archive/TheForceEngine-v0_02_001-107-g5977a8a.zip) <br>
* General Mohc has been integrated.
* The Mohc boss elevator is now properly handled.
* Homing missile collision has been fixed.

### CGL Pre-Release Build Version 0.02.001-106-g6ab2d35
[TheForceEngine-v0_02_001-106-g6ab2d35.zip](archive/TheForceEngine-v0_02_001-106-g6ab2d35.zip) <br>
* The LAIMLAME cheat now protects against health damage.
* Boba Fett is in and it is now possible to complete Imperial City fairly.

### CGL Pre-Release Build Version 0.02.001-100-g738bf7d
[TheForceEngine-v0_02_001-100-g738bf7d.zip](archive/TheForceEngine-v0_02_001-100-g738bf7d.zip) <br>
* If the save game file cannot be copied by TFE, a new file is created. This fixes the issue a few people had with saved games (starting without the pistol and data not being saved).
* Sound Effects are now paused when bringing up the Escape Menu.

### CGL Pre-Release Build Version 0.02.001-98-g4827535
[TheForceEngine-v0_02_001-98-g4827535.zip](archive/TheForceEngine-v0_02_001-98-g4827535.zip) <br>
* Executor is now completable (removing the last non-boss progress blocker as far as I know).
* The Moudly Crow now properly returns at the end of level 4.
* Player jumping behavior should now match DOS.
* Players now smoothly lower with second-height based elevators.
* Fixes corner case where 3DO clipping can produce vertices where z = 0, which causes a crash on Windows.
* Better handling of malformed data.

### CGL Pre-Release Build Version 0.02.001-93-g070d449
[TheForceEngine-v0_02_001-93-g070d449.zip](archive/TheForceEngine-v0_02_001-93-g070d449.zip) <br>
* Fixes HOM artifacts that occur in TFE but not DOS (Gromas, Robotics Facility).
* Fixes floor/ceiling INF texture transfer.
* Fixes various crashes in mods.
* Fixes some walls not being added to the automap when seen.
* Fixes weapons not be rendered as transparent in some mods.

### CGL Pre-Release Build Version 0.02.001-88-gc18215d
[TheForceEngine-v0_02_001-88-gc18215d.zip](archive/TheForceEngine-v0_02_001-88-gc18215d.zip) <br>
* Fixes a projectile collision bug, where projectiles can incorrectly "miss" an object when passing through multiple sectors in the same frame.
* Fixes a weapon pitch offset rounding error that can cause weapons to be rendered slightly too high on the screen when looking down.

### CGL Pre-Release Build Version 0.02.001-86-g2822c78
[TheForceEngine-v0_02_001-86-g2822c78.zip](archive/TheForceEngine-v0_02_001-86-g2822c78.zip) <br>
* Fixed collision bug where players would get stuck on walls instead of sliding.
* Fixed excessive collision jittering.
* Fixed terrible sound when dying from "gas sectors."
* Fixed phantom "gas sector" noise when dying.

### CGL Pre-Release Build Version 0.02.001-83-g7836c52
[TheForceEngine-v0_02_001-83-g7836c52.zip](archive/TheForceEngine-v0_02_001-83-g7836c52.zip) <br>
* Fixed missing Remote functionality (a sound effect).
* AI Bug: fixed incorrect random angle offest in actor_offsetTarget().
* AI Bug: fixed Phase 1 Dark Trooper movement bug when it loses sight of the player.
* AI Bug: fixed AI collision response bug.
* AI Bug: fixed bug where AI Actors were considered to be 1.5 units tall for movement collisions, which let them pass through windows and other small areas.
* Phase 2 Dark Trooper has been integrated, which makes it possible to beat all levels up to Imperial City.

### CGL Pre-Release Build Version 0.02.001-74-g60aa3ec
[TheForceEngine-v0_02_001-74-g60aa3ec.zip](archive/TheForceEngine-v0_02_001-74-g60aa3ec.zip) <br>
* Adds the ability to reset input to defaults.
* Fixes a visual issue due to not clearing the screen when rendering UI.

### CGL Pre-Release Build Version 0.02.001-73-g10a8083
[TheForceEngine-v0_02_001-73-g10a8083.zip](archive/TheForceEngine-v0_02_001-73-g10a8083.zip) <br>
This version adds support for input remapping and control settings. This includes:
* Enable/Disable controller.
* Controller axis to movement/turning adjustment.
* Controller sensitivity adjustment.
* The ability to invert controller axis.
* Mouse mode - menus only, turning only (which was available in DOS), and full mouse look.
* Mouse sensitivity.
* The ability to invert mouse axis.
* The ability to bind key inputs, controller inputs and mouse inputs to in-game actions.
* The ability to rebind the console toggle and in-game system menu toggle.

### CGL Pre-Release Build Version 0.02.001-66-ge625336
[TheForceEngine-v0_02_001-66-ge625336.zip](archive/TheForceEngine-v0_02_001-66-ge625336.zip) <br>
* Fixes a logic error preventing the basic AI enemies from moving around properly, this could cause issues such as spinning in place.
* Fixes Kell Dragon logic when it loses sight of the player.
* Clears HUD messages when disabling everything for Jabship.
* Fixes movement logic issues with the Phase 1 Dark Trooper.
* Fixes AI teleporting issues, most noticeable with the Phase 1.
* Fixes precision issue with vec2Length() that was causing the results to lose more precision than DOS.

### CGL Pre-Release Build Version 0.02.001-61-gb0b0073
[TheForceEngine-v02_001-61-gb0b0073.zip](archive/TheForceEngine-v02_001-61-gb0b0073.zip) <br>
* The console now pauses the game.
* Cheats can be entered using the console using the "cheat" command. Example: *cheat lacds*
* Unused console commands have been removed.
* A few new commands have been added to aid in debugging AI.

### CGL Pre-Release Build Version 0.02.001-55-g4620539
[TheForceEngine-v02_001-55-g4620539.zip](archive/TheForceEngine-v02_001-55-g4620539.zip) <br>
* Projectiles no longer collide with pickups, so shields won't block Thermal Detonators.
* Music will pause when opening up the Escape Menu.
* Music no longer glitches when going back to the Agent Menu or loading the next level.
* When creating a new Agent, the first level is automatically selected - avoiding bugs when starting a mission with no level selected.
* If you create a new agent and then quit the game, the first level will now be selected - avoid the above issue.

### CGL Pre-Release Build Version 0.02.001-48-g7a8237a
[TheForceEngine-v0_02_001-48-g7a8237a.zip](archive/TheForceEngine-v02_001-48-g7a8237a.zip) <br>
This is a "hot-fix" that fixes a possible crash on Jabba's Ship when retrieving your stolen gear.

### CGL Pre-Release Build Version 0.02.001-47-g2fa28c4
[TheForceEngine-v0_02_001-47-g2fa28c4.zip](archive/TheForceEngine-v0_02_0001-47-g2fa28c4.zip) <br>
This is a pre-release version of the Core Game Loop Release. In this version 3 enemies are still missing (the Phase 2 Dark Trooper, Boba Fett, and General Mohc) and there are numerous bugs and known issues - including being forced to play in 320x200 since the floating-point sub-renderer had to be removed temporarily due to refactoring.

### Pre-Release Build Version 0.01.006-1; Win64
[TheForceEngine_0_01_0061.zip](archive/TheForceEngine_0_01_0061.zip) <br>
Changes:
  * "Hot-fix" due to an error in the registry code not verifying the final source data directory.
  * Fixes a "freeze" in "Prelude to Harkov's Defection" when shooting at certain walls.
  * Fixes hardcoded GOG game source data paths for Dark Forces.
  * Fixes Steam game source data paths for Outlaws.
  * Outlaws paths are always filled out now if possible, though only Dark Forces is playable.
  * Now uses the registry to find Steam and GOG game paths, making auto-detecting the game data much more robust - similar to Doom ports like ZDoom and Chocolate Doom.

### Pre-Release Build Version 0.01.005; Win64
[TheForceEngine_0_01_005.zip](archive/TheForceEngine_0_01_005.zip) <br>
Changes:
  * PrintScreen will now take screenshots which will be saved in the /Documents/Screenshots/ folder.
  * The "Configure" menu option now opens up configuration menus.
  * Game paths can now be set in the application in the "Game" configuration menu.
  * A few graphics settings such as resolution, Fullscreen/windowed can be set in the Graphics menu. "Custom" is available as a resolution choice, which provides additional UI to manually set the desired resolution.
  * About tells you the Build version and provides useful links.

### Pre-Release Build Version 0.01.004; Win64
[TheForceEngine_0_01_004.zip](archive/TheForceEngine_0_01_004.zip)

### Experimental Builds; Win64
[TheForceEngine-Experimental-01172021-6](archive/TheForceEngine-Experimental-01172021-6.zip)
