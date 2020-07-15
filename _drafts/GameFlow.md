## Game Flow
This is an alternative way of specifying the game flow in a more extensible way. This basically combines Jedi.lvl, Cutmuse.txt and Cutscene.lst into one file. New (non-vanilla) mods can use this to customize the gameflow (add more or fewer levels for example).

```C++
GameInfo
{
  Name: <string>
  // Cutscenes that play at the beginning of the game before the player hits a key.
  Introduction
  {
    // Cutscenes are just listed in order, one flows directly into the next cutscene. Skipping a cutscene will being the next.
    Cutscene
    {
      Asset: <string>     // Cutscene asset, usually an LFD or video file.
      Scene: <string>     // Scene within the asset, omit if unneeded (such as a video).
      Speed: <int>        // Playback speed
      MusicVolume: <int>  // Volume as percent of normal, i.e. 100 = 100% volume.
      // Music Cues, these match cues provided by the cutscene system. Note that thse will not be necessary when using video.
      Cue { Name: <string>; iMuse: <int>, <int>, <int>, <int> }
      Cue { Name: <string>; iMuse: <int>, <int>, <int>, <int> }
      // ...
    }
    Cutscene { ... }
    // ...
  }
  // Cutscenes that play once the final level has been completed after its cutscenes are complete.
  // In Dark Forces, this was the final credits.
  Ending
  {
    Cutscene { ... }
    // ...
  }
  // List of all levels in the game, played in order.
  // Note that unneeded blocks can be omitted. For example if there are no "PreLevelCutscenes" than it can be omitted and the briefing will start immediately.
  // If Briefing is omitted (such as for Outlaws), then the previous or global difficulty level will be used.
  Levels: 14
  {
    // Level 1
    Level
    {
      SlotName: <name>    // "SlotName" maps to the level file name, such as "SECBASE"; Display name and other info is pulled directly from the level file.
      PreLevelCutscenes
      {
        Cutscene { ... }
        // ...
      }
      Briefing
      {
        Asset: <string> // The LFD to pull the briefing from.
        Name: <string>  // Name of the briefing assets inside the archive - such as "sebase" or "robotics"
      }
      PostLevelCutscenes
      {
        Cutscene { ... }
        // ...
      }
    },
    // Level 2
    Level
    {
      ...
    }
    // ...
  }
}
```
