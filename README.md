# aurora-nx

[Aurora](docs/AURORA_README.md) with a Nintendo Switch backend, for
[wii-nx](https://github.com/nx-mod/wii-nx).

Aurora is a source-level GameCube/Wii compatibility layer: it implements the console SDK - GX graphics,
pads, VI - on top of modern APIs and renders through WebGPU. On Switch that path ends at
[dawn-nx](https://github.com/nx-mod/dawn-nx) over [nxvk](https://github.com/nx-mod/nxvk), Mesa's NVK
driver on the Tegra X1.

Upstream Aurora's own README, features and build instructions are
[docs/AURORA_README.md](docs/AURORA_README.md).

## Status

The Switch bring-up currently lives in the copy vendored inside
[wiicompiled-nx](https://github.com/nx-mod/wiicompiled-nx) (`aurora-main/`), not here yet:

- Switch replacements for the SDL-based window and input layers
- ImGui without a renderer (the overlay is built each frame and dropped)
- Shader-cache fixes for a platform with no working directory, on
  [sqlite-nx](https://github.com/nx-mod/sqlite-nx)
- Dawn cache API updates

It runs: Mario Kart Wii boots, renders and saves on hardware through this path.

## Plan

1. Move that backend here - window, input, audio output, thread and core placement, paths, shader cache.
2. Decide the base. Upstream has moved on since WiiCompiled vendored Aurora, and that copy changes 110
   files (+14.4k/-5.9k). Each change is either already upstream (drop), generally useful (offer
   upstream), or specific to one game (keep out of here).
3. Aim for **upstream Aurora plus a Switch backend, nothing else**, so any Aurora-based port gains
   Switch support by pointing at this.

## Building

As upstream, with the devkitPro toolchain and nxvk installed as a portlib:

```sh
cmake -S . -B build -G Ninja -DCMAKE_TOOLCHAIN_FILE=$DEVKITPRO/cmake/Switch.cmake
cmake --build build
```

In practice it is composed by [wii-nx](https://github.com/nx-mod/wii-nx), which builds the libraries,
the engine and a game together.

## License

As upstream Aurora; see [LICENSE](LICENSE). No game code or assets here.
