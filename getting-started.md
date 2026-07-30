# Getting Started

## Runtime

The scripting runtime is based on `LuaJIT`, not stock Lua 5.4.  
This means scripts can use:

```lua
local ffi = ffi or require("ffi")
```

## Script Folder

Scripts are loaded from:

```text
C:\Antikira\scripts
```

The first launch creates an `example.lua` file automatically.

## Menu

Open the cheat menu, then go to `SCRIPTS`.

Available actions:

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

Scripts can read and change existing cheat settings:

```lua
config.set_bool("m_enabled_bunny_hop", true)
config.set_int("m_autostrafe_mode", 1)
config.set_color("m_enemy_glow_color", color_t(1.0, 0.2, 0.2, 1.0))
```

You can also inspect what is available:

```lua
local all_bools = config.list("bool")
for i = 1, #all_bools do
    antikira.log(all_bools[i])
end
```
