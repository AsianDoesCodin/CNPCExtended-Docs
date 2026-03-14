---
layout: default
title: HTML API (window.cnpc)
---

## HTML API — `window.cnpc`

The `window.cnpc` object is automatically injected into every HTML GUI. Available immediately on page load.

---

### Properties

| Property | Type | Description |
|----------|------|-------------|
| `window.cnpc.initData` | Object | Parsed JSON from the `jsonInitData` parameter passed to `openHtmlGui` |

```javascript
// Server script
cnpcext.openHtmlGui(e, "gui.html", 0, 0, JSON.stringify({
    name: "Steve",
    balance: 100,
    items: [{id: "sword", price: 10}]
}))
```

```javascript
// HTML script
var data = window.cnpc.initData
console.log(data.name)    // "Steve"
console.log(data.balance) // 100
```

---

### Methods

#### `window.cnpc.sendEvent(name, data)`

Send an event to the server. Fires `htmlGuiEvent(e)` on the script that opened this GUI.

```javascript
window.cnpc.sendEvent("buy", { itemId: "minecraft:diamond", qty: 5 })
```

- `name` — String, alphanumeric + underscore only (`[a-zA-Z0-9_]+`)
- `data` — Object, serialized as JSON automatically

#### `window.cnpc.close()`

Close the GUI. Equivalent to pressing ESC.

```javascript
window.cnpc.close()
```

This fires `htmlGuiEvent(e)` with `e.eventName === "__guiClosed"` on the server, then cleans up the session.

#### `window.cnpc.onEvent(name, callback)`

Listen for server-pushed events (via `bridge.sendToBrowser`).

```javascript
window.cnpc.onEvent("buyResult", function(data) {
    if (data.success) {
        document.getElementById('balance').textContent = data.balance
    } else {
        alert("Not enough gold!")
    }
})
```

#### `window.cnpc.setResult(data)`

Shorthand for `sendEvent("__result", data)`. Useful for simple request/response patterns.

```javascript
window.cnpc.setResult({ choice: "optionA" })
```

---

### Full Example

```html
<!DOCTYPE html>
<html>
<head>
<style>
  body { background: transparent; color: white; font-family: sans-serif;
         display: flex; justify-content: center; align-items: center;
         height: 100vh; margin: 0; }
  .panel { background: rgba(0,0,0,0.85); padding: 30px; border-radius: 8px;
           border: 2px solid #c9a83e; text-align: center; }
  .balance { font-size: 24px; color: #f0d060; margin: 16px 0; }
  button { padding: 8px 16px; margin: 4px; cursor: pointer; background: #333;
           color: white; border: 1px solid #c9a83e; border-radius: 4px; }
  button:hover { background: #555; }
  .status { color: #aaa; margin-top: 12px; min-height: 20px; }
</style>
</head>
<body>
  <div class="panel">
    <h2>Shop</h2>
    <div class="balance">Balance: <span id="bal">0</span> emeralds</div>
    <button onclick="buy('minecraft:diamond_sword', 10)">Diamond Sword (10)</button>
    <button onclick="buy('minecraft:golden_apple', 5)">Golden Apple (5)</button>
    <div class="status" id="status"></div>
    <button onclick="window.cnpc.close()">Close</button>
  </div>
  <script>
    var data = window.cnpc.initData
    document.getElementById('bal').textContent = data.balance || 0

    function buy(itemId, price) {
      document.getElementById('status').textContent = 'Buying...'
      window.cnpc.sendEvent('buy', {itemId: itemId, price: price, qty: 1})
    }

    window.cnpc.onEvent('buyResult', function(result) {
      if (result.success) {
        document.getElementById('bal').textContent = result.balance
        document.getElementById('status').textContent = 'Purchased!'
      } else {
        document.getElementById('status').textContent = result.error || 'Failed'
      }
      setTimeout(function() {
        document.getElementById('status').textContent = ''
      }, 2000)
    })
  </script>
</body>
</html>
```

---

### HTML Capabilities

Since the GUI runs in a real Chromium browser, you have full access to:

- **Modern CSS** — flexbox, grid, animations, transitions, gradients, backdrop-filter
- **Modern JavaScript** — ES6+, fetch, promises, async/await (only the HTML side; CNPC scripts are ES5)
- **Canvas / WebGL** — draw 2D/3D graphics (games, charts, visualizations)
- **Text inputs** — `<input>`, `<textarea>`, `<select>` all work normally
- **Audio** — `<audio>` elements and Web Audio API (though MC sounds via `world.playSoundAt()` is recommended)

<div class="warn-box">
<strong>No localStorage.</strong> HTML runs from <code>data:</code> URLs which don't support localStorage/sessionStorage. Use <code>sendEvent</code> to persist data server-side via CNPC's <code>storeddata</code>.
</div>

---

### Entity Display

Render full Minecraft entities (NPCs, players, mobs) inside your HTML GUI. Entities render with their full custom skin, equipment, and model — using CNPC's native entity renderer.

#### Setup

1. **Server script** — pass entity IDs in `overlayEntities` (with optional display options):

```javascript
cnpcext.openHtmlGui(e, "dialogue.html", 0, 0, JSON.stringify({
    overlayEntities: [
        {slot: 0, entityId: cnpcext.entityId(e.npc)},
        {slot: 1, entityId: cnpcext.entityId(e.player), rotation: 90, followCursor: false, animate: false}
    ]
}))
```

2. **HTML** — add `data-mc-entity` attributes with the slot number:

```html
<div data-mc-entity="0" style="width: 150px; height: 210px;"></div>
<div data-mc-entity="1" style="width: 150px; height: 210px;"></div>
```

The entity renders at the element's position and size. Resize or reposition the element with CSS to control where and how big the entity appears.

#### `cnpcext.entityId(entity)`

Extracts the network entity ID from any CNPC IEntity wrapper.

- **Input**: `e.npc`, `e.player`, or any CNPC entity wrapper
- **Returns**: `int` — the network entity ID, or `-1` if extraction fails

#### Behavior

- Entity head tracks the mouse cursor (`followCursor = true` by default)
- Entity is rendered with CNPC's `CustomGuiEntityDisplay.drawEntity()`
- The entity's feet anchor at the **bottom-center** of the `data-mc-entity` div
- To hide an entity, set the div's `width` and `height` to `0` (CSS `opacity: 0` alone won't hide it — the renderer ignores opacity)
- Works in both HTML GUIs and HUD overlays

#### Per-Entity Display Options

Each entity entry supports optional display options:

| Option | Default | Description |
|--------|---------|-------------|
| `rotation` | `180` | Y rotation in degrees. 180 = facing camera, 0 = facing away, 90 = left profile |
| `followCursor` | `true` | Entity head tracks mouse cursor. Set `false` for static pose |
| `animate` | `true` | Living animations (idle bobbing, arm swing, walk cycle). Set `false` to freeze |

<div class="info-box">
<strong>Fabric 1.21.1 only.</strong> Entity overlays are not yet available on Forge 1.20.1.
</div>
