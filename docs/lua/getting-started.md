# Getting Started

## Runtime

Antikira uses `LuaJIT`, not stock Lua 5.1 or Lua 5.4.

That means scripts can use:

```lua
local ffi = ffi or require("ffi")
```

## Scripts Folder

Scripts are loaded from:

```text
C:\Antikira\scripts
```

On first initialization the runtime creates `example.lua` automatically.

## Menu Workflow

Open the cheat menu and go to `SCRIPTS`.

Current actions:

- `Refresh`
- `Open folder`
- `Load`
- `Unload`
- `Reload`

## First Script

```lua
register_callback("draw", function()
    render.text(20, 20, "hello from lua", color_t(1.0, 1.0, 1.0, 1.0), 12)
end)
```

## Event Example

```lua
register_callback("player_hurt", function(event)
    local victim = event:get_player_pawn("userid")
    if victim and victim:is_valid() then
        antikira.notify("hurt: " .. victim:get_name())
    end
end)
```

## Create Move Example

```lua
register_callback("create_move", function(cmd)
    if cmd:has_button(buttons.IN_JUMP) then
        cmd:add_button(buttons.IN_DUCK)
    end
end)
```

## Config Example

Lua can change the same backing config values that power the menu.

```lua
config.set_bool("m_enabled_autostrafe", true)
config.set_int("m_autostrafe_mode", 1)
config.set_int("m_autostrafe_boost", 100)
config.set_int("m_hitchance_awp", 70)
```

## Discovering Variable Names

If you do not know the exact internal config name yet:

```lua
local ints = config.list("int")
for i = 1, #ints do
    antikira.log(ints[i])
end
```

Useful examples already present in this project:

- `m_enabled_autostrafe`
- `m_autostrafe_mode`
- `m_autostrafe_boost`
- `m_hitchance_awp`
- `m_hitchance_scout`
- `m_hitchance_ar`

## Recommended Reading Order

1. [Runtime](runtime.md)
2. [Callbacks](callbacks.md)
3. [Module: render](modules/render.md)
4. [Module: config](modules/config.md)
5. [Object: entity](objects/entity.md)
6. [Object: cmd](objects/cmd.md)
7. [FFI Notes](ffi.md)
