---
layout: default
title: Event Flow
---

## Event Flow

How events travel between the CNPC script (server) and the HTML GUI (client).

---

### Full Chain: HTML Button → Server Script

<div class="flow-diagram">1. HTML:     user clicks button
2. HTML:     window.cnpc.sendEvent("buy", {id: "sword"})
3. Bridge:   queues event → rAF flushes → console.log("CNPC:{ev:[...]}")
4. MCEF:     CefDisplayHandler.onConsoleMessage() fires
5. Client:   BrowserGuiScreen parses JSON → extracts events
6. Network:  PacketClientEvent("htmlGuiEvent", {eventName, eventData}) → server
7. Server:   ServerEventDispatcher → ScriptIntegration.fireHtmlGuiEvent()
8. Script:   ScriptContainer.run("htmlGuiEvent", wrapper) → your function fires
</div>

### Full Chain: Server Push → HTML Update

<div class="flow-diagram">1. Script:   bridge.sendToBrowser("result", JSON.stringify({ok: true}))
2. Server:   PacketClientScriptAction(SEND_TO_BROWSER, data) → client
3. Client:   ClientActionHandler → BrowserManager.sendJsonEventToBrowser()
4. MCEF:     cefBrowser.executeJavaScript("window.cnpc._dispatchEvent(...)")
5. HTML:     window.cnpc.onEvent("result", callback) → callback({ok: true})
</div>

---

### Session Lifecycle

```
cnpcext.openHtmlGui(e, "gui.html", ...)
    │
    ├─ Session created: stores player, npc, API, ScriptContainer
    ├─ Keyed by player UUID
    │
    ├─ (events flow back and forth)
    │
    └─ GUI closes (ESC, window.cnpc.close(), or server calls bridge.closeHtmlGui())
        │
        ├─ "__guiClosed" event fires on script
        └─ Session removed from map
```

- **One session per player** — opening a new GUI replaces the previous session
- **ScriptContainer captured** — the script that was running when `openHtmlGui` was called receives all future events
- **Player disconnect** — sessions are cleaned up on logout

---

### Communication Channel

The bridge uses `console.log("CNPC:" + json)` to send data from the browser to Java:

```json
{
  "ov": [{"s": 0, "x": 100, "y": 50, "w": 32, "h": 32}],
  "ev": [{"n": "buy", "d": {"id": "sword"}}],
  "cl": false,
  "clip": {"x": 10, "y": 40, "w": 400, "h": 300}
}
```

| Key | Purpose |
|-----|---------|
| `ov` | Overlay item positions (from `data-mc-slot` elements) |
| `ev` | Pending events (flushed each animation frame) |
| `cl` | Close request flag |
| `clip` | Clip rectangle for scroll container (from `data-mc-clip`) |

This is all handled automatically by the injected bridge JS — you never need to write `console.log("CNPC:...")` yourself.
