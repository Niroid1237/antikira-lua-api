# Antikira Lua API

LuaJIT scripting API for Antikira CS2 cheat.

## Overview

Scripts run in a LuaJIT runtime with access to:

- Render primitives (text, lines, shapes)
- Game state (entities, globals, engine)
- Config read/write
- Event callbacks
- FFI for advanced use

Script folder: `C:\Antikira\scripts`

## Documentation

- [Getting Started](getting-started.md)
- [API Reference](api.md)
- [FFI Notes](ffi.md)

## Quick Example

```lua
register_callback("draw", function()
    render.text(20, 20, "hello from lua", color_t(1.0, 1.0, 1.0, 1.0), 12)
end)
```
