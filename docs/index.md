# Antikira Lua API

Antikira now ships with a built-in `LuaJIT` runtime, `ffi` support, script management in the menu, and a documented in-process API for callbacks, rendering, entity access, user commands, game events, and config values.

This documentation is organized as a small docs site so it can be published to GitHub Pages in a format closer to projects such as [neverfair cs2 docs](https://neverfair.github.io/cs2-docs/).

## What Is Available

- `LuaJIT` runtime
- `ffi` support
- callback registration
- drawing API
- entity and event access
- `create_move` command access
- config value read/write access
- script environment helpers

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
