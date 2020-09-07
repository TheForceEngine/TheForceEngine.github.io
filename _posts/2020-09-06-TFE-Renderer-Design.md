---
layout: post
title: TFE Renderer Design
---

It has been awhile since the last update but some of that has been cleaning up the design of the overall renderer structure. There is are two forces at play, pulling in separate directions - a desire to preserve the original DOS renderer with all of its quirks and a desire to clean up artifacts, especially at higher resolutions, and provide a robust, forward thinking renderer. In either case the renderer needs to be faithful to the original and existing Mods and levels need to work as is (which means rendering correctly as well).

Fortunately the needed reverse-engineering for the renderer is complete, this issue now is to support all of the required features while preserving the original renderer while making sure the result is clean and maintainable. This means this release is taking longer than planned but, as the bedrock of the entire project, it needs to be done well.

## Design
The TFE Dark Forces renderer consists of the following matrix of combinations:

|              | __Classic__                                                                                              | __Perspective__                                                                                           |
|--------------|----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| __Software__ | Fixed point DOS 320x200 software renderer. 8-bit only.                                                   | Floating point software renderer. 8-bit or true color.                                                    |
|              | Floating point software renderer. 8-bit or true color.                                                   |                                                                                                           |
| __Hardware__ | Floating point hardware renderer - OpenGL 3.3 with future support for Vulkan/Metal. 8-bit or true color. | Floating point hardware renderer - OpenGL 3.3 with future suppport for Vulkan/Metal. 8-bit or true color. |
|              | Floating point hardware renderer - Compute. 8-bit or true color.                                         | Floating point hardware renderer - Compute. 8-bit or true color.                                          |

The “Classic Renderer Release” focuses on the “Classic” column. The “Fixed-point DOS” renderer is the reverse-engineered DOS renderer. Rather than trying to have a hybrid renderer using higher precision fixed point – an approach taken until recently which is not compatible with GPU rendering - the higher precision software renderer instead uses floating point except for inner column/scanline loops. This means that much of the code can be shared between the CPU and GPU renderers with the inner loops being swapped out.

The Compute based renderer, which moves the majority of the renderer to the GPU – including visibility and all transformations – promises to greatly improve the performance of highly detailed custom levels and greatly reduced the data being transferred from the CPU to GPU. It also opens new possibilities such as raytracing effects without requiring RTX hardware. However, this is a non-trivial endeavor and WILL NOT happen until after the gameplay is complete. So, it is included for completeness and future planning only.

The perspective renderers will also be work for a future, post-gameplay release. It is here for future planning.

Note that 8-bit versus true color does not add an extra combination, each sub-renderer has support for either.

## TFE_RenderBackend
The Render Backend is responsible for abstracting the low level rendering API and providing the renderers with an API to manipulate GPU buffers, shaders, GPU textures, render targets and virtual displays, render state, and low level GPU draw and compute commands.

## TFE_PostProcess
The Post Processing system handles blitting virtual displays and render targets to the window, color correction, and post process shaders such as Bloom. Note that the post processing stack is independent of the renderer, this means that color correction and post processing shaders can be applied just as well to CPU based renderers if the minimum GPU requirements are met. This also means that the post processing system can be used to convert from 8-bit to true color using the GPU, which can save CPU time and CPU to GPU bandwidth on supported hardware.

Note that if no usable hardware (GPU) support is available, such as on some low-end Intel iGPUs, then GDI (or equivalent technologies) will be used instead to blit the virtual frame buffer to the window. This will allow The Force Engine to be usable even when lacking GPU support – but Editor support will be disabled, and the menu system may be more limited. This feature may not make it in for the “Classic Renderer Release” but is planned before the “1.0” release.

## TFE_JediRenderer
The TFE “Jedi” derived renderer, which consists of several sub-renderers based on feature sets and hardware being used. The goal of the entire family of “Classic” renderers is to faithfully reproduce the original renderer and algorithms with minimal changes that might disrupt Mods or prevent correct rendering of existing levels. Any changes of this nature, even if they are a good idea, should be optional in order to provide the most faithful experience possible by default.

### TFE_JediRenderer
High level functionality used by various sub-renderers. This includes fixed point   functionality and other higher-level constructs. Shared functionality between RClassic_Float and RClassic_GPU will also find itself here.

### RClassic_DOS
The reverse-engineered DOS renderer only works properly at 320x200. This renderer is always 8-bit and provides minimal changes to preserve the original. However, if a similar look is desired, even in 8-bit, but without the artifacts the Classic Float renderer can be used instead. Originally, I partially implemented a fixed-point renderer with improved precision to avoid code duplication but realized I needed the floating-point renderer anyway for GPU support – I was overcomplicating the issue.

### RClassic_Float
The Classic_Float renderer uses the original algorithms but uses floating point instead of fixed point and fixes artifacts that can be done in a non-destructive way (i.e. a way that does not interfere with existing mods or tricky effects). This means that a lot of the code can be shared between the floating point and GPU renderers – this code will be pulled into Common. Classic_Float can use 8-bit or true color rendering by using the color map to inform color interpolation.

### RClassic_GPU
The Classic_GPU renderer is similar to the Classic_Float renderer but moves low level rendering to the GPU (such as wall and floor rasterization). It uses the same algorithms as the Classic_Float renderer, including sorting and 1D depth buffer for object versus wall visibility.  The goal is to share as much as possible between the software and GPU renderers – but only when that sharing does not greatly increase complexity or make maintenance more difficult. Classic_GPU can render in 8-bit color or true color by using the same color map interpolation technique as the software true color renderer. Note OpenGL 3.3, or equivalent in the case of Metal or Vulkan, will be required.

### RClassic_Compute (Post-Gameplay Addition)
The goal of Classic_Compute is to implement most or all of the Classic_Float renderer entirely using the GPU with very little communication to the CPU – mainly viewpoint data and changes to sectors or objects. The goal is to improve scalability of the portal-based renderer and better utilize modern GPUs. Note that Compute Shader support will be required, probably requiring OpenGL 4.5 or 4.6 or equivalent in the case of Metal or Vulkan.
