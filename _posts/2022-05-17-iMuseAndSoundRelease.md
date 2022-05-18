---
layout: post
title: iMuse and Sound Release
---

# Version 0.9
Version 0.9 has been a long time coming, taking much longer than originally anticipated. Version 0.9 is focused on sound playback and music accuracy, ambient sound support, and a few bug fixes.

# iMuse
IMuse (**I**nteractive **M**usic **S**treaming **E**ngine) was the last system needed to complete Dark Forces support in TFE. It is the dynamic music system that Lucas Arts developed and used in many of their games such as Monkey Island 2, Tie Fighter and, of course, Dark Forces. See https://en.wikipedia.org/wiki/IMUSE for a general description.

iMuse, as used in Dark Forces for music, is basically scripted Midi - the midi data itself contains *sysex* events, such as jumps (like **goto** in C). The host (Dark Forces game code) can interact with the Imuse playback, such as manually jumping to different places in the midi, changing tracks, or midi files on the fly.

There are often loops in the midi and the cutscene playback system would set **hooks** at certain points that will cause IMuse to break out of those loops or jump to new places in the midi at specific points in the cutscene - allowing for musical cues, looping while waiting for an animation to finish, and similar control.

Dark Forces used IMuse **triggers** to set callbacks when certain points of the midi are hit, allowing for smooth transitions between tracks ("stalk" and "fight") based on what is happening in-game. A level starts with the stalk track playing and when a certain number of enemies become agressive for long enough, the music transitions to the fight track by taking the next transition and then looping. Finally, when things have calmed down, the music transitions back to the stalk track. To help with transitions, IMuse can intelligently **sustain** individual notes from one track while the next track plays, so that the notes don't suddenly stop too early.

Imuse has a variety of other features such as fading and panning sound, playing multiple tracks at once, and a variety of other features not used by Dark Forces - such as the streaming music.

Games did not link in IMuse directly, but rather the IMuse binary was shipped with the game data. The code used a header file along with some code to commuicate with the IMuse binary, similar to modern DLLs. The game would call IMuse functions specified in the header file, which then called an internal command dispatch function which finally called the internal equivalent to the requested function.

TFE simplifies the system, integrating the IMuse code into the project directly and removing the command dispatch system - instead the game code calls the IMuse commands directly. IMuse features that are not used in Dark Forces are stubbed out for the most part, mostly because I have no good way to test them.

Rather than call into the driver directly, the iMuse code sends midi commands to the TFE low-level midi player which handles the midi device, acting as the driver layer for iMuse. In order to run in the background as the game played, iMuse setup an interrupt handler running the update every 6944 ns, or about 144 Hz. For TFE, instead of an interrupt handler, I added support for a callback on the midi thread - in order to avoid thread contention - which fires at a fixed time step. Of course this caused complications, such as interactions between the Landru/Cutscene thread (with updates running at ~291.3 Hz) and iMuse, necessitating the use of atomics for a few of the iMuse state variables.

iMuse is also used for low-level digital audio playback and normalization, linking to the TFE AudioSystem thread for updates in a similar way that midi was implemented. In the original code, the digital audio updated occured in the same interrupt handler as the midi update. The way it worked is that it would query the driver if it was ready for the next set of sound samples (512) and if not, skip the update. For TFE, the iMuse digital audio update is instead called by the low-level audio thread to provide the samples instead. Interestingly iMuse features such as sound fading and triggers work the same way for digital audio as music tracks.

In terms of complexity, iMuse is very similar to the INF system - which is also a psuedo scripted system. Fortunately, iMuse is the last major system needed to support Dark Forces. Except for bug fixes, the reverse-engineering phase for Dark Forces is complete.

# Game Sound
On top of iMuse, Dark Forces basically implements two sound systems - one for Landru (cutscenes), most likely directly from Tie Fighter, and the other using Dark Forces game data and Jedi math functions to handle in-game sounds. Because there are only 8 ditigal audio channels available, though iMuse (and now TFE) support 16, sound priority is very important and every loaded in-game sound is provided a prority so that you always hear the most important sounds.

The sound falloff in TFE was approximated up to this point, but I knew it would not be accurate. 3D Sound in Dark Forces can be heard from up to 150 units away and will play at full volume at 30 units. Between 30 and 150 units from the eye, the volume is linearly interpolated.

Ambient sounds were also implemented. These are objects placed in the world that emit 3D sound that loops continuously. They are used for effects such as the wind ambient sounds in Nar Shaddaa.

# Other Features
Other features that were implemented include the ability to bind the mouse wheel to controls, such as switching weapons (the new default), the use of mouse wheel as an option in various game screens - such as mission briefings, System UI scaling to better support 1440p and 4k, a proper crash handler to write out minidumps on event of a crash, and a variety of fixes. In addition the System UI sound panel is now working and gives you the ability to adjust sound fx volume and music volume separately for cutscenes and in-game. The Sound config also has an option to enable 16-audio channels for iMuse, and the Game config allows you to disable the fight music in-game if desired.

# Version 1.0 Plans
With version 0.9 finally released, the next major release will be version 1.0 - complete support for Dark Forces in TFE. Unlike the 0.9 release, the plan is to split up the release into several smaller releases. There will be 2 main parts:
* Bug Fixes. I plan on splitting bug fixes by system and do one or more 0.9x release for each system. Examples include AI bugs, weapon bugs, collision issues, INF issues, etc..
* The GPU renderer - the last major feature for version 1.0. The GPU renderer will support both shearing for looking up and down (which emulates the software renderer) and accurate perspective projection to allow the player to look up and down further without distortion like modern 3D games. Initially it will support 8-bit color emulation with optional colormap interpolation to remove banding. Later, after version 1.0 is released, true color rendering, dynamic lights and other features will be added.
