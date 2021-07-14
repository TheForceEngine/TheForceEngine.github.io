---
layout: post
title: Game Loop
---
The shape of the core game loop is now clear, so this post will go over its structure and also talk about any changes being implemented for TFE. It will also talk about progress towards the next test release and what has been accomplished so far.

# Progress
Before talking about the game loop itself, it seems useful to talk about the progress towards the next test release. Missing (skipped) functionality in the Load Mission Task has been reverse-engineered, the Task System has been reverse-engineered and implemented, though there are still some tweaks to be made before release, reverse-engineering has been completed for the following (including support functions): runGame(), Load Mission Task, Mission Task (was the “main” task), the Player Weapon Task (though some individual weapon fire functions need work), the Projectile task, Hit Effects, the Pickup task, the Sprite Animation task, the Texture Animation task, Object Update task, the INF system, and more. The structure of the AI logics tasks though more work is required here for individual AI types.

Work currently is progressing on the Player Controller task, though it is mostly complete. I expect it to be finished this week.

Work is still needed on the Vue, Generator and Sound Emitter tasks, though they are fairly simple compared to the Player Controller, weapon tasks, and Task System and shouldn’t take very long.

Overall there is a couple of weeks worth of work still to go before the Core Game Loop test release is ready. The work has been steady and consistent but ultimately guessing how long reverse-engineering will take can be a bit dicey. To put this release in perspective, the Player Controller, by itself, is a few _thousand_ lines of C code and that isn't even the largest chunk of code.

It has been a long road, but this release will be a major milestone for the project and certainly the top of the mountain. There will be more work before version 1.0 is ready, but this release will get us most of the way there.

# TFE Game Loop
The main game loop consists of the game specific code, contained in TFE_DarkForces, and engine code that is consistent between games (TFE_TaskSystem, Game Loop below).

Each game will have a “main” module, which will consist of three functions: runGame(), exitGame(), and loopGame(). The entry and exit points (runGame() and exitGame()) are required but loopGame() is optional if all of the per-frame game logic is handled by tasks. Dark Forces handles the game loop this way, setting up the required tasks during runGame() and thus loopGame() is omitted.

# TFE_Game
The core game interface. There will be an implementation for Dark Forces (next test release) and Outlaws (once Dark Forces is complete).
IGameMain
The game main interface consisting of just three functions:
 * __runGame():__ Required. Game entry point.
 * __exitGame():__ Required. Game exit point.
 * __loopGame():__ Optional. Called every frame to update and render the game.

# TFE_DarkForces
## DarkForcesMain
The Dark Forces implementation of IGameMain,  the main entry point to the game. Note that loopGame() is not implemented since the game is updated using only the task system.
 * __runGame():__ Entry point, sets up tasks. This function is run when preparing to load a mission. This sets up the Load Mission Task, reads agent data, fills in the PlayerInfo struct, and allocates memory for state if needed.
 * __exitGame():__ Called when aborting a mission or exiting the game. This unwinds the tasks, cleans everything up and saves any data.

## Mission
The main mission entry point, this handles loading the mission from a high level and kicks off the Mission Task, which will handle the rendering, time keeping, and serve as the main task after loading.
 * Load Mission Task
 * Mission Task
### Load Mission Task
Handles loading the mission - calling functions to load the level geometry, objects, setup the palette, setup object logics, and setup the Mission Task. Once the mission task is finished loading and the Mission Task is ready, it is put to sleep. When it resumes it will then unload the mission data.
### Mission Task
The main mission task function. This function is designated as the “frame break” - which means that a new frame begins _before_ the start of this function. The Mission Task handles the camera, rendering, effects, and time keeping. Once it completes, which occurs when the player decides to go to the next level, abort the current mission or quit, the Load Mission Task is made active in order to properly unload.

Note: In the original game there were no frame breaks, but on modern systems, such as Windows, this break allows TFE to interact properly with the rest of the OS and simplifies systems such as input and interaction with the GPU.

## Player
The player consists of two main elements - player data, such as inventory, health, and other state, and the Player Controller Task. The player controller handles player input, physics, collision detection, weapon animation, level interactivity using messages to the INF system.
 * Player Controller Task
 * PlayerInfo
 * Player objects - the physical object and the “eye.”

## Player Weapon
The Player Weapon Task handles switching weapons, primary and secondary fire, and animating the weapon on or off the screen. When fired, each weapon has its own function that is called. This is handled by a table of function pointers indexed by the current weapon.

## Projectile
The projectile task handles the movement of projectiles over time, projectile collision, damage messages on hit.

## Hit Effect
The hit effect task handles creating hit effects, handling their lifespan, playing sound effects, waking up enemies within range of a hit, and explosions.

## Pickup
The pickup task is mostly idle but is directly called from the Player Controller Task when the player collides with a pickup. Pickups include everything in the levels that the player can collect such as ammo, powerups, health and shields, keys, inventory items, and goal items.

## Sprite Animation
This task handles the animation of all sprites (WAXs) with “ANIM” Logic. This is also used to animate hit effects, explosions, and other cases where simple one time or looping sprite animation is required.

## Texture Animation
The Texture Animation Task handles all texture animation. It loops through all of the animated textures in the level and updates the current texture stored in the level data based on the animation and time elapsed.

