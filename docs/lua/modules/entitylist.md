# Module: `entitylist`

Entity lookup helpers.

## `entitylist.get_local_pawn() -> entity|nil`

Returns the local player pawn if available.

## `entitylist.get_local_controller() -> entity|nil`

Returns the local player controller if available.

## `entitylist.get_highest_index() -> integer`

Returns the current highest entity index reported by the entity system.

## `entitylist.get_entity(index) -> entity|nil`

Returns the entity for a raw entity index.

Parameters:

- `index`: integer entity index

## `entitylist.get_players() -> table`

Returns an array-style Lua table of player pawns.

Notes:

- the returned entries are pawns, not controllers
- invalid or missing players are skipped
- indexes in the returned Lua table are compacted from `1`

Example:

```lua
for i, player in ipairs(entitylist.get_players()) do
    if player:is_valid() and player:is_alive() then
        antikira.log(player:get_name())
    end
end
```
