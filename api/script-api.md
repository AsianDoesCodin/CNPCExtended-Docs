---
layout: default
title: Script API (cnpcext)
---

## Script API — `cnpcext`

The `cnpcext` global is auto-injected into every CNPC script (NPC, Player, Block, Item). No imports needed.

---

### `cnpcext.openHtmlGui(eventOrPlayer, filename, width, height, jsonInitData)`

Opens an HTML GUI on a player's screen.

| Parameter | Type | Description |
|-----------|------|-------------|
| `eventOrPlayer` | Event or IPlayer | A CNPC event object (`e`) or any `IPlayer` reference |
| `filename` | String | HTML file path relative to `<world>/customnpcs/scripts/ecmascript/` |
| `width` | Number | Browser width in pixels (`0` = fullscreen) |
| `height` | Number | Browser height in pixels (`0` = fullscreen) |
| `jsonInitData` | String | JSON string — available as `window.cnpc.initData` in the browser |

#### With an event (recommended)

Stores `e.player`, `e.npc`, `e.API` and the current ScriptContainer for event routing:

```javascript
function interact(e) {
    cnpcext.openHtmlGui(e, "shop.html", 0, 0, JSON.stringify({gold: 100}))
}
```

#### With an IPlayer (target any player)

Works like `target.showCustomGui(gui)` — opens the GUI on any player:

```javascript
function interact(e) {
    var target = e.player.getWorld().getPlayer("OtherPlayer")
    if (target) {
        cnpcext.openHtmlGui(target, "invite.html", 0, 0, JSON.stringify({
            from: e.player.getDisplayName()
        }))
    }
}
```

<div class="warn-box">
When targeting an IPlayer directly, <code>e.npc</code> will be <code>null</code> in <code>htmlGuiEvent</code>. <code>e.player</code> and <code>e.API</code> still work.
</div>

---

### `cnpcext.getClientBridge(mcPlayer)`

Returns an `IClientBridge` for querying client-side state or sending data to an open browser.

```javascript
var bridge = cnpcext.getClientBridge(player.getMCEntity())
bridge.sendToBrowser("update", JSON.stringify({score: 42}))
```

See [Client Queries]({{ '/api/queries' | relative_url }}) for query methods.

---

### `htmlGuiEvent(e)` — Event Handler

Define this function in any script that calls `openHtmlGui`. It fires when the HTML calls `window.cnpc.sendEvent()`.

```javascript
function htmlGuiEvent(e) {
    e.player      // IPlayer — the player with the open GUI
    e.npc         // ICustomNpc — the NPC (null if opened via IPlayer)
    e.API         // NpcAPI instance
    e.eventName   // String — event name from sendEvent()
    e.data        // String — JSON data (use JSON.parse(e.data))
}
```

#### Example

```javascript
function htmlGuiEvent(e) {
    var data = JSON.parse(e.data)

    if (e.eventName === "buy") {
        var cost = data.price * data.qty
        if (e.player.inventoryItemCount("minecraft:emerald") >= cost) {
            e.player.removeItem("minecraft:emerald", cost)
            e.player.giveItem(data.itemId, data.qty)

            var bridge = cnpcext.getClientBridge(e.player.getMCEntity())
            bridge.sendToBrowser("buyResult", JSON.stringify({
                success: true,
                balance: e.player.inventoryItemCount("minecraft:emerald")
            }))
        }
    }
}
```

---

### Server → Browser Push

Send data to an open HTML GUI at any time during a session:

```javascript
var bridge = cnpcext.getClientBridge(player.getMCEntity())
bridge.sendToBrowser("eventName", JSON.stringify({key: "value"}))
```

The browser receives it via:

```javascript
window.cnpc.onEvent("eventName", function(data) {
    // data.key === "value"
})
```

---

### Script Type Compatibility

`cnpcext.openHtmlGui` works with **all** CNPC script types:

| Script Type | Example Event | `e.npc` available? |
|-------------|---------------|:------------------:|
| NPC | `interact(e)`, `tick(e)` | Yes |
| Player | `interact(e)`, `chat(e)`, `keyPressed(e)` | No |
| Block | `interact(e)`, `clicked(e)` | No |
| Item | `interact(e)`, `attack(e)` | No |

The `htmlGuiEvent` handler always fires on the **same ScriptContainer** that called `openHtmlGui`, regardless of script type.

---

### `cnpcext.registerCommand(name, jsonDefinition)`

<span class="badge badge-version">New in v1.1.0</span>

Register a custom `/` command at runtime with full tab-completion. Commands registered this way are **runtime only** — they clear on server restart. For persistent commands, use `/cnpcext command create` instead.

| Parameter | Type | Description |
|-----------|------|-------------|
| `name` | String | Command name (alphanumeric + underscore, e.g. `"shop"`) |
| `jsonDefinition` | String | JSON string defining permission and arguments |

Registration is **idempotent** — calling with the same name again is a no-op. Safe to call in `init()` even on a server with many players.

```javascript
function init(e) {
    cnpcext.registerCommand("shop", JSON.stringify({
        permission: 0,
        args: [
            {name: "action", type: "string", suggestions: ["open", "list", "sell"]},
            {name: "item", type: "string"}
        ]
    }))
}
```

#### Argument Types

| Type | JSON | Tab Completion |
|------|------|----------------|
| `string` | `{name: "x", type: "string"}` | Free text |
| `string` + suggestions | `{name: "x", type: "string", suggestions: ["a","b"]}` | Shows suggestions |
| `integer` | `{name: "x", type: "integer", min: 1, max: 100}` | Number in range |
| `player` | `{name: "x", type: "player"}` | Online player names |
| `boolean` | `{name: "x", type: "boolean"}` | true / false |

---

### `customCommand(e)` — Event Handler

Define this in a **player script**. Fires when any script-registered or persistent command is executed.

```javascript
function customCommand(e) {
    e.player   // IPlayer — the player who ran the command
    e.command  // String — command name
    e.args     // String — JSON arguments (use JSON.parse(e.args))
}
```

#### Example

```javascript
function customCommand(e) {
    var player = e.player
    var args = JSON.parse(e.args)

    if (e.command === "shop") {
        if (args.action === "open") {
            cnpcext.openHtmlGui(player, "shop.html", 0, 0, "{}")
        } else if (args.action === "list") {
            player.message("§eSword - 100 coins")
            player.message("§eArmor - 250 coins")
        }
    }
}
```

<div class="info-box">
<strong>Tip:</strong> <code>customCommand(e)</code> fires on <strong>all player script tabs</strong>. Each tab can handle different commands, or you can put all handlers in one tab.
</div>
