---
layout: page
title: Downloads
---

Current Releases are for testing only, the gameplay is incomplete.

### Warning
These builds are for testing only. The following features still do not work:
* iMuse - only the base track plays.
* Sound volume and attenuation is inaccurate compared to DOS.
* Cutscenes do not play.
* There are no mission briefings.
* You cannot bring up the PDA.
* Only 320x200 mode works at the moment.
* There is no game end.

### Known Issues
Some of these are bugs, others simply haven't been integrated or implemented yet.
* Mines trigger through closed doors.
* LAREDLITE does nothing.
* Health damage flashes too fast when taking major damage.
* The System UI doesn't quite work fully.
* Sound volumes and attenuation do not match DOS.
* The Config option in the Escape menu does nothing.

### Timeline
For more information about when The Force Engine will be useful and what the plans are for 2021, please see the [TFE Roadmap](Roadmap.md)

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
