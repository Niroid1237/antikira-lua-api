# Module: `globals`

Alias: `global_vars`

Engine timing and shared state helpers.

## `globals.curtime() -> number`

Returns engine `curtime`.

## `globals.realtime() -> number`

Returns engine real time.

## `globals.frametime() -> number`

Returns current frame time.

## `globals.tickcount() -> integer`

Returns current engine tick count.

## `globals.map_name() -> string`

Returns current map name.

If no map is active, this returns an empty string.

## `globals.screen_size() -> number, number`

Returns:

- `screen_w`
- `screen_h`

## Example

```lua
register_callback("draw", function()
    local map = globals.map_name()
    local tick = globals.tickcount()
    render.text(20, 20, ("map=%s tick=%d"):format(map, tick), color_t(1.0, 1.0, 1.0, 1.0), 12)
end)
```
