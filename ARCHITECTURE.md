# Architecture — Kyojima Eki Living Archive Studio

## Overview

Single-file WebGL 1.0 studio. No build step, no npm, no Three.js. All geometry, textures, shaders,
and UI live in one HTML file. Two variants: monolithic (pre-loaded) and streaming (lazy LRU).

---

## File Inventory

| File | Size | Role |
|------|------|------|
| `kyojima-studio-pre-obj4.html` | 1.86 MB | Monolithic studio — 5 textures decoded at startup |
| `kyojima-studio-stream.html` | 2.76 MB | Streaming studio — lazy LRU per object |
| `kyojima-perf-bench.html` | 11.8 KB | Benchmark tool — loads both in iframes, measures FPS/heap/LBT |

Both studio files share identical structure. The streaming variant adds ~600 KB
(`TEXTURE_PAYLOADS` object) and replaces 5 `const xTex = loadTexture(b64)` calls
with the `LandmarkCache` streaming block.

---

## HTML Structure

```
<head>  Tailwind CDN, CSS custom properties
<body>
  .max-w-6xl container
    ├── Header row (title, dropdown Obj 01–16, 🍳 Bake Obj 16 strip)
    ├── Mode tabs (Washi 1D · 2D Refs · Photo · 3D Master)
    └── #viewport-container (relative, clamp 440px–850px height)
          ├── #gallery-layer    (display:none in 3D mode — 2D reference images)
          ├── #studio-canvas    (WebGL, z-index 10)
          ├── #controls-top-left  (Orbit 90°, Cel Shading, Sumi Lines)
          ├── #controls-top-right (Stop Spin, Reset Cam)
          └── #controls-bottom-hud
                ├── left: obj title, tri count (static from dossier)
                └── right: fps · tris · VRAM · heap · danger · 👁 mask · ⬇ Save Obj
  Architectural dossier footer (3-col metadata grid)
<script>(function() { ... all JS ... })();</script>
```

---

## GeometryBuffer Class

Defined inside the IIFE. All geometry objects are instances of this class.

```js
class GeometryBuffer {
  constructor()   // positions[], normals[], uvs[], colors[], emissives[], texModes[], vbo={}, count=0

  addQuad(p1,p2,p3,p4, color, emissive=0, texMode=0, uvs=[0,0,1,0,1,1,0,1], customNormal=null)
  addTriangle(p1,p2,p3, color, emissive=0, texMode=0, customNormal=null)
  addBox(center, size, color, emissive=0, texMode=0)
  addCylinder(p1, p2, radius, color, segments=8, emissive=0, texMode=0) // orthonormal basis, radial normals
  addSolidAwning(center, width, height, depth, thickness, colorTop, colorBot)
  addBeveledChassis(center, size, color)   // r=0.035 bevel, 3-segment arc corners

  mergeFrom(src, dx, dy, dz)  // translate src.positions by (dx,dy,dz), append all arrays
  freeGPU()                   // gl.deleteBuffer all vbos, reset count

  upload()  // Float32Array → gl.ARRAY_BUFFER for each channel
  draw()    // bind all VBOs, gl.drawArrays(TRIANGLES, 0, count)
}
```

**Vertex layout** (6 separate VBOs, 56 bytes/vertex total):
```
pos:      Float32 × 3   (12 bytes)
norm:     Float32 × 3   (12 bytes)
uv:       Float32 × 2   (8 bytes)
col:      Float32 × 4   (16 bytes)
emissive: Float32 × 1   (4 bytes)
texMode:  Float32 × 1   (4 bytes)
                        ─────────
                        56 bytes/vertex
```

---

## Shader System

Two-pass rendering: master geometry pass + ink outline pass (back-face extrude).

