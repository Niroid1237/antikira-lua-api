# Antikira Lua API

This document describes the current in-project LuaJIT API exposed by Antikira.

The API is inspired by public CS2 Lua APIs such as [neverfair Lua API](https://neverfair.github.io/cs2-docs/), but it is not a byte-for-byte clone. This file documents what is actually available in this repository right now.

## Runtime

- Runtime: `LuaJIT`
- FFI: available
- Script folder: `C:\Antikira\scripts`
- Load method: menu -> `SCRIPTS`

You can use FFI either way:

```lua
local ffi = ffi or require("ffi")
```

## Conventions

- Lua callback names are lowercase strings like `"draw"` and `"create_move"`.
- `callbacks.DRAW` and `callbacks.PAINT` are the same callback.
- Colors can be passed either as `r, g, b, a` integers in `0..255` or as `color_t(r, g, b, a)`.
- `color_t(...)` uses normalized floats `0.0..1.0`.
- Vector-style config access uses Lua `1`-based indexes.
- Config variable names are the exact C++ identifiers from [`Antikira/src/cheat/config/vars.h`](../../Antikira/src/cheat/config/vars.h).

## Global Functions

### `register_callback(name, fn)`

Registers a callback for the current script.

```lua
register_callback("draw", function()
    render.text(20, 20, "hello", color_t(1.0, 1.0, 1.0, 1.0), 12)
end)
```

### `unregister_callback(name)`

Unregisters a callback previously registered by the current script.

### `color_t(r, g, b, a)`

Creates a color table compatible with the render and config APIs.

```lua
local red = color_t(1.0, 0.2, 0.2, 1.0)
```

## Module: `antikira`

### `antikira.log(text)`

Writes a Lua message into the cheat log.

### `antikira.notify(text)`

Shows an in-game notification.

### `antikira.script_name() -> string`

Returns the current script file name without extension.

## Module: `callbacks`

### Functions

- `callbacks.register(name, fn)`
- `callbacks.unregister(name)`

### Built-in callback names

- `callbacks.DRAW`
- `callbacks.PAINT`
- `callbacks.CREATE_MOVE`
- `callbacks.EVENT`
- `callbacks.SHUTDOWN`

### Supported callback names

- `"draw"` or `"paint"`
- `"create_move"`
- `"event"`
- `"shutdown"`
- any game event name such as `"player_hurt"` or `"round_start"`

### Notes

- Registering the same callback name again replaces the previous function for that script.
- `"event"` receives every game event.
- Registering `"player_hurt"` only receives that specific event.

## Module: `globals`

Alias: `global_vars`

### `globals.curtime() -> number`

Current game time.

### `globals.realtime() -> number`

Real time from engine globals.

### `globals.frametime() -> number`

Current frame time.

### `globals.tickcount() -> integer`

Current engine tick count.

### `globals.map_name() -> string`

Returns the current map name or an empty string.

### `globals.screen_size() -> number, number`

Returns `screen_w, screen_h`.

## Module: `engine`

### `engine.is_in_game() -> boolean`

### `engine.is_connected() -> boolean`

### `engine.execute_cmd(cmd)`

Executes a client command.

Aliases:

- `engine.exec(cmd)`
- `engine.execute_client_cmd(cmd)`

### `engine.get_level_name() -> string`

Alias for current map name.

## Module: `entitylist`

### `entitylist.get_local_pawn() -> entity|nil`

### `entitylist.get_local_controller() -> entity|nil`

### `entitylist.get_highest_index() -> integer`

### `entitylist.get_entity(index) -> entity|nil`

### `entitylist.get_players() -> table`

Returns an array-like Lua table of player pawns.

## Module: `render`

Alias: `imgui`

### `render.screen_size() -> number, number`

### `render.get_screen_size() -> number, number`

### `render.text(x, y, text, r, g, b, a[, size])`

### `render.text(x, y, text, color[, size])`

```lua
render.text(20, 20, "plain rgba", 255, 255, 255, 255)
render.text(20, 40, "color_t", color_t(0.2, 0.8, 1.0, 1.0), 14)
```

### `render.line(x1, y1, x2, y2, r, g, b, a[, thickness])`

### `render.line(x1, y1, x2, y2, color[, thickness])`

### `render.rect(x, y, w, h, r, g, b, a[, rounding[, thickness]])`

### `render.rect(x, y, w, h, color[, rounding[, thickness]])`

### `render.rect_filled(x, y, w, h, r, g, b, a[, rounding])`

### `render.rect_filled(x, y, w, h, color[, rounding])`

### `render.circle(x, y, radius, r, g, b, a[, segments[, thickness]])`

### `render.circle(x, y, radius, color[, segments[, thickness]])`

### `render.circle_filled(x, y, radius, r, g, b, a[, segments])`

### `render.circle_filled(x, y, radius, color[, segments])`

### `render.world_to_screen(x, y, z) -> boolean, number, number`

Returns:

- `visible`
- `screen_x`
- `screen_y`

## Module: `menu`

### `menu.is_open() -> boolean`

### `menu.get_pos() -> number, number`

Returns menu window top-left position.

### `menu.get_size() -> number, number`

Returns menu window size.

## Module: `environment`

### `environment.scripts_path() -> string`

Returns the scripts directory path.

### `environment.script_path() -> string`

Returns the current script full path.

### `environment.script_name() -> string`

Returns the current script name.

## Module: `config`

This module gives Lua access to already existing cheat settings from the C++ config system.

### Important rule

Names are the exact variable ids from [`Antikira/src/cheat/config/vars.h`](../../Antikira/src/cheat/config/vars.h), for example:

- `m_enabled_bunny_hop`
- `m_enemy_glow`
- `m_enemy_glow_color`
- `m_autostrafe_mode`
- `m_removals`

### Discovery

#### `config.has(name) -> boolean`

Checks whether a config variable exists.

#### `config.get_type(name) -> string`

Returns the config type string, for example:

- `"bool"`
- `"int"`
- `"float"`
- `"hellcolor"`
- `"std::vector<bool>"`
- `"std::vector<int>"`

#### `config.list([type_name]) -> table`

Returns an array-like table of all available config variable names.

Examples:

```lua
local all_vars = config.list()
local bool_vars = config.list("bool")
local color_vars = config.list("hellcolor")
```

#### `config.size(name) -> integer`

Returns vector size for vector-backed config variables.

For non-vector values this returns `0`.

### Bool values

#### `config.get_bool(name) -> boolean`

#### `config.set_bool(name, value)`

#### `config.toggle_bool(name) -> boolean`

Examples:

```lua
config.set_bool("m_enabled_bunny_hop", true)
config.set_bool("m_enemy_glow", true)
local new_state = config.toggle_bool("m_enabled_watermark")
```

### Int values

#### `config.get_int(name) -> integer`

#### `config.set_int(name, value)`

Examples:

```lua
config.set_int("m_autostrafe_mode", 1)
config.set_int("m_third_person_distance", 140)
```

### Float values

#### `config.get_float(name) -> number`

#### `config.set_float(name, value)`

Examples:

```lua
config.set_float("m_bar_glow_intensity", 1.5)
config.set_float("m_custom_fog_end_distance", 2600.0)
```

### Color values

#### `config.get_color(name) -> color`

Returns a `color_t`-style table with both array and named fields:

- `color[1]..color[4]`
- `color.r`, `color.g`, `color.b`, `color.a`

All values are normalized floats in `0.0..1.0`.

#### `config.set_color(name, r, g, b, a)`

#### `config.set_color(name, color)`

Examples:

```lua
local c = config.get_color("m_enemy_glow_color")
config.set_color("m_enemy_glow_color", color_t(1.0, 0.15, 0.15, 1.0))
config.set_color("m_world_color", 255, 200, 200, 255)
```

### Vector bool values

Some menu options are backed by `std::vector<bool>`.

#### `config.get_bool_at(name, index) -> boolean`

#### `config.set_bool_at(name, index, value)`

#### `config.size(name) -> integer`

Indexes are `1`-based in Lua.

Example:

```lua
for i = 1, config.size("m_removals") do
    antikira.log(("m_removals[%d] = %s"):format(i, tostring(config.get_bool_at("m_removals", i))))
end
```

Useful example for `m_removals`:

- `1` = scope
- `2` = local name
- `3` = team names
- `4` = smoke
- `5` = flash
- `6` = legs
- `7` = aimpunch

Example:

```lua
config.set_bool_at("m_removals", 4, true) -- smoke
config.set_bool_at("m_removals", 5, true) -- flash
```

### Vector int values

#### `config.get_int_at(name, index) -> integer`

#### `config.set_int_at(name, index, value)`

#### `config.size(name) -> integer`

Indexes are `1`-based in Lua.

### Error behavior

If you call a config function with:

- an unknown variable name,
- a wrong variable type,
- an out-of-range vector index,

the Lua call raises an error for that script callback.

## Module: `buttons`

Current command button constants:

- `buttons.IN_ATTACK`
- `buttons.IN_ATTACK2`
- `buttons.IN_JUMP`
- `buttons.IN_DUCK`
- `buttons.IN_FORWARD`
- `buttons.IN_BACK`
- `buttons.IN_USE`
- `buttons.IN_MOVELEFT`
- `buttons.IN_MOVERIGHT`
- `buttons.IN_SPEED`
- `buttons.IN_WALK`
- `buttons.IN_RELOAD`
- `buttons.IN_SCORE`
- `buttons.IN_ZOOM`
- `buttons.IN_SPRINT`

Note:

- `buttons.IN_WALK` is exposed as a compatibility alias and maps to the same underlying bit as `IN_SPEED` in the current project.

## Object: `entity`

Entity objects are returned by `entitylist` and by some event helpers.

### `entity:is_valid() -> boolean`

### `entity:get_index() -> integer`

### `entity:get_address() -> integer`

Returns the raw entity pointer value as an integer.

### `entity:get_class_name() -> string`

### `entity:get_origin() -> number, number, number`

Returns world origin.

### `entity:get_velocity() -> number, number, number`

### `entity:get_health() -> integer`

### `entity:get_team() -> integer`

### `entity:is_alive() -> boolean`

### `entity:is_scoped() -> boolean`

### `entity:get_eye_position() -> number, number, number`

### `entity:get_name() -> string`

For player controller or player pawn, this returns the player name.  
For other entities, this falls back to class name.

### `entity:get_controller() -> entity|nil`

If this is a pawn, returns its controller.  
If this is already a controller, returns itself.

### `entity:get_pawn() -> entity|nil`

If this is a controller, returns its pawn.  
If this is already a pawn, returns itself.

### `entity:is_enemy() -> boolean`

### `entity:get_active_weapon() -> entity|nil`

### `entity:get_weapon_name() -> string`

### `entity:get_steamid() -> integer`

## Object: `cmd`

`cmd` is passed into the `"create_move"` callback.

### `cmd:get_forward_move() -> number`

### `cmd:set_forward_move(value)`

### `cmd:get_side_move() -> number`

### `cmd:set_side_move(value)`

### `cmd:get_up_move() -> number`

### `cmd:set_up_move(value)`

### `cmd:get_view_angles() -> number, number, number`

Returns `pitch, yaw, roll`.

### `cmd:set_view_angles(pitch, yaw[, roll])`

### `cmd:get_buttons() -> integer`

### `cmd:has_button(mask) -> boolean`

### `cmd:add_button(mask)`

### `cmd:remove_button(mask)`

Example:

```lua
register_callback("create_move", function(cmd)
    if cmd:has_button(buttons.IN_JUMP) then
        cmd:add_button(buttons.IN_DUCK)
    end
end)
```

## Object: `event`

Event objects are passed into `"event"` and specific game event callbacks.

### `event:get_name() -> string`

### `event:get_bool(key) -> boolean`

### `event:get_int(key) -> integer`

### `event:get_float(key) -> number`

### `event:get_uint64(key) -> number`

### `event:get_string(key) -> string`

### `event:get_player_pawn(key) -> entity|nil`

### `event:get_player_controller(key) -> entity|nil`

Example:

```lua
register_callback("player_hurt", function(event)
    local victim = event:get_player_pawn("userid")
    local attacker = event:get_player_controller("attacker")

    if victim and victim:is_valid() then
        antikira.log("hurt victim: " .. victim:get_name())
    end

    if attacker and attacker:is_valid() then
        antikira.log("attacker: " .. attacker:get_name())
    end
end)
```
