---
layout: page
title: Downloads
---

Current Releases are for testing only, the gameplay is incomplete.

### Timeline
For more information about when The Force Engine will be useful and what the plans are for 2022, please see the [TFE Roadmap](Roadmap.md)

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
