# Module: `menu`

Menu state helpers and custom script UI widgets.

## Menu Callback

Use `register_callback("menu", fn)` to build custom UI for your script.
Widget functions only work inside a `"menu"` callback.

## Menu State

### `menu.is_open() -> boolean`

Returns whether the Antikira menu is currently open.

### `menu.get_pos() -> number, number`

Returns:

- `x`
- `y`

This is the menu window top-left position.

### `menu.get_size() -> number, number`

Returns:

- `w`
- `h`

This is the current menu window size.

## Custom Script UI Widgets

These functions create interactive UI widgets in the script's menu section.
They only work inside a `register_callback("menu", fn)` callback.
Widgets bind directly to existing config variables by their internal name.

### `menu.checkbox(label, var_name) -> boolean`

Creates a checkbox bound to a `bool` config variable.

- `label` — display text
- `var_name` — name of a `bool` config variable

Returns `true` if the value was toggled this frame.

### `menu.slider_int(label, var_name, min, max) -> boolean`

Creates an integer slider bound to an `int` config variable.

- `label` — display text
- `var_name` — name of an `int` config variable
- `min` — minimum value
- `max` — maximum value

Returns `true` if the value was changed this frame.

### `menu.slider_float(label, var_name, min, max) -> boolean`

Creates a float slider bound to a `float` config variable.

- `label` — display text
- `var_name` — name of a `float` config variable
- `min` — minimum value
- `max` — maximum value

Returns `true` if the value was changed this frame.

### `menu.combo(label, var_name, items) -> boolean`

Creates a combo box bound to an `int` config variable.

- `label` — display text
- `var_name` — name of an `int` config variable
- `items` — Lua table of string options, e.g. `{"Off", "On", "Rage"}`

Returns `true` if the selection changed this frame.

### `menu.button(label) -> boolean`

Creates a clickable button.

- `label` — button text

Returns `true` if the button was clicked this frame.

### `menu.label(text)`

Draws static label text.

- `text` — label text

### `menu.color_picker(id, var_name) -> boolean`

Creates a color picker bound to a `hellcolor` config variable.

- `id` — unique identifier for the picker
- `var_name` — name of a `hellcolor` config variable

Returns `true` if the color was changed this frame.

### `menu.same_line([offset])`

Places the next widget on the same line.

- `offset` — optional offset from start (default 0)

### `menu.separator()`

Draws a horizontal separator line.

### `menu.new_line()`

Inserts a blank line.

## Example

```lua
register_callback("menu", function()
    menu.checkbox("Auto Strafe", "m_enabled_autostrafe")
    menu.same_line()
    if menu.button("Toggle Watermark") then
        config.toggle_bool("m_enabled_watermark")
    end

    menu.separator()

    menu.label("Hitchance")
    menu.slider_int("AWP", "m_hitchance_awp", 0, 100)
    menu.slider_int("Scout", "m_hitchance_scout", 0, 100)

    menu.separator()

    menu.combo("Autostrafe Mode", "m_autostrafe_mode", {"Off", "Directional", "Rage"})
    menu.slider_int("Boost", "m_autostrafe_boost", 0, 100)
end)
```