**texMode values:**
```
0  → vertex color only (no texture)
1  → uChassisTex   (machine front glass panel, PNG 358 KB)
2  → uWindowTex    (machine product display, WebP 108 KB)
3  → uSideMuralTex (facade side mural, WebP 42 KB)
4  → uGroundTex    (ground threshold washi, WebP 59 KB)
5  → uUpperTex     (upper window washi, WebP 34 KB)
```

**Uniforms**: `uModel`, `uView`, `uProjection`, `uNormalMatrix`, `uInkExtrude`,
`uLightDir`, `uLightColor`, `uAmbientColor`, `uCameraPos`, `uCelSteps`, `uInkColor`,
`uChassisTex`…`uUpperTex`, `uTex0`…`uTex4`, `isInkPass`.

**Ink pass**: `uInkExtrude > 0` → vertex shader extrudes along normal by 0.008 units,
fragment shader returns solid `uInkColor`. Depth mask off, back-face culled in master pass,
front-face culled in ink pass.

---

## Object Geometry Pipeline

```
At script init (runs once, synchronous):

obj1Washi.upload()
obj1Master.upload()      ← 27-call vending machine, centered [0, 1.02, 0] (3,858 tris)

obj2Washi.upload()
obj4Washi.upload()
obj4Master.upload()      ← 1,276-tri striped sun awning & cantilever hardware

obj2Master               ← facade + Kawara roof backprop
  .mergeFrom(obj4Master, 0, 1.35, 2.41)   ← backpropagates awning directly into facade master
  .upload()

obj2CompositeGeom        ← full facade with all attached landmarks
  .mergeFrom(obj2Master, 0, 0, 0)         ← facade + roof + awning
  .mergeFrom(obj1Master, 2.45, 0, 2.65)   ← full crimson vending machine at street position
  .upload()

obj3Washi.upload()
obj3Master.upload()      ← standalone Kawara roof study (1,752 tris)

genericQueueGeom.upload() ← grey placeholder box for Obj 05–15
pedestalGeom.upload()     ← 40-segment circular ground turntable disc

obj16FusedGeom = null     ← created only when bakeSceneComposite() is called
```

**Render loop object selection:**
```js
if      (selectedObject === "1")                                curMaster = obj1Master
else if (selectedObject === "2")                                curMaster = obj2CompositeGeom  ← composite (facade + roof + awning + machine)
else if (selectedObject === "3")                                curMaster = obj3Master
else if (selectedObject === "4")                                curMaster = obj4Master         ← striped sun awning & hardware
else if (selectedObject === "16" && obj16FusedGeom?.count > 0) curMaster = obj16FusedGeom
else if (selectedObject === "16")                               curMaster = genericQueueGeom   ← pre-bake fallback
else                                                            curMaster = genericQueueGeom
```

---

## Streaming Architecture (studio-stream only)

```js
const TEXTURE_PAYLOADS = {
  "1":  { chassisTex:{b64,mime}, windowTex:{b64,mime}, sideMuralTex:{b64,mime}, groundTex:{b64,mime}, upperTex:{b64,mime} },
  "2":  { chassisTex:{b64 from obj1 payload}, windowTex, sideMuralTex, groundTex, upperTex },
  "3":  { all empty b64 strings — obj3 is vertex-color only },
  "16": { chassisTex from obj1, rest from obj2 — full composite texture set }
}
```

**Sentinel textures**: `makeSentinel(r,g,b)` → 1×1 GPU texture placeholder.
All 5 slots start as sentinels. Canvas renders immediately on frame 1.

**Loading flow** (`loadTexturesForObject(objId)`):
1. Skip if same object already loaded or load in progress
2. `gl.deleteTexture` on all previous textures (LRU eviction)
3. `loadNext()` called via `requestAnimationFrame` — decodes one texture per frame
4. On completion: stores `elapsed` ms → `_lastLoadMs` (read by saccadic mask HUD)

**Object 16 texture routing**: `TEXTURE_PAYLOADS["16"]` has chassisTex from obj1 (for the
machine panels) and the four facade textures from obj2. No alias needed.

---

## Object 16 Bake System

