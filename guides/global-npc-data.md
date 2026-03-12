---
layout: default
title: Global NPC Data
---

## Global NPC Data Preloading

<span class="badge badge-version">New in v1.1.0</span>

Pre-populate every new world with your NPC clones, dialog trees, quests, and linked NPC data from a global template folder.

---

### Setup

Create the folder structure inside your Minecraft instance:

```
<minecraft>/config/cnpcextended/
    global_cnpc/
        clones/
            MyNPCs/
                Guard.json
                Merchant.json
        dialogs/
            Villager/
                1.json
                2.json
                3.json
        linkednpcs/
            (linked NPC data files)
        quests/
            MainQuest/
                1.json
                2.json
```

Copy your existing NPC data from any world's `customnpcs/` folder into the matching subfolder under `global_cnpc/`.

---

### Supported Folders

Only these 4 folders are copied:

| Folder | Contents | Source |
|--------|----------|--------|
| `clones/` | Saved NPC templates | Tab-organized subfolders with `.json` files |
| `dialogs/` | Dialog trees | Category subfolders with numbered `.json` files |
| `linkednpcs/` | Linked NPC definitions | `.json` files |
| `quests/` | Quest definitions | Category subfolders with `.json` files |

Other folders like `playerdata/`, `schematics/`, and `scripts/` are **not** copied. Scripts are handled by [Global Scripts]({{ '/guides/global-scripts' | relative_url }}).

---

### How to Export From an Existing World

1. Open your existing world
2. Navigate to `<world>/customnpcs/`
3. Copy the folders you want into `config/cnpcextended/global_cnpc/`:
   - `clones/` → `global_cnpc/clones/`
   - `dialogs/` → `global_cnpc/dialogs/`
   - `linkednpcs/` → `global_cnpc/linkednpcs/`
   - `quests/` → `global_cnpc/quests/`

The folder structure inside each must match exactly — CNPC uses the subfolder names as categories.

---

### Configuration

In `config/cnpcextended-common.toml`:

```toml
[global]
    # Enable NPC data preloading
    enableGlobalNpcData = true

    # Overwrite existing files (false = skip if file exists)
    overwriteExisting = false
```

---

### Behavior Details

| Scenario | Behavior |
|----------|----------|
| New world, first load | All NPC data copied recursively |
| Existing world, first load with mod | Data copied (one-time, doesn't overwrite) |
| World already initialized | Skipped (use `/cnpcext sync` to re-run) |
| File already exists in world | Skipped (unless `overwriteExisting = true`) |
| Empty `global_cnpc/` subfolder | Nothing copied for that folder |

---

### Re-syncing

```
/cnpcext sync          ← copy new files, skip existing
/cnpcext sync force    ← overwrite all files from template
```

<div class="warn-box">
<strong>Clone IDs:</strong> Cloned NPCs reference internal IDs. If you export clones from one world, the IDs should be unique. Avoid mixing clones from different worlds that might have conflicting IDs — use distinct category (tab) names to keep them organized.
</div>

<div class="info-box">
<strong>Tip:</strong> Use this feature to distribute complete NPC setups. Put the mod + your <code>config/cnpcextended/</code> folder in a modpack → every player gets identical NPCs, dialogs, and quests on world creation.
</div>
