# Module: `antikira`

Utility functions owned by the runtime itself.

## `antikira.log(text)`

Writes a log line prefixed as Lua output in the cheat log.

Parameters:

- `text`: string

Example:

```lua
antikira.log("hello from lua")
```

## `antikira.notify(text)`

Shows an in-game notification through the overlay notification system.

Parameters:

- `text`: string

Example:

```lua
antikira.notify("script loaded")
```

## `antikira.script_name() -> string`

Returns the current script file name without the `.lua` extension.

Example:

```lua
antikira.log("current script: " .. antikira.script_name())
```
