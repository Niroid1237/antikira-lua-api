# API Overview

This page is the fast reference for the currently exposed Lua API.

If you want full argument descriptions and examples, use the per-module pages from the sidebar.

<div class="ak-panel">
  <div class="ak-kicker">Runtime Snapshot</div>
  <p>This page is the shortest path to understanding what the Antikira Lua runtime exposes right now: globals, callback names, object types, and the main modules you can script against.</p>
</div>

## Runtime Summary

- Runtime: `LuaJIT`
- `ffi`: available
- Script folder: `C:\Antikira\scripts`
- Auto-created example script: yes
- Script search paths are appended to Lua `package.path` and `package.cpath`

<div class="ak-mini-grid">
  <div class="ak-mini-card">
    <strong>Callbacks</strong>
    <span><code>draw</code>, <code>create_move</code>, generic <code>event</code>, exact event names, and <code>shutdown</code>.</span>
  </div>
  <div class="ak-mini-card">
    <strong>State Access</strong>
    <span>Read entities, events, globals, engine state, menu state, and script environment information.</span>
  </div>
  <div class="ak-mini-card">
    <strong>Mutation</strong>
    <span>Change config values, edit command buttons and movement, and draw on the overlay.</span>
  </div>
</div>

## Global Helpers

- `register_callback(name, fn)`
- `unregister_callback(name)`
- `color_t(r, g, b, a)`

## Global Tables

- `antikira`
- `callbacks`
- `globals`
- `global_vars`
- `engine`
- `entitylist`
- `render`
- `imgui`
- `menu`
- `environment`
- `config`
- `buttons`

## Callback Names

- `"draw"`
- `"paint"`
- `"create_move"`
- `"event"`
- `"menu"` — build custom script UI in the SCRIPTS tab
- `"shutdown"`
- any concrete game event name such as `"player_hurt"` or `"round_start"`

## Type Summary

### Color

`color_t(...)` returns a Lua table with both array and named fields:

```lua
local c = color_t(1.0, 0.2, 0.2, 1.0)
print(c[1], c[2], c[3], c[4])
print(c.r, c.g, c.b, c.a)
```

### Entity

`entity` values are returned by:

- `entitylist.get_local_pawn()`
- `entitylist.get_local_controller()`
- `entitylist.get_entity(index)`
- `entitylist.get_players()`
- `event:get_player_pawn(key)`
- `event:get_player_controller(key)`

### User Command

`cmd` is passed into the `"create_move"` callback.

### Game Event

`event` is passed into `"event"` and event-specific callbacks.

## Main References

- [Getting Started](getting-started.md)
- [Runtime](runtime.md)
- [Callbacks](callbacks.md)
- [FFI Notes](ffi.md)
- [Module: antikira](modules/antikira.md)
- [Module: globals](modules/globals.md)
- [Module: engine](modules/engine.md)
- [Module: entitylist](modules/entitylist.md)
- [Module: render](modules/render.md)
- [Module: menu](modules/menu.md)
- [Module: environment](modules/environment.md)
- [Module: config](modules/config.md)
- [Module: buttons](modules/buttons.md)
- [Object: entity](objects/entity.md)
- [Object: cmd](objects/cmd.md)
- [Object: event](objects/event.md)
