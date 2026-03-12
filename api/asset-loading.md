---
layout: default
title: Asset Loading (cnpc://)
---

## Asset Loading — `cnpc://` Scheme

Load images, CSS, JavaScript, fonts, and other files directly from the scripts folder in your HTML GUIs and overlays.

**Requires**: MCEF mod on client. Fabric 1.21.1 only (Forge planned).

---

### The Problem

HTML GUIs load as `data:` URIs, so relative paths like `<img src="icon.png">` don't resolve to anything. Previously, you had to embed images as Base64 data URIs or use external URLs.

### The Solution

CNPCExtended registers a `cnpc://` custom scheme in the embedded Chromium browser. It serves files directly from the world's scripts folder:

```
cnpc://assets/icon.png
→ <world>/customnpcs/scripts/ecmascript/assets/icon.png
```

---

### Usage

#### In HTML

```html
<!-- Images -->
<img src="cnpc://assets/sword_icon.png">
<div style="background-image: url('cnpc://assets/panel_bg.png')"></div>

<!-- CSS -->
<link rel="stylesheet" href="cnpc://css/theme.css">

<!-- JavaScript -->
<script src="cnpc://js/utils.js"></script>

<!-- Fonts -->
<style>
  @font-face {
    font-family: 'MCFont';
    src: url('cnpc://fonts/minecraft.woff2');
  }
</style>
```

#### Using `window.cnpc.assetUrl`

The base URL is also available programmatically:

```javascript
// window.cnpc.assetUrl = "cnpc://"
var img = document.createElement('img')
img.src = window.cnpc.assetUrl + 'assets/icons/' + skillName + '.png'
document.body.appendChild(img)
```

---

### File Structure

Place your assets anywhere inside the scripts folder:

```
<world>/customnpcs/scripts/ecmascript/
    my_gui.html          ← your GUI file
    skillbar.html        ← your overlay file
    assets/
        sword.png        ← cnpc://assets/sword.png
        panel_bg.png     ← cnpc://assets/panel_bg.png
        icons/
            fire.png     ← cnpc://assets/icons/fire.png
    css/
        theme.css        ← cnpc://css/theme.css
    js/
        utils.js         ← cnpc://js/utils.js
```

---

### Security

- Path traversal (`..`) is blocked — you cannot access files outside the scripts folder
- Backslashes (`\`) are rejected
- Only regular files are served (no directories)
- The scripts path is synced from server to client on join and cleared on disconnect

---

### Supported File Types

Any file type works. MIME types are auto-detected from the extension:

| Extension | MIME Type |
|-----------|----------|
| `.png` | `image/png` |
| `.jpg`, `.jpeg` | `image/jpeg` |
| `.gif` | `image/gif` |
| `.svg` | `image/svg+xml` |
| `.css` | `text/css` |
| `.js` | `application/javascript` |
| `.json` | `application/json` |
| `.woff`, `.woff2` | `font/woff`, `font/woff2` |
| `.mp3`, `.ogg` | `audio/mpeg`, `audio/ogg` |

---

### Works With

| Context | `cnpc://` available? |
|---------|:-------------------:|
| HTML GUI | ✅ |
| HTML Overlay (HUD) | ✅ |
| Persistent Overlay | ✅ |

<div class="info-box">
<strong>Tip:</strong> Use <code>cnpc://</code> paths for images in your overlays — they render faster than Base64-encoded data URIs since the browser can cache the fetched resources.
</div>
