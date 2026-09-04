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
  addQuad(p1, p2, p3, p4, color, emissive=0, texMode=0, uvs=[0,0,1,0,1,1,0,1], customNormal=null) { /* 2 triangles with shared or custom normal */ }
  addTriangle(p1, p2, p3, color, emissive=0, texMode=0, customNormal=null) { /* 1 triangle with computed cross-product normal */ }
  addBox(center, size, color, emissive=0, texMode=0) { /* 6 faces via addQuad */ }
  addCylinder(p1, p2, radius, color, segments=8, emissive=0, texMode=0) {
    /* Orthonormal basis (dir, u, v) via Gram-Schmidt, smooth radial normals, quad side fan */
  }
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

## 4. Object Build Order & Inheritance Pipeline

Build and upload in this exact sequential order:

```
1.  obj1Washi.upload()
2.  obj1Master.upload()          ← full 27-call crimson vending machine (centered [0, 1.02, 0])
3.  obj2Washi.upload()
4.  obj4Washi.upload()
5.  obj4Master.upload()          ← 1,276-tri striped sun awning & cantilever hardware
6.  obj2Master                   ← facade + Kawara roof backprop
      .mergeFrom(obj4Master, 0, 1.35, 2.41)   ← backpropagates awning directly into facade master
      .upload()
7.  obj2CompositeGeom = new GeometryBuffer()
      .mergeFrom(obj2Master, 0, 0, 0)         ← facade + roof + awning
      .mergeFrom(obj1Master, 2.45, 0, 2.65)   ← finalized crimson vending machine on street
      .upload()
8.  obj3Washi.upload()
9.  obj3Master.upload()          ← standalone Kawara ceramic roof study
10. genericQueueGeom.upload()    ← placeholder box for queued objects (Obj 05–15)
11. obj16FusedGeom = null        ← not built at startup; bakeSceneComposite() creates it on demand
12. pedestalGeom.upload()        ← 40-segment ground turntable disc
```

---

## 4b. Step-by-Step Object Reconstruction Checklists

### Object 01 — Crimson Vending Machine (自販機)
- **Geometry**: 27 builder calls, 3,858 triangles.
- **Body**: `addBeveledChassis([0, 1.02, 0], [0.95, 2.05, 0.85], redPaint)` with 3-segment bevels (r=0.035m).
- **Cooling Louvers**: 12× horizontal `addBox` on right side at `X = +0.478m`.
- **Button Row**: 3 elevation tiers `addBox` at `Y = [0.42, 1.05, 1.68]`.
- **PVC Drain Pipe**: `addBox` down rear corner at `[0.45, 0.52, -0.38]`.
- **Display Quads**: Front glass quad (`texMode=2`, emissive=0.45), chassis panel quad (`texMode=1`, emissive=0.05).
- **Hardware**: Coin return pocket, bill slot, 4 threaded leveling foot bolts.

### Object 02 — Timber Facade & Lattice Doors (木造ファサード・格子戸)
- **Geometry**: 7,782 triangles (facade baseline).
- **Wall & Threshold**: Concrete sidewalk slab `addBox`, stucco wall box, washi threshold quad (`texMode=4`), washi upper window quad (`texMode=5`).
- **Cedar Trim & Corbels**: Yakisugi perimeter dark cedar frame and sculpted structural corner corbels.
- **Roof Integration**: 38 builder calls backpropagated from Object 03 (Hon-gawara flutes, Munegawara ridge, Onigawara end crests, Nokidoi copper gutter and downspout).
- **Awning Integration**: `obj2Master.mergeFrom(obj4Master, 0, 1.35, 2.41)` mounts the striped awning over the central entrance.
- **Vending Integration**: `obj2CompositeGeom.mergeFrom(obj1Master, 2.45, 0, 2.65)` places the full crimson machine at the right street corner.

### Object 03 — Kawara Ceramic Roof & Sheltering Eaves (和瓦屋根・本瓦葺き)
- **Geometry**: 1,752 triangles (standalone study).
- **Main Pitch**: Front slope, rear slope, soffit, and gable end quads.
- **24 Hon-gawara Flutes**: Concave pan tiles (*pingawa*) and convex semi-cylindrical cover tiles (*torabusuma*) alternating in quad loops.
- **Ridge Crown**: 3-tier stepped Munegawara ridge topped with curved ridge-capping tiles.
- **End Crests**: Sculpted Onigawara ogre-mask end tiles on left and right ridge terminals.
- **Drainage & Rafters**: Nokidoi gutter box with downspout and 16 exposed scorched-cedar rafter tails (*taruki*).

