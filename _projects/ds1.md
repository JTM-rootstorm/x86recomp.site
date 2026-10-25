---
title: DS1-Rebuilt
short: Dungeon Siege
game: Dungeon Siege
year: 2002
order: 1
stage: playable
status: Playable
summary: Single player plays from a new game to Wesrin Cross, with sound, music, voices and movies. Where x86recomp was developed.
platforms: Linux x86-64; macOS on Apple Silicon (in progress)
release: GOG, version 1.11.1
repo: https://github.com/JTM-rootstorm/DS1-Rebuilt
updated: 2026-10-14
---

The project x86recomp grew out of: the lifter, x87 model, runtime and
HLE were written for Dungeon Siege and factored out into the shared
library on 2026-10-12.

## Status

Single player is playable from a new game to Wesrin Cross (about an
hour of hand-played testing). Verified in play:

- menus, hero creation, the intro cinematic, Options and Exit;
- movement and combat, with the frame rate holding with a party at the
  krug camp;
- inventory, journal, map, spells, potions, hotkeys, skill level-ups;
- NPC conversations with voice, multi-stage quests, shops and the pack
  mule, party members, death and resurrection;
- region and basement transitions through Stonebridge to Wesrin Cross,
  and the first crypt;
- saving and loading;
- Miles audio (with EAX) and Bink movies.

Debug and release builds hold the game's own 60 fps cap in game.

Not yet seen: regions past Wesrin Cross, the ending.

### macOS

Builds and runs on Apple Silicon with SDL_GPU on native Metal. Scripted
runs reach the farm in game (terrain, animated water, fog, the HUD, the
pause menu) with sound and voices; not yet played by hand or compared
frame by frame against the reference backend.

## Native replacements

- **Widescreen**: the game's window and display mode follow the host
  desktop instead of a fixed 1024x768.
- **Software cursor on the GPU**: the cursor is blended on the GPU with
  an asynchronous readback, which took a 5K display from ~50 to a steady
  60 fps with the window focused.

## Known gaps

- The GDI "Lucida Console" font texture is blank (dev console and debug
  text).
- IME functions are not provided.
- The game's own resolution list stops at 1024x768.

The project's [FINDINGS.md]({{ page.repo }}/blob/main/FINDINGS.md)
tracks what works, what was fixed and what is known to be missing.
