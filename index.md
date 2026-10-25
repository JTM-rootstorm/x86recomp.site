---
title: x86recomp
---

# x86recomp

<p class="lede">Static recompilation of x86 Windows games into native
64-bit programs for Linux and macOS: the scaffold that gets a game running
natively while its code is replaced, piece by piece, with hand-written
C++.</p>

A game's machine code is translated ahead of time into C++ and linked
against a runtime that reimplements the parts of Windows and its
middleware the game uses. There is no emulator, interpreter or Wine in
the result, and no game code or data in any of the repositories: each
port builds from your own copy of the game.

## Projects

<div class="cards">
{%- assign projects = site.projects | sort: "order" -%}
{%- for p in projects %}
  <a class="card" href="{{ p.url | relative_url }}">
    <h3>{{ p.title }}</h3>
    <p class="game">{{ p.game }} ({{ p.year }})</p>
    <span class="badge badge-{{ p.stage }}">{{ p.status }}</span>
    <p class="summary">{{ p.summary }}</p>
  </a>
{%- endfor %}
</div>

<div class="table-scroll">
<table>
  <thead><tr><th>Port</th><th>Game</th><th>Status</th><th>Platforms</th><th>Updated</th></tr></thead>
  <tbody>
  {%- for p in projects %}
    <tr>
      <td><a href="{{ p.url | relative_url }}">{{ p.title }}</a></td>
      <td>{{ p.game }} ({{ p.year }}{% if p.arch %}, {{ p.arch }}{% endif %})</td>
      <td><span class="badge badge-{{ p.stage }}">{{ p.status }}</span></td>
      <td>{{ p.platforms }}</td>
      <td>{{ p.updated | date: "%Y-%m-%d" }}</td>
    </tr>
  {%- endfor %}
  </tbody>
</table>
</div>

## What x86recomp provides

- **Lifter** (`recomp_lift`): decodes a PE with Zydis and emits C++ for
  every function, one basic block at a time, with exact x86 integer and
  flag semantics. 32-bit images are the main target; x64 images (with
  AVX) lift too, for Quake II Enhanced.
- **x87 and SSE models**: exact 80-bit x87 (precision and rounding
  control, status-word flags) and the XMM registers with MXCSR, on
  Berkeley SoftFloat, tested bit for bit against the real CPU.
- **Runtime**: the guest address space, PE loading, threads, SEH, crash
  and hang reports.
- **HLE**: Win32 on POSIX and SDL3, plus Miles Sound System (with EAX 1-3
  on its own reverb), Bink, DirectDraw 7/Direct3D 7, OpenGL 1.x,
  Direct3D 9 and D3DX 9, DirectSound 8, DirectInput 8 and XInput.
  Graphics run on SDL_GPU: Vulkan on Linux, native Metal on macOS.
- **Shader translators**: D3DX 9's HLSL dialect and compiled Direct3D 9
  shaders (models 1-3) to GLSL.

The lifted code is an exact oracle, not the end product: each port
replaces lifted functions with native C++ one subsystem at a time,
checked against the lifted original, until nothing lifted is left.

The [repository]({{ site.repo }}) has the build instructions and
[ARCHITECTURE.md]({{ site.repo }}/blob/main/ARCHITECTURE.md), the
design.
