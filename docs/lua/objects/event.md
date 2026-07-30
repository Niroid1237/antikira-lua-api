# Object: `event`

`event` objects are passed into:

- the generic `"event"` callback
- event-specific callbacks such as `"player_hurt"`

## `event:get_name() -> string`

Returns the event name.

## `event:get_bool(key) -> boolean`

Reads a boolean event field.

## `event:get_int(key) -> integer`

Reads an integer event field.

## `event:get_float(key) -> number`

Reads a float event field.

## `event:get_uint64(key) -> number`

Reads an unsigned 64-bit event field and returns it as a Lua number.

Use this carefully if exact large integer fidelity matters.

## `event:get_string(key) -> string`

Reads a string event field.

## `event:get_player_pawn(key) -> entity|nil`

Resolves an event player field as a pawn.

Example keys often used by Source events:

- `"userid"`
- `"attacker"`
- `"assister"`

## `event:get_player_controller(key) -> entity|nil`

Resolves an event player field as a controller.

## Example

```lua
register_callback("player_hurt", function(event)
    local attacker = event:get_player_controller("attacker")
    local victim = event:get_player_pawn("userid")
    local dmg = event:get_int("dmg_health")

    if attacker and attacker:is_valid() and victim and victim:is_valid() then
        antikira.log(("%s hurt %s for %d"):format(
            attacker:get_name(),
            victim:get_name(),
            dmg
        ))
    end
end)
```
