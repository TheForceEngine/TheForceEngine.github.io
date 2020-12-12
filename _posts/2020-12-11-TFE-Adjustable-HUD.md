---
layout: post
title: Adjustable HUD
---

Last post I talked about the remaining work for the Classic Renderer and the next steps. In the meantime, based on feedback regarding widescreen, it came to light that just moving the status HUD elements to the edges of the screen in widescreen may not be ideal - especially for ultrawide resolutions. So I decided to implement some basic HUD options, including the ability to move the HUD elements away from the edges. This, of course, appears unnatural since the grapics were designed to sit at the edges of the screen. "Dzierzan" - a member of the discord server - quickly made some art to fix these cutoff edges so I spent a little bit of time to implement an adjustable HUD.

# Adjustable HUD
I added a new tab to the System UI Settings dialog in order to adjust the HUD. Like the Graphics tab, as you adjust the HUD settings, you will see the in-game HUD respond immediately, allowing you to easily tweak to taste.

![HUD UI](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/HUD_Settings_Final3.png?raw=true)
![HUD UI 2](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/HUD_Settings_Final1.png?raw=true)

## Hud Scale Type
The HUD scale type determines how the HUD scales with resolution.

### Proportional
The HUD is scaled to stay the same size as the original game in screenspace regardless of the resolution. This is the default option and will look the most like the original game.

### Scaled
With the scaled option, the HUD gets smaller with higher resolutions. Using this option, you can then use the Scale slider to adjust the size of the HUD. Note that changing resolution will change the apparent size on screen.

## Hud Position Type
This determines how the HUD is position by default. In either case further adjustments are possible by modifying the OffsetX and OffsetY sliders.

### Edge
The Status elements of the HUD are always aligned to the edges of the screen. This is the way the original art was designed.

### 4:3
In this mode, the HUD will stay in its original 4:3 positions even if in widescreen. With this mode it is easier to see the full HUD at once.

![HUD UI 3](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/HUD_Settings_Final2.png?raw=true)
![HUD UI 3](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/HUD_Settings_Final4.png?raw=true)
![HUD UI 3](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/HUD_Settings_Final5.png?raw=true)

# The Final Results
In this screenshot you can see the 4:3 HUD in action in widescreen.

![HUD Results](https://github.com/TheForceEngine/TheForceEngine.github.io/blob/master/screenshots/AdjustableHUD.png?raw=true)

# Next Steps
The next steps haven't changed from the last post, though some progress has been made integrating the 3D object rendering code into The Force Engine.
