# Module: `config`

This module exposes direct access to existing Antikira config variables from Lua.

That means a script can change the same underlying values used by checkboxes, combos, sliders, and color pickers in the menu.

## Important Rules

- names are exact internal C++ variable names from `Antikira/src/cheat/config/vars.h`
- Lua indexes are `1`-based
- current public support is limited to:
  - `bool`
  - `int`
  - `float`
  - `hellcolor`
  - `std::vector<bool>`
  - `std::vector<int>`

## Common Examples

- `m_enabled_autostrafe`
- `m_autostrafe_mode`
- `m_autostrafe_boost`
- `m_hitchance_awp`
- `m_hitchance_scout`
- `m_hitchance_ar`
- `m_enemy_glow`
- `m_enemy_glow_color`
- `m_removals`

## Discovery

### `config.has(name) -> boolean`

Returns whether a config variable exists.

### `config.get_type(name) -> string`

Returns the config type string.

Possible values include:

- `"bool"`
- `"int"`
- `"float"`
- `"hellcolor"`
- `"std::vector<bool>"`
- `"std::vector<int>"`

### `config.list([type_name]) -> table`

Returns an array-style Lua table of all known config variable names.

If `type_name` is passed, the result is filtered by exact type string.

Examples:

```lua
local all_vars = config.list()
local bool_vars = config.list("bool")
local int_vars = config.list("int")
```

### `config.size(name) -> integer`

Returns the size of a vector-backed config variable.

For non-vector values this returns `0`.

## Bool Access

### `config.get_bool(name) -> boolean`

### `config.set_bool(name, value)`

### `config.toggle_bool(name) -> boolean`

Example:

```lua
config.set_bool("m_enabled_autostrafe", true)
local new_state = config.toggle_bool("m_enabled_watermark")
```

## Int Access

### `config.get_int(name) -> integer`

### `config.set_int(name, value)`

Examples:

```lua
config.set_int("m_autostrafe_mode", 1)
config.set_int("m_autostrafe_boost", 100)
config.set_int("m_hitchance_awp", 70)
```

## Float Access

### `config.get_float(name) -> number`

### `config.set_float(name, value)`

Example:

```lua
config.set_float("m_bar_glow_intensity", 1.5)
```

## Color Access

### `config.get_color(name) -> color`

Returns a `color_t`-style table with both array and named fields:

- `color[1] .. color[4]`
- `color.r`, `color.g`, `color.b`, `color.a`

Returned values are normalized floats in `0.0 .. 1.0`.

### `config.set_color(name, r, g, b, a)`

### `config.set_color(name, color)`

Examples:

```lua
local c = config.get_color("m_enemy_glow_color")
config.set_color("m_enemy_glow_color", color_t(1.0, 0.15, 0.15, 1.0))
config.set_color("m_world_color", 255, 200, 200, 255)
```

## Vector Bool Access

### `config.get_bool_at(name, index) -> boolean`

### `config.set_bool_at(name, index, value)`

Example:

```lua
for i = 1, config.size("m_removals") do
    antikira.log(("m_removals[%d] = %s"):format(i, tostring(config.get_bool_at("m_removals", i))))
end
```

Known `m_removals` indexes in this project:

- `1` = scope
- `2` = local name
- `3` = team names
- `4` = smoke
- `5` = flash
- `6` = legs
- `7` = aimpunch

Example:

```lua
config.set_bool_at("m_removals", 4, true)
config.set_bool_at("m_removals", 5, true)
```

## Vector Int Access

### `config.get_int_at(name, index) -> integer`

### `config.set_int_at(name, index, value)`

Use this for flat `std::vector<int>` config values.

## Practical Examples

### Autostrafe

```lua
config.set_bool("m_enabled_autostrafe", true)
config.set_int("m_autostrafe_mode", 1)
config.set_int("m_autostrafe_boost", 100)
```

### Hitchance

```lua
config.set_int("m_hitchance_awp", 72)
config.set_int("m_hitchance_scout", 68)
config.set_int("m_hitchance_ar", 55)
```

### Enumerating All Int Variables

```lua
for i, name in ipairs(config.list("int")) do
    antikira.log(name .. " = " .. tostring(config.get_int(name)))
end
```

## Error Behavior

The runtime raises a Lua error if you:

- use an unknown variable name
- call a getter or setter with the wrong variable type
- use an out-of-range vector index

That error aborts the current callback invocation for that script.
