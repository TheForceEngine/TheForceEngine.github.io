---
layout: post
title: DF Classic Renderer Progress 2
---

Its about time to post another update regarding the progress towards the Classic Renderer Release.
`RE = fully reverse-engineered and ported to the engine.`

## Task List
The following task list are the items required for the release. The biggest remaining items are Object/Sector assignment and RE Object 3D rendering. Once those are complete the remaining tasks will be completed quickly. The release is still on track for this month. Also note that the reverse engineering efforts touch many systems in the DOS exe, so this work is also laying the foundation for the rest of the reverse-engineering effort, accelerating this project towards release.

- [x] RE Lighting.
- [x] RE Wall clipping/sorting.
- [x] RE Wall Rendering.
- [x] RE Sign Rendering.
- [x] RE Sky Rendering.
- [x] RE Flat (floor/ceiling) Rendering.
- [x] RE Sector Rendering.
- [x] RE Adjoin/portal traversal.
- [x] RE Sprite Rendering.
- [x] RE Sprite/3D Object/Wall sorting.
- [x] RE Level Geometry loading.
- [x] RE Object Asset loading.
- [x] RE Sector updates.
- [ ] RE Object/sector assignment.
- [ ] RE Object3D rendering.
- [ ] Classic Renderer Verification (i.e. go through levels and verify visual correctness).
- [x] Updated graphics settings UI.
- [x] Graphics settings can be changed on the fly instantly updating the 3D view.
- [ ] Hardware Rendering (partial).
- [ ] Fully replace current Test Release renderer with Classic Renderer / Refactor.
- [ ] Color correction.
- [ ] Post FX (Bloom).
- [x] Basic controller support.

## Next Steps
Once this release is finished, the next non-bugfix release will be input/control binding - which will include being able to bind controls to the keyboard, mouse and controller but also things like mouse and thumbstick sensivity.

After that future releases will start fleshing out the gameplay - player movement and collision, weapons, logics/AI and remaining INF issues until the core gameplay is complete.
