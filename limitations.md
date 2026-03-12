---
layout: default
title: Known Limitations
---

## Known Limitations

### 1. MCEF Required on Client

If MCEF isn't installed, HTML GUIs won't open. There's no fallback to CNPC's built-in `ICustomGui`. Players without MCEF will see nothing.

### 2. One GUI Per Player

Opening a new HTML GUI closes the previous one. It's a Minecraft `Screen` — only one can be active at a time.

### 3. No localStorage

HTML runs from `data:` URLs which don't support `localStorage` or `sessionStorage`. Use `window.cnpc.sendEvent()` to persist data server-side via CNPC's `storeddata`.

### 4. ES5 Only for CNPC Scripts

NPC/Player/Block/Item scripts run in GraalJS with **ES5 syntax** — no `let`, `const`, arrow functions, or template literals. The HTML browser side runs full modern JavaScript (ES6+).

### 5. CompoundTag Not Accessible in Scripts

Methods like `putString()` throw TypeError when called from GraalJS scripts. Always use the **JSON string overloads**:

```javascript
// Don't do this:
var tag = new CompoundTag()  // won't work in scripts

// Do this:
cnpcext.openHtmlGui(e, "gui.html", 0, 0, JSON.stringify({key: "value"}))
bridge.sendToBrowser("event", JSON.stringify({data: 123}))
```

### 6. Event Name Restrictions

Event names must match `[a-zA-Z0-9_]+`. Names with spaces, hyphens, or special characters are rejected by the server.

### 7. Packet Size

The entire HTML file (with injected bridge JS) is Base64-encoded in one network packet. Keep HTML files under ~100KB. For larger GUIs, load external CSS/JS from a CDN or split into multiple files.

### 8. Session Lifetime

The event routing session lasts until the GUI is closed or the player disconnects. Opening a new GUI for the same player replaces the previous session. There's no way to have multiple simultaneous sessions per player.

### 9. Entity Overlays Not Yet Available

Item overlays (`data-mc-slot`) work. Entity rendering (`data-mc-entity`) is planned for a future version. Use CNPC's built-in `addEntityDisplay()` for entity displays in native GUIs.

### 10. Queries Are Read-Only

Client settings (FOV, render distance, volume, keybinds, etc.) can be **queried** but not **changed** from the server.