```js
var obj16FusedGeom = null;
var obj16BakeState = "idle"; // "idle" | "baking" | "done" | "error"

function bakeSceneComposite() {
  if (obj16BakeState === "done")   { updateObjectView("16"); return; }  // already baked
  if (obj16BakeState === "baking") return;                               // guard: no double-run
  obj16BakeState = "baking";
  // update button text, then defer 16ms for UI repaint
  setTimeout(function() {
    try {
      var fused = new GeometryBuffer();
      fused.mergeFrom(obj2Master, 0, 0, 0);          // building + roof + placeholder
      fused.mergeFrom(obj1Master, 2.45, 0, 2.65);    // finalized machine
      if (fused.positions.length === 0) throw new Error("empty");
      if (obj16FusedGeom) obj16FusedGeom.freeGPU();  // release previous
      obj16FusedGeom = fused;
      obj16FusedGeom.upload();
      obj16BakeState = "done";
      // update dropdown → "16", call updateObjectView("16")
    } catch(err) {
      obj16BakeState = "error";
      // show error on button, console.error
    }
  }, 16);
}
window.bakeSceneComposite = bakeSceneComposite; // must expose — defined inside IIFE
```

**Critical**: use `obj2Master` (not `obj2CompositeGeom`) as bake base.
`obj2CompositeGeom` already contains `obj1Master` at [2.45,0,2.65].
Using it as the bake base would double the machine geometry.

---

## Performance HUD

Located in `#controls-bottom-hud`, right side. Updates every 60 frames.

```js
function updatePerfHUD(curMasterGeom) {
  if (++_perfFrames < 60) return;
  _perfFPS = Math.round(60000 / (now - _perfLastT));

  tris    = curMasterGeom.count / 3
  vramMB  = curMasterGeom.count * 56 / 1048576   // 56 bytes/vertex
  heapMB  = performance.memory?.usedJSHeapSize / 1048576

  // Danger thresholds
  DANGER:  fps < 30  || tris > 80000 || vramMB > 200
  WATCH:   fps < 50  || tris > 30000 || vramMB > 80
  OK:      otherwise

  // Saccadic mask
  loadMs = Math.max(_lastLoadMs, _startupDecodeMs)
  // _lastLoadMs    — set by streaming texture loader (elapsed ms per object)
  // _startupDecodeMs — set at init in monolithic studio wrapping 5 loadTexture() calls
  // _SACCADE_MS = 150 (medium-to-large saccade suppression window, Matin 1974)
  pct = loadMs / 150 * 100
  GREEN:  loadMs <= 150  → "Xms / 150ms (Y% — within mask)"
  RED:    loadMs > 150   → "Xms / 150ms (+Zms — pop-in visible)"
}
```

Called from render loop: `updatePerfHUD(curMaster)` after `curMaster.draw()`.

---

## Deployment

```jsonc
// wrangler.jsonc (in context/kyojimakokogarden/claude-world/kokechan/)
{
  "name": "kokechan-claude-edition",
  "compatibility_date": "2026-08-31",
  "assets": { "directory": "./dist" },
  "routes": [{ "pattern": "kokechan.preattention.ai", "custom_domain": true }]
}
```

```bash
# Copy source files to dist, then:
npx wrangler@4.127.1 deploy
# from: context/kyojimakokogarden/claude-world/kokechan/
```

Routes: `studio.html` → `/studio`, `studio-stream.html` → `/studio-stream`,
`perf-bench.html` → `/perf-bench`

---

## Scale Projection (173 Landmarks)

| Metric | Monolithic | Streaming |
|--------|-----------|-----------|
| Startup decode (865 textures) | ~104 seconds | 0 ms |
| Peak VRAM | ~1,038 MB (browser crash) | ~6 MB (active object only) |
| First paint | Blocked until all decoded | Immediate (sentinel) |
| Object switch | Instant | ~80–150 ms (within saccadic mask) |
