# FFI Notes

Antikira uses `LuaJIT`, so scripts can use:

```lua
local ffi = ffi or require("ffi")
```

## What This Gives You

With `ffi` you can:

- declare C structs
- cast pointers
- call exported functions
- load additional native DLL exports

## Minimal Example

```lua
local ffi = ffi or require("ffi")

ffi.cdef[[
    typedef struct {
        float x;
        float y;
        float z;
    } vec3_t;
]]
```

## Example With `ffi.new`

```lua
local ffi = ffi or require("ffi")

ffi.cdef[[
    typedef struct {
        float x;
        float y;
        float z;
    } vec3_t;
]]

local pos = ffi.new("vec3_t")
pos.x = 10.0
pos.y = 20.0
pos.z = 30.0
```

## Important Risk

`ffi` is not sandboxed.

Bad `ffi` code can crash the game process immediately if a script:

- reads an invalid pointer
- writes through a bad pointer
- uses the wrong calling convention
- defines the wrong structure layout
- calls a function with a wrong signature

Treat `ffi` code like native C or C++, not like safe scripting.

## Recommended Usage

Start with:

- `ffi.cdef`
- `ffi.new`
- read-only memory access
- pointer guards
- `antikira.log` for validation

Avoid aggressive memory writes until the script is already stable.

## Scope

The project does not try to restrict `ffi`.

If LuaJIT starts correctly, `ffi` is available to scripts.
