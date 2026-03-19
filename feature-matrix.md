---
layout: default
title: Feature Matrix
---

<h2 style="margin-bottom: 4px;">Feature Matrix</h2>
<span class="badge badge-version">v1.5.10</span>
<span class="badge badge-mc">1.20.1 / 1.21.1</span>
<span class="badge badge-forge">Forge</span>
<span class="badge badge-fabric">Fabric</span>

<p style="color: var(--text-muted); margin-top: 12px;">Everything CNPCExtended offers, compared across platforms at a glance.</p>

<div class="summary-grid">
  <div class="summary-card">
    <div class="num">30+</div>
    <div class="lbl">Total Features</div>
  </div>
  <div class="summary-card">
    <div class="num" style="color: #50c878;">30+</div>
    <div class="lbl">Shared (Both)</div>
  </div>
  <div class="summary-card">
    <div class="num">0</div>
    <div class="lbl">Platform-Only</div>
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
  <tr><td>ModConfig (common.toml)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>  <tr><td>ClientConfig (skip menu)</td><td class=\"s s-yes\">&#x2714;</td><td class=\"s s-yes\">&#x2714;</td></tr>
  <tr><td>Skip Menu (auto-load world/server)</td><td class=\"s s-yes\">&#x2714;</td><td class=\"s s-yes\">&#x2714;</td></tr></table>

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
  <tr><td>Entity Overlays</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td><td class="note">Full entity rendering (NPCs, players) via <span class="feat-name">data-mc-entity</span></td></tr>
  <tr><td>Clip Rects (<span class="feat-name">data-mc-clip</span>)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td><td class="note">Scissor clipping for scrollable item lists</td></tr>
  <tr><td>Client Queries</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td><td class="note">Video, keybinds, sound, player state, packs</td></tr>
  <tr><td>Client Script Engine</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td><td class="note">JSR-223 JavaScript on client side</td></tr>
</table>

<!-- ============ OVERLAYS ============ -->
<div class="section-hdr">
  <div class="icon">&#x1F4FA;</div>
  <h3>HTML Overlays (HUD)</h3>
  <span class="tag tag-both">Forge + Fabric</span>
</div>
<p class="section-desc">Render HTML on the HUD layer &mdash; skill bars, HP bars, quest trackers. Game stays fully playable.</p>

<table class="ftable">
  <tr><th>Feature</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th></tr>
  <tr><td><span class="feat-name">openOverlay(name, file, x, y, w, h, data)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">updateOverlay(name, data)</span> &mdash; auto-dedup</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">hideOverlay</span> / <span class="feat-name">showOverlay</span> / <span class="feat-name">closeOverlay</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Multiple simultaneous overlays (up to 8)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Persistent overlays (survive relog)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Auto-cleanup on disconnect</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Item overlays on HUD</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Entity overlays on HUD</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Fade-in animation</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Interactive mode (cursor unlock)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<!-- ============ HUD HIDING ============ -->
<div class="section-hdr">
  <div class="icon">&#x1F3A8;</div>
  <h3>Vanilla HUD Hiding</h3>
  <span class="tag tag-both">Forge + Fabric</span>
</div>
<p class="section-desc">Selectively hide vanilla HUD elements. Resets on disconnect.</p>

<table class="ftable">
  <tr><th>Element</th><th><span class="feat-name">hideHudElement()</span> Name</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th></tr>
  <tr><td>Hotbar + item name</td><td><span class="feat-name">hotbar</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>XP bar + level number</td><td><span class="feat-name">experience</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Hearts + food + armor + air</td><td><span class="feat-name">health</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Armor icons only</td><td><span class="feat-name">armor</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Hunger bar only</td><td><span class="feat-name">food</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Crosshair</td><td><span class="feat-name">crosshair</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Potion effects</td><td><span class="feat-name">effects</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Action bar text</td><td><span class="feat-name">actionbar</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Chat display</td><td><span class="feat-name">chat</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Sidebar scoreboard</td><td><span class="feat-name">scoreboard</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Tab player list</td><td><span class="feat-name">tablist</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><strong>All at once</strong></td><td><span class="feat-name">all</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<!-- ============ ASSET LOADING ============ -->
<div class="section-hdr">
  <div class="icon">&#x1F4C1;</div>
  <h3>Asset Loading</h3>
  <span class="tag tag-both">Forge + Fabric</span>
</div>
<p class="section-desc">Load images, CSS, JS, and fonts from the scripts folder via the <span class="feat-name">cnpc://</span> custom CEF scheme.</p>

<table class="ftable">
  <tr><th>Feature</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th></tr>
  <tr><td><span class="feat-name">cnpc://</span> custom CEF scheme</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">window.cnpc.assetUrl</span> in bridge JS</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Auto-sync scripts path on join</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Path traversal protection</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Works in HTML GUIs</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Works in HTML Overlays</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<!-- ============ CUTSCENE SYSTEM ============ -->
<div class="section-hdr">
  <div class="icon">&#x1F3AC;</div>
  <h3>Cutscene System</h3>
  <span class="tag tag-both">Forge + Fabric</span>
</div>
<p class="section-desc">Keyframe-based camera cutscenes with visual HTML editor, fade transitions, player protection, and script phase events.</p>

