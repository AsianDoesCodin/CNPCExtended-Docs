---
layout: default
title: Item & Entity Overlays
---

## MC Item Overlays

Render **real Minecraft items** on top of your HTML GUI — with enchant glint, durability bars, stack counts, and hover tooltips.

---

### How It Works

1. Your script passes item data in `overlayItems` within `initData`
2. HTML contains `<div data-mc-slot="N">` placeholder elements
3. The bridge JS tracks element positions via `getBoundingClientRect()` every frame
4. Java renders real `ItemStack` at those screen coordinates on top of the browser

---

### Setup

#### Server script

```javascript
function interact(e) {
    var initData = JSON.stringify({
        overlayItems: [
            // Simple item ID:
            {slot: 0, item: "minecraft:diamond_sword", count: 1},
            {slot: 1, item: "minecraft:golden_apple", count: 5},
            // Full SNBT (enchantments, custom name, damage, components):
            {slot: 2, nbt: e.player.getMainhandItem().getItemNbt().toJsonString()},
            {slot: 3, item: "minecraft:enchanted_book", count: 1}
        ]
    })
    cnpcext.openHtmlGui(e, "items.html", 0, 0, initData)
}
```

**Item format options:**

| Field | Description |
|-------|-------------|
| `item` | Simple item ID string (e.g. `"minecraft:diamond_sword"`) |
| `count` | Stack count (default 1) |
| `nbt` | Full SNBT string from `getItemNbt().toJsonString()` — preserves enchantments, custom names, damage, all components |

If both `nbt` and `item` are present, `nbt` takes priority.

#### HTML

```html
<div style="display: flex; gap: 12px;">
  <div class="item-cell">
    <div data-mc-slot="0" style="width:32px; height:32px;"></div>
    <span>Diamond Sword</span>
  </div>
  <div class="item-cell">
    <div data-mc-slot="1" style="width:32px; height:32px;"></div>
    <span>Golden Apple x5</span>
  </div>
</div>
```

---

### Item Scaling

Use `data-mc-scale` to resize the rendered item. Default is `1` (16×16 MC pixels). Make the HTML element larger to match:

```html
<!-- Normal size (16×16) -->
<div data-mc-slot="0" style="width:32px; height:32px;"></div>

<!-- 2x scale (32×32 MC pixels) -->
<div data-mc-slot="1" data-mc-scale="2" style="width:64px; height:64px;"></div>

<!-- 3x scale (48×48 MC pixels) -->
<div data-mc-slot="2" data-mc-scale="3" style="width:96px; height:96px;"></div>

<!-- Half size -->
<div data-mc-slot="3" data-mc-scale="0.5" style="width:16px; height:16px;"></div>
```

The item is rendered centered in the HTML element. Enchant glint, durability bars, and stack count decorations all scale with the item.

---

### Scroll Clipping

For scrollable lists, add `data-mc-clip` to the scroll container. Items outside the visible scroll area won't render:

```html
<div class="scroll-list" data-mc-clip
     style="height: 300px; overflow-y: auto;">
  <div class="row">
    <div data-mc-slot="0" style="width:24px; height:24px;"></div>
    <span>Item 1</span>
  </div>
  <div class="row">
    <div data-mc-slot="1" style="width:24px; height:24px;"></div>
    <span>Item 2</span>
  </div>
  <!-- items scrolled out of view are clipped -->
</div>
```

---

## Entity Overlays

Render full CNPC entities (NPCs, players, mobs) on HTML GUIs and HUD overlays. **Fabric 1.21.1 only.**

### Setup

There are two ways to provide entity data:

#### Via NBT (recommended) — entity doesn't need to be spawned

```javascript
cnpcext.openHtmlGui(e, "gui.html", 0, 0, JSON.stringify({
    overlayEntities: [
        {slot: 0, nbt: cnpcext.entityNbt(e.npc)},
        {slot: 1, nbt: cnpcext.entityNbt(e.npc), rotation: 90, followCursor: false}
    ]
}))
```

`cnpcext.entityNbt(entity)` serializes the entity to SNBT. The client creates a standalone entity from this data — it renders even if the original entity despawns, unloads, or was never spawned (clones, `world.createEntity()`).

#### Via entity ID — requires entity to be in render range

```javascript
cnpcext.openHtmlGui(e, "gui.html", 0, 0, JSON.stringify({
    overlayEntities: [
        {slot: 0, entityId: cnpcext.entityId(e.npc)},
        {slot: 1, entityId: cnpcext.entityId(e.player), animate: false}
    ]
}))
```

The entity must be spawned in the world and within the player's render distance. If it despawns or the player moves away, it disappears from the GUI.

#### HTML

```html
<div data-mc-entity="0" style="width:150px; height:210px;"></div>
<div data-mc-entity="1" style="width:100px; height:140px;"></div>
```

### Per-entity options

| Option | Default | Description |
|--------|---------|-------------|
| `rotation` | `180` | Y rotation degrees. `180` = facing camera, `0` = facing away, `90` = left profile |
| `followCursor` | `true` | Head tracks mouse cursor |
| `animate` | `true` | Living animations (idle bobbing, arm swing). `false` = frozen pose |

Entity feet anchor at bottom-center of the div. Size the div to control entity scale.

To hide an entity: set `width: 0; height: 0` (CSS `opacity: 0` won't work — renderer ignores opacity).

---

### Key Rules

| Rule | Details |
|------|---------|
| Slot matching | `data-mc-slot="N"` / `data-mc-entity="N"` must match the `slot` index |
| Key names | Use `overlayItems` for items, `overlayEntities` for entities |
| Scaling | `data-mc-scale="N"` controls item render size (default 1) |
| Tooltips | Hovering a rendered item shows the vanilla MC tooltip |
| Clipping | `data-mc-clip` on a scrollable parent enables scissoring |
| Works everywhere | Both HTML GUIs and HUD overlays support item/entity overlays |

---

## Interactive Overlays (Cursor Unlock)

HUD overlays are non-interactive by default. Use `setOverlayInteractive` to unlock the cursor so the player can click HTML elements (buttons, links, etc).

### Server script

```javascript
var bridge = cnpcext.getClientBridge(e.player.getMCEntity())
bridge.openOverlay("menu", "menu.html", 0, 0, 400, 300, JSON.stringify({items: [...]}))
bridge.setOverlayInteractive("menu", true)   // unlock cursor
// later:
bridge.setOverlayInteractive("menu", false)  // re-lock cursor
```

### Escape key

Player can press Escape to re-lock the cursor (closes the interaction layer, not the overlay).

### Events from overlays

`window.cnpc.sendEvent()` works from interactive overlays. Events fire as `htmlGuiEvent` in the script:

```javascript
function htmlGuiEvent(e) {
    var data = JSON.parse(e.data)
    if (data.__overlayName === "menu") {
        // This event came from the "menu" overlay
    }
}
```

`e.data.__overlayName` identifies which overlay sent the event.

### Close all overlays

```javascript
bridge.closeAllOverlays()  // destroy all overlays for this player
```
