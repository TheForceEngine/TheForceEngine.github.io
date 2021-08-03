---
layout: default
title: Task System
permalink: TD_Task_System.html
---
# Task System

### Contents
* [Description](#description)
* [Usage](#usage)
* [Task Functions](#task-functions)
* [Prioritization](#prioritization)

Prev: [Jedi Overview](TD_Jedi_Overview.md) ... Next: [Inf System](TD_Inf_System.md)

---

# Description
The Task System is the core method used to construct the main loop using the Jedi Engine.  The concept is similar to Fibers or Co-routines, in that task functions stay alive as long as they loop and processor time is given to other tasks using the `task_yield()` command. Yield causes the current task function to return but it will resumed in the future (next frame or after a fixed delay) from the same place. Tasks allocate internal local state which is maintained so that the functions are re-entrant.

The system was derived from Dark Forces, however changes were made to make the system more portable, rather than using their assembly code directly. The main changes are:
* Local State is now allocated and accessed directly using macros, rather than the system directly manipulating the stack.
* Sub-functions called from task functions that use yields need to be created as **Sub-Tasks**.
* Re-entry support is implemented using C hacks instead of using custom assembly code. The way this is implemented will probably be revisited but is good enough for the base game. I plan on adding proper co-routine support to the script system - so that might be the better way to go for mods.
* Task functions require some "decoration" - marking the beginning, end and local state - though it is minimal.
* A frame break is added, which basically means that a primary task is marked such that the frame ends right *before* the task is run. In this way the task system can be used with a modern OS, such as Windows.

Source Code: `TFE_Jedi_Task/`

# Usage
There are two "tracks" used by the system. The primary track consists of major tasks, such as the main game task (`mainTask()` in the Dark Forces code) - these are created using the `pushTask()` function - and the secondary track, which are tasks attached to the current primary task - created using `createTask()`, see [[Dark Forces Game Loop]] for an example.

Launching a task can be done using `launchCurrentTask()` which launches the most recently *pushed* task, `runTask()` which runs the task that is passed in along with its parameter - this runs the task and then returns to the calling task when finished or a yield is encountered. `task_yield()` can be called, which returns from the current task and selects a secondary task attached to the current task or if there are none, moves on to the next primary task. Note that is a value in ticks is passed in, the current task will not be resumed until that time elapses. Finally, when exiting from a task function (instead of yielding), it is automatically removed and then another task is selected.

When running a task, an integer parameter can be passed along (default = 0) that can be used to perform specific actions. Generally the default loop action is performed with `parameter = 0` but other values can be used for special or one-time actions. When tasks need to be shut down, the convention is to pass in `-1` as the parameter, which the task functions should be on the look out for.

Often tasks are suspended indefinitely `task_yield(TASK_SLEEP);` - which means there needs to be a way to wake them up. This can be done from any task, using `task_makeActive(task);`.

Example:
```C
Task* task = TFE_TaskSystem::createTask(taskFunction);
```

# Task Functions
A task function is similar, in principle, to a main function of a thread, fiber or co-routine. Most tasks will loop forever and use `task_yield()` at least once in the loop. Below is the anatomy of a task function:

```C
void taskFunction(s32 param)
{
	struct LocalContext
	{
		// Any local variables that need to be preserved go here.
		s32 example;
	};
	task_begin_ctx;
	
	while (param != -1)
	{
		// Do stuff
		
		// Access local variables using: taskCtx->name
		taskCtx->example++;

		// delay = TASK_NO_DELAY (the task will be resumed next frame),
		// TASK_SLEEP (the task will sleep until it is made active),
		// or number of ticks.
		task_yield(delay);
	}
	
	task_end;
}
```

If no local state is required, a simpler form can be used instead:
```C
void taskFunctionNoLocalState(s32 param)
{
	task_begin;
	
	// stuff
	
	task_end;
}
```

# Prioritization
TODO
