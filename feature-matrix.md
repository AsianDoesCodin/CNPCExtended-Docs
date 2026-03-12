---
layout: default
title: Feature Matrix
---

<style>
  /* ===== Summary Cards ===== */
  .summary-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
    gap: 14px;
    margin: 24px 0 36px;
  }
  .summary-card {
    background: linear-gradient(135deg, var(--bg-card), rgba(42, 34, 64, 0.6));
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 20px 16px;
    text-align: center;
    transition: border-color 0.2s, transform 0.2s;
  }
  .summary-card:hover {
    border-color: var(--gold);
    transform: translateY(-2px);
  }
  .summary-card .num {
    font-size: 32px;
    font-weight: 800;
    background: linear-gradient(135deg, var(--gold), var(--gold-bright));
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    line-height: 1;
  }
  .summary-card .lbl {
    font-size: 11px;
    color: var(--text-muted);
    margin-top: 6px;
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  /* ===== Legend ===== */
  .legend {
    display: flex;
    gap: 24px;
    margin: 0 0 24px;
    font-size: 13px;
    color: var(--text-muted);
    flex-wrap: wrap;
  }
  .legend-item { display: flex; align-items: center; gap: 6px; }

  /* ===== Section Headers ===== */
  .section-hdr {
    display: flex;
    align-items: center;
    gap: 12px;
    margin: 44px 0 18px;
    padding-bottom: 12px;
    border-bottom: 2px solid var(--border);
    flex-wrap: wrap;
  }
  .section-hdr .icon {
    font-size: 22px;
    width: 36px;
    height: 36px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 8px;
    background: rgba(201, 168, 62, 0.08);
  }
  .section-hdr h3 {
    margin: 0 !important;
    padding: 0 !important;
    border: none !important;
    font-size: 19px;
    color: var(--gold);
  }
  .tag {
    display: inline-block;
    font-size: 11px;
    padding: 3px 10px;
    border-radius: 12px;
    font-weight: 600;
    letter-spacing: 0.4px;
    white-space: nowrap;
  }
  .tag-new { background: rgba(80, 200, 120, 0.12); color: #50c878; border: 1px solid rgba(80, 200, 120, 0.25); }
  .tag-fabric { background: rgba(100, 170, 220, 0.1); color: #7fb8e0; border: 1px solid rgba(100, 170, 220, 0.2); }
  .tag-both { background: rgba(201, 168, 62, 0.08); color: var(--gold); border: 1px solid rgba(201, 168, 62, 0.15); }

  .section-desc {
    color: var(--text-muted);
    font-size: 14px;
    margin: -8px 0 16px;
    line-height: 1.5;
  }

  /* ===== Feature Tables ===== */
  .ftable {
    width: 100%;
    border-collapse: separate;
    border-spacing: 0;
    margin: 0 0 8px;
    border-radius: 8px;
    overflow: hidden;
    border: 1px solid var(--border);
  }
  .ftable th {
    background: linear-gradient(180deg, rgba(42, 34, 64, 0.9), rgba(22, 18, 34, 0.95));
    color: var(--gold);
    font-weight: 700;
    text-align: left;
    padding: 12px 16px;
    font-size: 12px;
    text-transform: uppercase;
    letter-spacing: 0.8px;
    border-bottom: 2px solid var(--border);
  }
  .ftable th.center { text-align: center; }
  .ftable td {
    padding: 10px 16px;
    font-size: 14px;
    border-bottom: 1px solid rgba(42, 34, 64, 0.5);
    color: var(--text);
    transition: background 0.1s;
  }
  .ftable tr:last-child td { border-bottom: none; }
  .ftable tr:hover td { background: rgba(201, 168, 62, 0.04); }
  .ftable tr:nth-child(even) td { background: rgba(22, 18, 34, 0.3); }
  .ftable tr:nth-child(even):hover td { background: rgba(201, 168, 62, 0.06); }

  /* Status cells */
  .s { text-align: center; font-size: 18px; width: 110px; }
  .s-yes { color: #50c878; }
  .s-no { color: rgba(255,255,255,0.15); }
  .s-na { color: #e06060; }

  .feat-name { font-family: 'Cascadia Code', 'Fira Code', monospace; font-size: 13px; color: var(--gold-bright); }
  .note { color: var(--text-muted); font-size: 13px; }
</style>

<h2 style="margin-bottom: 4px;">Feature Matrix</h2>
<span class="badge badge-version">v1.2.0</span>
<span class="badge badge-mc">1.20.1 / 1.21.1</span>
<span class="badge badge-forge">Forge</span>
<span class="badge badge-fabric">Fabric</span>

<p style="color: var(--text-muted); margin-top: 12px;">Everything CNPCExtended offers, compared across platforms at a glance.</p>

<div class="summary-grid">
  <div class="summary-card">
    <div class="num">20+</div>
    <div class="lbl">Total Features</div>
  </div>
  <div class="summary-card">
    <div class="num">14</div>
    <div class="lbl">Shared (Both)</div>
  </div>
  <div class="summary-card">
    <div class="num">3</div>
    <div class="lbl">Fabric-Only</div>
  </div>
  <div class="summary-card">
    <div class="num">2</div>
    <div class="lbl">Platforms</div>
  </div>
</div>

<div class="legend">
  <span class="legend-item"><span class="s-yes" style="font-size:18px;">&#x2714;</span> Supported</span>
  <span class="legend-item"><span class="s-no" style="font-size:18px;">&#x2500;</span> Not yet</span>
  <span class="legend-item"><span class="s-na" style="font-size:16px;">&#x2718;</span> N/A</span>
</div>

<!-- ============ CORE ============ -->
<div class="section-hdr">
  <div class="icon">&#x2699;</div>
  <h3>Core (Server-Side)</h3>
  <span class="tag tag-both">Forge + Fabric</span>
</div>

<table class="ftable">
  <tr><th>Feature</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th></tr>
  <tr><td>Script Injection (<span class="feat-name">cnpcext</span> global)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Client Bridge API (<span class="feat-name">getClientBridge()</span>)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Global Script Preloading</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Global NPC Data Preloading</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Script Commands (<span class="feat-name">registerCommand()</span>)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">/cnpcext</span> CLI Commands</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>ModConfig (common.toml)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<!-- ============ HTML GUI ============ -->
<div class="section-hdr">
  <div class="icon">&#x1F310;</div>
  <h3>HTML GUI (Client)</h3>
  <span class="tag tag-both">Forge + Fabric</span>
</div>

<table class="ftable">
  <tr><th>Feature</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th><th>Notes</th></tr>
  <tr><td>HTML GUI (MCEF Chromium)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td><td class="note">Full HTML/CSS/JS rendered in-game</td></tr>
  <tr><td>Bridge JS (<span class="feat-name">window.cnpc</span>)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td><td class="note">sendEvent, onEvent, close, initData</td></tr>
  <tr><td>MC Item Overlays</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td><td class="note">Real ItemStack rendering on HTML elements</td></tr>
  <tr><td>Clip Rects (<span class="feat-name">data-mc-clip</span>)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td><td class="note">Scissor clipping for scrollable item lists</td></tr>
  <tr><td>Client Queries</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td><td class="note">Video, keybinds, sound, player state, packs</td></tr>
  <tr><td>Client Script Engine</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td><td class="note">JSR-223 JavaScript on client side</td></tr>
</table>

<!-- ============ OVERLAYS ============ -->
<div class="section-hdr">
  <div class="icon">&#x1F4FA;</div>
  <h3>HTML Overlays (HUD)</h3>
  <span class="tag tag-new">NEW in v1.2</span>
  <span class="tag tag-fabric">Fabric Only</span>
</div>
<p class="section-desc">Render HTML on the HUD layer &mdash; skill bars, HP bars, quest trackers. Game stays fully playable.</p>

<table class="ftable">
  <tr><th>Feature</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th></tr>
  <tr><td><span class="feat-name">openOverlay(name, file, x, y, w, h, data)</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">updateOverlay(name, data)</span> &mdash; auto-dedup</td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">hideOverlay</span> / <span class="feat-name">showOverlay</span> / <span class="feat-name">closeOverlay</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Multiple simultaneous overlays (up to 8)</td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Persistent overlays (survive relog)</td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Auto-cleanup on disconnect</td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<!-- ============ HUD HIDING ============ -->
<div class="section-hdr">
  <div class="icon">&#x1F3A8;</div>
  <h3>Vanilla HUD Hiding</h3>
  <span class="tag tag-new">NEW in v1.2</span>
  <span class="tag tag-fabric">Fabric Only</span>
</div>
<p class="section-desc">Selectively hide vanilla HUD elements via Mixin. Resets on disconnect.</p>

<table class="ftable">
  <tr><th>Element</th><th><span class="feat-name">hideHudElement()</span> Name</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th></tr>
  <tr><td>Hotbar + item name</td><td><span class="feat-name">hotbar</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>XP bar + level number</td><td><span class="feat-name">experience</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Hearts + food + armor + air</td><td><span class="feat-name">health</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Armor icons only</td><td><span class="feat-name">armor</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Hunger bar only</td><td><span class="feat-name">food</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Crosshair</td><td><span class="feat-name">crosshair</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Potion effects</td><td><span class="feat-name">effects</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Action bar text</td><td><span class="feat-name">actionbar</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Chat display</td><td><span class="feat-name">chat</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Sidebar scoreboard</td><td><span class="feat-name">scoreboard</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Tab player list</td><td><span class="feat-name">tablist</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><strong>All at once</strong></td><td><span class="feat-name">all</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<!-- ============ ASSET LOADING ============ -->
<div class="section-hdr">
  <div class="icon">&#x1F4C1;</div>
  <h3>Asset Loading</h3>
  <span class="tag tag-new">NEW in v1.2</span>
  <span class="tag tag-fabric">Fabric Only</span>
</div>
<p class="section-desc">Load images, CSS, JS, and fonts from the scripts folder via the <span class="feat-name">cnpc://</span> custom CEF scheme.</p>

<table class="ftable">
  <tr><th>Feature</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th></tr>
  <tr><td><span class="feat-name">cnpc://</span> custom CEF scheme</td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">window.cnpc.assetUrl</span> in bridge JS</td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Auto-sync scripts path on join</td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Path traversal protection</td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Works in HTML GUIs</td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Works in HTML Overlays</td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<!-- ============ API REFERENCE ============ -->
<div class="section-hdr">
  <div class="icon">&#x1F4E1;</div>
  <h3>API Method Reference</h3>
</div>

<h4 style="color: var(--gold); margin-top: 24px;"><span class="feat-name">cnpcext</span> &mdash; Server Script Global</h4>

<table class="ftable">
  <tr><th>Method</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th></tr>
  <tr><td><span class="feat-name">getClientBridge(mcPlayer)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">openHtmlGui(e, file, w, h, json)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">registerCommand(name, json)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">openOverlay(e, name, file, x, y, w, h, json)</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">updateOverlay(e, name, json)</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">hideOverlay</span> / <span class="feat-name">showOverlay</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">closeOverlay</span> / <span class="feat-name">hasOverlay</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">hideHudElement(e, element)</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">showHudElement(e, element)</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<h4 style="color: var(--gold); margin-top: 24px;"><span class="feat-name">IClientBridge</span> &mdash; via getClientBridge()</h4>

<table class="ftable">
  <tr><th>Method</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th></tr>
  <tr><td><span class="feat-name">openHtmlGui(file, w, h, json)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">closeHtmlGui()</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">sendToBrowser(event, json)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">queryVideoSettings(cb)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">queryKeybinds(cb)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">querySoundSettings(cb)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">queryPlayerState(cb)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">queryResourcePacks(cb)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">openOverlay(name, file, x, y, w, h, json)</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">updateOverlay(name, json)</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">hideOverlay</span> / <span class="feat-name">showOverlay</span> / <span class="feat-name">closeOverlay</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">hasOverlay(name)</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">hideHudElement(element)</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">showHudElement(element)</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<h4 style="color: var(--gold); margin-top: 24px;"><span class="feat-name">window.cnpc</span> &mdash; Browser-Side JS</h4>

<table class="ftable">
  <tr><th>Property / Method</th><th class="center">HTML&nbsp;GUI</th><th class="center">HTML&nbsp;Overlay</th></tr>
  <tr><td><span class="feat-name">initData</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">assetUrl</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">onEvent(name, cb)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">sendEvent(name, data)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">close()</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">setOverlayItems(items)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">setClipRect(rect)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<!-- ============ NETWORK PACKETS ============ -->
<div class="section-hdr">
  <div class="icon">&#x1F4E6;</div>
  <h3>Network Packets</h3>
</div>

<table class="ftable">
  <tr><th>ActionType</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th></tr>
  <tr><td><span class="feat-name">OPEN_HTML_GUI</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">CLOSE_HTML_GUI</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">SEND_TO_BROWSER</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">RUN_CLIENT_SCRIPT</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">SEND_TO_CLIENT</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">OPEN_OVERLAY</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">UPDATE_OVERLAY</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">CLOSE_OVERLAY</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">HIDE_OVERLAY</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">SHOW_OVERLAY</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">HIDE_HUD_ELEMENT</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">SHOW_HUD_ELEMENT</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">SYNC_SCRIPTS_PATH</span></td><td class="s s-no">&#x2500;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<!-- ============ KNOWN ISSUES ============ -->
<div class="section-hdr">
  <div class="icon">&#x26A0;</div>
  <h3>Known Issues &amp; Fixes</h3>
  <span class="tag tag-new">v1.2.0</span>
</div>
<p class="section-desc">Discovered via user testing on Fabric 1.21.1. May also affect Forge 1.20.1.</p>

<table class="ftable">
  <tr><th>Issue</th><th class="center">Status</th><th>Details</th></tr>
  <tr>
    <td>Blurry overlay text</td>
    <td class="s" style="color: #50c878; font-size: 13px;">FIXED</td>
    <td class="note">Overlay browser was sized at <span class="feat-name">width &times; guiScale</span> instead of native window pixel ratio. Text rendered at half resolution then stretched.</td>
  </tr>
  <tr>
    <td>Black flash on HTML load</td>
    <td class="s" style="color: #50c878; font-size: 13px;">FIXED</td>
    <td class="note">CEF needs a few frames to paint after creation. Overlay rendered immediately &rarr; brief black rectangle. Added 6-frame ready delay.</td>
  </tr>
  <tr>
    <td>Cursor detaches from game</td>
    <td class="s" style="color: #50c878; font-size: 13px;">FIXED</td>
    <td class="note">CEF's default <span class="feat-name">cursorChangeListener</span> calls <span class="feat-name">glfwSetInputMode(GLFW_CURSOR_NORMAL)</span> during HTML load and browser close, breaking Minecraft's mouselook. Fix: no-op listener on overlay browsers.</td>
  </tr>
  <tr>
    <td>HTML GUI black flash</td>
    <td class="s" style="color: #e0c050; font-size: 13px;">INVESTIGATING</td>
    <td class="note">Same first-paint delay may affect full-screen HTML GUIs. <span class="feat-name">BrowserGuiScreen</span> shows loading text but a brief black frame may still appear.</td>
  </tr>
</table>
