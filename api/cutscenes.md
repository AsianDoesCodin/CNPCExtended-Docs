---
layout: default
title: Cutscene System
---

## Cutscene System

Keyframe-based camera cutscenes with a visual HTML editor, smooth interpolation, fade transitions, and player protection. Create cutscenes in-game, edit with a timeline GUI, play via script or command.

**Requires**: Fabric 1.21.1 (Forge planned). MCEF for the editor GUI.

---

### Creating Cutscenes

```
/cnpcext cutscene create <name>          — Create + open editor
/cnpcext cutscene edit <name>            — Open editor for existing
/cnpcext cutscene delete <name>          — Delete
/cnpcext cutscene list                   — List all saved
```

### Playing Cutscenes (Commands)

```
/cnpcext cutscene play <name>            — Preview on yourself
/cnpcext cutscene play <name> <player>   — Play on another player
/cnpcext cutscene stop                   — Stop your cutscene
/cnpcext cutscene stop <player>          — Stop a player's cutscene
```

---

### Script API

```javascript
// Play a saved cutscene
cnpcext.startCutscene(player, "village_intro")

// With options
cnpcext.startCutscene(player, "village_intro", JSON.stringify({
    speed: 1.5,        // playback speed multiplier (default 1.0)
    hideHud: true,     // hide all HUD elements (default true)
    protect: true,     // freeze + invulnerable (default true)
    bars: true         // show cinematic black bars (default false)
}))

// Control
cnpcext.stopCutscene(player)         // stop + restore player
cnpcext.pauseCutscene(player)        // freeze timeline
cnpcext.resumeCutscene(player)       // continue from pause
cnpcext.isInCutscene(player)         // returns boolean

// Ad-hoc camera (no saved cutscene needed)
cnpcext.moveCamera(player, JSON.stringify({
    keyframes: [
        {x: 100, y: 70, z: -200, pitch: -15, yaw: 90, travelTicks: 0, holdTicks: 10},
        {x: 120, y: 80, z: -180, pitch: -30, yaw: 45, travelTicks: 60, holdTicks: 0}
    ],
    protect: true
}))
```

---

### Phase Events

The `cutscene(e)` handler fires at each keyframe arrival on the script that started the cutscene:

```javascript
function cutscene(e) {
    var name = e.cutsceneName   // "village_intro"
    var phase = e.phase         // keyframe index (0-based), or -1 for end

    if (name === "village_intro") {
        if (phase === 0) {
            // First keyframe — start NPC animation
        }
        if (phase === 2) {
            // Third keyframe — trigger dialogue
            cnpcext.pauseCutscene(e.player)
            cnpcext.openHtmlGui(e, "dialogue.html", 0, 0, JSON.stringify({text: "Welcome!"}))
        }
        if (phase === -1) {
            // Cutscene ended
        }
    }
}

function htmlGuiEvent(e) {
    if (e.eventName === "dialogue_done") {
        cnpcext.resumeCutscene(e.player)
    }
}
```

---

### Keyframe Properties

| Property | Type | Description |
|----------|------|-------------|
| `x, y, z` | number | Camera world position |
| `pitch, yaw` | number | Camera look direction (degrees) |
| `travelTicks` | int | Ticks to travel from previous keyframe (0 = instant) |
| `holdTicks` | int | Ticks to hold at this position before advancing |
| `transition` | string | `"travel"` (smooth interpolation) or `"fade"` (fade to black) |
| `fadeTicks` | int | Fade duration for `"fade"` transitions (default 20) |

---

### Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `speed` | float | 1.0 | Playback speed multiplier |
| `hideHud` | boolean | true | Hide all vanilla HUD elements |
| `protect` | boolean | true | Freeze player (speed 0) + invulnerable |
| `bars` | boolean | false | Show cinematic letterbox bars |

---

### Features

- **Catmull-Rom interpolation** — smooth spline curves between keyframes
- **FOV locked** — speed modifiers don't affect FOV during cutscene
- **Hand hidden** — player's held item is not rendered
- **Mouse look blocked** — camera is fully script-controlled
- **Disconnect failsafe** — player state saved to file, restored on rejoin
- **Timeout safety** — auto-stops after max duration + buffer

### Storage

Cutscenes are saved as JSON files at `<world>/cnpcextended/cutscenes/<name>.json`. Loaded automatically on server start.
