---
title: PlayStation 4
full: PlayStation 4
order: 2
cpu: x86-64 (AMD Jaguar, family 16h)
base: x86recomp Orbis platform module
state: Module in progress
summary: The first console module on x86recomp's core. The PS4's CPU is x86-64, so it reuses the x64 lifter and adds a platform (executable format, system libraries, GPU).
---

The PS4 runs x86-64 code on an AMD Jaguar CPU, which x86recomp's x64
lifter already models. What a PS4 game needs on top of it is a
**platform module**, Orbis, that plugs into the shared core instead of
forking it: PC builds never compile or link it.

The module is in progress on its own branch of x86recomp (not public
yet):

- **Image reader**: decrypted SELF/ELF executables with SCE dynamic
  tables, function starts from `.eh_frame`, imports by NID.
- **Process loader**: maps the executable and its bundled PRX modules,
  links them, and runs their initialisers.
- **HLE by NID**: libkernel, system services and libSceLibcInternal so
  far, on the core's System V x64 ABI (also used for TLS through `fs`).
- **Next**: VideoOut and the GPU path (GnmDriver's command buffers onto
  x86recomp's graphics device).

Core lifter work it brought: CMPXCHG16B, FXSAVE/FXRSTOR, 256-bit
conversions, `jrcxz`, locked `xchg`.

Games come from your own console: a decrypted dump of a copy you own.
