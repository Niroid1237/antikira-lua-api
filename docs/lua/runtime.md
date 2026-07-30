# Runtime

## Engine

Antikira embeds `LuaJIT`.

This is important for two reasons:

- you get `ffi`
- most public CS2 Lua snippets written for LuaJIT are easier to adapt

## Script Loading

Scripts are loaded from:

```text
C:\Antikira\scripts
```

The runtime:

- creates the scripts directory if it does not exist
- creates `example.lua` on first initialization
- keeps one Lua state per loaded script
- unloads and destroys the state when the script is unloaded

## Package Search Paths

When a script is loaded, Antikira appends script-local paths to Lua's package search path:

- `C:\Antikira\scripts\?.lua`
- `C:\Antikira\scripts\?\init.lua`
- `C:\Antikira\scripts\?.dll`

This means you can organize helper modules like:

```text
C:\Antikira\scripts\mylib.lua
C:\Antikira\scripts\myfolder\init.lua
```

and load them with:

```lua
local mylib = require("mylib")
local myfolder = require("myfolder")
```

## FFI

`ffi` is exposed globally if LuaJIT can load it:

```lua
local ffi = ffi or require("ffi")
```

See [FFI Notes](ffi.md) for safety notes and examples.

## Error Behavior

If a callback throws a Lua error:

- the error is logged
- an in-game notification is shown
- the current callback invocation stops

The script is not automatically deleted from disk.

## Script Identity

The runtime tracks the current script and exposes helpers for:

- current script file name
- current script full path
- scripts directory path

See the [`antikira`](modules/antikira.md) and [`environment`](modules/environment.md) modules.

## Example

```lua
local ffi = ffi or require("ffi")

register_callback("draw", function()
    local name = environment.script_name()
    render.text(20, 20, "loaded: " .. name, color_t(0.9, 0.9, 0.9, 1.0), 12)
end)
```
