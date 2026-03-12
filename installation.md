---
layout: default
title: Installation
---

## Installation

### Prerequisites

- Minecraft **1.20.1** with **Forge 47+**
- [CustomNPCs Unofficial](https://www.curseforge.com/minecraft/mc-mods/customnpcs-unofficial) installed
- [MCEF](https://www.curseforge.com/minecraft/mc-mods/mcef) installed (client-side)

### Steps

1. Download the latest `cnpcextended-*.jar`
2. Place it in your `mods/` folder
3. Launch the game

**For servers:** The mod must be on both server and client. HTML files are stored on the server; MCEF renders them on the client.

### Verify

In the game log you should see:

```
CNPCExtended v1.1.0 loaded — client scripting + MCEF HTML GUI addon
Injected 'cnpcext' into ScriptContainer.Data
```

### File Structure

HTML files go in your world's CNPC scripts folder:

```
<world>/
  customnpcs/
    scripts/
      ecmascript/
        my_gui.html          ← HTML files
        shop.html
        npc_script.js        ← CNPC scripts
```

### Config Folder (v1.1+)

On first launch, CNPCExtended creates:

```
<minecraft>/config/
  cnpcextended-common.toml     ← Forge config (auto-generated)
  cnpcextended/
    global_scripts/            ← Put player .js files here
    global_cnpc/
      clones/                  ← NPC clone templates
      dialogs/                 ← Dialog trees
      linkednpcs/              ← Linked NPC data
      quests/                  ← Quest definitions
```

See [Global Scripts]({{ '/guides/global-scripts' | relative_url }}) and [Global NPC Data]({{ '/guides/global-npc-data' | relative_url }}) for details.

<div class="warn-box">
<strong>Important:</strong> HTML files must be in <code>customnpcs/scripts/ecmascript/</code> within the world save folder. Path traversal (<code>..</code>) is blocked for security.
</div>
