# Module: `engine`

Client engine helpers.

## `engine.is_in_game() -> boolean`

Returns whether the engine is currently in a game session.

## `engine.is_connected() -> boolean`

Returns whether the client is connected.

## `engine.execute_cmd(cmd)`

Executes a client command through the unrestricted client command path.

Parameters:

- `cmd`: string

Aliases:

- `engine.exec(cmd)`
- `engine.execute_client_cmd(cmd)`

Example:

```lua
engine.execute_cmd("say hello from lua")
```

## `engine.get_level_name() -> string`

Returns the current map name.

This is effectively an alias for `globals.map_name()`.
