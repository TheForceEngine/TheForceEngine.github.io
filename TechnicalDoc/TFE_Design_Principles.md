---
layout: default
title: TFE Design Principles
permalink: TFE_Design_Principles.html
---
# TFE Design Principles

### Contents
* [Core Principles](#core-principles)
  * [Accuracy](#accuracy)
  * [Preservation](#preservation)
  * [Performance](#performance)
  * [Cross Platform](#cross-platform)
  * [KISS](#kiss)
  * [Clean Code](#clean-code)
  * [Simple Code](#simple-code)
* [Code Structure](#code-structure)
* [Source](#source)

[Table of Contents](TD_Table_Of_Contents.md)<br>
Next: [Core Loop](TD_Core_Loop.md)

---

# Core Principles
### Accuracy
Implement the games as they *are* not as a re-imagining. This is why the original game and engine code is being reconstructed by reverse-engineering the original executables.
### Preservation
Preserve the original code when possible, even if it means making separate derivative systems to extend it. An example of this is keeping the original fixed-point renderer for Dark Forces, along with all of its limitations, and then building different sub-renderers to extend it without modifying the original functionality.
### Performance
Performance, both in terms of memory and speed, should be considered when writing code and designing systems.

### Cross Platform
Support multiple platforms going forward (Linux, OS X, Windows). There is a lot of work to be done here still.

### KISS
Keep the code simple, implement what is needed and avoid over-generalizing systems. Implement what we need now, not what we might need a year from now.

### Clean Code
Avoid hacky or hard to read code when possible. When not possible (such as when dealing with reverse-engineered code or third party libraries), make sure the code is documented sufficiently to be understandable months down the road.

### Simple Code
Prefer simple, direct code over layers of abstraction. Code should be shared as a means of compression, to avoid repition, and to ease future programming. Excessive, up front abstractions usually do little to improve maintenence and often make debugging more challenging. This extends to the idea that we should prefer Composition over Inheritance and to keep hierarchies flat as possible.

Avoid code that is overly complicated, abstracted, or hard to understand what is *really* going on and hard to debug. This means limiting the use of templates, *auto*, and similar constructs. It is generally better to be explicit except in cases where there is a *large* benefit or the nature of the implicit code is self-evident. In other words, reduce hidden complexity.

# Code Structure
In general, the idea is to organize the code while keeping the tree relatively flat. Deep code trees can make discovery and navigation painful and so the code is organized at a high level in just a few categories. In general, the structure is: `Source/Category/System/leaf files`.

For examples: `Source/TFE/Audio/audioDevice.h`, `Source/TFE/Archive/gobArchive.h`

Note that everything under TFE/ is fully open source without any licensing issues. However, code under TFE_Jedi, TFE_DarkForces, and TFE_Outlaws was reconstructed from reverse-engineered code. Even in the case of derivative code, such as the floating-point sub-renderer, using the code in other projects is dubious at best without express permission from *LucasArts* and/or *Disney*.

# Source
The main source tree, holds main, OS specific application files, and convenient access to shaders, scripts and other data.

## Source/TFE
The TFE framework, this includes archives support, low level audio, low level midi, the file system, System UI, memory management, render backend, settings, and other framework related systems. Everything under TFE/ uses the **TFE** namespace. This code is fully open source and third party libraries that are used have compatible licenses.

## Source/TFE_Jedi
The Dark Forces and Outlaws Jedi renderer, reconstructed by reverse-engineering the original games. Everything under TFE_Jedi/ uses the **TFE_Jedi** namespace.

## Source/TFE_DarkForces
Dark Forces specific game functionality, such as the player controller, logics, and the main game loop. Source code was reconstructed by reverse-engineering Dark Forces (DOS). Everything under TFE_DarkForcess/ uses the **TFE_DarkForces** namespace.

## Source/TFE_Outlaws
Outlaws specific game functionality. Source code will be reconstructed by reverse-engineering Outlaws. Everything under TFE_Outlaws/ uses the **TFE_Outlaws** namespace.
