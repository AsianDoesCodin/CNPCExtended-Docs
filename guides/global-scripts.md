---
layout: default
title: Global Scripts
---

## Global Player Scripts

<span class="badge badge-version">New in v1.1.0</span>

Automatically inject player scripts into every new world. Place `.js` files in a config folder — they get copied into the world's script directory and registered in CNPC's player script system.

---

### Setup

Create the folder structure inside your Minecraft instance:

```
<minecraft>/config/cnpcextended/
    global_scripts/
        player_main.js
        chat_commands.js
        keybind_handler.js
        shop.html
        admin_panel.html
```

That's it. On the next new world creation (or first load with the mod), CNPCExtended will:

1. Copy all `.js` and `.html` files from `global_scripts/` into `<world>/customnpcs/scripts/ecmascript/`
2. Create or update `<world>/customnpcs/scripts/player_scripts.json`
3. Set `ScriptEnabled` to true and register each `.js` script in `ScriptList`

<div class="info-box">
<strong>HTML files</strong> are copied alongside scripts so your HTML GUIs are available in every world. They are <strong>not</strong> registered in player_scripts.json (only .js files are) — they’re just placed in the ecmascript folder where <code>cnpcext.openHtmlGui()</code> can find them.
</div>

---

### How It Works

CNPC stores player script registrations in `player_scripts.json`:

```json
{
    "ScriptEnabled": "1b",
    "ScriptLanguage": "ECMAScript",
    "Scripts": [
        {
            "Script": "",
            "Console": [],
            "ScriptList": [
                {"Line": "player_main.js"},
                {"Line": "chat_commands.js"}
            ]
        }
    ]
}
```

CNPCExtended **merges** into this file — it won't remove existing scripts or overwrite entries that are already registered. If a world already has player scripts, your global scripts get added alongside them.

---

### Configuration

In `config/cnpcextended-common.toml`:

```toml
[global]
    # Enable global player scripts
    enableGlobalScripts = true
    
    # Overwrite existing script files (false = skip if file exists)
    overwriteExisting = false
```

---

### Behavior Details

| Scenario | Behavior |
|----------|----------|
| New world, first load | Scripts copied + registered automatically |
| Existing world, first load with mod | Scripts copied + registered (one-time) |
| World already initialized | Skipped (use `/cnpcext sync` to re-run) |
| Script file already exists in world | Skipped (unless `overwriteExisting = true`) |
| Script already in `player_scripts.json` | Not duplicated |

---

### Re-syncing

After adding new scripts to `global_scripts/`, use the command to push them to the current world:

```
/cnpcext sync          ← copy new files, skip existing
/cnpcext sync force    ← overwrite everything
```

<div class="warn-box">
<strong>Important:</strong> CNPC loads scripts from <code>player_scripts.json</code> on world load. After syncing, you may need to <strong>reload the world</strong> (or use <code>/noppes script reload</code>) for CNPC to pick up the new scripts.
</div>

---

### Example: Global Chat Handler

Place this in `config/cnpcextended/global_scripts/chat_handler.js`:

```javascript
function chat(e) {
    var msg = e.message
    if (msg === "!info") {
        e.player.message("§eCNPCExtended v1.1.0")
        e.player.message("§7Type !help for commands")
        e.setCanceled(true)
    }
}
```

Every new world will automatically have this chat handler active for all players.
