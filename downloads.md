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
* 3 of the bosses do not work yet (Phase 2 Dark Trooper, Boba Fett, General Mohc).
* There is no game end.

### Known Issues
Some of these are bugs, others simply haven't been integrated or implemented yet.
* Gromas Mines' cliffside near the elevator into the facility has a HOM when you look up.
* Mines trigger through closed doors.
* LAIMLAME does not project you from health damage.
* LAREDLITE does nothing.
* The Moudly Crow does not return at the end of Test Base (though the level can still be finished).
* In-mission Vue animations don't seem to be triggering (Cargo containers in Nar Shaddaa, Tie Fighters on Executor), though pre-mission/post-mission animations are playing.
* Health damage flashes too fast when taking major damage.
* The System UI doesn't quite work fully.
* Sound volumes and attenuation do not match DOS.
* The Config option in the Escape menu does nothing.

### Timeline
For more information about when The Force Engine will be useful and what the plans are for 2021, please see the [TFE Roadmap](Roadmap.md)

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
