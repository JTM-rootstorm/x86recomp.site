---
title: LSWTCS_Rebricked
short: LEGO Star Wars
game: "LEGO Star Wars: The Complete Saga"
year: 2009
theme: lswtcs
fonts: "family=Fredoka:wght@400;600;700"
order: 3
stage: ingame
status: In game
summary: Menus, the cantina and several levels load and play, with every shader translated and an Xbox pad working. The first Direct3D 9 user.
platforms: Linux x86-64; macOS on Apple Silicon
release: Steam (app 32440)
repo: https://github.com/JTM-rootstorm/LSWTCS_Rebricked
updated: 2026-10-19
---

A native port of LEGO Star Wars: The Complete Saga, and the game that
brought Direct3D 9, D3DX 9 and the HLSL translator into x86recomp: its
renderer generates HLSL at run time. Goals beyond running natively:
widescreen at any resolution and aspect ratio, and an uncapped frame
rate as an option.

## Status

The Steam EXE unpacks statically (SteamStub 2.1), is lifted, and runs
natively. Working:

- the attract loop, the menus, and New Game into the Mos Eisley cantina;
- with the `LSWTCS_LEVEL` test hook, New Game starts any level directly:
  Negotiations, the pod race, the Episode III space battle, Tatooine and
  the Hoth snowspeeders load and play (walking, jumping, lightsaber, the
  Force, blasters) with no fatal error;
- every shader translated, both the run-time HLSL and the precompiled
  ones;
- keyboard through DirectInput and an Xbox pad through XInput;
- Bink movies and DirectSound.

Negotiations plays through to its end tally.

## Next

1. Pipeline compile stalls when a level first meets a material.
2. Play on past the Negotiations tally: the minikit build, the status
   screen, back to the cantina, saving and loading, the next chapters.
3. More shaders as levels reach more materials.
4. The enhancements: arbitrary aspect ratios, an uncapped frame rate,
   the resolution list.

The project's [FINDINGS.md]({{ page.repo }}/blob/main/FINDINGS.md)
tracks progress and [ARCHITECTURE.md]({{ page.repo }}/blob/main/ARCHITECTURE.md)
the plan.
