# Object: `cmd`

`cmd` objects are passed into the `"create_move"` callback.

They expose movement, view-angle, and button-state control for the current user command.

## `cmd:get_forward_move() -> number`

Returns current forward move value.

## `cmd:set_forward_move(value)`

Writes forward move value.

## `cmd:get_side_move() -> number`

Returns current side move value.

## `cmd:set_side_move(value)`

Writes side move value.

## `cmd:get_up_move() -> number`

Returns current up move value.

## `cmd:set_up_move(value)`

Writes up move value.

## `cmd:get_view_angles() -> number, number, number`

Returns:

- `pitch`
- `yaw`
- `roll`

If no view-angle buffer is available, the call returns `nil`.

## `cmd:set_view_angles(pitch, yaw[, roll])`

Writes new view angles.

If `roll` is omitted, `0.0` is used.

## `cmd:get_buttons() -> integer`

Returns the raw current button mask.

## `cmd:has_button(mask) -> boolean`

Checks whether a button bit is set.

Use masks from [`buttons`](../modules/buttons.md).

## `cmd:add_button(mask)`

Sets the given button bit and synchronizes the internal button state buffer.

## `cmd:remove_button(mask)`

Clears the given button bit and synchronizes the internal button state buffer.

## Example

```lua
register_callback("create_move", function(cmd)
    if cmd:has_button(buttons.IN_JUMP) then
        cmd:add_button(buttons.IN_DUCK)
    end

    local pitch, yaw, roll = cmd:get_view_angles()
    if pitch then
        cmd:set_view_angles(pitch, yaw + 1.0, roll)
    end
end)
```
