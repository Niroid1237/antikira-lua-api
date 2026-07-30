# FFI Notes

The scripting layer uses `LuaJIT`, so scripts can access:

```lua
local ffi = ffi or require("ffi")
```

## Example

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

## Important Risk

`ffi` is powerful enough to crash the game process if a script:

- reads an invalid pointer,
- writes to the wrong address,
- declares a wrong C layout,
- calls an engine function with a bad signature.

That means `ffi` should be treated like native code, not like safe sandboxed scripting.

## Recommended Usage

Start with:

- reading values,
- defining simple structs,
- debugging with `antikira.log`,
- guarding pointers before dereferencing them.

Avoid writing memory until the script is already stable.

## Scope

This project does not try to restrict `ffi`.  
If LuaJIT loads successfully, `require("ffi")` is available to scripts by default.
