---
layout: default
title: Progress Tracker
permalink: ProgressTracker.html
---
# Progress Tracker
This page shows the current list of tasks being worked on, with the most recent week on top. The list shows one week at a time since day-to-day tasks often change depending on what was accomplished previously, shifting priorities, and new discoveries. For more long-term planning, I will still use stand GitHub tasks and milestones. For longer-term plans, please see the [roadmap](Roadmap.html).

## Bugs
I have changed this list to include all of the major bugs for version 1.0. Note that some minor bugs have been excluded but remain in the Bugs forum.
- [ ] Health damage flashes too fast when taking major damage, like falling.
- [ ] Mines will trigger through closed doors when the player is in their proximity.
- [ ] Player slides on rotating sectors which may end up pushing them off. Best observed with Fuel Stations rotating sector area.
- [ ] LAREDLITE does not work. Putting in the cheat does not show the message and the enemy ai remains active.
- [ ] (INF) "Shelves" on Jabba's ship lower too soon. see https://the-force-engine.freeforums.net/thread/38/current-bugs
- [ ] Gammorean Guard corpses will slide slightly forward after dying.
- [ ] Physical damaging enemies will continue to attack you after you are dead, and keep turning the screen red.
- [ ] Some mid-level VUEs are not triggering, see level 9 Cargo 3do does not move around central area and Tie Fighters on Executor.
- [ ] Enemies don't die when falling off a ledge (the "terminal velocity" check).
- [ ] Some decorations do not have proper collision (see Level 10 Jan Ors).
- [ ] (INF) You should not be able to reactivate an elevator in motion (causes the sliding puzzle in level 11 to break if clicking on the switch multiple times).
- [ ] Sound effect objects are missing (https://the-force-engine.freeforums.net/thread/51/lack-wind-environment-sound-shaddaa).
- [ ] Mines still drop too fast (https://the-force-engine.freeforums.net/thread/52/dropping-mines-tfe-faster-dos).

## 11-15-2021
### Bugs
- [x] The AT-AT model used in some mods is still incorrect (see Dark Tide 2).
- [ ] Enemies don't die when falling off a ledge (the "terminal velocity" check).
- [ ] (INF) You should not be able to reactivate an elevator in motion (causes the sliding puzzle in level 11 to break if clicking on the switch multiple times).

### CGL Release
- [x] Mod support for TFE.
- [ ] Finalize release - which includes a GitHub tag and version update.

### Cutscenes & UI Release
- [ ] Initial work on cutscenes.

## 11-08-2021
### Bugs
- [x] Hitting with the fist attack is more difficult in TFE than DOS.
- [x] Compressed loading screens not showing up correctly.
- [x] 3DO loading with zero-vertex parts.
- [x] Timing issues when forcing vsync off externally and switching refresh mid-session.

### CGL Release
- [x] Restore high resolution and widescreen support.
- [ ] Mod support for TFE.

### Finish AI
- [x] General Mohc (Phase 3).

## 11-01-2021
### Bugs
- [x] Hall of mirror errors in TFE that don't exist in vanilla, see Robotics Facility and Gromas Mines.
- [x] Specific type of walls not being added to the automap when seen.
- [x] Executor level does not end correctly - you can reach the end but complete level is never called.
- [x] The Mouldy Crow return animation is never played in level 4 (but the level is completable anyway).

### Other
- [x] LAIMLAME cheat does not protect from health damage.

### Finish AI
- [x] Boba Fett (WIP)

## 10-25-2021
### Bugs
- [x] Add missing remote functionality.
- [x] Cleanup the Classic Renderer and prepare for the reintroduction of high resolution and widescreen support.
- [x] Phase 1 Dark Trooper issues when the player is out of sight.
- [x] AI Actors can erronenously fit through spaces that the player has to crouch to get through.
- [x] Flying AI Actors can clip into the ceiling, making it harder to hit them.
- [x] The player can get stuck on walls instead of smoothly sliding.
- [x] Player collision jitters more then DOS.
- [x] The sound when falling into vaccuum or dying in a gas sector is terrible and doesn't match DOS.
- [x] Sometimes projectiles miss when they should hit due to crossing multiple sectors.
- [x] The weapon vertical pitch offset is slightly incorrect when looking down.

### Finish AI
- [x] Phase 2

## 10-18-2021
### Bugs
- [x] Missiles and missile packs cannot be picked up.
- [x] The concussion rifle looks green while shooting in dark sectors on Nar Shaddaa instead of blue.
- [x] Fix moving/rotating sector collision INF bug (blocks completion in Ramsees Hed).
- [x] Elevators do not "crush" corpses (sometimes blocks completion in Ramsees Hed).
- [x] Crushers should only affect the player if the player height is less than the original limit, not the limit adjusted for water sectors.
- [x] Fix 3DO Second Height Movement/INF Bug (blocks proper completion in Detention Center).
- [x] Fusion Cutter secondary fire speed (it is too fast).
- [x] Re-check vertical projectile push force on enemies.
- [x] Music should pause when opening the Escape menu.
- [x] Shield pickups seem to have collision with player Thermal Detonators though Mortars don't seem to be effected.
- [x] When creating a new agent, SecBase is automatically selected.
- [x] Fix AI Movement Bug for basic enemies when reacting to walls, impassable ledges, and drops (noticeable with Ree-Yees in Ramsees Hed).
- [x] Fix the similar AI movement bug for boss enemies.
- [x] Phase 1 teleporting (see https://the-force-engine.freeforums.net/post/138)
- [x] Sometimes "hit effects" trigger too high when shooting enemies.
- [ ] LAIMLAME cheat does not prevent health damage.

### Pre-Release
- [x] Pre-Release Public Builds (320x200, 4:3 only).

## 10-11-2021
### Talay Update
- [x] Finish Vue Logic.
- [x] Generator Logic.
- [x] Level complete function.
- [x] Fix master-off INF triggering bug (noticeable in Talay).
- [x] Fix bug where level-end message and ship return are not triggered.
- [x] Fix texturing bug with transparent mid-textures and vertical scaling (noticeable in Talay).
- [x] Update video running through Talay to demonstrate above work and general progress.

### Bugs
- [x] Auto aim kicks in even when enemies aren't in the player's view.
- [x] Fix texture animation INF bug.
- [x] Weapon should switch when picking up a better weapon.
- [x] The player falls when an elevator is lowering instead of smoothly lowering with it.
- [x] Fix land sound effect playing too often.

### Level Transitions
- [x] Escape Menu with Abort/Next Level.
- [x] Level transitions.
- [x] Player Death, respawning, and failure.

### Other (may slip, Pre-Release build will not be delayed for these).
- [x] Level cheats.
- [x] Finish proper inventory handling in Jabba's Ship.

## 10-04-2021
- [ ] AI Integration
  - [x] Sewer Creatures.
  - [x] Kell Dragons.
  - [x] Welder.
  - [x] Remote.
  - [x] Phase 1 Dark Trooper.
  - [ ] Phase 2 Dark Trooper.
  - [ ] Phase 3 Dark Trooper.
  - [ ] Boba Fett.
- [x] Probe Droids going "under water" in Anoat City (was a sign issue with desired vertical movement).
- [ ] Generators.
- [ ] Escape menu, to support level abort/next level.
- [ ] Finish cheats - level changing cheats are all that is left.

## 9-20-2021
- [ ] AI Integration
  - [x] Fix-up different types of Actors (some structs should be shared that are not).
  - [x] Actor boilerplate.
  - [x] Mousebot
  - [x] Exploding Barrel
  - [x] Scenery
  - [x] Troopers (officer, commando, storm trooper).
  - [x] Flying Enemies (Int Droid, Probe Droid).
  - [x] Turrets.
  - [x] Gamorrean Guards
  - [x] Transhodans
  - [ ] Melee Enemies (Sewer bugs, Dragons).
  - [ ] Other basic enemies.
  - [ ] Dark Troopers.
  - [ ] Bosses (Boba Fett, Phase 3).

## 9-13-2021
- [x] fix memory errors.
- [x] memory region support, to allow for clean level changes, de-fragmenting memory, etc.
- [x] fixed sound errors - the code could stop the incorrect sounds, causing them to "cut off".
- [x] finish weapon task integration.
  - [x] WTID_HOLSTER.
  - [x] Integrate weapon fire functions:
    - [x] Fist
    - [x] Pistol
    - [x] Rifle
    - [x] Thermal Detonator
    - [x] Repeater
    - [x] Fusion
    - [x] Mortar
    - [x] Mine
    - [x] Concussion
    - [x] Cannon
- [x] Player damage and explosion messages.
- [ ] AI Integration
  - [x] Land Mine (Pre-placed)

## 9-06-2021
- [x] finish player task integration.
  - [x] integrate handlePlayerMoveControls().
  - [x] integrate handlePlayerPhysics().
  - [x] integrate handlePlayerActions().
  - [x] integrate handlePlayerScreenFx().
- [ ] test, verify, debug and fix issues with the integration up to this point.
  - [x] collision errors - some adjoins are still impassable.
  - [ ] inf errors - there are still some minor bugs to find.
  - [x] task errors - there are still some issues with task calling order not matching DOS.
  - [x] rendering errors - some switches are misaligned, some objects are not properly rendered (even though the sectors are).
- [ ] finish weapon task integration.
  - [x] WTID_SWITCH_WEAPON (tested).
  - [x] WTID_START_FIRING (untested, covered later).
  - [x] WTID_STOP_FIRING.
  - [ ] WTID_HOLSTER.
  - [x] Integrate weapon fire functions for: pistol, rifle.
- [x] hook up sound system.
  - [x] get the music playing and stopping again.
  - [x] hook up the Jedi Sound API stubs to the TFE sound system. Note: propogation and 3D panning may not match Dark Forces exactly, but this will be handled in a future release.

## 8-30-2021
- [x] finish main task integration.
  - [x] integrate automap.
  - [x] figure out sin/cos differences, look at table results versus TFE results (causing odd looking circles compared to DOS in the automap).
  - [x] integrate handlePaletteFx().
  - [x] integrate hud_drawAndUpdate().
  - [x] integrate hud_drawHudText().
  - [x] integrate updateScreensize().
  - [x] integrate setupCamera().
  - [x] integrate drawWorld().
  - [x] integrate weapon and mask drawing.
  - [x] integrate handleGeneralInput().
