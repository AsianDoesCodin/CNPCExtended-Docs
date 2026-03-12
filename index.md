---
layout: default
title: Home
---

# CNPCExtended

<span class="badge badge-version">v1.2.0</span>
<span class="badge badge-mc">MC 1.20.1 / 1.21.1</span>
<span class="badge badge-forge">Forge 47+</span>
<span class="badge badge-fabric">Fabric 1.21.1</span>

**Extension framework for [CustomNPCs](https://www.curseforge.com/minecraft/mc-mods/custom-npcs).** HTML GUIs, HUD overlays, client queries, custom commands, and global content preloading — all from CNPC scripts.

---

## What It Does

CNPCExtended bridges **CNPC server-side scripts** with **real HTML/CSS/JS** rendered by [MCEF](https://www.curseforge.com/minecraft/mc-mods/mcef-web-browser) (an embedded Chromium browser inside Minecraft).

- **Open HTML GUIs** from any CNPC script (NPC, Player, Block, Item)
- **HTML Overlays** — render HTML on the HUD layer (skill bars, HP bars, quest trackers) without blocking input
- **Hide vanilla HUD** — selectively hide hotbar, health, food, XP, crosshair, chat, etc.
- **Bidirectional events** — HTML sends events to the server, server pushes data back
- **Real MC item overlays** — render actual `ItemStack` with enchant glint, durability bars, tooltips on top of HTML
- **Query client settings** — read FOV, render distance, keybinds, sound volumes, resource packs
- **Custom commands** — register runtime commands from scripts
- **Global preloading** — auto-deploy scripts + NPC data into new worlds
- **Target any player** — open GUIs/overlays on other players, not just the one who triggered the script

## See It In Action

<div style="display: flex; flex-direction: column; gap: 16px; margin: 20px 0;">
  <iframe width="100%" height="315" src="https://www.youtube.com/embed/IEuh_z1yEmw" frameborder="0" allowfullscreen style="border-radius: 8px;"></iframe>
  <iframe width="100%" height="315" src="https://www.youtube.com/embed/icsmLyiY9Rw" frameborder="0" allowfullscreen style="border-radius: 8px;"></iframe>
  <iframe width="100%" height="315" src="https://www.youtube.com/embed/OrKyYy1FwUA" frameborder="0" allowfullscreen style="border-radius: 8px;"></iframe>
</div>

## How It Works

```
CNPC Script (Server/GraalJS)         HTML GUI (Client/Chromium)
━━━━━━━━━━━━━━━━━━━━━━━━━━━         ━━━━━━━━━━━━━━━━━━━━━━━━━━

cnpcext.openHtmlGui(e, "gui.html")
    │ reads HTML from world folder
    │ injects bridge JS
    └── packet ──────────────────→   browser renders HTML
                                     window.cnpc.initData ready
                                          │
                                     user clicks a button
                                     window.cnpc.sendEvent("buy",{})
                                          │
htmlGuiEvent(e) ←────────────────── packet to server
    │
    ├─ e.player.giveItem(...)
    ├─ bridge.sendToBrowser(...)
    │       │
    │       └────────────────────→   window.cnpc.onEvent("result",cb)
    │                                updates HTML dynamically
    │
    └─ continues until GUI closes
```

## Requirements

| Mod | Side | Purpose |
|-----|------|---------|
| [CustomNPCs](https://www.curseforge.com/minecraft/mc-mods/custom-npcs) | Server | Script engine + NPC system |
| [MCEF](https://www.curseforge.com/minecraft/mc-mods/mcef-web-browser) | Client | Embedded Chromium browser |
| **CNPCExtended** | Both | This mod — bridges CNPC scripts with HTML |

<div class="info-box">
<strong>New to CNPCExtended?</strong> Start with the <a href="{{ '/quickstart' | relative_url }}">Quick Start</a> guide.
</div>
