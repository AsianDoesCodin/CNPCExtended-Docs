---
layout: default
title: Examples
---

## Examples

### Simple Dirt Giver

**Script:**
```javascript
function interact(e) {
    cnpcext.openHtmlGui(e, "dirt.html", 0, 0, JSON.stringify({
        name: e.player.getDisplayName()
    }))
}

function htmlGuiEvent(e) {
    if (e.eventName === "giveDirt") {
        e.player.giveItem("minecraft:dirt", 64)
        e.player.message("§a+64 Dirt!")
    }
}
```

**HTML (`dirt.html`):**
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
  button { padding: 10px 20px; cursor: pointer; background: #333;
           color: white; border: 1px solid #c9a83e; border-radius: 4px; }
</style>
</head>
<body>
  <div class="panel">
    <h2>Free Dirt!</h2>
    <button onclick="window.cnpc.sendEvent('giveDirt', {})">Get 64 Dirt</button>
    <button onclick="window.cnpc.close()">Close</button>
  </div>
</body>
</html>
```

---

### Credit-Based Shop with Server Push

**Script:**
```javascript
function interact(e) {
    var balance = parseInt(e.player.getStoreddata().get("shopBalance") || "0")
    cnpcext.openHtmlGui(e, "shop.html", 0, 0, JSON.stringify({
        balance: balance,
        items: [
            {id: "sword", mc: "minecraft:diamond_sword", name: "Diamond Sword", price: 10},
            {id: "apple", mc: "minecraft:golden_apple", name: "Golden Apple", price: 5}
        ]
    }))
}

function htmlGuiEvent(e) {
    var data = JSON.parse(e.data)
    var sd = e.player.getStoreddata()
    var balance = parseInt(sd.get("shopBalance") || "0")
    var bridge = cnpcext.getClientBridge(e.player.getMCEntity())

    if (e.eventName === "deposit") {
        var emeralds = e.player.inventoryItemCount("minecraft:emerald")
        var amount = Math.min(data.amount || 0, emeralds)
        if (amount > 0) {
            e.player.removeItem("minecraft:emerald", amount)
            balance += amount
            sd.put("shopBalance", "" + balance)
        }
        bridge.sendToBrowser("balanceUpdate", JSON.stringify({balance: balance}))
    }

    if (e.eventName === "buy") {
        var cost = data.price * data.qty
        if (balance >= cost) {
            balance -= cost
            sd.put("shopBalance", "" + balance)
            e.player.giveItem(data.mc, data.qty)
            bridge.sendToBrowser("buyResult", JSON.stringify({
                success: true, balance: balance
            }))
        } else {
            bridge.sendToBrowser("buyResult", JSON.stringify({
                success: false, error: "Not enough credits"
            }))
        }
    }
}
```

---

### Show GUI to Another Player

Send a notification to all other players on the server:

```javascript
function interact(e) {
    var world = e.player.getWorld()
    var players = world.getAllPlayers()
    for (var i = 0; i < players.length; i++) {
        var target = players[i]
        if (target.getDisplayName() !== e.player.getDisplayName()) {
            cnpcext.openHtmlGui(target, "alert.html", 0, 0, JSON.stringify({
                from: e.player.getDisplayName(),
                message: "Hello from across the server!"
            }))
        }
    }
}
```

---

### Player Script with Keybind

Open an admin panel when a player presses H:

```javascript
function keyPressed(e) {
    if (e.key === 72) {
        cnpcext.openHtmlGui(e, "admin_panel.html", 0, 0, JSON.stringify({
            admin: e.player.getDisplayName()
        }))
    }
}

function htmlGuiEvent(e) {
    var data = JSON.parse(e.data)
    if (e.eventName === "teleport") {
        e.player.setPos(data.x, data.y, data.z)
    }
    if (e.eventName === "giveItem") {
        e.player.giveItem(data.item, data.count)
    }
}
```

---

### Item Overlays in a Scrollable List

```javascript
function interact(e) {
    var overlayItems = []
    var items = ["minecraft:diamond_sword", "minecraft:iron_sword",
                 "minecraft:golden_apple", "minecraft:netherite_helmet",
                 "minecraft:elytra", "minecraft:totem_of_undying"]
    for (var i = 0; i < items.length; i++) {
        overlayItems.push({slot: i, item: items[i], count: 1})
    }
    cnpcext.openHtmlGui(e, "overlay_list.html", 0, 0, JSON.stringify({
        overlayItems: overlayItems
    }))
}
```

**HTML (`overlay_list.html`):**
```html
<div class="scroll-container" data-mc-clip style="height:200px; overflow-y:auto;">
  <div class="row"><div data-mc-slot="0" style="width:24px;height:24px;display:inline-block;"></div> Diamond Sword</div>
  <div class="row"><div data-mc-slot="1" style="width:24px;height:24px;display:inline-block;"></div> Iron Sword</div>
  <div class="row"><div data-mc-slot="2" style="width:24px;height:24px;display:inline-block;"></div> Golden Apple</div>
  <div class="row"><div data-mc-slot="3" style="width:24px;height:24px;display:inline-block;"></div> Netherite Helmet</div>
  <div class="row"><div data-mc-slot="4" style="width:24px;height:24px;display:inline-block;"></div> Elytra</div>
  <div class="row"><div data-mc-slot="5" style="width:24px;height:24px;display:inline-block;"></div> Totem of Undying</div>
</div>
```

---

### Query Client Settings

```javascript
function interact(e) {
    var Consumer = Java.type("java.util.function.Consumer")
    var bridge = cnpcext.getClientBridge(e.player.getMCEntity())

    bridge.queryVideoSettings(Java.extend(Consumer, {
        accept: function(tag) {
            e.player.message("§e--- Your Settings ---")
            e.player.message("§7FOV: §f" + tag.getInt("fov"))
            e.player.message("§7Render Distance: §f" + tag.getInt("renderDistance"))
            e.player.message("§7Graphics: §f" + tag.getString("graphicsMode"))
        }
    }))
}
```
