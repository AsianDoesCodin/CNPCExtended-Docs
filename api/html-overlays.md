---
layout: default
title: HTML Overlays (HUD)
---

## HTML Overlays (HUD Layer)

Render HTML on the game HUD. Overlays **don't capture input** — the game stays fully playable. Use for: skill bars, HP/mana bars, quest trackers, minimap frames, cinematic bars.

**Requires**: MCEF mod on client. Fabric 1.21.1 only (Forge planned).

---

### Opening an Overlay

Two approaches — convenience methods on `cnpcext` or full control via `bridge`:

```javascript
// Convenience (extracts player from event automatically)
cnpcext.openOverlay(e, "skillbar", "skillbar.html", 0.5, 0.92, 260, 80, JSON.stringify({
    skills: [{name: "Fireball", icon: "🔥", key: "1"}],
    hp: e.player.getHealth(),
    maxHp: e.player.getMaxHealth()
}))

// Full control via bridge
var bridge = cnpcext.getClientBridge(e.player.getMCEntity())
bridge.openOverlay("skillbar", "skillbar.html", 0.5, 0.92, 260, 80, jsonData)

// Persistent overlay (survives relog) — 8th parameter
bridge.openOverlay("hud", "hud.html", 0.5, 0.95, 400, 60, jsonData, true)
```

**Position values:**
- `x`, `y` in range `0.0–1.0` = percentage of screen (`0.5` = center)
- `x`, `y` > `1` = raw pixel coordinates

---

### Updating an Overlay

Push data to the overlay's JS. Triggers `window.cnpc.onEvent("overlayUpdate", data)`.

**Automatic dedup**: if data hasn't changed since last call, no packet is sent. Safe to call every tick.

```javascript
function tick(e) {
    cnpcext.updateOverlay(e, "skillbar", JSON.stringify({
        hp: Math.round(e.player.getHealth()),
        maxHp: Math.round(e.player.getMaxHealth()),
        selected: getSelectedSkill(e.player)
    }))
}
```

---

### Hide / Show / Close

```javascript
cnpcext.hideOverlay(e, "hud")      // hide (still in memory)
cnpcext.showOverlay(e, "hud")      // show again
cnpcext.closeOverlay(e, "hud")     // destroy

// Check if exists before opening
if (!cnpcext.hasOverlay(e, "skillbar")) {
    cnpcext.openOverlay(e, "skillbar", "skillbar.html", 0.5, 0.92, 260, 80, "{}")
}
```

---

### Overlay HTML Template

Same `window.cnpc` bridge as HTML GUIs. Key difference: use `background: transparent`.

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        body { background: transparent; font-family: Arial; overflow: hidden; }
        .bar { background: rgba(0,0,0,0.6); border-radius: 8px; padding: 6px; }
        .hp { height: 8px; background: linear-gradient(90deg, #f33, #f66); border-radius: 4px; }
    </style>
</head>
<body>
    <div class="bar">
        <div class="hp" id="hpBar" style="width: 100%"></div>
    </div>
    <script>
        var hp = window.cnpc.initData.hp || 20
        var maxHp = window.cnpc.initData.maxHp || 20

        window.cnpc.onEvent("overlayUpdate", function(d) {
            if (d.hp !== undefined) hp = d.hp
            if (d.maxHp !== undefined) maxHp = d.maxHp
            document.getElementById("hpBar").style.width = (hp/maxHp*100) + "%"
        })

        // Send events back to server
        window.cnpc.sendEvent("skillUse", {index: 0})
    </script>
</body>
</html>
```

---

### Limits

| Limit | Value |
|-------|-------|
| Max simultaneous overlays | 8 |
| Input capture | None (game stays playable) |
| Cleanup | Auto-closed on disconnect |
| Persistent overlays | Re-open on relog |

---

### Key Differences from HTML GUI

| Property | HTML GUI | HTML Overlay |
|----------|----------|-------------|
| Input capture | Full (mouse + keyboard) | None |
| Pauses game | Depends on `isPauseScreen` | Never |
| Max instances | 1 | 8 |
| Position | Fullscreen | Configurable (%, px) |
| Use case | Menus, shops, dialogs | HUD elements, bars |

---

### Cutscene Pattern

Combine overlay hiding with vanilla HUD hiding for cinematic effect:

```javascript
function startCutscene(e) {
    cnpcext.hideOverlay(e, "hud")
    cnpcext.hideHudElement(e, "all")
    cnpcext.openOverlay(e, "cinematic", "cinematic_bars.html", 0, 0, 400, 400, "{}")
}

function endCutscene(e) {
    cnpcext.showOverlay(e, "hud")
    cnpcext.showHudElement(e, "all")
    cnpcext.closeOverlay(e, "cinematic")
}
```

<div class="info-box">
<strong>Vanilla HUD Hiding</strong> — see <a href="{{ '/feature-matrix' | relative_url }}">Feature Matrix</a> for the full list of hideable HUD elements.
</div>
