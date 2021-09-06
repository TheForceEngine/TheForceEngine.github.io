---
layout: default
title: Progress Tracker
permalink: ProgressTracker.html
---
# Progress Tracker
This page shows the current list of tasks being worked on, with the most recent week on top. The list shows one week at a time since day-to-day tasks often change depending on what was accomplished previously, shifting priorities, and new discoveries. For more long-term planning, I will still use stand GitHub tasks and milestones. For longer-term plans, please see the [roadmap](Roadmap.html).

## 9-06-2021
- [ ] finish player task integration.
  - [ ] integrate handlePlayerMoveControls().
  - [ ] integrate handlePlayerPhysics().
  - [ ] integrate handlePlayerActions().
  - [ ] integrate handlePlayerScreenFx().
- [ ] finish weapon task integration.
  - [x] WTID_SWITCH_WEAPON (tested).
  - [x] WTID_START_FIRING (untested, covered later).
  - [ ] WTID_STOP_FIRING.
  - [ ] WTID_HOLSTER.
  - [ ] Test and verify shooting and hit effects.

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
