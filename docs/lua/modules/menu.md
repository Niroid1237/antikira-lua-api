# Module: `menu`

Read-only menu state helpers.

This module does not directly create or modify menu widgets yet.

Instead, scripts interact with existing menu-backed values through the [`config`](config.md) module.

## `menu.is_open() -> boolean`

Returns whether the Antikira menu is currently open.

## `menu.get_pos() -> number, number`

Returns:

- `x`
- `y`

This is the menu window top-left position.

## `menu.get_size() -> number, number`

Returns:

- `w`
- `h`

This is the current menu window size.

## Example

```lua
register_callback("draw", function()
    if not menu.is_open() then
        return
    end

    local x, y = menu.get_pos()
    render.text(x, y - 18, "menu open", color_t(1.0, 0.8, 0.2, 1.0), 12)
end)
```