### Object 04 — Striped Sun Awning & Cantilever Hardware (日除けテント・天幕・金物)
Reconstruct this object from zero using the following exact spatial specification:

1. **Spatial Profile & Key Dimensions**:
   - Total width: `W = 6.40m` (from `X = -3.20m` to `X = +3.20m`).
   - Top wall ledger: `Y = 1.45m, Z = 0.00m`.
   - Front eave lip: `Y = 1.04m, Z = 1.25m` (slope pitch: 18.2° downward).
   - Valance bottom hem: `Y = 0.82m, Z = 1.25m` (valance drop: 0.22m vertical).
   - Side valance return anchor: `Y = 1.45m, Z = 0.00m` to `Y = 1.04m, Z = 1.25m` to `Y = 0.82m, Z = 1.25m`.

2. **18-Stripe Canopy Slope**:
   - Divide width into 18 equal stripes: `dx = 6.40 / 18 ≈ 0.3556m`.
   - Alternating colors: Even indices = Hunter Green `[0.12, 0.38, 0.24, 1.0]`, Odd indices = Warm Cream `[0.93, 0.90, 0.82, 1.0]`.
   - Canopy top quad: `p1 = [x0, 1.45, 0.0]`, `p2 = [x1, 1.45, 0.0]`, `p3 = [x1, 1.04, 1.25]`, `p4 = [x0, 1.04, 1.25]`.
   - Normal: upward-forward `[0, 0.950, -0.312]`.

3. **Watertight Underside Ceiling Lining**:
   - Offset parallel quads 15mm downward: `p1 = [x0, 1.435, 0.0]`, `p2 = [x1, 1.435, 0.0]`, `p3 = [x1, 1.025, 1.245]`, `p4 = [x0, 1.025, 1.245]`.
   - Inverted downward normal: `[0, -0.312, -0.950]`.
   - Completely eliminates back-face culling transparency when viewed from sidewalk.

4. **Vertical Front Valance**:
   - Forward-facing quads (`Nz = +1.0`): `p1 = [x0, 1.04, 1.25]`, `p2 = [x1, 1.04, 1.25]`, `p3 = [x1, 0.82, 1.25]`, `p4 = [x0, 0.82, 1.25]`.
   - Underside back-face quad offset 10mm backward at `Z = 1.240m` with `Nz = -1.0`.

5. **Scallop Wave Hem Tabs & Continuous Piping Cord**:
   - For each stripe, create downward curve tab via `addTriangle([x0, 0.82, 1.25], [x1, 0.82, 1.25], [xMid, 0.77, 1.25], color)`.
   - Cap the bottom curve with continuous 8mm diameter braided white piping cord (`cPipe = [0.96, 0.96, 0.94, 1.0]`):
     - `addCylinder([x0, 0.82, 1.25], [xMid, 0.77, 1.25], 0.004, cPipe, 6)`
     - `addCylinder([xMid, 0.77, 1.25], [x1, 0.82, 1.25], 0.004, cPipe, 6)`

6. **Seamless Side Valance Returns (Zero Artifact Lines)**:
   - Left side triangular skirt: `addQuad([-3.20, 1.45, 0.0], [-3.20, 1.04, 1.25], [-3.20, 0.82, 1.25], [-3.20, 1.45, 0.0], cGreen, 0, 0, [0,0,1,0,1,1,0,1], [-1, 0, 0])`.
   - Right side triangular skirt: `addQuad([+3.20, 1.45, 0.0], [+3.20, 1.04, 1.25], [+3.20, 0.82, 1.25], [+3.20, 1.45, 0.0], cGreen, 0, 0, [0,0,1,0,1,1,0,1], [+1, 0, 0])`.
   - **Crucial Rule**: Do NOT place any horizontal cutting boxes across the side valances. Keep them as single outward-facing quads to avoid coplanar Z-fighting and diagonal ink bleeding.