<table class="ftable">
  <tr><th>Feature</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th></tr>
  <tr><td><span class="feat-name">startCutscene(player, name, options)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">stopCutscene</span> / <span class="feat-name">pauseCutscene</span> / <span class="feat-name">resumeCutscene</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">isInCutscene(player)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">moveCamera(player, json)</span> &mdash; ad-hoc keyframes</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">cutscene(e)</span> phase event handler</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Visual editor GUI (HTML)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Fade transitions</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Cinematic black bars</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>FOV lock + hand hidden</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Mouse look blocked</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Player protection (freeze + invulnerable)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Disconnect/reconnect failsafe</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Catmull-Rom camera interpolation</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td>Sub-tick camera smoothing (60fps+)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">/cnpcext cutscene play &lt;name&gt; &lt;player&gt;</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<!-- ============ API REFERENCE ============ -->
<div class="section-hdr">
  <div class="icon">&#x1F4E1;</div>
  <h3>API Method Reference</h3>
</div>

<h4 style="color: var(--text); margin-top: 24px;"><span class="feat-name">cnpcext</span> &mdash; Server Script Global</h4>

<table class="ftable">
  <tr><th>Method</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th></tr>
  <tr><td><span class="feat-name">getClientBridge(mcPlayer)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">openHtmlGui(e, file, w, h, json)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">registerCommand(name, json)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">openOverlay(e, name, file, x, y, w, h, json)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">updateOverlay(e, name, json)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">hideOverlay</span> / <span class="feat-name">showOverlay</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">closeOverlay</span> / <span class="feat-name">hasOverlay</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">hideHudElement(e, element)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">showHudElement(e, element)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">startCutscene(player, name, optionsJson)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">stopCutscene(player)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">pauseCutscene</span> / <span class="feat-name">resumeCutscene</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">isInCutscene(player)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">moveCamera(player, keyframesJson)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>  <tr><td><span class=\"feat-name\">setGuiEscapable(e, boolean)</span></td><td class=\"s s-yes\">&#x2714;</td><td class=\"s s-yes\">&#x2714;</td></tr>  <tr><td><span class="feat-name">entityId(entity)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">entityNbt(entity)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<h4 style="color: var(--text); margin-top: 24px;"><span class="feat-name">IClientBridge</span> &mdash; via getClientBridge()</h4>

<table class="ftable">
  <tr><th>Method</th><th class="center">Forge&nbsp;1.20.1</th><th class="center">Fabric&nbsp;1.21.1</th></tr>
  <tr><td><span class="feat-name">openHtmlGui(file, w, h, json)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">closeHtmlGui()</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">setGuiEscapable(boolean)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">sendToBrowser(event, json)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">queryVideoSettings(cb)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">queryKeybinds(cb)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">querySoundSettings(cb)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">queryPlayerState(cb)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">queryResourcePacks(cb)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">openOverlay(name, file, x, y, w, h, json)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">updateOverlay(name, json)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">hideOverlay</span> / <span class="feat-name">showOverlay</span> / <span class="feat-name">closeOverlay</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">hasOverlay(name)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">hideHudElement(element)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">showHudElement(element)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">setGuiEscapable(boolean)</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<h4 style="color: var(--text); margin-top: 24px;"><span class="feat-name">window.cnpc</span> &mdash; Browser-Side JS</h4>

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
  <tr><td><span class="feat-name">OPEN_OVERLAY</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">UPDATE_OVERLAY</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">CLOSE_OVERLAY</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">HIDE_OVERLAY</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">SHOW_OVERLAY</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">SET_OVERLAY_INTERACTIVE</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">CLOSE_ALL_OVERLAYS</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">HIDE_HUD_ELEMENT</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">SHOW_HUD_ELEMENT</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">SYNC_SCRIPTS_PATH</span></td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">PacketCutsceneStart</span> (S&rarr;C)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
  <tr><td><span class="feat-name">PacketCutsceneStop</span> (S&rarr;C)</td><td class="s s-yes">&#x2714;</td><td class="s s-yes">&#x2714;</td></tr>
</table>

<!-- ============ KNOWN ISSUES ============ -->
<div class="section-hdr">
  <div class="icon">&#x26A0;</div>
  <h3>Known Issues &amp; Fixes</h3>
  <span class="tag tag-new">v1.5</span>
</div>
<p class="section-desc">Discovered via user testing. Fixed on both platforms.</p>

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
    <td class="note">CEF needs a few frames to paint after creation. Added fade-in animation (skip 8 frames + fade over 10 frames).</td>
  </tr>
  <tr>
    <td>Cursor detaches from game</td>
    <td class="s" style="color: #50c878; font-size: 13px;">FIXED</td>
    <td class="note">CEF's default <span class="feat-name">cursorChangeListener</span> calls <span class="feat-name">glfwSetInputMode(GLFW_CURSOR_NORMAL)</span> during HTML load. Fix: no-op cursor listener on overlay browsers.</td>
  </tr>
  <tr>
    <td>Overlay breaks on window resize</td>
    <td class="s" style="color: #50c878; font-size: 13px;">FIXED</td>
    <td class="note">Item/entity overlay positions misaligned after resizing MC window. Fix: auto-resize browser each frame via <span class="feat-name">checkResize()</span>.</td>
  </tr>
</table>
