---
layout: default
title: Progress Tracker
permalink: ProgressTracker.html
---
# Progress Tracker
This page shows the current list of tasks being worked on, with the most recent week on top. The list shows one week at a time since day-to-day tasks often change depending on what was accomplished previously, shifting priorities, and new discoveries. For more long-term planning, I will still use stand GitHub tasks and milestones. For longer-term plans, please see the [roadmap](Roadmap.html).

## 10-04-2021
- [ ] AI Integration
  - [ ] Melee Enemies (Sewer bugs, Dragons).
  - [ ] Basic enemies: Remote, Welder.
  - [ ] Dark Troopers.
  - [ ] Bosses (Boba Fett, Phase 3).
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
