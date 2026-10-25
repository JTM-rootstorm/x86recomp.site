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
summary: Menus, the cantina and several levels load and play, with keyboard and Xbox pad. Hitches on new effects; past the first chapter untested. The first Direct3D 9 user.
platforms: Linux x86-64; macOS on Apple Silicon (not built yet)
release: Steam (app 32440)
repo: https://github.com/JTM-rootstorm/LSWTCS_Rebricked
updated: 2026-10-25
---

A native port of LEGO Star Wars: The Complete Saga, and the game that
brought Direct3D 9, D3DX 9 and the HLSL translator into x86recomp: its
renderer generates HLSL at run time. Goals beyond running natively:
widescreen at any resolution and aspect ratio, and an uncapped frame
rate as an option.

## Status

The Steam EXE unpacks statically (SteamStub 2.1), is lifted, and runs
natively on Linux. Verified:

- the legal screens, the attract movie (Bink) and the title screen;
- the menus, and New Game into the Mos Eisley cantina;
- Negotiations played by hand from the cantina through its chapter and
  cutscenes to the end tally;
- with the `LSWTCS_LEVEL` test hook, which makes New Game start any
  level, the pod race, the Episode III space battle, Tatooine and the
  Hoth snowspeeders load and play (walking, jumping, lightsaber, the
  Force, blasters) with no fatal error;
- every shader met so far translates, both the run-time HLSL and the
  precompiled ones;
- keyboard through DirectInput and an Xbox Series X pad through XInput.

Not yet seen: the minikit build and status screen after a tally,
returning to the cantina, saving and loading, chapters past
Negotiations, the ending.

## Known issues

- **Hitches on new effects.** The first time a level meets a new
  material or effect (entering a level, the first minikit) the game
  stalls while its graphics pipelines are built: 60-90 ms each, up to
  about a second at a time. They are not cached between runs.
- **The Negotiations tally crashed** just after "True Jedi" on an
  indirect jump the lifter had not recovered. The lifter now recovers
  it, but the tally has not been replayed since.
- Two C runtime jump tables are still dispatched dynamically; neither
  has been reached.
- In-level sound and music have not been checked by ear.
- macOS has not been built.

## Next

1. Fix the pipeline stalls: build pipelines off the render thread, or
   cache and replay them at startup.
2. Play on past the Negotiations tally: the minikit build, the status
   screen, back to the cantina, saving and loading, the next chapters.
3. More shaders as levels reach more materials.
4. The enhancements: arbitrary aspect ratios, an uncapped frame rate,
   the resolution list.

The project's [FINDINGS.md]({{ page.repo }}/blob/main/FINDINGS.md)
tracks progress and [ARCHITECTURE.md]({{ page.repo }}/blob/main/ARCHITECTURE.md)
the plan.
