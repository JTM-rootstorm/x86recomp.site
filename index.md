---
title: x86recomp
---

# x86recomp

<p class="lede">Static recompilation of games into native 64-bit programs
for Linux and macOS (x86 and x86-64 PC games on main; PowerPC and
AArch64 consoles on their own branches): the scaffold that gets a game running
natively while its code is replaced, piece by piece, with hand-written
C++.</p>

A game's machine code is translated ahead of time into C++ and linked
against a runtime that reimplements the parts of its operating system
and middleware the game uses. There is no emulator, interpreter or Wine
in the result, and no game code or data in any of the repositories: each
port builds from your own copy of the game.

## Systems

{% assign systems = site.systems | sort: "order" -%}
<div class="cards">
{%- for s in systems %}
  {%- assign ports = site.projects | where: "system", s.slug %}
  <a class="card" href="{{ s.url | relative_url }}">
    <h3>{{ s.full }}</h3>
    <p class="game">{{ s.cpu }}</p>
    <span class="badge badge-system">{{ s.state }}</span>{% if s.branch %} <span class="branch">on branch <code>{{ s.branch }}</code></span>{% endif %}
    <p class="summary">{{ s.summary }}</p>
    <p class="summary count">{% if ports.size == 0 %}No ports yet{% elsif ports.size == 1 %}1 port{% else %}{{ ports.size }} ports{% endif %}</p>
  </a>
{%- endfor %}
</div>

## All ports

<div class="table-scroll">
<table>
  <thead><tr><th>Port</th><th>Game</th><th>Status</th><th>Platforms</th><th>Updated</th></tr></thead>
  {%- for s in systems %}
  {%- assign ports = site.projects | where: "system", s.slug | sort: "order" %}
  {%- if ports.size > 0 %}
  <tbody>
    <tr class="group"><th colspan="5"><a href="{{ s.url | relative_url }}">{{ s.full }}</a></th></tr>
    {%- for p in ports %}
    <tr>
      <td><a href="{{ p.url | relative_url }}">{{ p.title }}</a></td>
      <td>{{ p.game }} ({{ p.year }}{% if p.arch %}, {{ p.arch }}{% endif %})</td>
      <td><span class="badge badge-{{ p.stage }}">{{ p.status }}</span></td>
      <td>{{ p.platforms }}</td>
      <td>{% if p.repo %}{% include updated.html repo=p.repo %}{% else %}{% include updated.html repo=site.repo branch=s.branch %}{% endif %}</td>
    </tr>
    {%- endfor %}
  </tbody>
  {%- endif %}
  {%- endfor %}
</table>
</div>

## What x86recomp provides

- **Lifter** (`recomp_lift`): emits C++ for every function of a game's
  executables, one basic block at a time, with exact integer and flag
  semantics.
  - **x86** (32-bit PE): integer, x87 and SSE/SSE2.
  - **x86-64**: PE32+ images on the Win64 ABI, and through platform
    modules other formats on System V; AVX and the SSE3-4 extensions,
    against a fixed CPU model (AMD family 16h) that grows only as the
    lifter implements each feature bit-exactly.
  - **AArch64** (on the `horizon` branch): a second core with its own
    lifter (`recomp_lift_a64`) and CPU model, for the Switch.
  - **PowerPC** (on the `x360` branch): a core for 64-bit PowerPC in
    32-bit mode (`recomp_lift_ppc`), with exact floating point and VMX,
    for the Xbox 360.
- **CPU models**: exact 80-bit x87 (precision and rounding control,
  status-word flags) and the XMM/YMM registers with MXCSR, on Berkeley
  SoftFloat, tested bit for bit against the real CPU (or, for console
  CPUs, an oracle: Unicorn for AArch64, QEMU for PowerPC).
- **Runtime**: the guest address space, image loading, threads,
  exceptions (SEH and x64 unwinding), crash and hang reports.
- **Windows HLE**: Win32 on POSIX and SDL3, the UCRT and MSVCP140, Miles
  Sound System (with EAX 1-3 on its own reverb), Bink, DirectDraw/Direct3D
  7, OpenGL 1.x, Direct3D 9 and D3DX 9, DirectSound 8, DirectInput 8 and
  XInput. Graphics run on SDL_GPU: Vulkan on Linux, native Metal on macOS.
- **Shader translators**: D3DX 9's HLSL dialect and compiled Direct3D 9
  shaders (models 1-3) to GLSL.
- **Platform modules** (in progress): consoles plug into the shared
  core and host layer instead of forking them, each on its own branch
  until it is merged: Orbis for the
  [PlayStation 4]({{ '/ps4/' | relative_url }}) on
  [`ps4`]({{ site.repo }}/tree/ps4), and Horizon for the
  [Switch]({{ '/switch/' | relative_url }}) on
  [`horizon`]({{ site.repo }}/tree/horizon), and the Xbox 360 module
  for the [Xbox 360]({{ '/x360/' | relative_url }}) on
  [`x360`]({{ site.repo }}/tree/x360).

The lifted code is an exact oracle, not the end product: each port
replaces lifted functions with native C++ one subsystem at a time,
checked against the lifted original, until nothing lifted is left.

The [repository]({{ site.repo }}) has the build instructions and
[ARCHITECTURE.md]({{ site.repo }}/blob/main/ARCHITECTURE.md), the
design.