7. **Coaxial Cantilever Strut Assemblies**:
   - 4 strut stations at `X = [-2.70, -0.90, +0.90, +2.70]`.
   - Wall anchor baseplate on yakisugi lintel: `addBox([sx, 0.72, 0.02], [0.08, 0.14, 0.04], cIron)`.
   - Wall clevis hinge: `[sx, 0.72, 0.045]`.
   - Front knuckle: `[sx, 1.015, 1.215]`.
   - True strut vector: `dx = 0, dy = 0.295, dz = 1.170` (14.0° upward incline).
   - Coaxial components placed along this vector:
     - 32mm tubular iron strut: `addCylinder(pWall, pFront, 0.016, cIron, 8)`.
     - Concentric turnbuckle sleeve: 48mm diameter `addCylinder(pT1, pT2, 0.024, cBolt, 8)`.
     - Hex lock nuts: 56mm diameter `addCylinder(pT1, pN1, 0.028, cIron, 8)` and `addCylinder(pN2, pT2, 0.028, cIron, 8)`.
   - Continuous 36mm front tubular crossbar: `addCylinder([-3.18, 1.015, 1.215], [+3.18, 1.015, 1.215], 0.018, cIron, 8)`.
   - 4 longitudinal upper rafter tubes under canvas: `addCylinder([sx, 1.43, 0.03], [sx, 1.025, 1.215], 0.014, cIron, 8)`.
   - **Crucial Rule (Recessed Knuckles)**: Place the front knuckles at `Z = 1.215m` with compact depth `0.034m` (max `Z = 1.232m`). This keeps all hardware 18mm behind the canvas at `Z = 1.250m`, completely eliminating dark square protrusion artifacts.

8. **Backpropagation**:
   - In Object 02 builder: call `obj2Master.mergeFrom(obj4Master, 0, 1.35, 2.41)`.
   - Result: Awning sits above central entrance threshold, below Kawara roof rafters.
   - Total Object 04 triangles: **1,276** (well within 1,800 tri limit).

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

---

## 10. Metaverse Exploration Landmark Mapping & Instant Fallback

The primary cultural landmark house at Kyojima Eki in the 3D metaverse exploration at `https://kokechan.preattention.ai` is constructed by mapping and fusing all four finalized objects:

- **Object 01**: Crimson Vending Machine (自販機) [27-call master with showcase window, coin slot, louvers, PVC tube]
- **Object 02**: Timber Facade & Lattice Doors (木造ファサード・格子戸) [Apron foundation, sliding doors, Kumiko windows, timber frame]
- **Object 03**: Kawara Ceramic Roof & Sheltering Eaves (瓦屋根・庇) [24 Hon-gawara corrugated flutes, Tomoe medallions, 3-tier Munegawara ridge crown, Onigawara, Nokidoi gutter & downspout, 16 rafter tails]
- **Object 04**: Striped Sun Awning & Cantilever Hardware (日除けテント・天幕) [18 alternating green/cream stripes, scallop hem, piping, 4 cantilever struts with coaxial turnbuckles & brass lock nuts]

### Spatial Coordinate Translation (Studio to Metaverse Anchor)
In the metaverse engine (`WorldEngine-C2hBfGVL.js`), the Kyojima Eki landmark anchor `o` is centered at world coordinates `[-11, 3.43, -11.84]`, with dimensions `width = 10.15m`, `height = 6.76m` (`r = 6.76m`):
- `X_anchor = X_studio`
- `Y_anchor = Y_studio - r/2 = Y_studio - 3.38m` (ground plane aligns at `Y = -3.38m` relative to anchor origin)
- `Z_anchor = Z_studio - 2.41m` (facade front wall aligns at `Z = 0.0m` relative to anchor origin)

### Triple-Tier Fail-Safe Fallback System
1. **Runtime Query Parameter**: Append `?legacy_house=1` or `?legacy_awning=1` to the URL (e.g., `https://kokechan.preattention.ai/?legacy_house=1`) to immediately activate `buildLegacyKyojimaEki(o, n, s, r)`.
2. **Automated Error Guard**: The composite construction is wrapped in a `try/catch` block that automatically falls back to `buildLegacyKyojimaEki` if any runtime exception occurs.
3. **Byte-for-Byte File Backup**: A verified backup file `WorldEngine-C2hBfGVL.js.bak-legacy-house` is maintained in `dist/assets/` for instant recovery.

