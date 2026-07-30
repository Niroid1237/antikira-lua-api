# Module: `render`

Alias: `imgui`

Immediate drawing helpers backed by the ImGui background draw list.

<div class="ak-panel">
  <div class="ak-kicker">Overlay Primitives</div>
  <p>Use this module for on-screen diagnostics, indicators, labels, and lightweight visual debugging from Lua. All coordinates are in screen space unless a function explicitly says otherwise.</p>
</div>

## Color Input Rules

Every drawing function that accepts a color supports two forms:

### Integer RGBA

```lua
render.text(20, 20, "hello", 255, 255, 255, 255, 12)
```

### `color_t(...)`

```lua
render.text(20, 20, "hello", color_t(1.0, 1.0, 1.0, 1.0), 12)
```

`color_t(...)` uses normalized `0.0 .. 1.0` values.

## `render.screen_size() -> number, number`

Returns:

- `screen_w`
- `screen_h`

## `render.get_screen_size() -> number, number`

Alias for `render.screen_size()`.

## `render.text(x, y, text, r, g, b, a[, size])`

## `render.text(x, y, text, color[, size])`

<div class="ak-signature"><code>render.text(x, y, text, color[, size])</code></div>

Draws text on the background draw list.

Parameters:

- `x`, `y`: screen position
- `text`: string
- `size`: optional font size, default is the runtime's medium font legacy size

## `render.line(x1, y1, x2, y2, r, g, b, a[, thickness])`

## `render.line(x1, y1, x2, y2, color[, thickness])`

<div class="ak-signature"><code>render.line(x1, y1, x2, y2, color[, thickness])</code></div>

Draws a line.

## `render.rect(x, y, w, h, r, g, b, a[, rounding[, thickness]])`

## `render.rect(x, y, w, h, color[, rounding[, thickness]])`

<div class="ak-signature"><code>render.rect(x, y, w, h, color[, rounding[, thickness]])</code></div>

Draws an outlined rectangle.

## `render.rect_filled(x, y, w, h, r, g, b, a[, rounding])`

## `render.rect_filled(x, y, w, h, color[, rounding])`

<div class="ak-signature"><code>render.rect_filled(x, y, w, h, color[, rounding])</code></div>

Draws a filled rectangle.

## `render.circle(x, y, radius, r, g, b, a[, segments[, thickness]])`

## `render.circle(x, y, radius, color[, segments[, thickness]])`

<div class="ak-signature"><code>render.circle(x, y, radius, color[, segments[, thickness]])</code></div>

Draws an outlined circle.

Default segment count: `32`

## `render.circle_filled(x, y, radius, r, g, b, a[, segments])`

## `render.circle_filled(x, y, radius, color[, segments])`

<div class="ak-signature"><code>render.circle_filled(x, y, radius, color[, segments])</code></div>

Draws a filled circle.

Default segment count: `32`

## `render.world_to_screen(x, y, z) -> boolean, number, number`

<div class="ak-signature"><code>render.world_to_screen(x, y, z) -&gt; visible, screen_x, screen_y</code></div>

Returns:

- `visible`
- `screen_x`
- `screen_y`

Compatibility note:

- `math.world_to_screen(x, y, z)` is also exposed as an alias

## Example

```lua
register_callback("draw", function()
    local local_pawn = entitylist.get_local_pawn()
    if not local_pawn or not local_pawn:is_valid() then
        return
    end

    local x, y, z = local_pawn:get_origin()
    local visible, sx, sy = render.world_to_screen(x, y, z + 72.0)
    if visible then
        render.circle_filled(sx, sy, 4, color_t(0.2, 1.0, 0.4, 1.0), 24)
        render.text(sx + 8, sy - 6, local_pawn:get_name(), color_t(1.0, 1.0, 1.0, 1.0), 12)
    end
end)
```
