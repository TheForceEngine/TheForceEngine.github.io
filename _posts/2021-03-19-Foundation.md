---
layout: post
title: TFE Foundation and Test Release
---
The Jedi Renderer and INF System have been completely reverse-engineered and the collision detection system is almost complete. But a new problem looms on the horizon.

# The Problem
Reverse-engineering the Jedi Renderer was completed sometime back and was integrated into The Force Engine along side the existing temporary renderer. In order to support higher resolutions while preserving the original renderer as-is, a Fixed-Point sub-renderer was implemented and then a Floating-Point sub-renderer was derived from that. This works great and allows for arbitrary output resolutions and cleans up sub-texel precision issues nicely.

The issue is that the INF system, recently reverse-engineered but not yet fully integrated and the collision system, now partially reverse-engineered, are written against the original fixed point implementation. Converting those to floating point might be beneficial but might also have unforseen consequences that can subtly modify existing functionality, especially in mods. Ideally any such change should be tested and implemented carefully. This suggests that the original fixed point implementation should be preserved for now and not rely on the state of the renderer.

# The Solution
For the initial release, I think it is clear that the fixed point data should be in memory and kept up to date. The idea is to factor out the fixed point sector data so that it is accessible by the INF, collision and render systems and to maintain and keep it up to date as the level changes. Then, if needed, this floating point data is mirrored and cached so that it can be used by the floating point renderer. This suggests possible issues:
 * More memory consumed by level data - given modern systems, even doubling the amount of memory used to store sector data seems trivial. For performance reasons, all elements required for rendering should be duplicated but even with tens of thousands of sectors the memory increase will be modest and the amount of memory being fetched at runtime unchanged except when sectors change - which is generally a small percentage of the total number of sectors.
 * Decreased performance due to updating both fixed point and floating point data - this is true and unavoidable for this approach. However, sector data is updated only when needed. This means that a small amount of data needs to be updated and cached at any time.
 * Forcing vanilla level spatial size limits due to fixed point limitations - this is again unavoidable but necessary in the short-term.
 
# The Plan
The plan is to split out the level fixed-point level geometry into its own system, which is then accessible by the INF system, Collision detection system and Renderer. Specialized sub-renderers, such as the Floating-point and GPU sub-renderers will then cache any required data internally since it is not needed by the rest of the game. To communicate that floating point or GPU data needs to be updated for a sector a dirty flag will be set and the data will be updated in a "lazy" manner (as-needed). This should be both consistent with the original DOS code and allow for specialized and improved sub-renderers.

 * TFE_LevelGeometry - this will store all of the level geometry in the original fixed point format.
 * TFE_InfSystem - references and updates level geometry as needed and will flag sectors as "dirty" so that the floating point data can be cached when needed.
 * TFE_Collision - the collision detection system can be called directly from the game systems or INF system. This system can also directly reference level geometry and can change it, but since it only changes collision related information does not need to trigger updates to the floating point cached data.
 * TFE_JediRenderer - the Jedi renderer can reference the fixed point level geometry. If using the floating point or GPU sub-renderer, cached data is stored internally since it is not needed by any game system.
 
The core idea is to avoid costly runtime conversions whenever possible and to intelligently cache the floating point data only when needed. This should minimize the performance impact while enabling the renderer to fully support high resolutions and high quality texturing, like it does now, while allowing the reverse-engineered gameplay code to be fully integrated and tested against the original game.

# The Future
Clearly using floating point for the source level data is desired as that will unlock the ability to have larger levels and improve performance in many cases. However, I do not think that straying too far from the reverse-engineered code when dealing with gameplay elements is a good idea without being able to do proper A/B comparisons and ensuring that this doesn't break existing functionality in obscure ways. Or at least, we need to know what functionality, if any, is affected so that proper work arounds can be implemented.

Finally, my goal is still to finish an initial release this year - which seems tantilizingly close to reality given the recent progress in reverse-engineering INF, collision detection code, and player contoller code. Achieving this goal means being able to integrate the reverse-engineered code as-is as much as possible and avoid worrying about Fixed-Point vs Floating-Point issues until after the first release.

# Current Progress Towards the Test Release
Percentages are approximate.

 * Reverse-engineering the original Renderer: 100%
 * Reverse-engineering the INF system: 100%
 * Reverse-engineering the collision system: 80%
 * Reverse-engineering the player controller / player physics: 50%
 * Integrating Jedi Renderer: 100%
 * Integrating INF System into TFE: 90%
 * Integrating player controller / player physics: not started.
 * Refactoring: 10%
 
# Test Release Target
Due to new findings, the target needs to be moved once more due to the increase in scope. It is still close, the reverse-engineering has been going well and the above refactor should only add a few weeks. So, given the current rate of progress, my new target is end of April. This will be a huge release, with the following features - most of which are already complete:
 * Accurate renderer that supports the original 320x200 fixed-point sub-renderer and higher resolutions using the floating-point sub-renderer.
 * Large performance improvements at higher resolutions thanks to GPU color conversion, asynchronous frame buffer uploads and general improved rendering performance.
 * Accurate game timing up to 145 fps, which should produce a much smoother experience when running on lower end systems or running without vsync.
 * Improved System UI with the ability to alter graphics settings while in-game, so you can see the changes as you make them in real-time.
 * Optional color correction.
 * The ability to adjust the Scale and Positioning of the HUD elements in-game using the System UI.
 * The ability to drag & drop mod zip files or load them from the System UI to more easily test mods.
 * Accurate player control, physics and collision detection. This means that the "feel" of the game will finally match the DOS experience.
 * Accurate player weapons instead of the current placeholder system.
 * Accurate INF system, this means that not only will the core levels function correctly but so will mods (except in cases where they rely on AI logic).
 
And obviously this list barely touches the behind the scenes updates since the last Test Release. As you can see this huge release sets the foundation - with the rest Logic/AI following relatively soon afterward (but definitely a future release).
