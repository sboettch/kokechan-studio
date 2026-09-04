# Object Queue — Kyojima Eki Living Archive

15-object street-level inventory for the Kyojima Eki landmark, plus Object 16 (baked scene composite).
All geometry is built in pure vanilla WebGL using the `GeometryBuffer` class — no external libraries.

## Approved & Locked

### Obj 01 — 🔴 Crimson Vending Machine (自販機)
- **Status**: APPROVED & LOCKED
- **Tris**: 3,858
- **Dimensions**: 0.95m × 2.05m × 0.85m
- **Camera**: `camCenter: [0, 1.02, 0]`, `camRadius: 3.2`
- **Textures**: `chassisTex` (texMode=1, PNG 358 KB front panel), `windowTex` (texMode=2, front glass display)
- **Key geometry** (27 builder calls):
  - `addBeveledChassis` — beveled red body (r=0.035 corner radius)
  - 12× ventilation louver `addBox` (right side, 0.478m x-offset)
  - 2× side rear panel `addBox`
  - 3× LED button row `addBox` at [−0.47, hy, 0.42] for hy in [0.42, 1.05, 1.68]
  - PVC drain tube `addBox` at [0.45, 0.52, −0.38]
  - Front glass quad `addQuad` texMode=2, emissive=0.45
  - Chassis texture quad `addQuad` texMode=1, emissive=0.05
  - Coin slot, brand stripe top cap, foot bolts (×4)
- **World position in composite**: `[2.45, 0, 2.65]` (offset applied by `mergeFrom`)

### Obj 02 — 🪵 Timber Facade & Lattice Doors (木造ファサード・格子戸)
- **Status**: APPROVED & LOCKED
- **Tris**: 7,782 (facade alone), ~11,640 (as `obj2CompositeGeom` with finalized Obj 01)
- **Dimensions**: 6.60m × 5.35m × 4.80m
- **Camera**: `camCenter: [0, 2.7, 0]`, `camRadius: 9.8`
- **Textures**: `windowTex` (2), `sideMuralTex` (3), `groundTex` (4), `upperTex` (5) + `chassisTex` (1) inherited from Obj 01
- **Key geometry**:
  - Concrete ground slab `addBox`
  - Stucco wall `addBox` [0, 2.75, 0] 6.4m × 5.35m × 4.8m
  - Washi ground threshold quad texMode=4
  - Washi upper window panel quad texMode=5
  - Cedar trim frame (left/right/top edge strips)
  - `addSolidAwning` — green-striped solid overhang
  - Corner corbel boxes ×2
  - **Kawara roof section** (38 calls, backpropagated from Obj 03):
    - Gabled roof quads (front slope, rear slope, soffit)
    - Gable end quads ×2
    - 24 Hon-gawara flute pairs (`addQuad` loop)
    - Munegawara ridge crown (3 stacked `addBox`)
    - Onigawara end crests ×2
    - Nokidoi gutter + downspout + elbow box
    - 6× rafter tail `addBox` at eave front
  - Front planters loop ×3 (`addBox` each)
  - Simplified machine placeholder (5 calls at vx=2.45, vz=2.65) — **covered by obj2CompositeGeom merge**

### Obj 03 — 🏯 Kawara Ceramic Roof & Sheltering Eaves (瓦屋根・庇)
- **Status**: APPROVED & LOCKED (standalone study; geometry also backpropagated into Obj 02)
- **Camera**: `camCenter: [0, 1.55, 0.2]`, `camRadius: 6.2`
- **Textures**: none — pure vertex-color geometry
- **Colors**: `rTileBase [0.25,0.27,0.30,1]`, `rTileDark [0.10,0.11,0.13,1]`, `rTileLight [0.40,0.43,0.48,1]`, `rGutter [0.20,0.22,0.25,1]`
- **Key geometry** (116-line builder block):
  - Roof planes: front slope, rear slope, soffit, gable ends (5 quads)
  - 24 Hon-gawara flute loops: each flute = eb1/eCrest/rCrest/rb1 quad pair
  - Continuous rib `addBox` per step
  - Tomoe crest discs `addBox` (round approximation)
  - Ridge + onigawara + gutter + downspout

## Object 16 — 🎬 Scene Composite (手動ベイク)
- **Status**: BAKE TO ACTIVATE (press 🍳 Bake Obj 16 button in header strip)
- **Tris**: ~11,640 (same as obj2CompositeGeom — obj2Master + obj1Master translated)
- **Dimensions**: full street section
- **Camera**: `camCenter: [1.2, 2.8, 0]`, `camRadius: 11.0`
- **Construction**:
  ```js
  fused.mergeFrom(obj2Master, 0, 0, 0)       // building + roof + placeholder
  fused.mergeFrom(obj1Master, 2.45, 0, 2.65) // finalized machine at street position
  fused.upload()
  ```
- **Note**: uses `obj2Master` (not `obj2CompositeGeom`) to avoid doubling the machine

## Queue (Objects 04–15)

| # | Emoji | Name | Japanese | Tris Budget | Dimensions |
|---|-------|------|----------|------------|------------|
| 04 | 🎪 | Striped Sun Awning | 日除けテント・天幕 | 1,800 | 6.40m × 1.02m × 1.25m |
| 05 | 🚲 | Alley Commuter Bicycle | ママチャリ・自転車 | TBD | TBD |
| 06 | 🎨 | Artist Mural & Noticeboard | 外壁ミューラル・掲示板 | TBD | TBD |
| 07 | 🪴 | Eaves Garden & Potted Flora | 軒下植木鉢・プランター | TBD | TBD |
| 08 | 🪑 | Weathered Engawa Bench | 木製縁台・ベンチ | TBD | TBD |
| 09 | 💧 | Rojison Rainwater Hand Pump | 路地尊・手押しポンプ | TBD | TBD |
| 10 | ⚡ | Concrete Utility Pole & Transformer | 電柱・変圧器・配線 | TBD | TBD |
| 11 | 🏮 | Street Lantern & Paper Chouchin | 軒下提灯・街路灯 | TBD | TBD |
| 12 | ❄️ | AC Outdoor Compressor Unit | 室外機・配管 | TBD | TBD |
| 13 | 📦 | Beverage Delivery Crates Stack | 飲料P箱スタック | TBD | TBD |
| 14 | 🪣 | Fire Defense Bucket & Stand | 消火バケツ・スタンド | TBD | TBD |
| 15 | 🪨 | Granite Paver & Alley Gutter | 敷石・側溝グレーチング | TBD | TBD |

## Geometry Color Palette

```js
const redPaint      = [0.82, 0.12, 0.12, 1.0]; // vending machine body
const steelMetal    = [0.82, 0.84, 0.88, 1.0]; // machine accents
const cedarDark     = [0.24, 0.17, 0.13, 1.0]; // facade trim
const cedarLight    = [0.46, 0.32, 0.22, 1.0]; // rafter tails
const stuccoWall    = [0.88, 0.84, 0.76, 1.0]; // building wall
const concreteGround= [0.45, 0.48, 0.52, 1.0]; // ground slab
const rTileBase     = [0.25, 0.27, 0.30, 1.0]; // kawara tile mid
const rTileDark     = [0.10, 0.11, 0.13, 1.0]; // kawara shadow
const rTileLight    = [0.40, 0.43, 0.48, 1.0]; // kawara highlight
const rGutter       = [0.20, 0.22, 0.25, 1.0]; // nokidoi gutter
```
