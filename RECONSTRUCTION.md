# Zero-Shot Reconstruction Guide

This document provides everything needed to rebuild the Kyojima Eki Living Archive Studio
from scratch, in order. Written for handover to a fresh model session.

---

## Prerequisites

- Any modern browser with WebGL 1.0 (Chrome, Firefox, Safari)
- Node.js ≥ 18 (for `npx wrangler`)
- Cloudflare account with Workers enabled
- `gh` CLI authenticated (`gh auth login`)

No npm install, no bundler, no framework. The studio is a single `.html` file.

## 0. Authoritative Source Documents (Google Drive Mirror)

Before reading code, review the authoritative dossier and meta-references exported directly from Google Drive into [`docs/meta-references/`](./docs/meta-references/):

1. **[`01_LANDMARK_PRODUCTION_QUEUE.md`](./docs/meta-references/01_LANDMARK_PRODUCTION_QUEUE.md)** — Master queue of all 168 editorial landmark prompts and spatial coordinates.
2. **[`02_173_CULTURAL_SITES_REGISTRY.md`](./docs/meta-references/02_173_CULTURAL_SITES_REGISTRY.md)** — Cross-verified directory of all 173 physical sites across Kyojima & Koganecho.
3. **[`03_KYOJIMA_EKI_ARCHITECTURAL_DOSSIER.md`](./docs/meta-references/03_KYOJIMA_EKI_ARCHITECTURAL_DOSSIER.md)** — Deep architectural survey and 15-object sequence for Kyojima Eki.
4. **[`04_BEYOND_POLYGON_BLOAT_SHADER_ARCHITECTURE.md`](./docs/meta-references/04_BEYOND_POLYGON_BLOAT_SHADER_ARCHITECTURE.md)** — Shading manifesto, Half-Lambert lighting, Morado proxy textures, and master to-do.
5. **[`05_GENERATION_PROCESS_AND_META_REFERENCES_LEDGER.md`](./docs/meta-references/05_GENERATION_PROCESS_AND_META_REFERENCES_LEDGER.md)** — Detailed generation ledger, 2D reference bibles, math, and Z-fighting resolutions.

---

## 1. Single-File Architecture

Everything lives in one file:
```html
<!DOCTYPE html>
<html>
<head>
  <!-- Tailwind CDN for layout, no local CSS build needed -->
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
  <!-- All UI markup here -->
  <script>
    (function() {
      // ALL JS inside this IIFE — WebGL context, geometry, render loop
      // Textures are base64 strings embedded inline
      // No external script tags, no module imports
    })();
  </script>
</body>
</html>
```

**Critical rule**: Never assemble this by string concatenation of parts.
Injecting HTML fragments after `<script>` opens causes parse failures that
silently prevent WebGL from initializing (canvas goes blank, no JS errors).
Always patch the file using exact string replacement on the full source.

---

## 2. WebGL Initialization

```js
const canvas = document.getElementById('studio-canvas');
const gl = canvas.getContext('webgl', { antialias: true, alpha: false });
if (!gl) { console.error('WebGL not supported'); return; }
```

Compile shaders, link program, get attrib/uniform locations — standard pattern.
Attribs: `aPosition` (3f), `aNormal` (3f), `aTexCoord` (2f), `aColor` (4f),
`aEmissive` (1f), `aTexMode` (1f).

---

## 3. GeometryBuffer Class

Copy this class verbatim before building any geometry objects:

```js
class GeometryBuffer {
  constructor() {
    this.positions = []; this.normals = []; this.uvs = [];
    this.colors = []; this.emissives = []; this.texModes = [];
    this.vbo = {}; this.count = 0;
  }
  addQuad(p1, p2, p3, p4, color, emissive=0, texMode=0, uvs=[0,0,1,0,1,1,0,1], customNormal=null) { ... }
  addBox(center, size, color, emissive=0, texMode=0) { /* 6 faces via addQuad */ }
  addSolidAwning(center, width, height, depth, thickness, colorTop, colorBot) { ... }
  addBeveledChassis(center, size, color) { /* r=0.035, 3-segment arc corners */ }
  mergeFrom(src, dx, dy, dz) {
    // Append src arrays, translating positions by (dx,dy,dz)
    for (var i=0; i<src.positions.length; i+=3)
      this.positions.push(src.positions[i]+dx, src.positions[i+1]+dy, src.positions[i+2]+dz);
    for (var j=0; j<src.normals.length; j++) this.normals.push(src.normals[j]);
    // ... same for uvs, colors, emissives, texModes
  }
  freeGPU() {
    try { ['pos','norm','uv','col','emissive','texMode'].forEach(k => gl.deleteBuffer(this.vbo[k])); } catch(e) {}
    this.vbo = {}; this.count = 0;
  }
  upload() {
    function makeVBO(data) {
      const buf = gl.createBuffer();
      gl.bindBuffer(gl.ARRAY_BUFFER, buf);
      gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(data), gl.STATIC_DRAW);
      return buf;
    }
    this.vbo.pos = makeVBO(this.positions); this.vbo.norm = makeVBO(this.normals);
    this.vbo.uv = makeVBO(this.uvs); this.vbo.col = makeVBO(this.colors);
    this.vbo.emissive = makeVBO(this.emissives); this.vbo.texMode = makeVBO(this.texModes);
    this.count = this.positions.length / 3;
  }
  draw() {
    if (!this.count) return;
    function bind(loc, buf, size) {
      gl.bindBuffer(gl.ARRAY_BUFFER, buf);
      gl.enableVertexAttribArray(loc);
      gl.vertexAttribPointer(loc, size, gl.FLOAT, false, 0, 0);
    }
    bind(attribs.pos, this.vbo.pos, 3); bind(attribs.norm, this.vbo.norm, 3);
    bind(attribs.uv, this.vbo.uv, 2); bind(attribs.col, this.vbo.col, 4);
    bind(attribs.emissive, this.vbo.emissive, 1); bind(attribs.texMode, this.vbo.texMode, 1);
    gl.drawArrays(gl.TRIANGLES, 0, this.count);
  }
}
```

---

## 4. Object Build Order

Build and upload in this exact order (obj2CompositeGeom depends on both obj1 and obj2):

```
1. obj1Washi.upload()
2. obj1Master.upload()          ← full 27-call vending machine
3. obj2Washi.upload()
4. obj2Master.upload()          ← facade + roof (38-call backprop) + 5-call placeholder
5. obj2CompositeGeom = new GeometryBuffer()
   obj2CompositeGeom.mergeFrom(obj2Master, 0, 0, 0)
   obj2CompositeGeom.mergeFrom(obj1Master, 2.45, 0, 2.65)
   obj2CompositeGeom.upload()
6. obj3Washi.upload()
7. obj3Master.upload()
8. genericQueueGeom.upload()
9. obj16FusedGeom = null        ← not built here; bakeSceneComposite() creates it on demand
10. pedestalGeom.upload()
```

---

## 5. Texture System

### Monolithic Studio
```js
// Measure startup decode for saccadic mask HUD
var _t_texStart = performance.now();
const chassisTex   = loadTexture("iVBOR...");  // PNG 358 KB
const windowTex    = loadTexture("UklGRr...");  // WebP 108 KB
const sideMuralTex = loadTexture("UklGRt...");  // WebP 42 KB
const groundTex    = loadTexture("UklGRo...");  // WebP 59 KB
const upperTex     = loadTexture("UklGRg...");  // WebP 34 KB
_startupDecodeMs = Math.round(performance.now() - _t_texStart);
```

