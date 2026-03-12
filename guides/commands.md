---
layout: default
title: Commands
---

## Commands

<span class="badge badge-version">New in v1.1.0</span>

CNPCExtended adds the `/cnpcext` command for managing global preloading and checking mod status.

All commands require **OP level 2** (operator permissions).

---

### `/cnpcext status`

Show the current state of global preloading for this world.

**Output includes:**
- Whether the world has been initialized by CNPCExtended
- Initialization date and version
- Number of global scripts in `config/cnpcextended/global_scripts/`
- Number of NPC data files in `config/cnpcextended/global_cnpc/`
- Current config values (scripts enabled, NPC data enabled, overwrite mode)

**Example output:**
```
--- CNPCExtended Status ---
World initialized: Yes
  version=1.1.0
  date=2026-03-08
Global scripts: 3 .js files
Global NPC data: 12 files
Config: scripts=ON, npcData=ON, overwrite=NO
```

---

### `/cnpcext sync`

Re-run the global preloader on the current world. Copies new files from the config template without overwriting existing files.

Use this after:
- Adding new scripts to `global_scripts/`
- Adding new NPC data to `global_cnpc/`
- If the initial preload was skipped for some reason

**Output:**
```
Syncing global content...
Sync complete: 2 scripts, 5 NPC data files (scripts registered)
```

---

### `/cnpcext sync force`

Same as `sync`, but **overwrites all existing files** with the global template — regardless of the `overwriteExisting` config setting.

<div class="warn-box">
<strong>Destructive:</strong> This will replace any per-world edits to scripts and NPC data with the global template versions. Use with caution on worlds where you've customized things locally.
</div>

---

### `/cnpcext version`

Display the mod version.

```
CNPCExtended v1.1.0 — MC 1.20.1 Forge
```

---

### `/cnpcext command create <name> [argDefs]`

Create a **persistent** custom `/` command. Saved to `world/customnpcs/cnpcextended/commands.json` — survives server restarts.

| Parameter | Description |
|-----------|-------------|
| `name` | Command name (alphanumeric + underscore) |
| `argDefs` | Optional argument definitions (see format below) |

**Argument definition format:**

Each argument is `type:name` or `type:name=options`, separated by spaces:

| Type | Syntax | Example |
|------|--------|---------|
| String | `string:name` | `string:action` |
| String + suggestions | `string:name=opt1,opt2` | `string:action=open,list,sell` |
| Integer + range | `integer:name=min-max` | `integer:amount=1-10000` |
| Player | `player:name` | `player:target` |
| Boolean | `boolean:name` | `boolean:enabled` |

**Examples:**

```
/cnpcext command create coins
/cnpcext command create shop string:action=open,list,sell
/cnpcext command create pay player:target integer:amount=1-10000
/cnpcext command create teleport player:target string:location=spawn,home,arena
```

After creation, players can use the commands with full tab-completion:
```
/coins
/shop open
/pay Steve 100
```

Handle them in a player script's `customCommand(e)` function. See [Script API]({{ '/api/script-api' | relative_url }}).

---

### `/cnpcext command delete <name>`

Delete a registered command. Tab-completes existing command names.

```
/cnpcext command delete shop
```

---

### `/cnpcext command list`

List all registered script commands (both persistent and runtime).

```
--- Script Commands (3) ---
  /coins
  /shop
  /pay
```

---

### Summary

| Command | Permission | Description |
|---------|:----------:|-------------|
| `/cnpcext status` | OP 2 | Show preload status and config |
| `/cnpcext sync` | OP 2 | Re-copy global content (skip existing) |
| `/cnpcext sync force` | OP 2 | Re-copy global content (overwrite all) |
| `/cnpcext version` | OP 2 | Show mod version |
| `/cnpcext command create <name> [args]` | OP 2 | Create a persistent custom command |
| `/cnpcext command delete <name>` | OP 2 | Delete a command |
| `/cnpcext command list` | OP 2 | List all registered commands |
| `/cnpcext commands` | OP 2 | Shorthand for command list |
