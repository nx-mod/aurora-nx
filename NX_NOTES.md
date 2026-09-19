# aurora-nx

Aurora with a Nintendo Switch backend, for [wii-nx](https://github.com/nx-mod/wii-nx).

Aurora is a source-level GameCube/Wii compatibility layer: it implements the console SDK (GX graphics,
pads, VI) on top of modern APIs, and renders through WebGPU. On Switch that means
[dawn-nx](https://github.com/nx-mod/dawn-nx) over [nxvk](https://github.com/nx-mod/nxvk).

## Status

Bring-up work currently lives in the vendored copy inside
[wiicompiled-nx](https://github.com/nx-mod/wiicompiled-nx) (`aurora-main/`), not here yet:

- Switch replacements for the SDL-based window and input layers
- ImGui without a renderer (the overlay is built each frame and dropped)
- Shader-cache database fixes for a platform with no working directory
- Dawn cache API updates

## Plan

1. Move that Switch backend here: window, input, audio output, thread and core placement, paths,
   shader cache.
2. Decide the base. Upstream has moved on since WiiCompiled vendored Aurora, and WiiCompiled's copy
   changes 110 files (+14.4k/-5.9k). Each change is either already covered upstream (drop), generally
   useful (offer upstream), or specific to one game (keep out of here).
3. Aim for: **upstream Aurora + the Switch backend, nothing else**, so any Aurora-based port gains Switch
   support.

Notes and the wider roadmap: [wii-nx/PLAN.md](https://github.com/nx-mod/wii-nx/blob/main/PLAN.md).
