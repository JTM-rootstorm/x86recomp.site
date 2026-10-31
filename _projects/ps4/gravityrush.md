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
summary: The first PS4 port, on the Orbis module. Runs into the title flow and the attract movie with its frame loop at 60 Hz; no picture until the GPU front end.
platforms: Linux x86-64 and macOS (planned)
release: CUSA01130, version 01.00 (decrypted dump of your own copy)
---

The first game on x86recomp's PS4 platform module, Orbis, and the test
case it is being built against. It tracks the module's `ps4` branch.

## Status

- The executable plus its bundled `libc` and `libSceFios2` lift (40,881
  functions, 3.75M instructions) with nothing unimplemented, and build
  into one native program.
- Start-up runs through libc and Fios2 into the game's own: 4.3 GiB of
  direct memory, job threads and fibers, PlayGo and disc-map reads,
  VideoOut (three 1080p display buffers, flips at 60 Hz), the sound
  engine's NGS2 set-up, PSN (signed out), networking, save data, fonts,
  the pad and trophies.
- It reaches the title flow ("EULA OK", the save data check) and plays
  the attract movie through AvPlayer, running its frame loop: GPU
  submissions with draws and compute dispatches, flips at 60 Hz, audio
  out.
- No picture yet: the GPU's command buffers are processed but nothing
  draws them. NGS2 is answered by a probe that renders silence.

## Next

- The NGS2 sound engine HLE.
- The GPU front end on x86recomp's graphics device: draws, GCN shaders,
  tiled surfaces.
- libSceFont's FreeType glue, matched exactly.

The repository is not public yet.
