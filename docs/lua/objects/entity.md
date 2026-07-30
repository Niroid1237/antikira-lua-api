# Object: `entity`

Entity objects are returned by `entitylist` and by some event helpers.

They internally track entity index and serial, so stale references can become invalid after entity reuse.

## Validity

Always guard dynamic entities when the source can disappear:

```lua
local pawn = entitylist.get_local_pawn()
if not pawn or not pawn:is_valid() then
    return
end
```

## `entity:is_valid() -> boolean`

Returns whether the entity reference still resolves to a valid entity.

## `entity:get_index() -> integer`

Returns the stored entity index.

## `entity:get_address() -> integer`

Returns the raw entity pointer value as an integer.

This is mainly useful for debugging and advanced `ffi` workflows.

## `entity:get_class_name() -> string`

Returns the class name if available, otherwise an empty string.

## `entity:get_origin() -> number, number, number`

Returns world origin.

If the entity has no scene node, the call returns `nil`.

## `entity:get_velocity() -> number, number, number`

Returns absolute velocity.

If the entity does not resolve, the call returns `nil`.

## `entity:get_health() -> integer`

Returns health or `0`.

## `entity:get_team() -> integer`

Returns team number or `0`.

## `entity:is_alive() -> boolean`

For player pawns this uses the pawn-specific alive check.

For non-pawn entities it falls back to `health > 0`.

## `entity:is_scoped() -> boolean`

Returns whether a player pawn is scoped.

For non-player entities this returns `false`.

## `entity:get_eye_position() -> number, number, number`

Returns the eye position for a player pawn.

For non-player entities this returns `nil`.

## `entity:get_name() -> string`

Behavior:

- controller: player name
- pawn: resolves controller and returns player name
- other entity types: class name fallback

## `entity:get_controller() -> entity|nil`

Behavior:

- pawn: returns its controller
- controller: returns itself
- other types: `nil`

## `entity:get_pawn() -> entity|nil`

Behavior:

- controller: returns its pawn
- pawn: returns itself
- other types: `nil`

## `entity:is_enemy() -> boolean`

Returns enemy state for player pawn or controller based references.

For unrelated entities this returns `false`.

## `entity:get_active_weapon() -> entity|nil`

Returns the active weapon entity for a player pawn.

## `entity:get_weapon_name() -> string`

If the entity is a weapon, returns its weapon data name.

Otherwise returns an empty string.

## `entity:get_steamid() -> integer`

Returns SteamID for controllers and pawns when available.

Otherwise returns `0`.

## Example

```lua
register_callback("draw", function()
    local players = entitylist.get_players()
    for i = 1, #players do
        local player = players[i]
        if player:is_valid() and player:is_alive() and player:is_enemy() then
            local x, y, z = player:get_origin()
            local visible, sx, sy = render.world_to_screen(x, y, z + 72.0)
            if visible then
                render.text(sx, sy, player:get_name(), color_t(1.0, 0.25, 0.25, 1.0), 12)
            end
        end
    end
end)
```
