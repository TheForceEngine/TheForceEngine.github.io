## 

| Contents |
|:------|
| [About](#about) |
| [Native Application](#native-application) |
| [Built-in Modding Tools](#built-in-modding-tools) |
| [TFE Framework](#tfe-framework) |
| [Core Game Code](#core-game-code) |

Next: [Table Of Contents](TFE_Table_of_contents.md)

---

## About
![Logo](TFE_ProgramIcon.png)
**The Force Engine** (TFE) is an Open Source project that aims to port the *Dark Forces* and *Outlaws* games to modern operating systems, extend the feature set, and implement modern modding tools. This means that the original data is required - it is not included with the project. The good news is that both games are available for purchase on digital storefronts such as GOG and Steam.

This consists of several components:
* [Native Application](#native-application)
* [Built-in Modding Tools](#built-in-modding-tools)
* [TFE Framework](#tfe-framework)
* [Core Game Code](#core-game-code)

## Native Application
A native application designed to make running the games easy without emulation. This includes a *System UI* used to setup game data paths, graphics and sound settings, rebind inputs, provide simple methods to use mods, and other expected features.

## Built-in Modding Tools
Built-in modding tools, including a modern *level editor*. These tools are tightly integrated with the runtime allowing for much quicker iteration.

## TFE Framework
 This includes OS level functionality, file access, GPU access using the Rendering Backend, logging, and other low level systems.

## Core Game Code
Derived from the original source using reverse-engineering. The goal is "source port" accuracy. The OS and library components, such as raw input, timing, file access, and screen blitting use the TFE Framework while the game and rendering code uses the refactored, reverse-engineered code - as close as possible to the original source.

From this optional extensions are derived, such as the ability to support higher resolutions, post processing and color correction, modern controls and other features. This will also include full GPU rendering support in the future, and full multiplayer.

---

Next: [Table Of Contents](TFE_Table_of_contents.md)
