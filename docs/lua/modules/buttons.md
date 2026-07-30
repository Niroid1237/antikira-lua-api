# Module: `buttons`

Bitmask constants for the `cmd` object used inside `"create_move"` callbacks.

## Available Constants

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

## Compatibility Note

`buttons.IN_WALK` is currently exposed as a compatibility alias and maps to the same underlying bit as `IN_SPEED` in this project.

## Example

```lua
register_callback("create_move", function(cmd)
    if cmd:has_button(buttons.IN_JUMP) then
        cmd:add_button(buttons.IN_DUCK)
    end
end)
```
