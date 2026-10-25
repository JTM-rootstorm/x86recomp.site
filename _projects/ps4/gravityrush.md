---
title: GravityRush
short: Gravity Rush Remastered
game: Gravity Rush Remastered
year: 2015
arch: x64
theme: gravityrush
fonts: "family=Marcellus&family=Alegreya+Sans:ital,wght@0,400;0,700;1,400"
order: 1
stage: boots
status: Boots
summary: The first PS4 port, on the Orbis module. Lifts and builds; runs through libc and Fios2 into the game's own startup.
platforms: Linux x86-64 and macOS (planned)
release: CUSA01130, version 01.00 (decrypted dump of your own copy)
updated: 2026-10-24
---

The first game on x86recomp's PS4 platform module, Orbis, and the test
case it is being built against.

## Status

- The executable plus its bundled `libc` and `libSceFios2` lift (40,881
  functions, 3.75M instructions) with nothing unimplemented, and build
  into one native program.
- It runs through libc's and Fios2's initialisers and the game's
  `_start` into its own startup: the game maps 4.3 GiB of its 5 GiB
  direct-memory pool, starts a worker thread, reads `/app0/args.txt`
  through Fios2 and the system language, and turns off screenshots.
- It stops at `sceVideoOutOpen`.

## Next

The display and the GPU: VideoOut, then GnmDriver's command buffers onto
x86recomp's graphics device.

The repository is not public yet.
