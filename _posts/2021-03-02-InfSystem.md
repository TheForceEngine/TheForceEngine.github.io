---
layout: post
title: INF System and TFE Progress
---
In the last post - [TFE Update and 2021 Plans](https://theforceengine.github.io/2021/01/18/TFE-Update-2021-Plans.html) - I talked about the INF & Classic Renderer release which was to be followed by a "Player Control & Physics" release later in the year. Due to the way the renderer, INF and player controller are connected there has been a change of near-term plans. This post will go over those changes, talk about how the INF system works internally and provide a general update regarding the progress towards this year's goal of reaching the 1.0 release.

# Connections
## What do I mean about connections?

In order to render the world correctly, the sector geometry must be correct (such as floor and ceiling heights) and texture offsets for the various elements must be set (such as floor and ceiling offsets). However, some of these values are not correct until the INF data is loaded and the initial stops are setup. So here, we can see that the visuals are incorrect until the INF system is working.

Similarly, the INF system affects the player - elements like scrolling textures do not directly update the player position, rather the player controller queries the sector "links" (see INF System Overview below) and then handles any needed updates. Conversely, the interaction between the player and INF system, such as hitting switches, landing on the floor, and crossing lines are also handled by the player controller and collision detection systems. In other words the INF system is incomplete without the player controller and collision detection systems.

## What does this mean for the "Classic Renderer" release?
Essentially this means that the Classic Renderer release will take longer than planned, the new target being the end of March. However, it also means that the Classic Renderer release will not only have correct rendering, correct INF functionality - greatly improving the usability of mods, but also that the "Player Control & Physics" milestone is being moved up and completed as part of this build. This means the next build will _feel_ like Dark Forces - with accurate physics, jumps, control and collision.

# Progress Update and Timelines
## Progress
Reverse-engineering for the INF System is nearly complete, the last elevator update function will be finished in the next few days and the code integration is not too far behind and should be done this week. The entry points for the player controller, physics, and collision detection have been reverse-engineered, though work in that area is just beginning. As mentioned above the new target is the end of March for the next build.

## The Build
I consider the next build the turning point for the project, essentially meaning it will be at "top of the peak." There will be a lot of work to do afterwards, of course, but the most challenging and time consuming elements will be behind us. In other words, for me at least, it will be the most exciting build yet and will lay the foundation for the future of TFE. Unfortunately for most players, there won't be much new to experience - though mods/user-levels will work much better and the game will _feel_ like Dark Forces. That said, the build will require a lot of testing to make sure the visuals, INF, and player control are accurate and to make sure bugs have not been introduced.

## Overall Timeline
Because the player controller and physics are included in this release rather than being a seperate milestone for later, this delay should not impact the overall timeline for the project - its more of a re-ordering of tasks. It does mean that the cross platform build is getting delayed a bit (by about a month or so) - but there will be more there when it does happen.

## A Note on Timelines
_All timelines presented here are targets and are subject to change as "real life" and future discoveries dictate._ I like having targets to strive toward which also serve to way to communicate with others the scope of the work and to keep a feeling of forward momentum, however they are **not** promises and further delays may happen.

# INF System Overview
## What is INF?
The INF acronym, like COG, doesn't actually mean anything according to an interview with the original team. However it handles all interactivity with the level - the system controls switches, doors, elevators, lighting changes, moving and rotating sectors, scrolling textures, when mission goals are completed, text and audio that play or is displayed as you complete objectives, determining when you have successfully completed the mission, and more.

The level INF is a text based data file consisting of various "items," where each item consists of one or more elements which control and interact with sectors, walls, or the system. In general these elements consist of _Elevators_ - sectors that change in some way, such as changing height, rotating, or changing light level, _Triggers_ - these generally trigger other INF items, such as switches, and _Teleporters_ - which consist of only "chutes," sectors meant to seamlessly teleport the player vertically between sectors to allow for vertical connections between areas.

Example Elevator:
```
item: sector            name: complete
  seq
    class: elevator move_floor
    stop: 55 hold
    stop: 56 hold
      page: 1 m01kyl01.voc
      message: 1 rickenbacker master_on
    stop: 56 4
    stop: 56.5 2
      message: 3 parking_space wakeup
    stop: 57 0
      message: 4 text_boy m_trigger
    stop: 57 complete
    speed: 0
  seqend
```

Example Trigger:
```
item: line      name: blocker_panel     num: 2
  seq
    class: trigger switch1
    client: blocker1
    client: blocker2
  seqend
```

Of course I'm leaving out details, a single "item" can actually have multiple INF elements. A sector can have multiple elevators and triggers, for example. There are older INF resources that are mostly accurate and later I will add full INF up-to-date documentation to this site for furture reference, along with any extra functionality that gets added for TFE mods. But for this post, I think a basic summary will suffice. From a glance, it is easy to see that the INF system is very flexible and essentially acts like a very limited scripting language. The rest of this post will cover the internal workings of the system rather than exhaustively covering how to use the system.

## A Note on Timing
Dark Forces quantizes time to 145 ticks per second. So any time "ticks" are mentioned, it means 1/145th of a second. These are always whole numbers. Also note that **delays**, which are stored as floating point in the data, are actually multiplied by 145.5 and then truncated when converting to ticks. This means that converting from seconds to ticks slightly overestimates the **delay** length. This is done to essentially "round up" - since rounding down could make it impossible to make certain jumps, get through an area in time, etc. in low framerate situations if the timing is too tight.

## Level Geometry INF Setup
### Message Addresses
During level load, every named sector is added to a list of "message addresses" - this is basically just a way of mapping from sector name to level sector. This way the INF system does not have to search through the level data during load. This also means that the name to sector mapping is static beyond this point and cannot be changed. It also means that multiple sectors with the same name may not be handled intuitively.

### Automatic INF Items
INF items are also automatically created for sectors with the "door" and "exploding wall" flags during level geometry loading. Those particular "special" INF types automatically create the necessary _stops_ and maps to one of the 11 core _elevator_ types. Explainations of what those terms mean can be found in sections that follow.

## Loading and Parsing INF
As mentioned above, the INF data for a level is loaded from a separate text file. This file is parsed during load which creates links, elevators and triggers as internal structures. Unlike an actual script language, there is no interpreter or VM, though there is an equivalent in the form of an update function.

### Links
Sectors and walls have pointer to an optional list of "InfLinks." These are exactly what they sound like - they *link* a sector or wall to an INF element, such as a *elevator* or a *trigger*. These link to the source (the sector or wall), to the target (the INF element), and they also hold information about when the link can be used. This comes in the form of an *entity mask* and *event mask*. I will talk about these more later, but briefly the *event mask* tells us *what action or event* triggers the link and the *entity mask* tells us *what type of thing* can trigger the event. This might be an enemy crossing a sector wall from the front - these masks decide if this event by the enemy entity can trigger the link. _Triggering the link_ then causes that event to be passed on to the target elevator, trigger, or sector as appropriate.

### Triggers
The main purpose of Triggers is to trigger other INF items. Which seems redundant but makes sense. When a player interacts with a switch, the player controller code doesn't know what to do next. It just decides if the associated link (the one attached to the wall with the trigger) can to triggered. From there the Trigger itself will recieve the "nudged" event from the player entity. The trigger also has a list of links, built from the clients specified in the INF data, that connect it with the trigger targets. The trigger has an event that it sends, which is usually different than the one it received. By default this event is 0 - basically meaning it should be ignored. The trigger also has a "message" that it passes along which tells the elements being triggered what to do. You can specify what message to send, though the default is "m_trigger."

However, in addition to sending messages to clients, a trigger can also change the texture frame of its source wall (like a switch), display a text message to the screen and play a sound.

### Elevators
Elevators are the workhorse elements of the INF system. There are 11 core elevator types:
* __move ceiling__ - _moves the sector ceiling height._
* __move floor__ - _moves the sector floor height._
* __move offset__ - _moves the sector second height._
* __move wall__ - _translates sector walls horizontally in the direction derived by the angle variable._
* __rotate wall__ - _rotates sector walls around the center variables by the angle variable._
* __scroll wall__ - _scrolls the sector wall textures in the direction specified by the angle variable. Note each wall section has separate flags to determine what parts are affected._
* __scroll floor__ - _scrolls the sector floor texture, again in the direction defined by the angle variable._
* __scroll ceiling__ - _scrolls the sector ceiling texture by the direction defined by the angle variable._
* __change light__ - _change the sector light level._
* __move fc (move floor ceiling)__ - _moves both the floor and ceiling heights of a sector together by the same amount._
* __change wall light__ - _changes the light offset of any walls in the sector with the correct flag set._

Of course there are many more types presented to the mapper, such as _door, door inverse, inverse, basic_auto,_ and more. These all map to one of the 11 core types, but some of these change flags and settings or automatically generate stops for common types. This also allows doors and exploding walls to be specified as sector flags when creating levels, greatly simplifying the work flow.

An elevator consists of _stops_, these are similar to key frames - these determine _how_ an elevator changes. Each stop defines a _value_, which may be relative, and this value determines how much the sector moves, changes light level or other value. What it does is determined by the type of elevator. In addition stops can have a delay - this tells the system how long the elevator should pause before going to the next stop. Some delay values, such as Terminate, tell the elevator to shut down for good.

At each stop an elevator can also play a special sound ("page") or send out messages to other INF elements, sectors, or itself. These messages range from enabling or disabling other elements, changing to the floor or ceiling texture of a sector based on another sector, changing the adjoins of one or more pairs of walls, sending another elevator to the next, previous or specific stop, and more.

In-between stops, the elevator changes its value, moving it towards its next stop and updates the sector based on the type of elevator. This is where the heartbeat of the system comes in.

### Elevator Update
The core task of the INF system is an update function that runs as often as necessary - or that was the plan anyway. Basically the code takes a fair amount of effort to determine when the next update time should be and only update as often as possible. Unfortunately, since some elevator is almost always active somewhere in a level it really runs almost every frame (for TFE it will run every frame to simplify the code slightly without changing the functionality).

Whenever the update runs, it loops through all of the elevators, determines if it should be updated - its "next tick" being less than the current tick - and then updates its value based on the associate elevator update function. How quickly this value gets updated is based on its _speed_, another variable you can set in the INF data. If you don't set it, every elevator has its own default. A speed of zero (0) causes the elevator to update to the next stop instantly.

When the elevator reaches the next stop, the page is played and any messages are sent. Then the "next tick" is updated, it is "current tick" + delay. A special value is written if the elevator is to stop until triggered. If the elevator is complete (delay is complete or teriminate), then it is deleted, as are any links pointing to it.

## Final Words
This was a fairly brief overview and skimped on details, but that will be rectified in the future with complete INF documentation. It is a complex system with a lot of moving parts, but ultimately it isn't hard to use or understand when you get used to it.

The TFE level editor will simplify the creation of INF with a tool dedicated to the task (already partially complete) and in the future INF elements will be able to call script functions to add greater flexibility the TFE-based mods. But for now, the INF system nears completion finally unlocking the rich set Dark Forces level mods.

