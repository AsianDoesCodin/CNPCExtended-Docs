---
layout: default
title: Quick Start
---

## Quick Start

Build your first HTML GUI in 5 minutes.

### 1. Create the HTML file

Save this as `<world>/customnpcs/scripts/ecmascript/my_gui.html`:

```html
<!DOCTYPE html>
<html>
<head>
<style>
  body {
    background: transparent;
    color: white;
    font-family: sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
  }
  .panel {
    background: rgba(0, 0, 0, 0.85);
    padding: 30px;
    border-radius: 8px;
    border: 2px solid #c9a83e;
    text-align: center;
  }
  button {
    padding: 10px 20px;
    margin: 8px;
    cursor: pointer;
    background: #333;
    color: white;
    border: 1px solid #c9a83e;
    border-radius: 4px;
    font-size: 14px;
  }
  button:hover {
    background: #555;
    border-color: #f0d060;
  }
</style>
</head>
<body>
  <div class="panel">
    <h2 id="title">Hello!</h2>
    <p>Click a button to test the event system:</p>
    <button onclick="window.cnpc.sendEvent('greet', {})">Say Hi</button>
    <button onclick="window.cnpc.sendEvent('giveDirt', {})">Get 64 Dirt</button>
    <button onclick="window.cnpc.close()">Close</button>
  </div>
  <script>
    var data = window.cnpc.initData
    if (data && data.name) {
      document.getElementById('title').textContent = 'Welcome, ' + data.name
    }
  </script>
</body>
</html>
```

### 2. Create the NPC script

Set an NPC's script language to `ecmascript` and add this code:

```javascript
function interact(e) {
    var initData = JSON.stringify({
        name: e.player.getDisplayName()
    })
    cnpcext.openHtmlGui(e, "my_gui.html", 0, 0, initData)
}

function htmlGuiEvent(e) {
    var name = e.eventName

    if (name === "greet") {
        e.npc.say("Hello, " + e.player.getDisplayName() + "!")
    }

    if (name === "giveDirt") {
        e.player.giveItem("minecraft:dirt", 64)
        e.player.message("\u00a7a+64 Dirt added to your inventory!")
    }
}
```

### 3. Test it

1. Right-click the NPC
2. The HTML GUI opens with your player name
3. Click **Say Hi** — the NPC speaks
4. Click **Get 64 Dirt** — dirt appears in your inventory
5. Click **Close** or press ESC to close

### What Just Happened

1. `interact(e)` called `cnpcext.openHtmlGui(e, ...)` — this stored the event context (player, NPC, ScriptContainer) and sent the HTML to the client
2. MCEF rendered the HTML in Chromium inside Minecraft
3. When you clicked a button, `window.cnpc.sendEvent()` sent a message back to the server
4. The server routed it to `htmlGuiEvent(e)` on the same ScriptContainer, with the original `e.player` and `e.npc`

<div class="info-box">
The HTML runs in a real browser (Chromium) on the client. It has no access to Java or CNPC APIs. It can only communicate with the server script via <code>sendEvent</code> / <code>onEvent</code>.
</div>
