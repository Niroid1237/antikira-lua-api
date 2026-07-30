<div class="ak-hero">
  <div class="ak-hero__badge">LuaJIT + FFI + In-Game Script Manager</div>
  <h2>Built for the runtime that ships in this repository</h2>
  <p>Use these pages as the ground truth for callbacks, modules, objects, config access, render functions, and script lifecycle behavior.</p>
  <div class="ak-badges">
    <span class="ak-badge ak-badge--blue">LuaJIT Runtime</span>
    <span class="ak-badge ak-badge--green">FFI Support</span>
    <span class="ak-badge ak-badge--purple">Drawing API</span>
    <span class="ak-badge ak-badge--orange">Entity Access</span>
    <span class="ak-badge ak-badge--blue">Config R/W</span>
    <span class="ak-badge ak-badge--green">Event System</span>
  </div>
</div>

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

<div class="ak-func-list">
<span class="ak-func-tag">antikira</span>
<span class="ak-func-tag">globals</span>
<span class="ak-func-tag">engine</span>
<span class="ak-func-tag">entitylist</span>
<span class="ak-func-tag">render</span>
<span class="ak-func-tag">menu</span>
<span class="ak-func-tag">environment</span>
<span class="ak-func-tag">config</span>
<span class="ak-func-tag">buttons</span>
</div>

- [`antikira`](lua/modules/antikira.md) — Utility functions owned by the runtime
- [`globals`](lua/modules/globals.md) — Engine timing and shared state (alias: `global_vars`)
- [`engine`](lua/modules/engine.md) — Client engine helpers
- [`entitylist`](lua/modules/entitylist.md) — Entity lookup helpers
- [`render`](lua/modules/render.md) — Immediate drawing (alias: `imgui`)
- [`menu`](lua/modules/menu.md) — Menu state helpers
- [`environment`](lua/modules/environment.md) — Script path helpers
- [`config`](lua/modules/config.md) — Config variable access
- [`buttons`](lua/modules/buttons.md) — Bitmask constants

## Objects

<div class="ak-func-list">
<span class="ak-func-tag">entity</span>
<span class="ak-func-tag">cmd</span>
<span class="ak-func-tag">event</span>
</div>

- [`entity`](lua/objects/entity.md) — Entity objects from `entitylist` and events
- [`cmd`](lua/objects/cmd.md) — Command objects in `create_move` callbacks
- [`event`](lua/objects/event.md) — Event objects in `event` and event-specific callbacks

## Notes

- The docs describe what is exposed by this repository right now, not a theoretical future API.
- Menu widgets are not directly scripted yet, but Lua can already read and change the underlying config values through [`config`](lua/modules/config.md).
