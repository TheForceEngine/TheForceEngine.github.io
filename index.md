---
layout: default
title: Home
---

# The Force Engine (TFE)

## About
The Force Engine is a project with the goal to reverse engineer and rebuild the Jedi Engine for modern systems and the games that used that engine - **Dark Forces** and **Outlaws**. The project will include modern, built-in tools, such as a level editor and will make it easy to play **Dark Forces** and **Outlaws** on modern systems as well as the many community **mods** designed to work with the original games.

Playing Dark Forces or Outlaws using the Force Engine will add ease of use and modern features such as higher resolutions and modern control schemes such as mouse-look. Using the built-in tools will allow for easier modding with more modern UI, greater flexibility and the ability to use enhancements made to the Jedi Engine for Outlaws in custom Dark Forces levels - such as slopes, stacked sectors, per-sector color maps and more.

Note that while Dark Forces support is nearly complete (version 0.9), Outlaws is **not** playable yet - the focus so far has been on the framework, Dark Forces support, and JEDI reverse-engineering. However, Outlaws support is planned and will be complete in TFE version 2.0. See **Current State** below.

## Current State
The project is in a pre-release state, version 0.9. While it shares a legacy with DarkXL, it is a complete rewrite - rebuilt from the ground up with a much greater focus on accuracy. It is much more focused than the XL Engine, focused on being a Jedi Engine replacement/port only - thus full support for Dark Forces and later Outlaws. Please check the [Roadmap](Roadmap.md) for more information on release timetable and planned feature-set.

### Current Release
The current release is **version 0.9** and only supports Dark Forces. All weapons, AI, items, and all other systems function, including IMuse. You can play through Dark Forces from beginning to end and play some Dark Forces mods. There are still bugs, that will be addressed for version 1.0.

### Next Release
**Version 1.0**, though I plan on doing smaller releases as bugs are fixed.

## Minimum Requirements for Test Builds
* Windows 7, 64 bit.
* OpenGL 3.3

## Minimum Requirements at Release
Note that older OS versions might work (such as Vista) but at least Windows 7 is highly recommended. Software rendering still relies on OpenGL to accelerate blitting. Generally a 2010 or later PC is recommended, though machines as old as 2009 or even 2006, depending on OS, may work but will likely not perform well unless running at a modest resolution. Note that some older GPUs may perform poorly with hardware rendering due to driver issues or poor support for required features (such as older integrated Intel chipsets) - in these cases software rendering should be used.
* Recommended 2010 era PC or newer
* Recommeded 2+ GB RAM
* Windows 7 (2009) / Linux (Version Info TBD)
* 32 bit or 64 bit
* CPU with SSE2 support (any desktop/laptop CPU released after 2004)
* OpenGL 2.1 for Software Rendering (2006 era GPU)
* OpenGL 3.3 for Hardware Rendering (2010 era GPU)

## Some Planned Features at Release
The project is focused on accuracy - by using reverse engineering techniques to reconstruct the original code and algorithms - the Force Engine is designed to be extremely accurate, a complete replacement for the original executables. The engine supports three feature templates to make it easier to tune the experience:
* **Classic** - `a recreation of the original software renderer, controls and gameplay - providing the original experience as close as possible while still properly supporting modern systems.`
* **Retro** - `close to the original experience while being enhanced with modern controls and high resolution rendering.`
* **Modern** - `modern enhancements such as proper perspective rendering, enhanced texture filtering, mipmapping, widescreen and more.`

From these general templates, settings can be fine tuned. One example is "Classic" settings with higher resolutions or mouse look. Or using the perspective renderer but sticking to 320x200. Both the "Classic" and Perspective renderers support pure software rendering and gpu based rendering, though some features - such as enhanced texture filtering - are only available using gpu rendering.

Additional control methods will be supported, such as gamepads with the ability to freely rebind keys and buttons at any time.