## Object Update
The Object Update Task handles all objects with the “UPDATE” logic. This is also used to handle simple objects with possible movement, and gravity; such as objects that should be affected by elevators or that should drop and bounce around.

## Vue
The Vue Task handles updating Vue animations and handles chaining them, “sleeping” and waking animations.

## Generator
The Generator Task handles “AI” generators, which are objects that can spawn new enemies of a certain type based on various parameters, such as player distance, number already active, and total spawned versus a maximum.

## Sound Emitter
The Sound Emitter Task handles sound emitting objects that can be placed throughout levels to provide effects such as continuous river and waterfall sounds.

## AI
All of the tasks mentioned above create a single task that loops through a list of objects. AI agents are handled differently with at least one task created for each agent. There are quite a number of AI tasks, so I won’t enumerate them here. As the AI tasks are finished, the tasks will probably be split into multiple files based on code sharing.

Using one or more tasks per entity allows agents to be put to sleep when not needed and be updated at different rates based on the current situation in order to control how much CPU time is needed.

# TFE_InfSystem
The INF System was also reverse-engineered and implemented as part of this release. It too uses the task system to update each frame and to allow the game code to interact with it. 

## INF Elevator Task
The Inf Elevator Task handles elevator updates, movement and other changes, and stops.

## INF Trigger Task
The Inf Trigger Task handles sending the appropriate messages from triggered elevators, switch textures, and other trigger based INF messages.

## INF Teleporter Task
This loops through the teleport sectors and teleports the player if they meet the required conditions.

# TFE_iMuse
The iMuse system will be left incomplete for this test release, but the structural code has been reverse-engineered in order to make going back to it after this release easier.
## iMuse Task
This is where the iMuse system adjusts the midi tracks being played, handles volume control, etc.. Note that this task will remain only partially complete until after the next test release.

# TFE_TaskSystem
The task system is directly derived from the Jedi system with some changes to work better with modern systems and to make it more portable.
 * Task functions manually handle creating and using persistent state. This process is simplified using helper macros and doesn’t significantly add to the complexity.
 * Task functions have “decorated” beginning and ending clauses - these are simply macros but they are required for every task function.
 * Child functions that use yield() need to be launched as child tasks.
 * The system has a notion of a “frame break” - a point where the task processing ends for a frame instead of using an infinite loop. This means that the task system can run on the main or rendering thread.

The task system has a simple scheduler that allows tasks to yield for a specific period of time before being resumed. Tasks can also delay indefinitely, meaning they never continue unless made active again, or have zero delay - meaning they will run the next frame regardless of the elapsed time (TASK_SLEEP and TASK_NO_DELAY delay values).

Tasks can yield control at any point, as mentioned above. Tasks can also create or push new tasks, which are then inserted into the lists. Tasks can run other tasks with a parameter used to define the requested action. When this occurs, the current task becomes the “return task” - and is resumed once the other task is executed. Finally, if a task function is exited the task is removed from the system and automatically destroyed.

In this way, only a single task needs to be created and then the tasks can create and remove tasks during runtime as needed.

# Game Loop
With the main systems in place, including others that were previously implemented such as TFE_InfSystem, TFE_JediRenderer, etc., I can talk about the game loop.

The Agent Dialog is still using the stand-in, non-reverse-engineered code - it is functional enough for this stage of development and will be finished along with the remainder of the in-game UI in a future release.

From the Agent Dialog, when the player starts a level - the core game loop begins:
 * runGame() is called from DarkForcesMain.
 * runGame() reads the agent data, fills in the PlayerInfo struct, and creates and launches the Load Mission Task. Afterward runGame() will return and the task system will take over.
 * When the Load Mission Task is run, which will happen the next time runTasks() is called from the Task System, the level will be loaded, Logics are set up, and the tasks will be created - including the main Mission and Player Controller tasks. Once this is done, the Load Mission Task is put to sleep.
 * Once the user or system requests the program to exit, the current mission to be aborted, or the System UI is used to return to the main menu exitGame() is called to stop and clean up all of the tasks and game state.

# Main Loop
Most of these systems were already in place before this next release. The main new entry is the Task System which is used by the game core loop.
 * Handle OS Messages
   * Window resizing requests.
   * Input which is stored by the Input System to make it accessible by the game code and UI code.
   * Mouse polling for input (how far has the mouse moved since last frame, etc.).
   * Other windows messages (close, minimize, etc.).
 * Tasks are run (runTasks() called from the task system), assuming the game is not paused.
   * Rendering is done through the Mission Task while the core game loop is running.
   * Reacting to input is handled through tasks, such as the Player Controller.
   * Sounds and music is also controlled through the various tasks, but actual mixing and playback occurs in the Audio and Music threads.
 * Blit the virtual frame buffer to the back buffer. If a valid GPU target is available, most of the work will occur using a shader on the GPU.
   * Conversion from 8-bit to 32-bit color.
   * Upscale.
   * Post processing (bloom, optional).
   * Color Correction (optional).
 * System UI
   * The System UI is The Force Engine UI designed to be used regardless of the game being played. Right now only Dark Forces is supported but the same UI will be used with Outlaws as well.
   * The System UI handles (or will handle in some cases) game data setup, control setup, sound volumes, easier mod loading, and graphics and window options.
 * Present
   * Vsync (optional).
   * Blit back buffer to screen or window.
