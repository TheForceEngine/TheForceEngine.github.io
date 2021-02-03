---
layout: page
title: Downloads
---

Current Releases are for testing only, the gameplay is incomplete.

### Warning
These builds are for testing only. While basic rendering, level interactivity, traversal and sound work the game is not really "playable" yet. The following elements either don't work or are placeholder for testing:
* Enemy AI - enemies can be killed but they do __NOT__ react in any other way.
* Game UI - the PDA does not work, though some elements like the Agent dialog and Esc menu do partially work (enough for testing).
* Cutscenes
* iMuse - midi music plays but the tracks do not dynamically update based on combat.
* Weapons - only a few weapons work and they do not use ammo.
* Most items - the headlamp works (F5) but most other items do not.
* Most pickups, with the exception of those needed for progression like keys and mission goals, cannot be picked up.
* INF mostly works for vanilla levels but often fails in mods - meaning level interactivity in mods usually doesn't work correctly (and there are a few examples in vanilla levels that don't quite work). The vanilla levels are completable, though most mods are not. The reverse-engineering for INF is currently in progress though, so this will be fixed soon.

### Timeline
For more information about when The Force Engine will be useful and what the plans are for 2021, please see the (TFE Update and 2021 Plans Blog Post)[https://theforceengine.github.io/2021/01/18/TFE-Update-2021-Plans.html]

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
