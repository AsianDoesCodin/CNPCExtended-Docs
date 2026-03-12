---
layout: default
title: Client Queries
---

## Client Queries

Query a player's client-side settings asynchronously. Results arrive in a callback.

<div class="warn-box">
Queries are <strong>read-only</strong>. Changing client settings from the server is not supported.
</div>

---

### Usage Pattern

All query methods take a `Consumer<CompoundTag>` callback:

```javascript
var Consumer = Java.type("java.util.function.Consumer")
var bridge = cnpcext.getClientBridge(player.getMCEntity())

bridge.queryVideoSettings(Java.extend(Consumer, {
    accept: function(tag) {
        player.message("Your FOV: " + tag.getInt("fov"))
    }
}))
```

---

### Available Queries

#### `queryVideoSettings(callback)`

| Key | Type | Description |
|-----|------|-------------|
| `fov` | int | Field of view (70–110) |
| `renderDistance` | int | Render distance (2–32) |
| `guiScale` | int | GUI scale (0 = auto, 1–4) |
| `graphicsMode` | String | `FAST`, `FANCY`, or `FABULOUS` |
| `maxFps` | int | Frame rate limit (10–260) |
| `fullscreen` | boolean | Fullscreen mode |
| `vsync` | boolean | VSync enabled |

#### `queryKeybinds(callback)`

| Key Pattern | Type | Description |
|-------------|------|-------------|
| `key.<binding>` | String | Bound key name (e.g. `key.mouse.left`) |
| `down.<binding>` | boolean | Whether the key is currently held |

Example bindings: `key.attack`, `key.use`, `key.forward`, `key.jump`, `key.inventory`

#### `querySoundSettings(callback)`

| Key | Type | Description |
|-----|------|-------------|
| `master` | double | Master volume (0.0–1.0) |
| `music` | double | Music volume |
| `weather` | double | Weather volume |
| `blocks` | double | Blocks volume |
| `hostile` | double | Hostile creatures volume |
| `neutral` | double | Friendly creatures volume |
| `players` | double | Players volume |
| `ambient` | double | Ambient volume |
| `voice` | double | Voice/speech volume |

#### `queryPlayerState(callback)`

| Key | Type | Description |
|-----|------|-------------|
| `xRot` | float | Camera pitch |
| `yRot` | float | Camera yaw |
| `x`, `y`, `z` | double | Player position |
| `screenWidth` | int | GUI-scaled screen width |
| `screenHeight` | int | GUI-scaled screen height |
| `currentScreen` | String | Current open screen class name, or `"none"` |

#### `queryResourcePacks(callback)`

| Key | Type | Description |
|-----|------|-------------|
| `packCount` | int | Number of active resource packs |
| `pack.0`, `pack.1`, ... | String | Pack IDs |

---

### Full Example

```javascript
function interact(e) {
    var Consumer = Java.type("java.util.function.Consumer")
    var bridge = cnpcext.getClientBridge(e.player.getMCEntity())

    bridge.queryVideoSettings(Java.extend(Consumer, {
        accept: function(tag) {
            e.player.message("§eYour Settings:")
            e.player.message("§7  FOV: §f" + tag.getInt("fov"))
            e.player.message("§7  Render Distance: §f" + tag.getInt("renderDistance"))
            e.player.message("§7  Graphics: §f" + tag.getString("graphicsMode"))
            e.player.message("§7  GUI Scale: §f" + tag.getInt("guiScale"))
        }
    }))
}
```

<div class="info-box">
Queries are asynchronous — the callback fires when the client responds. Don't rely on the result being available immediately after calling the query method.
</div>
