---
title: CoD1-Reissued
short: Call of Duty
game: Call of Duty
year: 2003
order: 2
stage: ingame
status: In game
summary: The training level plays through to completion. Widescreen, Hor+ FOV, a scaled HUD and exact frame caps are in; hot engine code is going native.
platforms: Linux x86-64; macOS on Apple Silicon (in progress)
release: Steam (app 2620), v1.5b, single player
repo: https://github.com/JTM-rootstorm/CoD1-Reissued
updated: 2026-10-19
---

A native port of Call of Duty's single player. Goals beyond running
natively: widescreen at any resolution with a UI and HUD that scale
properly, Hor+ field of view, and high refresh rates without the Quake 3
engine family's frame-rate-dependent physics.

## Status

The game's five modules (`CoDSP.exe`, `gamex86.dll`, `cgamex86.dll`,
`uix86.dll` and `EaxMan.dll`) are lifted and linked into one native
program. It boots through the intro cinematics to the main menu with its
music, starts a new game through the briefing, and the training level
plays through to completion (played by hand). EAX 3 works through the
game's own EAX Manager on x86recomp's providers.

### macOS

Builds and starts on Apple Silicon with SDL_GPU on Metal; scripted runs
play the intro and reach the training level. Not yet played by hand or
compared against the reference backend.

## Native replacements

Each replaces lifted functions and is checked bit for bit against the
lifted original by the project's tests.

- **Widescreen and frame rate**: any resolution, borderless or exclusive
  fullscreen, Hor+ FOV (`cg_fov` is the 4:3 horizontal FOV), and an
  exact `com_maxfps` that sleeps instead of spinning.
- **HUD on wide screens**: elements anchored to the edges keep their
  shapes; menus, briefings and cinematics stay 4:3.
- **Player movement**: footsteps at any step length, `pmove_fixed`
  without rounding.
- **Collision traces**, once about 45% of the main thread in training.
- **Renderer hot path**: culling, sky clipping, texture coordinate
  generation and the draw surface sort; lifted renderer code on the main
  thread went from 12.9% to 4.5%.
- **XAnim** evaluation and updates.
- **Files**: the pk3 directory scan, zlib and the JPEG inverse DCT on
  the host.
- CPU skinning and a cinematic fix.

## Next

A renderer that drives x86recomp's graphics device directly, building
on the native hot path above.

The project's [FINDINGS.md]({{ page.repo }}/blob/main/FINDINGS.md)
tracks progress and [ARCHITECTURE.md]({{ page.repo }}/blob/main/ARCHITECTURE.md)
the plan.
