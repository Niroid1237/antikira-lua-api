# Callbacks

Callbacks are the main integration point between Lua and the cheat runtime.

You can register them either through the global helpers or through the `callbacks` table.

## Registration

### `register_callback(name, fn)`

Registers a callback for the current script.

Parameters:

- `name`: callback name
- `fn`: Lua function

Example:

```lua
register_callback("draw", function()
    render.text(20, 20, "hello", color_t(1.0, 1.0, 1.0, 1.0), 12)
end)
```

### `unregister_callback(name)`

Removes a previously registered callback for the current script.

### `callbacks.register(name, fn)`

Alias for `register_callback`.

### `callbacks.unregister(name)`

Alias for `unregister_callback`.

## Built-In Constants

- `callbacks.DRAW`
- `callbacks.PAINT`
- `callbacks.CREATE_MOVE`
- `callbacks.EVENT`
- `callbacks.SHUTDOWN`

## Normalized Names

The runtime normalizes several names internally:

- `"draw"` and `"paint"` both map to the paint callback
- `"createmove"` and `"create_move"` both map to the movement callback

Using the constant names avoids typos:

```lua
callbacks.register(callbacks.CREATE_MOVE, function(cmd)
    if cmd:has_button(buttons.IN_JUMP) then
        cmd:add_button(buttons.IN_DUCK)
    end
end)
```

## Supported Callback Kinds

### Paint

Names:

- `"draw"`
- `"paint"`

Arguments:

- none

Use this for:

- text
- lines
- boxes
- indicators
- debug overlays

### Create Move

Name:

- `"create_move"`

Arguments:

- `cmd`: [`cmd`](objects/cmd.md) object

Use this for:

- input modification
- button changes
- movement helpers
- angle edits

### Generic Event

Name:

- `"event"`

Arguments:

- `event`: [`event`](objects/event.md) object

This receives every incoming game event.

### Specific Game Event

Name:

- any exact event name such as `"player_hurt"`, `"round_start"`, `"item_purchase"`

Arguments:

- `event`: [`event`](objects/event.md) object

This only fires for that concrete event.

### Shutdown

Name:

- `"shutdown"`

Arguments:

- none

Use this to clean up state before the script is unloaded.

## Replacement Behavior

Registering the same callback name again in the same script replaces the previous function for that name.

## Examples

### Draw

```lua
register_callback("draw", function()
    local w, h = render.screen_size()
    render.text(20, h - 30, "frame active", color_t(0.8, 0.9, 1.0, 1.0), 12)
end)
```

### Create Move

```lua
register_callback("create_move", function(cmd)
    if cmd:has_button(buttons.IN_JUMP) then
        cmd:add_button(buttons.IN_DUCK)
    end
end)
```

### Specific Event

```lua
register_callback("player_hurt", function(event)
    local attacker = event:get_player_controller("attacker")
    if attacker and attacker:is_valid() then
        antikira.log("attacker: " .. attacker:get_name())
    end
end)
```
