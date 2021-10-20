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
* The key rebinding menu does not function (though you can bring it up).
* 3 of the bosses do not work yet (Phase 2 Dark Trooper, Boba Fett, General Mohc).
* There is no game end.

### Timeline
For more information about when The Force Engine will be useful and what the plans are for 2021, please see the [TFE Roadmap](Roadmap.md)

### CGL Pre-Release Build Version 0.02.001-47-g2fa28c4
[TheForceEngine-v0_02_001-47-g2fa28c4.zip](archive/TheForceEngine-v0_02_0001-47-g2fa28c4.zip) <br>
This is a pre-release version of the Core Game Loop Release. In this version 3 enemies are still missing (the Phase 2 Dark Trooper, Boba Fett, and General Mohc) and there are numerous bugs and known issues - including being forced to play in 320x200 since the floating-point sub-renderer had to be removed temporarily due to refactoring.
#### Known Issues
Some of these are bugs, others simply haven't been integrated or implemented yet.
* Sometimes "hit effects" trigger too high when shooting enemies.
* Gromas Mines' cliffside near the elevator into the facility has a HOM when you look up.
* Mines trigger through closed doors.
* Players slip on rotating sectors.
* Phase 1 teleports and has trouble when losing sight of the player.
* Enemies have buggy movement when hitting solid walls, drops, or ledges that are too high.
* LAIMLAME does not project you from health damage.
* LAREDLITE does nothing.
* The Moudly Crow does not return at the end of Test Base (though the level can still be finished).
* Shield pickups have collision with thermal detonators.
* Health damage flashes too fast when taking major damage.
* Probe Droid explosions have a very small radius. 
* The System UI doesn't quite work fully.
* Sound volumes and attenuation do not match DOS.
* Only 320x200 is supported for now, widescreen and higher resolutions will be coming back soon.
* Cutscenes do not work.
* Mission briefings do not work.
* iMuse does not work - the fight track does not play (but the base track does).
* You cannot bring up the PDA.
* The Config option in the Escape menu does nothing.

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
