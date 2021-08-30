---
layout: post
title: Progress Update And Plans
---
As The Force Engine (TFE) approaches the Core Game Loop Completion milestone, I thought it was time for another update and to talk about plans for reaching TFE version 1.0 and beyond.

### Contents
* [Update](#update)
* [Core Loops](#core-loops)
* [Plans](#plans)

# Update
All of the major systems are structurally complete, with only smaller "loose ends" left to deal with in terms of reverse-engineering. Thus I recently switched over to the integration process and getting this reverse-engineered code into TFE with all of the necessary refactoring. Here is the integration process for various phases:
* Dark Forces startup - "main": Finished.
* Main game loop: Finished. This release is skipping cutscenes and mission briefings, so technically the loop still has some incomplete elements, but it is done for this release.  * Agent Dialog: Finished. It now works properly with save game data (DARKPILO.CFG) - reading and writing save data. You can create and remove agents and select levels. Using save game data also means it will be now possible with progress properly through the game.
* Level Load: 95% Complete - loading geometry, objects, and INF is complete. Loading the "goals" is a loose end, though it isn't strictly necessary for this release.
* Mission Startup: Finished. This includes creating the "main task," creating tasks such as player task, loading the level, setting up the HUD, setting up the projectile system, clearing out screen effects, displaying the loading screen, and similar tasks.
* The Main Task: The structure is complete, but this area is still a work in progress. My goal is to have the Main Task complete this week.

The goal is to be testing levels properly with the fully reverse-engieered game loop this week. Once I have tested out the already completed systems, such as INF and the player controller, then I can go back and finish the loose ends and prepare for the release. The loose ends include some of the weapon firing functions (each weapon gets its own), some AI routines, and whatever else I find during the integration or testing process.

# Core Loops
Note: this section goes over some code, though it is mostly pseudocode and isn't too complicated. However, if you would rather skip ahead to [Plans](#plans) below - I will understand.

Going into detail about all of the work that has gone into reverse-engineering and rebuilding Dark Forces and the Jedi engine would take a long time, I thought it would be interesting to show what the "core loops" look like. The two most important loops for this release are the "Main Loop" - that is the loop that runs in main() and controls the game flow and the "Game Loop" - the "Main Task" that runs using the task system, and controls the rendering and general input. To make things more confusing, the "Player Controller Task" is separate from these, and this is what handles general player control, input, player collision, etc. - but I will save that for another day.

## Main Loop
Here I will show the main loop in pseudocode:
```C
while (1)  // <- This is replaced by the function call from the main TFE loop.
{
	// TFE: This becomes a game state in TFE - where runAgentMenu() gets an update function - it can't loop forever.
	s32 levelIndex = runAgentMenu();  <- this loops internally until complete and returns the level to load.
	updateAgentSavedData();	// handle any agent changes.

	// Invalid level index just maps back to the runAgentMenu().
	if (levelIndex <= 0) { continue; }  // <- This becomes a return in TFE, back off and try again.

	// Then we go through the list of cutscenes, looking for the first instance that matches our desired level.
	s32 cutsceneIndex;	// <- this is the index into the cutscene list.
	for (s32 i = 0; ; i++)
	{
		if (cutsceneData[i].levelIndex >= 0 && cutsceneData[i].levelIndex == levelIndex)
		{
			cutsceneIndex = i;
			break;
		}
	}
  // Then do some init setup for the next level ahead of time; the actual loading will happen
  // after the cutscenes and mission briefing.
  setLevelByIndex(levelIndex);
		
  // The inner most loop - this cycles through the cutscene entries, each of which lists the game mode.
  // TFE: Again this becomes a game state, where each iteration through this loop is from a single
  // function call into loopGame().
  while (!s_invalidLevelIndex && !s_abortLevel)
	{
		GameMode mode = cutsceneData[cutsceneIndex].nextGameMode;
		switch (mode)
		{
			case GMODE_ERROR:
				// Error out.
			break;
			case GMODE_CUTSCENE:
				// TFE: Cutscene playback becomes a state.
				// Play the cutscene
				cutsceneIndex++;	// <- next loop, this goes to the next cutscene or instruction.
			break;
			case GMODE_BRIEFING:
				// TFE: Briefing becomes a state.
				// Handle the mission briefing.
				cutsceneIndex++;	// <- next loop, this goes to the next cutscene or instruction.
			break;
			case GMODE_MISSION:
				// TFE: In Mission becomes a state, but here the Task System will take up the slack (which will act very similarly to the original game).
				// Create the loadMission task, which will then create the main task, etc.
				// Start the level music.
				// Read saved game data for this agent and this level.
				// Launch the level load task.
				// After returning from the level load task, stop the music.
				// If not complete set abortLevel to true (which breaks out of this inner loop) otherwise
        
				// Save the game state and level completion info to disk.
				cutsceneIndex++;	// <- next loop, this goes to the next cutscene or instruction.
				levelIndex++;
				setNextLevelByIndex(levelIndex);	// <- prepares the next level for when we get to it after the cutscenes and briefing.
			break;
		}
	}  // Inner Loop
}  // Outer Loop
```

As you can see, the main challenge is that the loop contains a bunch of smaller loops. So, for TFE, this loop had to be broken down into states with transitions. Then each state, such as the Agent Menu, can be called from here when it is active. So all of the original code still exists in TFE, but the structure is a bit different in order to handle running only a single frame at a time.

## Game Loop
The Jedi Engine has a Task system that is used once the in-mission code takes over. Each task acts like a fiber or co-routine, and they support yielding control at arbitrary points. The yield can have a delay, such as TASK_NO_DELAY (meaning it will be called again next frame), TASK_SLEEP (meaning it will never be called again unless it is made active again), or a number of ticks.

In the original code, the task system is recursive, the next task is selected during the yields or when tasks complete and this continues until all of the tasks are complete (i.e. the player exits the game, or aborts or completes the current level). Obviously this won't work well with a modern OS, so TFE makes the task system iterative rather than recursive and adds a "framebreak" marker to a task - which basically means the frame ends once this task is complete. This allows TFE to exit out of the task loop every frame and resume on the next.

The main Game Loop, only active while actually playing a mission, is one of these tasks - the "Main Task" in the DOS code (that is the actual name, which I found from error messages).

```C
void mission_mainTaskFunc(s32 id)
{
	task_begin;
	while (id != -1)
	{
		// This means it is time to abort, we are done with this level.
		if (s_curTick >= 0 && (s_exitLevel || id < 0))
		{
			break;
		}
		// Handle delta time.
		s_deltaTime = div16(intToFixed16(s_curTick - s_prevTick), FIXED(145));
		s_deltaTime = min(s_deltaTime, FIXED(64));
		s_prevTick = s_curTick;
		s_playerTick = s_curTick;

		setupCamera();

		switch (s_missionMode)
		{
			case MISSION_MODE_LOADING:
			{
				blitLoadingScreen();
			} break;
			case MISSION_MODE_MAIN:
			{
				updateScreensize();
				drawWorld();
			} break;
			case MISSION_MODE_LOAD_START:
			{
				clearPalette();
			} break;
		}

		handleGeneralInput();
		handlePaletteFx();
		if (s_drawAutomap)
		{
			automap_draw();
		}
		hud_drawAndUpdate();
		hud_drawHudText();
    
		// vgaSwapBuffers() in the DOS code.
		setPalette(s_palette);
		TFE_RenderBackend::updateVirtualDisplay(s_framebuffer, 320 * 200);

		// Pump tasks and look for any with a different ID.
		do
		{
			task_yield(TASK_NO_DELAY);
			if (id != -1 && id != 0)
			{
				mainTask_handleCall(id);
			}
		} while (id != -1 && id != 0);
	}

  // Wake up the mission load task to finish the cleanup.
	s_mainTask = nullptr;
	task_makeActive(s_missionLoadTask);
	task_end;
}
```

Notice the while loop, which exits using the task_yield() function - and then resumes at that point next frame or when another task calls the main task with a non-zero id.

# Plans
## Core Game Loop Release
The Core Game Loop release is still the next planned release. While it has taken longer than I originally planned for, as you can see above it is getting close to the finish line. This release will include saving and loading Dark Forces save game data (meaning your current saves will work), creating and deleting agents, proper saved progression through the game, proper visuals using the reverse-engineered classic renderer, pickups, items, all weapons working correctly, accurate player control, physics and collision detection, accurate level interactivity (INF), full enemy AI, palette effects from picking up objects and getting hurt, all items - such as the gasmask - working correctly, Vue animations, basic controller support, key and button rebinding, mouse and controller sensitivity adjustment.

The editors will be temporarily off-line, due to the complete refactor of the code base to properly use the reverse-engineered code. However, they will come back in a future release (see below).

Note, however, with all of this being made available at once there will inevitably be bugs and issues. I consider this to be an __Alpha__ release - since it is not yet feature complete. Missing elements will include: cutscenes, mission briefings, some in-game UI (PDA), iMuse, and there will be some sound inaccuracies.

## Bug Fixes
There will be plenty of bugs to fix, so this is a placeholder here. This probably won’t be a big release by itself - instead it will be a bunch of smaller “point” releases. This will likely continue as the next releases are being worked on.

## UI & Mission Briefings
The next major system will be the in-game UI, especially useful when looking at mission objectives and key codes using the PDA. Once the UI and mission briefings are in place, the game is technically fully playable.

## Sound
This release will implement the correct sound falloff and 3D effects and finally fully implement the iMuse system.

## Version 1.0 Release
With this release, TFE will be a complete replacement for DosBox. I am still on track for completing this by the end of the year. If the Core Game Loop release makes it out this month, then I think this will be _very_ likely to be released as scheduled. However, there is still a chance that it can slip - I think we'll have a very good idea when the Core Game Loop Release is finished.

## Voxels!
Quite some time ago now, I implemented an experimental voxel renderer that integrated seamlessly with the Jedi classic renderer. However, there were some loose ends to deal with, such as not supporting the full VOX format and dealing with some palette issues. This release will integrate that code with the main branch and add support for replacing objects with their voxel counterpart.

## Tools
The focus of this release is to get the tools working again with the reverse-engineered code. This will include basic functionality like importing and exporting assets, viewing them, etc..

## Level Editor
The first release of the full level editor. It might still be missing some planned features, but as of this release it should be fully usable for building real levels and mods.

## Towards Version 2.0
Finally, hopefully early next year, I plan on beginning the process of adding Outlaws support to TFE. I don't yet have any real way of making any time estimates beyond this point, but I expect the reverse-engineering process to proceed at a much quicker rate for Outlaws for several reasons:
* I have become a lot faster at the process by going through the process of reverse-engineering Dark Forces.
* Outlaws was built from the Dark Forces code base, and shares the same engine. This means a lot of the structures will be the same or substaintally similar.
* I have a better sense of how to organize the process and reduce re-work and refactoring time.

## Perspective and Hardware Renderers
Once the Outlaws enhancements to the Jedi Engine are reverse-engineered, I will be in a much better place to tackle the Perspective and Hardware accelerated renderers for TFE.
