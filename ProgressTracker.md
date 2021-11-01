---
layout: default
title: Progress Tracker
permalink: ProgressTracker.html
---
# Progress Tracker
This page shows the current list of tasks being worked on, with the most recent week on top. The list shows one week at a time since day-to-day tasks often change depending on what was accomplished previously, shifting priorities, and new discoveries. For more long-term planning, I will still use stand GitHub tasks and milestones. For longer-term plans, please see the [roadmap](Roadmap.html).

## Bugs
A note for small bugs noticed during testing. This is not exhaustive, and there will be dedicated time to thoroughly test the game once the features for the release are complete. These bugs can be fixed at any time, and will be moved to the correct list when that happens.
- [ ] Re-check mine triggering (they trigger through closed doors).
- [ ] Re-check player movement on rotating sectors (see Fuel Station).

## 11-01-2021
### Bugs
- [x] Hall of mirror errors in TFE that don't exist in vanilla, see Robotics Facility and Gromas Mines.
- [x] Specific type of walls not being added to the automap when seen.
- [ ] Executor level does not end correctly - you can reach the end but complete level is never called.
- [ ] The Mouldy Crow return animation is never played in level 4 (but the level is completable anyway).
- [ ] Mid-level VUE animations don't play; examples: cargo containers in Nar Shaddaa or Tie Fighters in Executor.
- [ ] "Shelves" lowering too soon in Jabba's Ship (see [https://the-force-engine.freeforums.net/thread/38/current-bugs]([https://the-force-engine.freeforums.net/thread/38/current-bugs)).
- [ ] Enemies aren't killed when they hit "terminal velocity."
- [ ] Kell Dragon stops when player overlaps in another layer.

### Other
- [ ] Mod support for TFE.
- [ ] Missing sound emitting level objects (example: wind sound in Nar Shaddaa).
- [ ] LAREDLITE cheat.
- [ ] LAIMLAME cheat does not protect from health damage.

### Finish AI
- [ ] Boba Fett (WIP)
- [ ] General Mohc (Phase 3).

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
