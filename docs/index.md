# Antikira Lua API

Antikira now ships with a built-in `LuaJIT` runtime, `ffi` support, script management in the menu, and a documented in-process API for callbacks, rendering, entity access, user commands, game events, and config values.

This documentation is organized as a dedicated Antikira reference site for writing, testing, and maintaining Lua scripts against the current project runtime.

<div class="ak-hero">
  <div class="ak-hero__badge">LuaJIT + FFI + In-Game Script Manager</div>
  <h2>Built for the runtime that ships in this repository</h2>
  <p>Use these pages as the ground truth for callbacks, modules, objects, config access, render functions, and script lifecycle behavior.</p>
</div>

## What Is Available

- `LuaJIT` runtime
- `ffi` support
- callback registration
- drawing API
- entity and event access
- `create_move` command access
- config value read/write access
- script environment helpers

## Fast Paths

<div class="ak-grid">
  <a class="ak-card" href="lua/getting-started/">
    <strong>Getting Started</strong>
    <span>Load your first script, understand the folder layout, and verify the runtime quickly.</span>
  </a>
  <a class="ak-card" href="lua/callbacks/">
    <strong>Callbacks</strong>
    <span>See exactly when <code>draw</code>, <code>create_move</code>, <code>event</code>, and <code>shutdown</code> run.</span>
  </a>
  <a class="ak-card" href="lua/modules/render/">
    <strong>Render API</strong>
    <span>Text, lines, rectangles, circles, and world-to-screen helpers for overlay work.</span>
  </a>
  <a class="ak-card" href="lua/modules/config/">
    <strong>Config Access</strong>
    <span>Read and write the same values that drive the menu and gameplay features.</span>
  </a>
</div>

## Quick Links

- [Getting Started](lua/getting-started.md)
- [Runtime](lua/runtime.md)
- [Callbacks](lua/callbacks.md)
- [API Overview](lua/api.md)
- [FFI Notes](lua/ffi.md)

## Main Modules

- [`antikira`](lua/modules/antikira.md)
- [`globals`](lua/modules/globals.md)
- [`engine`](lua/modules/engine.md)
- [`entitylist`](lua/modules/entitylist.md)
- [`render`](lua/modules/render.md)
- [`menu`](lua/modules/menu.md)
- [`environment`](lua/modules/environment.md)
- [`config`](lua/modules/config.md)
- [`buttons`](lua/modules/buttons.md)

## Objects

- [`entity`](lua/objects/entity.md)
- [`cmd`](lua/objects/cmd.md)
- [`event`](lua/objects/event.md)

## Notes

- The docs describe what is exposed by this repository right now, not a theoretical future API.
- Menu widgets are not directly scripted yet, but Lua can already read and change the underlying config values through [`config`](lua/modules/config.md).