### Streaming Studio (replace the above with)
```js
const TEXTURE_PAYLOADS = {
  "1": { chassisTex:{b64:"iVBOR...",mime:"image/png"}, windowTex:{b64:"UklGRr...",mime:"image/webp"}, ... },
  "2": { chassisTex:{b64: /* COPY from obj1 payload */,mime:"image/png"}, windowTex:{b64:"..."}, ... },
  "3": { chassisTex:{b64:"",mime:"image/webp"}, ... },  // obj3 vertex-color, empty b64s
  "16":{ chassisTex:{b64: /* from obj1 */,...}, windowTex:{b64: /* from obj2 */,...}, ... }
};
function makeSentinel(r,g,b) { /* create 1×1 texture */ }
var chassisTex=makeSentinel(0.5,0.5,0.5), windowTex=makeSentinel(0.5,0.5,0.5), ...;
// loadTexturesForObject(objId) — progressive RAF-frame loader with LRU eviction
```

**Key**: TEXTURE_PAYLOADS["2"].chassisTex must be copied from TEXTURE_PAYLOADS["1"].chassisTex
because `obj2CompositeGeom` renders `obj1Master` geometry which uses texMode=1.

---

## 6. Object 16 Bake — Known Pitfalls

### Pitfall A: IIFE scope
`bakeSceneComposite` is defined inside `(function(){ ... })()`. Inline `onclick`
attributes run in global scope and cannot see it. Fix:
```js
window.bakeSceneComposite = bakeSceneComposite; // inside the IIFE, after function definition
```

### Pitfall B: Double machine
Object 16 uses `obj2Master` as its base, not `obj2CompositeGeom`.
`obj2CompositeGeom` already has `obj1Master` merged in.
Using it as the bake base doubles the machine geometry:
```js
// CORRECT:
fused.mergeFrom(obj2Master, 0, 0, 0);
fused.mergeFrom(obj1Master, 2.45, 0, 2.65);

// WRONG (doubles the machine):
fused.mergeFrom(obj2CompositeGeom, 0, 0, 0); // already has obj1Master inside
fused.mergeFrom(obj1Master, 2.45, 0, 2.65);
```

### Pitfall C: Bake button visibility
The button must be outside any `position:absolute` overlay that clips on mode-tab switch.
Place it in a dedicated strip between the mode tabs and the header, not inside the canvas overlay.

---

## 7. Performance HUD Reconstruction

```js
var _perfFrames=0, _perfLastT=performance.now(), _perfFPS=60;
var _lastLoadMs=0, _startupDecodeMs=0, _SACCADE_MS=150;

function updatePerfHUD(geom) {
  if (++_perfFrames < 60) return;
  // update FPS, tris (geom.count/3), VRAM (geom.count*56/1048576)
  // heap: performance.memory?.usedJSHeapSize/1048576
  // danger: fps<30||tris>80000 → DANGER, fps<50||tris>30000 → WATCH
  // saccade: Math.max(_lastLoadMs, _startupDecodeMs) vs _SACCADE_MS
}
// Call from render loop: updatePerfHUD(curMaster);
```

---

## 8. Deployment

```bash
# 1. Copy studio file to dist/
cp kyojima-studio-pre-obj4.html context/kyojimakokogarden/claude-world/kokechan/dist/studio.html
cp kyojima-studio-stream.html   context/kyojimakokogarden/claude-world/kokechan/dist/studio-stream.html

# 2. Deploy
cd context/kyojimakokogarden/claude-world/kokechan
npx wrangler@4.127.1 deploy
```

wrangler.jsonc:
```json
{
  "name": "kokechan-claude-edition",
  "compatibility_date": "2026-08-31",
  "assets": { "directory": "./dist" },
  "routes": [{ "pattern": "kokechan.preattention.ai", "custom_domain": true }]
}
```

---

## 9. Saccadic Mask Reference

The 150ms threshold is the standard suppression window for a medium-to-large saccade
(10–30° eye movement, e.g. user looking from page header to canvas).

Sources: Matin (1974), Bridgeman et al. (1975), Ross et al. (2001).

Streaming studio typical results:
- Obj 01 textures: ~80–120ms → within mask (invisible pop-in)
- Obj 02 textures: ~100–150ms → at edge
- Monolithic startup: ~400–900ms on mobile → exceeds mask (visible on load)

The monolithic approach is still acceptable because the startup decode happens
before the canvas is shown (user sees a loading state, not a pop-in).
