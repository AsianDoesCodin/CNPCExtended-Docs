---
layout: default
title: Item Overlays
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
  <div class="item-cell">
    <div data-mc-slot="2" style="width:32px; height:32px;"></div>
    <span>Netherite Helmet</span>
  </div>
  <div class="item-cell">
    <div data-mc-slot="3" style="width:32px; height:32px;"></div>
    <span>Enchanted Book</span>
  </div>
</div>
```

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

The bridge JS automatically detects the `data-mc-clip` container and reports its bounds to Java, which uses GL scissoring to clip overlay rendering.

---

### Key Rules

| Rule | Details |
|------|---------|
| Slot matching | `data-mc-slot="N"` must match the `slot` index in `overlayItems` |
| Key name | Use `overlayItems` in initData — not `items` (that's for your own data) |
| Sizing | Items scale to match the HTML element dimensions |
| Tooltips | Hovering a rendered item shows the vanilla MC tooltip |
| Clipping | Add `data-mc-clip` to a scrollable parent to enable scissoring |
| Re-render | Items only render while the page is open; positions update every frame |

<div class="info-box">
<strong>Entity overlays</strong> (<code>data-mc-entity</code>) are planned for a future version.
</div>

---

### Works in HUD Overlays

Item overlays and `data-mc-clip` also work in HUD overlays opened via `bridge.openOverlay()`. Use the same `overlayItems` format in the overlay's `initData` and `data-mc-slot` elements in the overlay HTML.
