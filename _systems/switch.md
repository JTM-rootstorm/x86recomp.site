---
title: Switch
full: Nintendo Switch
order: 3
cpu: AArch64 (ARM Cortex-A57)
base: nxrecomp, x86recomp's AArch64 sibling
state: Groundwork
summary: AArch64 needs its own lifter base, nxrecomp, built to the same shape and rules. No ports yet.
---

The Switch's CPU is AArch64, so it gets its own lifter and CPU model,
**nxrecomp**: a sibling of x86recomp with the same shape and the same
rules (no emulator, interpreter or JIT; exact CPU semantics; no game
code or data in the repository). The platform side (nnSdk, NVN, the
system services) plugs into the same interfaces as the PS4 module.

Status: milestone 1. The lifter and an integer-only runtime lift and run
a homebrew NRO fixture, checked against Unicorn, and the tests run on an
arm64 host too. Next: the FP/SIMD model (exact AArch64 floating point and
NEON on SoftFloat's ARM specialisation). Not public yet.
