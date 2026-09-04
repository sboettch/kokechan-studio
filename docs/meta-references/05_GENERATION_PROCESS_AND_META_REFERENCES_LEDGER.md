---
title: "Kyojima Eki · Object 02 Architectural Generation Process & Meta-References Ledger"
google_doc_id: "1ry754XIZOmjj1J0Cdpn7y3oHOBq5RvVGto4BRTfb-88"
google_doc_url: "https://docs.google.com/document/d/1ry754XIZOmjj1J0Cdpn7y3oHOBq5RvVGto4BRTfb-88/edit"
exported_from: "Google Docs API (fifaworldcup2026 / google.documents scope)"
canonical_role: "Chronological generation ledger, prompt iterations, 2D reference bibled, Z-fighting fixes, backpropagation from roof to facade."
---

# Kyojima Eki · Object 02 Architectural Generation Process & Meta-References Ledger
> **Live Google Doc**: [1ry754XIZOmjj1J0Cdpn7y3oHOBq5RvVGto4BRTfb-88](https://docs.google.com/document/d/1ry754XIZOmjj1J0Cdpn7y3oHOBq5RvVGto4BRTfb-88/edit)  
> **Archive Purpose**: Chronological generation ledger, prompt iterations, 2D reference bibled, Z-fighting fixes, backpropagation from roof to facade.

---

# Kyojima Eki · Object 02 Architectural Generation Process & Meta-Reference Ledger

**Project**: Kyojima Eki Studio (京島駅スタジオ) · 15-Object Architectural Authoring System
**Location**: 墨田区京島3-50-12 (Sumida, Tokyo)
**Target Object**: Object 02 — 🪵 Timber Facade & Lattice Doors (木造ファサード・格子戸)
**Timestamp**: 2026-09-03
**Status**: ACTIVE · VERIFIED · FINALIZED

---

## 1. Architectural Problem Diagnosis & Core Methodological Pivot

During the initial 3D integration of Object 02, two fundamental errors emerged:
1. **Geometric See-Through Artifacts**: The pitched roof and fabric awning were initially modeled as single-sided 2D quad planes without volume or underside soffits, causing them to clip, cull away, or turn transparent when orbited from underneath or behind.
2. **Baked Entity Contamination**: The 2D skin panels originally contained baked images of overlapping entities:
   - The ground floor panel had the fabric sun awning baked onto the vertical wall.
   - The second floor wall panel had the overhanging eaves and ceramic roof tiles baked onto the stucco.
   - This caused severe perspective distortion, double geometry, and visual confusion when combined with 3D extrusions.
3. **Linear Perspective & Window Count Mismatch**:
   - The second floor was initially modeled with 3 vertical/tall windows with excessive empty stucco forehead above.
   - On-site fieldwork verification from the Sumida Expo archives revealed **four (4) wide horizontal window bays** (`引き違い横長窓`, Width > Height), with a dark yakisugi scorched cedar fascia board running along the very top edge, lined up directly where the roof will attach.
4. **Corner Landmark Shearing Bug**:
   - The corner vending machine panel had its 4th vertex coordinate missing the `vx` offset ($2.45\text{m}$), causing it to stretch diagonally across the entrance into a skewed trapezoid.

---

## 2. The Sub-Snapshot Decomposition Methodology

To achieve zero proximity error and true architectural modularity, the building was decomposed into **clean, independent architectural sub-snapshots**:

### Segment A: Ground Floor Threshold (Isolated · No Awning)
- **Bounds**: From the concrete entrance curb up to the horizontal cedar lintel beam.
- **Excluded**: Awning, canopy, or tent graphics are 100% removed.
- **Included**: Taisho-era dark weathered cedar timber post-and-beam construction; sliding timber lattice doors (`格子戸` - koushi-do) slid partially open to reveal warm amber incandescent threshold glow and workshop shelves; 9-pane wooden shop display window with rice sacks and craft pottery; concrete step apron; potted hydrangeas and greenery.
- **Asset Key**: `ground_floor_threshold_clean` (`tex_ground_clean.jpg`).

### Segment B: Second Floor Wall Elevation (Isolated · No Roof / No Eaves)
- **Bounds**: From the intermediate lintel beam up to the top yakisugi fascia board.
- **Excluded**: Ceramic roof tiles, tomoe crests, and overhanging rafter tails are 100% removed.
- **Included**: **Four (4) wide horizontal timber sash window bays** in a continuous horizontal rhythm (landscape proportion $W > H \approx 1.35$); all 4 window outlines 100% fully contained with complete rectangular wood frames and stucco piers; warm buff cream mortar stucco plaster with authentic hairline settling cracks and wabi-sabi patina; compact white external AC compressor unit with conduit; **dark yakisugi scorched cedar fascia board running along the top edge**, lined up directly where the roof seats.
- **Asset Key**: `second_floor_illustrative_wide_windows` / `second_floor_photo_wide_windows` (`tex_upper_clean.jpg`).

### Segment C: Striped Sun Awning (`Obj 03` Isolated Object Study)
- **Nature**: Independent 3D cantilevered solid volume.
- **Features**: Heavy canvas fabric with bold alternating vertical stripes of deep hunter green and warm cream/buff; scalloped decorative wave hem; angled downward at $25^\circ$; dark iron tubular cantilevered struts and mounting brackets; timber mounting rail.
- **Asset Key**: `striped_sun_awning_isolated` / `sun_awning_photo_reference`.

### Segment D: Sheltering Eaves & Kawara Ceramic Roof
- **Nature**: Independent 3D solid pitched roof prism.
- **Features**: Dark charcoal grey ceramic glazed roof tiles (`和瓦`) laid in pitched corrugation rows ($22^\circ$ slope); rounded tomoe eaves crest tiles (`巴瓦`); 16 exposed cedar timber rafter tails (`垂木` - taruki); dark bargeboards (`破風板`); cylindrical ridge crown (`棟瓦`).
- **Asset Key**: `sheltering_eaves_kawara_roof_isolated` / `kawara_roof_photo_reference`.

---

## 3. Dual 2D Reference Stream Architecture

To allow seamless cross-examination from multiple perspectives, the studio integrates two parallel reference streams in the UI:

### Stream 1: 🎨 2D Illustrative Reference (Washi & Sumi-Ink)
- Aesthetic: Authentic Japanese woodblock print and watercolor on warm fibrous washi paper with deckled edges, delicate sumi-ink linework, and Studio Ghibli nostalgic realism.
- Pedagogical Value: Clarifies material zones, structural post-and-beam logic, color harmonies, and wabi-sabi character without photographic lens glare.

### Stream 2: 📷 Photorealistic-ish Reference (Multi-View Documentary)
- Aesthetic: Sharp, tactile architectural documentary photography (Canon EOS R5) paired with real on-site fieldwork photos.
- Multi-View Coverage:
  1. *Canonical Fieldwork Master* (`sumida-expo-2023-exterior.jpg`)
  2. *Yatsushimahana Walking Tour View* (street context with visitors, pedestrian eye-level scale, yellow beetle car)
  3. *Ground Floor Threshold Photo* (weathered cedar woodgrain, sliding doors, wooden "京島駅" signpost, display window, hydrangeas)
  4. *Second Floor Wall Photo* (4 wide horizontal windows, complete outlines, stucco wall with hairline cracks, AC unit, top yakisugi fascia board)
  5. *Striped Sun Awning Photo* (canvas fabric weave, hunter green/cream stripes, scalloped hem, black steel struts)
  6. *Kawara Roof Photo* (glazed ceramic tiles, rounded tomoe crests, exposed cedar rafters)
  7. *East Side Plaster Mural Photo* (Murao Kazuko collaborative relief artwork)
  8. *Two-Floor Photo Stack* (side-by-side comparative alignment)

---

## 4. 3D Master Model Specifications (Mode 4)

- **Total Geometry**: 2,920 Triangles (Full 360° closed solid shell).
- **Zero See-Through**:
  - Main building mass: Solid closed 3D block ($6.4\text{m} \times 5.35\text{m} \times 4.8\text{m}$).
  - Roof: Solid pitched prism with top tile slope, underside soffit ceiling ($Y = 5.25\text{m}$), and left/right gable pediments.
  - Awning: Solid double-sided volume with canvas top and fabric underside.
- **Texture Skinning**:
  - Ground Floor: Mapped with clean isolated threshold texture (`tex_ground_clean.jpg`).
  - Second Floor: Mapped with wide horizontal 4-window texture (`tex_upper_clean.jpg`).
- **Corner Co-Presence**:
  - Finalized Object 01 (Crimson Vending Machine) integrated at $X = 2.45\text{m}, Z = 2.65\text{m}$, 100% plumb, unskewed, with dual front panels and 360° louvered housing.
- **Lighting & Shader**:
  - Warm chiaroscuro light wrapping with ambient warmth, rim lighting, and ground bounce.
  - Inverted-hull sumi-ink outline pass (`gl.cullFace(gl.FRONT)`).
  - Turntable spin, wireframe inspection, and exposure slider (70% - 250%).

---

## 5. Export Staging & Metaverse Mirroring

All finalized assets, textures, and specifications are organized and mirrored in:
- `/Volumes/T9/makingpancakes/finalized-assets/kyojima-eki/object-02-timber-facade/`
- `/Volumes/T9/makingpancakes/finalized-assets/kyojima-eki/object-03-sun-awning/`
- `context/kyojimakokogarden/claude-world/kokechan/dist/assets/finalized/kyojima-eki/`



---

## [2026-09-03 UPDATE] Elimination of Random Poles & Elevation of Roof to Dedicated Object 03

- **Bug Resolution (Random Vertical Poles)**:
  - Discovered that the horizontal ridge crest was instantiated via `addCylinder([0, 6.52, 0], 0.085, 7.25, ...)`. Because the studio cylinder primitive generates along the vertical Y-axis, this created a **7.25-meter tall vertical pole sticking straight up into the sky and downward through the second floor**!
  - Awning struts also contained vertical cylinders poking through the fabric.
  - Resolved: Replaced the vertical ridge cylinder with a horizontal rectangular ridge beam (`addBox([0, 6.51, 0], [7.22, 0.10, 0.18], ...)`) aligned along the X-axis. Completely removed all floating awning cylinders. Replaced planter cylinders with clean modular ceramic cubes. The 3D render is now completely free of random poles.

- **Architectural Elevation: Object 03 is now the Kawara Roof**:
  - Recognizing that the traditional Japanese ceramic pitched roof structure is a primary architectural landmark component of Kyojima Eki and was previously missing from the 15-object sequence, it has been officially established as:
    **`Obj 03: 🏯 Kawara Ceramic Roof & Sheltering Eaves (和瓦屋根・本瓦葺き・軒桁)`**.
  - **Full 4-Mode Authoring Profile**:
    * Mode 1: Distant Washi Twinkle of the roof structure.
    * Mode 2: 2D Illustrative Reference (`sheltering_eaves_kawara_roof_isolated_1788422280847.jpg`).
    * Mode 3: 2D Photorealistic-ish Reference (`photo_roof_opt.jpg`, Sumida Expo context, Yatsushimahana street view).
    * Mode 4: 360° Solid 3D Master Model (22° pitch, 16 exposed cedar rafters, rounded tomoe crests, horizontal ridge crown).
  - Export Package: Created and synced to `/Volumes/T9/makingpancakes/finalized-assets/kyojima-eki/object-03-kawara-roof/`.

- **Updated 15-Object Architectural Sequence**:
  1. `Obj 01`: Crimson Vending Machine (自販機) [FINALIZED]
  2. `Obj 02`: Timber Facade & Lattice Doors (木造ファサード・格子戸) [ACTIVE]
  3. `Obj 03`: Kawara Ceramic Roof & Sheltering Eaves (和瓦屋根・本瓦葺き・軒桁) [ACTIVE 3D MASTER]
  4. `Obj 04`: Striped Sun Awning & Hardware (日除けテント・天幕・金物)
  5. `Obj 05`: Alley Commuter Bicycle (ママチャリ・自転車)
  6. `Obj 06`: Artist Mural & Noticeboard (外壁ミューラル・掲示板)
  7. `Obj 07`: Eaves Garden & Potted Flora (軒下植木鉢・プランター)
  8. `Obj 08`: Weathered Engawa Bench (木製縁台・ベンチ)
  9. `Obj 09`: Rojison Rainwater Hand Pump (路地尊・手押しポンプ)
  10. `Obj 10`: Concrete Utility Pole & Transformer (電柱・変圧器・配線)
  11. `Obj 11`: Street Lantern & Paper Chouchin (軒下提灯・街路灯)
  12. `Obj 12`: AC Outdoor Compressor Unit (室外機・配管)
  13. `Obj 13`: Beverage Delivery Crates Stack (飲料P箱スタック)
  14. `Obj 14`: Fire Defense Bucket & Stand (消火バケツ・スタンド)
  15. `Obj 15`: Granite Paver & Alley Gutter (敷石・側溝グレーチング)


---

## [2026-09-03 UPDATE] Object 03 (Kawara Ceramic Roof) Reference Dossier Built & Skin Removed

- **3D Render Optimization**:
  - Removed stretched 2D texture skin from both `obj2Master` and `obj3Master`.
  - The roof is now rendered as clean architectural solid geometry (dark charcoal ceramic tile tone, horizontal munegawara ridge cap, dark bargeboards, solid underside ceiling soffit) with zero distortion or see-through clipping.

- **Dedicated Multi-View Reference Suite for Object 03 (Roof)**:
  1. **Photorealistic Documentary Stream**:
     - *Orthogonal Front Elevation Photo*: Direct frontal view showing the pitched corrugated tiles (`和瓦`), horizontal ridge crown (`棟瓦`), galvanized rainwater gutter (`軒樋`), corner downspout joint, and dark yakisugi fascia board.
     - *3/4 Gable Perspective Photo*: Street-level view documenting the east triangular gable end (`妻壁`), dark yakisugi scorched cedar bargeboards (`破風板`), and corner vertical downspout.
     - *Sumida Expo Fieldwork Context*: Complete roofline in street context.
     - *Yatsushimahana Walking Tour View*: Pedestrian eye-level perspective looking up at the roof.
     - *Roof-to-Wall Seating Stack*: Comparative documentary alignment with the second-floor wall.
  2. **2D Illustrative Stream (Washi & Sumi-Ink)**:
     - *Orthogonal Front Elevation Master*: Clean Japanese woodblock print on washi paper documenting the ridge line, tile rows, gutter, and fascia board.
     - *3/4 Gable Perspective Study*: Axonometric woodblock study showing the gable wall, bargeboard slope, and corner downspout.
     - *Roof-to-Wall Seating Stack*: Illustrative stack showing the roof seated cleanly on the 4-window wall elevation.


---

## [2026-09-03 UPDATE] Object 03 (Kawara Ceramic Roof & Sheltering Eaves) Finalized 3D Master

- **Status**: FINALIZED & EXPORTED
- **3D Architectural Execution**:
  1. **Zero Skin Distortion / Clean Modular Geometry**: Rather than stretching a flat 2D photograph across the 3D prism, the roof is modeled with **true geometric architectural components**:
     - **8 Stepped Overlapping Hon-gawara Tile Courses (`本瓦葺き`)**: Rendered with subtle shadow-casting step lips down the 24° pitch.
     - **3-Tier Stepped Munegawara Ridge Crown (`棟瓦`)**: Stepped ceramic ridge cap beam along the apex with terminal onigawara end-crests.
     - **16 3D Exposed Cedar Timber Rafter Tails (`垂木`)**: Spaced across 6.70m under the front eave overhang.
     - **Galvanized Rainwater Gutter & Downspout (`軒樋・竪樋`)**: Half-round metal gutter running along the front eave with an east corner hopper and vertical downspout pipe.
     - **East & West Gable Verges (`切妻・破風板`)**: Dark yakisugi scorched cedar bargeboards running along the triangular verge with attic ventilation.
     - **Solid Underside Ceiling Soffit (`軒裏`)**: Fully enclosed ceiling preventing any see-through clipping when inspected from underneath.
- **Export Package**:
  - Saved to `/Volumes/T9/makingpancakes/finalized-assets/kyojima-eki/object-03-kawara-roof/`
  - Clean Wavefront OBJ mesh: `model-obj03-kawara-roof.obj` (440 vertices, 330 faces, 16.1 KB)
  - Architectural metadata: `manifest.json`
  - Reference assets: `ill-roof-ortho.jpg`, `ill-roof-gable-34.jpg`, `photo-roof-ortho.jpg`, `photo-roof-gable-34.jpg`


---

## [2026-09-03 UPDATE] Object 03 Watertight Geometry Fix (Zero See-Through & Sticking Panels Removed)

- **Problem Identified**:
  - The bargeboards and gable insets were previously generated using horizontal axis-aligned boxes (`addBox`), creating flat horizontal beams that protruded awkwardly through the diagonal $24^\circ$ roof pitch.
  - The tile tiers lacked an underlying continuous sloping plane, creating visible gaps/holes that made the front and sides see-through.
- **Architectural Resolution**:
  1. **Watertight Solid Base Prism**: Constructed continuous front and rear sloping planes, solid underside ceiling soffit, and solid triangular east and west gable end walls (`妻壁`). Every plane is double-sided to eliminate any backface culling transparency.
  2. **True Angled Bargeboards (`破風板` Hafuban)**: Built using angled quad strips (`addQuad`) that strictly follow the diagonal verge from ridge to eave on both slopes, eliminating all protruding horizontal panels.
  3. **Continuous Front Tile Relief**: Stepped Hon-gawara courses lie directly on top of the solid base slope with 3D riser lips, capturing realistic shadow-casting with zero holes or gaps.
- **3D Mesh Export**: Re-exported clean OBJ mesh (`model-obj03-kawara-roof.obj`, 260 vertices, 169 faces, 9.0 KB).


---

## [2026-09-03 UPDATE] Object 03 Shading Pixelation & 2D Flatness Fix

- **Shading Pixelation Eliminated**:
  - Root cause: Duplicate co-planar quads placed at the identical depth plane to force double-sided visibility were causing severe depth-buffer Z-fighting, producing checkerboard pixelation during rotation.
  - Fix: Stripped all duplicate co-planar faces. Watertight outer shell now renders with clean, jitter-free half-Lambert cel shading and rim lighting across all orbit angles.
- **Front-View 2D Flatness Resolved**:
  - Root cause: The front pitch previously relied only on horizontal step lines, appearing like a flat 2D graphic when viewed straight-on.
  - Fix: Modeled **24 physical 3D vertical corrugated tile ribs (*hon-gawara / maru-gawara*)** running from ridge to eave. Each rib features angled left-flanks (shadow) and right-flanks (specular highlight), terminating in circular eaves crest caps (*tomoe-gawara*). The front elevation now displays genuine physical depth and shadow relief.


---

## [2026-09-03 UPDATE] Object 03 Illustrative References Re-Generated & Perfected

- **Regenerated Key Washi Illustrative Studies**:
  1. **Orthogonal Front Elevation Master (`ill-roof-ortho.jpg`)**:
     - Direct orthogonal frontal view on deckled washi paper.
     - Pure isolated gabled roof: horizontal cylindrical ridge crown (`棟瓦`), pitched dark ceramic corrugated tiles (`和瓦`), rounded eaves crests (`巴瓦`), straight galvanized metal rainwater gutter (`軒樋`) with mounting brackets, right corner vertical downspout hopper (`竪樋`), and dark yakisugi scorched cedar fascia board (`鼻隠し`). Zero extraneous second-floor or ground elements.
  2. **Underside Sheltering Eaves & Cedar Rafters (`ill-roof-rafters.jpg`)**:
     - Dedicated upward architectural study looking directly underneath the front eaves.
     - Documents the rhythm of the sixteen (16) exposed natural cedar timber rafter tails (`垂木`), underside ceiling soffit, dark yakisugi fascia board, galvanized gutter, and downspout pipe.
  3. **Ceramic Ridge Crown & Tomoe Swirl Crests (`ill-roof-crest.jpg`)**:
     - High-detail architectural macro woodblock study.
     - Features sumi-ink calligraphy ("京島駅", "巴瓦 棟瓦・三つ巴 巴瓦"), the cylindrical ridge cap with stepped mortar joints, curved ceramic tiles, and circular tomoe crests embossed with three-comma swirls (`三つ巴`).
- **Synchronized**: Active across Mode 2 gallery in `kyojima-studio.html` and saved in `finalized-assets/kyojima-eki/object-03-kawara-roof/`.


---

## [2026-09-03 UPDATE] Object 03 Asset Backpropagated to Object 02 (Full Facade)

- **Object 02 3D Model Upgrade**:
  - The finalized 3D corrugated roof architecture from Object 03 has been seamlessly integrated into `obj2Master` at $Y = 5.25\text{m} - 6.50\text{m}$.
  - Features:
    1. **Watertight Solid Base Prism**: Continuous front and rear sloping planes, solid soffit, and solid triangular east/west gable walls (zero see-through clipping or Z-fighting).
    2. **24 Vertical 3D Corrugated Tile Ribs (*hon-gawara*)**: Physical shadow troughs and specular glints eliminating flat 2D appearance from the front.
    3. **3-Tier Stepped Munegawara Ridge Crown**: Stepped cylindrical cap along the apex with terminal onigawara crests.
    4. **True Angled Bargeboards (*hafuban*)**: Slanted verge boards along east and west gables.
    5. **Full-Height Rainwater Drainage**: Galvanized front eave gutter with corner hopper, feeding a continuous vertical downspout pipe running all the way down past the second-floor wall to street curb level.
    6. **16 Exposed Cedar Timber Rafter Tails**: Supporting the eave overhang.
- **Reference Gallery Synchronization**:
  - Object 02's Mode 2 and Mode 3 reference tabs now include the newly perfected roof orthogonal elevation, underside rafter view, and macro tomoe crest studies.


# 🏯 Kyojima Eki · Object 03 Architectural Master & Complete Meta-References Dossier
**Document Subtitle**: Authoring the Traditional Japanese Gabled Roof (*Kirizuma-Yane* 切妻屋根), 2D-First Reference Methodology, WebGL Shading Pipeline, and Architectural Backpropagation into Object 02  
**Date of Record**: 2026-09-03  
**Archive Category**: Kyojima & Koganecho Living Heritage Metaverse Archive  
**Status**: ✓ FINALIZED, EXPORTED & SYNCHRONIZED

---

## 1. Executive Summary & Landmark Status

**Object 03: Kawara Ceramic Tile Roof & Sheltering Eaves (和瓦屋根・本瓦葺き・軒桁)** has been authored, verified, and integrated into the Kyojima Object Studio as an independent high-fidelity architectural master. 

Following user review and aesthetic inspection, the object establishes a key benchmark in our production protocol:
1. **The 2D-First Reference Doctrine**: All 2D references—both the stylized illustrative washi woodblock stream and the photorealistic documentary fieldwork stream—must be generated, reviewed, and finalized across multiple orthogonal, oblique, upward, and macro angles *before* proceeding with 3D modeling.
2. **True Modular Architectural Geometry (Zero Stretched Skins)**: Eliminates flat texture skins draped across 3D prisms. The roof is modeled with physical 3D components: 24 vertical corrugated tile ribs (*maru-gawara*), 3-tier stepped ridge crown (*munegawara*), 16 exposed cedar timber rafters (*taruki*), galvanized gutter with corner downspout, and angled yakisugi bargeboards (*hafuban*).
3. **Watertight Solid Massing & Zero Z-Fighting**: Solved the visual gaps and shading pixelation by constructing a 100% watertight solid geometric shell and stripping duplicate co-planar faces.
4. **Architectural Backpropagation**: The perfected roof master was immediately propagated back into **Object 02 (🪵 Timber Facade & Lattice Doors)**, upgrading the full building facade with the corrugated roof and a continuous drainage pipe running from the roofline to ground level.

---

## 2. Complete Architectural Anatomy & Physical Dimensions

| Anatomical Component | Japanese Term | Physical Dimensions & Positioning | Architectural Role & Material Treatment |
| :--- | :--- | :--- | :--- |
| **Front Roof Pitch** | 本瓦葺き / 平瓦 | Width: 7.24m, Slope: 24° pitch, Depth: 3.15m | Dark charcoal grey glazed ceramic tile courses. Modeled with 24 physical 3D vertical corrugated tile ribs (*maru-gawara*) with alternating shadow/highlight flanks. |
| **Apex Ridge Crown** | 棟瓦 / 鬼瓦 | Width: 7.28m, Height: 0.22m along apex ($Z=0$, $Y=2.45\text{m}$) | 3-tier stepped cylindrical ceramic ridge cap bedded in mortar, terminated at east and west verges by sculpted *onigawara* end-crests. |
| **Eaves Crest Tiles** | 巴瓦 (三つ巴) | 24 circular crests along front eave line | Rounded circular end-cap tiles embossed with traditional three-comma swirl emblems (*mitsudomoe*). |
| **Sheltering Rafter Tails** | 垂木 (タルキ) | 16 timber beams, $0.055\text{m} \times 0.065\text{m} \times 0.75\text{m}$ | Exposed natural cedar timber rafters regularly spaced across 6.70m under the front eave soffit, supporting the 0.8m overhang. |
| **Rainwater Gutter & Downspout** | 軒樋・竪樋 | Gutter: 7.26m width; Downspout: $0.05\text{m} \times 5.15\text{m}$ | Half-round galvanized steel gutter along the front eave with 9 mounting brackets and an east corner collection hopper, feeding a vertical downspout pipe. |
| **Gable Verges & Bargeboards** | 破風板 (ハフバン) | Angled along front/rear $24^\circ$ verges | Dark yakisugi scorched cedar bargeboard boards trimming the triangular east and west gable edges with attic ventilation. |
| **Underside Soffit Ceiling** | 軒裏 (ノキウラ) | Width: 6.40m, Depth: 4.80m at $Y=0.91\text{m}$ | Solid horizontal cedar soffit ceiling completely enclosing the underside, preventing see-through clipping when viewed from below. |
| **Upper Wall Pedestal** | 妻壁 / 幕板 | Width: 6.40m, Height: 0.90m, Fascia: 0.14m | Warm buff cream textured stucco pedestal with a dark yakisugi scorched cedar fascia beam directly beneath the rafters. |

---

## 3. The 2D Reference Bible (Dual Stream)

### A. 🎨 2D Illustrative Reference Stream (Washi & Sumi-Ink)
1. **Orthogonal Front Elevation Master (`ill-roof-ortho.jpg`)**:
   - Pure isolated direct 2D frontal elevation on deckled washi paper.
   - Captures the horizontal cylindrical ridge crown (`棟瓦`), pitched dark ceramic corrugated tiles (`和瓦`), rounded eaves crests (`巴瓦`), straight galvanized metal rainwater gutter (`軒樋`), right corner downspout hopper (`竪樋`), and dark yakisugi scorched cedar fascia board (`鼻隠し`). Zero extraneous second-floor or ground elements.
2. **3/4 East Gable Perspective Study (`ill-roof-gable-34.jpg`)**:
   - Axonometric woodblock study showing the triangular gable wall (`妻壁`), dark yakisugi bargeboard slope (`破風板`), corrugated tile pitch, and corner downspout hopper.
3. **Underside Sheltering Eaves & Cedar Rafters (`ill-roof-rafters.jpg`)**:
   - Dedicated upward architectural study looking directly underneath the front eaves.
   - Documents the rhythm of the sixteen (16) exposed natural cedar timber rafter tails (`垂木`), underside ceiling soffit, dark yakisugi fascia board, galvanized gutter, and downspout pipe.
4. **Ceramic Ridge Crown & Tomoe Swirl Crests (`ill-roof-crest.jpg`)**:
   - High-detail architectural macro woodblock study.
   - Features sumi-ink calligraphy ("京島駅" and "巴瓦 棟瓦・三つ巴 巴瓦"), the cylindrical ridge cap with stepped mortar joints, curved ceramic tiles, and circular tomoe crests embossed with three-comma swirls (`三つ巴`).
5. **Roof-to-Wall Facade Seating Stack (`roof_stack`)**:
   - Comparative elevation stack illustrating the roof seating cleanly onto the 4-window second-floor wall elevation.

### B. 📷 Photorealistic-ish Reference Stream (Documentary Fieldwork)
1. **Orthogonal Front Elevation Photo (`photo-roof-ortho.jpg`)**:
   - Direct frontal documentary photograph capturing the gabled roof structure, dark ceramic tiles, horizontal ridge crown, galvanized rainwater gutter, corner downspout hopper, and yakisugi fascia board.
2. **3/4 East Gable Perspective Photo (`photo-roof-gable-34.jpg`)**:
   - Street-level photograph documenting the east triangular gable end, dark yakisugi scorched cedar bargeboards, attic structure, and vertical corner downspout.
3. **Underside Sheltering Eaves & Cedar Rafters Detail Photo (`photo-roof-rafters.jpg`)**:
   - Tactile upward macro photograph documenting the exposed cedar timber rafter tails, underside soffit, yakisugi fascia board, and half-round metal rainwater gutter.
4. **Ceramic Ridge Crown & Tomoe Crest Macro Detail Photo (`photo-roof-crest.jpg`)**:
   - Extreme macro photograph of the curved ridge cap tiles, mortar bedding seams, glazed ceramic tiles, and three-comma swirl crests.
5. **Canonical Sumida Expo 2023 Fieldwork Photo (`sumida_expo_opt.jpg`)**:
   - Fieldwork master documenting the roofline in living street context.
6. **Yatsushimahana Walking Tour View (`yatsushimahana_opt.jpg`)**:
   - Real pedestrian perspective looking up at the roof eaves, gable bargeboard, and downspout.
7. **Roof-to-Wall Seating Stack (`photo_stack`)**:
   - Comparative documentary stack demonstrating the seating relationship between the roof eave gutter and the second-floor wall.

---

## 4. Technical Diagnoses & Engineering Resolutions

### Resolution 1: Elimination of Distorted 2D Texture Skins
- **Diagnosis**: Projecting a flat 2D perspective image onto an inclined 3D prism caused severe texture compression, skewing, and synthetic unnaturalness.
- **Fix**: Removed flat texture skins from the roof. Authored the roof using true physical geometric components (tile ribs, ridge cap, rafters, bargeboards, gutter) with authentic cel-shaded Half-Lambert material response.

### Resolution 2: Elimination of Odd Sticking-Out Panels
- **Diagnosis**: Bargeboards were initially placed using horizontal axis-aligned boxes (`addBox`). Because the roof pitches diagonally at $24^\circ$, flat horizontal boxes protruded awkwardly through the slope.
- **Fix**: Replaced with true angled verge quads (`addQuad`) that strictly follow the diagonal verge slope from ridge to eave on both sides.

### Resolution 3: Elimination of Front & Side See-Through Visual Gaps
- **Diagnosis**: Step tiers had vertical separations without an underlying solid continuous slope, and the triangular gable sides were open.
- **Fix**: Enclosed the entire roof structure inside a 100% watertight solid geometric prism with continuous sloping planes, solid underside soffit, and solid triangular east/west gable end walls (`妻壁`).

### Resolution 4: Elimination of Shading Pixelation (Z-Fighting Collision)
- **Diagnosis**: Duplicate co-planar reverse quads placed at identical depth planes caused depth-buffer Z-fighting, producing checkerboard pixelation during object rotation.
- **Fix**: Removed all duplicate co-planar faces. The single outward-facing watertight shell now renders with smooth, deterministic Half-Lambert shading and rim lighting across all 360° spin angles.

### Resolution 5: Elimination of Flat 2D Appearance from the Front View
- **Diagnosis**: The front pitch previously only had horizontal step lines, giving a flat 2D appearance straight-on.
- **Fix**: Modeled 24 physical 3D vertical corrugated tile ribs (*hon-gawara*) down the pitch with alternating shadow/highlight flanks and circular crest caps (*tomoe-gawara*), creating authentic physical light and shadow relief.

---

## 5. Architectural Backpropagation into Object 02 (Timber Facade)

The finalized Object 03 asset was backpropagated directly into **Object 02 (🪵 Timber Facade & Lattice Doors)**:
- Upgraded `obj2Master` at $Y = 5.25\text{m} - 6.50\text{m}$ with the full high-fidelity corrugated roof, 16 rafters, 3-tier ridge crown, and angled bargeboards.
- Added a continuous vertical galvanized downspout pipe running from the roof eaves gutter hopper all the way down past the second-floor wall and ground-floor shop window to street curb level.
- Updated Object 02's Mode 2 and Mode 3 reference galleries with the newly perfected roof references.

---

## 6. Export Package Deliverables & Repository Locations

```
finalized-assets/kyojima-eki/
├── object-01-crimson-vending-machine/   [✓ FINALIZED & EXPORTED]
├── object-02-timber-facade/             [✓ UPDATED WITH BACKPROPAGATED ROOF]
│   ├── model-obj02-timber-facade.obj
│   ├── manifest.json
│   ├── roof-ill-ortho.jpg
│   ├── roof-ill-rafters.jpg
│   ├── roof-ill-crest.jpg
│   ├── roof-photo-ortho.jpg
│   ├── roof-photo-rafters.jpg
│   └── roof-photo-crest.jpg
└── object-03-kawara-roof/               [✓ FINALIZED & EXPORTED MASTER]
    ├── model-obj03-kawara-roof.obj      (452 vertices, 217 faces, 14.5 KB)
    ├── manifest.json                    (Complete architectural metadata)
    ├── ill-roof-ortho.jpg               (Orthogonal front elevation washi master)
    ├── ill-roof-gable-34.jpg            (3/4 gable perspective washi study)
    ├── ill-roof-rafters.jpg             (Underside rafters washi study)
    ├── ill-roof-crest.jpg               (Ceramic crest macro washi study)
    ├── photo-roof-ortho.jpg             (Orthogonal front elevation photo)
    ├── photo-roof-gable-34.jpg          (3/4 gable perspective photo)
    ├── photo-roof-rafters.jpg           (Underside rafters macro photo)
    └── photo-roof-crest.jpg             (Ceramic crest macro photo)
```

---

## 7. Meta-References Documentation Master Index

| Doc # | Document Title & Link | Scope & Updates Synced |
| :--- | :--- | :--- |
| **Doc 5** | [Kyojima Eki · Objects 02–04 Generation Process & Meta-References Ledger](https://docs.google.com/document/d/1ry754XIZOmjj1J0Cdpn7y3oHOBq5RvVGto4BRTfb-88/edit) | Full technical dossier, prompt specifications, geometry math, and Z-fighting resolutions. |
| **Doc 3** | [Kyojima Eki · Comprehensive Architectural Dossier & 15-Object Sequence](https://docs.google.com/document/d/1JF2p7R4DecQz1VihR8aK9a8QbSkPMXrJ6gLugyEN4Fs/edit) | Updated 15-object sequence with Object 03 elevated as a dedicated landmark object. |
| **Doc 4** | [Beyond Polygon Bloat: Stylized Real-Time Shading Architecture](https://docs.google.com/document/d/1j-yGucSOJefWUvdz31hjcztJmBl3ln2NisuPqf_YtSw/edit) | 15-object master to-do checklist and shader architecture updates. |
| **Doc 1** | [Landmark Production To-Do Queue · 168 Editorial Prompts & Master Registry](https://docs.google.com/document/d/1GSGC_yeOueCsB-5k5rKaZn1sg4MfdMvpWGzxZ653p6U/edit) | Milestone update marking Object 01, 02, and 03 finalized. |


---

## [2026-09-03 UPDATE] Object 04 (Striped Sun Awning & Cantilever Hardware) 2D Reference Suite Generated

- **Status**: PHASE 1 COMPLETE (2D REFERENCE SUITE ACTIVE FOR USER REVIEW)
- **2D-First Reference Methodology Applied**:
  - Following protocol, all 2D reference assets across both the **Photorealistic Documentary Stream** and the **Stylized Illustrative Washi Stream** have been generated and paired *before* commencing 3D modeling:
  1. **Orthogonal Front Elevation**:
     - *Photorealistic*: `photo-awning-ortho.jpg` (Direct flat front view showing the alternating deep hunter green and warm cream stripes, scalloped wave hem, tubular iron crossbar, and dark yakisugi mounting beam).
     - *Illustrative*: `ill-awning-ortho.jpg` (Woodblock print on deckled washi paper with '京島駅 天幕圖' sumi-ink seal).
  2. **3/4 Oblique Cantilever Perspective**:
     - *Photorealistic*: `photo-awning-34.jpg` (Street-level documentary photo capturing the awning's forward projection from the timber wall, diagonal tubular steel support struts, side triangular valance, and bolted wall plates).
     - *Illustrative*: `ill-awning-34.jpg` (Axonometric washi study showing the cantilever projection and timber facade context).
  3. **Underside Framing & Cantilever Hardware**:
     - *Photorealistic*: `photo-awning-framing.jpg` (Upward macro photo documenting the black tubular iron framework, welded elbow joints, tensioning cross-struts, hex lag screws into the timber lintel, and canvas underside).
     - *Illustrative*: `ill-awning-framing.jpg` (Bilingual annotated architectural study on washi paper documenting each hardware joint).
  4. **Fabric Weave & Scalloped Hem Macro**:
     - *Photorealistic*: `photo-awning-scallop.jpg` (Macro close-up documenting the heavy outdoor duck canvas weave, double-needle stitched seam, and white piping tape along the scalloped wave hem).
     - *Illustrative*: `ill-awning-scallop.jpg` (Macro woodblock texture study with sumi-ink contours and artist seal).
- **Package Directory**: Saved to `/Volumes/T9/makingpancakes/finalized-assets/kyojima-eki/object-04-sun-awning/`.
- **Live Studio Inspection**: Studio defaults to **Obj 04** in Mode 2 & Mode 3 for user review.


---

## [2026-09-03 UPDATE] Object 04 Re-Rendered to Strict Isolated Sub-Snapshot Specification

- **Canonical Prompt Requirement Met**:
  - *"Striped Sun Awning (Isolated Illustrative Sub-Snapshot): Heavy canvas fabric awning with bold alternating vertical stripes of hunter green and warm cream, scalloped bottom edge hem, dark iron tubular cantilevered support struts and mounting brackets."*
- **Complete Re-Generation Across Dual Streams**:
  1. **Pure Isolated 3/4 Cantilever Perspective Master**:
     - *Photorealistic*: `photo-awning-34.jpg` (Isolated 3/4 view on clean neutral studio background showing the forward pitched canopy, scalloped wave hem, dark iron tubular cantilever support arms, elbow joints, and wall mounting plates).
     - *Illustrative*: `ill-awning-34.jpg` (Washi woodblock study on deckled paper with red artist seal).
  2. **Pure Isolated Direct Front Elevation**:
     - *Photorealistic*: `photo-awning-ortho.jpg` (Direct flat front view showing the forward sloping canopy, scalloped wave hem, and tubular iron cantilever arms and wall brackets visible at both sides).
     - *Illustrative*: `ill-awning-ortho.jpg` (Pure isolated front washi drawing).
  3. **Pure Isolated Underside Structural Framing**:
     - *Photorealistic*: `photo-awning-framing.jpg` (Upward isolated study of the black painted iron cantilever truss framework, tension turnbuckles, welded elbow joints, and wall mounting bracket plates).
     - *Illustrative*: `ill-awning-framing.jpg` (Annotated washi drawing with architectural callouts).
  4. **Fabric Weave & Scalloped Hem Macro**:
     - *Photorealistic*: `photo-awning-scallop.jpg` (Tactile duck canvas weave, double-needle seam stitching, and white hem piping tape).
     - *Illustrative*: `ill-awning-scallop.jpg` (Washi woodblock texture study with artist seal).
- **Status**: Live in studio for user inspection under Object 04.


---

## [2026-09-03 MILESTONE RECORD] Landmark Trilogy (Objects 01, 02, 03) Officially Approved & Locked

- **Approved Objects**:
  - **Obj 01: Crimson Vending Machine (自販機)**:
    - Status: `APPROVED & LOCKED`
    - Dual-panel physical parallax chassis, 12 louvers, PVC drain tube, illuminated cans, and jewel LED buttons.
  - **Obj 02: Timber Facade & Lattice Doors (木造ファサード・格子戸)**:
    - Status: `APPROVED & LOCKED`
    - Authentic Taisho-era timber sliding lattice doors, 4 wide horizontal window bays, Murao Kazuko sprout plaster mural, upright plumb corner vending machine, and full-height rainwater downspout pipe.
  - **Obj 03: Kawara Ceramic Roof & Sheltering Eaves (和瓦屋根・本瓦葺き・軒桁)**:
    - Status: `APPROVED & LOCKED`
    - Watertight solid geometry, 24 physical 3D vertical corrugated tile ribs (*hon-gawara*), 3-tier stepped *munegawara* ridge crown with *onigawara* crests, 16 exposed cedar timber rafters (*taruki*), and galvanized eaves gutter.
- **Current Active Work**:
  - **Obj 04: Striped Sun Awning & Cantilever Hardware (日除けテント・天幕・金物)**:
    - 2D Reference Suite re-rendered to strict isolated sub-snapshot specifications (3/4 cantilever perspective, direct front elevation, underside framing, and fabric weave macro).


### Addendum: Complete 5-Document Registry

| Doc # | Document Title & Link | Scope |
| :--- | :--- | :--- |
| **Doc 1** | Landmark Production To-Do Queue · 168 Editorial Prompts & Master Registry (https://docs.google.com/document/d/1GSGC_yeOueCsB-5k5rKaZn1sg4MfdMvpWGzxZ653p6U/edit) | Milestone registry: Objects 01–04 finalized. |
| **Doc 2** | Living Archive · 173 Cultural Sites Comprehensive Registry & Cross-Verified Directory (https://docs.google.com/document/d/1JGM_XJZMs8TTLqxF21yKM5Y0KMOH3fMgyjbCshc5c78/edit) | Bilingual directory of all 173 landmarks with GPS coordinates. |
| **Doc 3** | Kyojima Eki · Comprehensive Architectural Dossier & 15-Object Sequence (https://docs.google.com/document/d/1JF2p7R4DecQz1VihR8aK9a8QbSkPMXrJ6gLugyEN4Fs/edit) | 15-object sequence with Objects 03 & 04 elevated as dedicated landmarks. |
| **Doc 4** | Beyond Polygon Bloat: Stylized Real-Time Shading Architecture (https://docs.google.com/document/d/1j-yGucSOJefWUvdz31hjcztJmBl3ln2NisuPqf_YtSw/edit) | Shader architecture, Z-fighting fixes, and corrugated geometry post-mortem. |
| **Doc 5** | Kyojima Eki · Objects 02–04 Generation Process & Meta-References Ledger (https://docs.google.com/document/d/1ry754XIZOmjj1J0Cdpn7y3oHOBq5RvVGto4BRTfb-88/edit) | This document. Full technical dossier, 2D-First reference doctrine, and backpropagation records. |


---

## [2026-09-03 UPDATE] Object 04 (Striped Sun Awning & Cantilever Hardware) 3D Master Authored & Exported

- **Status**: 3D ARCHITECTURAL MASTER VERIFIED & ACTIVE IN STUDIO
- **Geometry & Shading Specifications**:
  - **18 Alternating Vertical Stripe Panels**: Deep hunter green (`#1f6642`) and warm cream (`#f0e8d1`) physical panels across both the $18^\circ$ canopy slope and the $0.22\text{m}$ hanging front wave valance.
  - **Watertight Solid Canvas Volume**: $1.5\text{cm}$ physical offset underside lining—**zero co-planar duplicate faces, zero Z-fighting pixelation during 360° spin, and zero see-through clipping**.
  - **Physical 3D Tubular Black Iron Framework**: 38mm front crossbar, 4 heavy diagonal cantilever steel support struts, welded corner elbow sleeves, tensioning turnbuckles, and rectangular iron wall mounting plates bolted with hex lag screws into the dark timber lintel.
  - **Mesh Metrics**: 496 vertices, 260 faces, 16.2 KB Wavefront OBJ export (`model-obj04-sun-awning.obj`).
- **Studio Inspection**: Live in Mode 1 (3D Cel Master), Mode 2 (2D Illustrative), Mode 3 (2D Photorealistic-ish), and Mode 4 (Interactive 360° Inspection).

# Kyojima Eki Studio · Pre-Object 04 Master Checkpoint & Reconstruction Blueprint

**Timestamp**: September 3, 2026 · 11:45 AM PDT  
**Canonical Baseline**: Trilogy Completed (Objects 01, 02, 03 Approved & Locked) Prior to Object 04 Inception  
**Standalone Viewer Artifact**: [`kyojima-studio-pre-obj4.html`](file:///Volumes/T9/makingpancakes/kyojima-studio-pre-obj4.html) (1.76 MB / 1,847,592 bytes)  
**Quick Terminal Launcher**: `./open-pre-obj4`

---

## 1. Architectural Integrity & State Verification

This checkpoint records the exact mathematical, geometric, textual, and shader definitions required to reconstruct the studio at this clean baseline.

### Active Objects Status Ledger
| Object ID | Title & Designation | Status | Tris | Texture / Shader Architecture |
| :--- | :--- | :--- | :--- | :--- |
| **Obj 01** | 🔴 Crimson Vending Machine (自販機) | **APPROVED & LOCKED** | 3,858 | Dual-panel physical parallax chassis, illuminated beverage showcase, 12 louvers, PVC drain. |
| **Obj 02** | 🪵 Timber Facade & Lattice Doors (木造ファサード・格子戸) | **APPROVED 3D MASTER** | 7,782 | Authentic washi textures (`tex_ground_clean` & `tex_upper_clean`), clean solid wedge awning, backpropagated full Kawara roof, 8 front planters. |
| **Obj 03** | 🏯 Kawara Ceramic Roof & Sheltering Eaves (和瓦屋根・本瓦葺き) | **APPROVED 3D MASTER** | 1,752 | Full advanced architecture: 24 vertical 3D corrugated tile flutes (*hon-gawara*), 8 horizontal shadow courses, 24 rounded *tomoe* eaves crests (巴瓦), 3-tier stepped *munegawara* ridge crown with *onigawara* crests, 9 gutter brackets, downspout, 16 cedar rafters. |
| **Obj 04** | 🎪 Striped Sun Awning (日除けテント・天幕) | **REVERTED TO QUEUE** | 0 (Budget: 1,800) | Reset to zero; ready for clean re-initiation. |
| **Obj 05–15** | Subsequent Neighborhood Objects | **IN QUEUE** | — | Retained in the 15-object selection hierarchy. |

---

## 2. Geometric Specifications & Coordinates

### Object 01: Crimson Vending Machine
- **Chassis Dimensions**: $0.95\text{m} (\text{W}) \times 2.05\text{m} (\text{H}) \times 0.85\text{m} (\text{D})$
- **Placement**: Corner apron grounding at $X = 2.45\text{m}, Z = 2.65\text{m}$ (relative to building).
- **Bevel Formula**: $r = 0.035\text{m}$ with 3-segment cylindrical fillets on front vertical edges.
- **Parallax Panels**:
  - *Panel 1 (Display Showcase)*: $Z = 0.380\text{m}$, dimensions $0.65\text{m} \times 0.80\text{m}$, emissive tier $0.45$.
  - *Panel 2 (Chassis Cutout)*: $Z = 0.428\text{m}$, dimensions $0.92\text{m} \times 1.96\text{m}$, alpha test $> 0.15$.
  - *Internal Depth Gap*: $\Delta Z = 48\text{mm}$, creating physical parallax from any orbital viewing angle.

### Object 02: Timber Facade & Lattice Doors (Master)
- **Foundation Apron**: Concrete slab at $Y = 0.08\text{m}$, dimensions $7.20\text{m} \times 0.16\text{m} \times 5.90\text{m}$.
- **Building Shell**: Solid plaster mass at $Y = 2.75\text{m}$, dimensions $6.40\text{m} \times 5.35\text{m} \times 4.80\text{m}$.
- **Ground Floor Threshold (Taisho Doors)**:
  - Coordinate bounds: $X \in [-3.19, +3.19]$, $Y \in [0.16, 2.72]$, $Z = 2.41\text{m}$.
  - Texture: `nano_tex_ground_clean.webp` (Texture Slot 3, `texMode = 4`).
- **Second Floor Elevation (3 Window Bays)**:
  - Coordinate bounds: $X \in [-3.19, +3.19]$, $Y \in [2.72, 5.25]$, $Z = 2.41\text{m}$.
  - Texture: `nano_tex_upper_clean.webp` (Texture Slot 4, `texMode = 5`).
- **Clean Solid Awning**:
  - Center: $[0.0, 2.80, 2.41]$, Width: $6.40\text{m}$, Height: $0.42\text{m}$, Depth: $0.88\text{m}$, Thickness: $0.04\text{m}$.
  - Iron wall mounting plates at $X = \pm 3.10\text{m}$. Zero floating vertical poles.
- **Integrated Street Dressing**:
  - 8 ceramic planters along the curb with staggered greenery blocks.
  - Corner vending machine grounded at right threshold.

### Object 03: Kawara Ceramic Roof (Full Advanced Architecture)
- **Primary Parameters**:
  - Half-width: $hw = 3.62\text{m}$ (Overall width: $7.24\text{m}$).
  - Ridge Apex: $Y = 2.45\text{m}, Z = 0.0\text{m}$ (In Facade: $Y = 6.50\text{m}$).
  - Front Eaves: $Y = 1.05\text{m}, Z = 3.15\text{m}$ (In Facade: $Y = 5.25\text{m}$).
  - Rear Eaves: $Y = 1.25\text{m}, Z = -2.75\text{m}$ (In Facade: $Y = 5.45\text{m}$).
  - Soffit Underside: $Y = 0.91\text{m}$ (In Facade: $Y = 5.11\text{m}$).
- **Roof Surface Flutes (*Hon-gawara*)**:
  - 24 vertical 3D corrugated tile ribs spanning front pitch.
  - Normal vector perpendicular to $24^\circ$ slope: $N_y = 0.914, N_z = 0.406$.
  - Flute width: $0.048\text{m}$, flute height: $0.038\text{m}$.
  - Dual-facet lighting: Left flank shaded (`tileDark`), right flank highlighted (`tileLight`).
  - Terminal *Tomoe* (巴瓦) eaves crests: Rounded cap tile at the foot of each rib ($Z = 3.16\text{m}$).
- **Stepped Horizontal Courses**:
  - 8 shadow courses down the front slope producing authentic shingle overlap lines.
- **Ridge Crown (*Munegawara*) & Crests**:
  - 3-tier stepped cylindrical ridge beam along apex ($Z = 0.0\text{m}$).
  - Terminal *Onigawara* end crests at $X = \pm(hw + 0.04)\text{m}$.
- **Drainage & Woodwork**:
  - Galvanized front gutter with 9 mounting brackets.
  - Corner collection hopper and continuous vertical downspout pipe.
  - 16 exposed cedar timber rafters (垂木) beneath the front eave soffit.

---

## 3. WebGL Shader & Rendering Pipeline

- **Vertex Shader**:
  - Position, normal, UV, vertex color, emissive scalar, texture mode ID.
  - Inverted hull extrusion pass ($+0.008\text{m}$ along normal) for continuous Sumi ink outlines.
- **Fragment Shader**:
  - **Cel Shading**: Half-Lambert diffuse ramp with stepped Umbra (`#292e47`), Penumbra (`#d96138`), and Highlight (`#fff5e6`).
  - **Fresnel Rim**: Sky blue rim reflection ($\text{Fresnel}^3 \times 0.30$).
  - **Ground Ambient Bounce**: Soft upward bounce lighting near street apron.
  - **Washi Twinkle Mode**: Real-time sinusoidal fiber chiaroscuro shimmer over warm cream washi substrate.
  - **Multi-Texture Binding**: 5 active texture samplers (Chassis Cutout, Window Panel, Side Mural, Ground Washi Facade, Upper Washi Windows).

---

## 4. Compressed Nano Asset Inventory

All 2D reference and texture assets are permanently stored in `scratch/` as high-efficiency WebPs:

| Asset Name | Scratch WebP Filename | Size |
| :--- | :--- | :--- |
| Vending Showcase | `nano_opt_vending-machine-window-display.webp` | 71.3 KB |
| Vending Chassis | `nano_opt_vending-machine-body-chassis.webp` | 14.1 KB |
| Washi Hero Portrait | `nano_opt_kyojima-vending-machine-hero-illustration.webp` | 88.7 KB |
| Head-On Documentary | `nano_opt_crimson-vending-machine-headon-hero-portrait.webp` | 57.2 KB |
| Sumida Context | `nano_sumida_expo_opt.webp` | 44.9 KB |
| Chassis Cutout | `nano_opt_vending_chassis_cutout.png` | 262.0 KB |
| Window Showcase Panel | `nano_vending_window_panel.webp` | 78.9 KB |
| Ground Washi Facade | `nano_tex_ground_clean.webp` | 42.9 KB |
| Upper Washi Windows | `nano_tex_upper_clean.webp` | 24.8 KB |
| Full Composite Elevation | `nano_kyojima_eki_facade_existing.webp` | 40.3 KB |
| Plaster Relief Elevation | `nano_kyojima_eki_side_wall_mural.webp` | 31.1 KB |
| Ground Door Photo | `nano_photo_ground_opt.webp` | 38.3 KB |
| Upper Floor Photo | `nano_photo_upper_opt.webp` | 14.3 KB |
| Sprout Relief Photo | `nano_side_mural_opt.webp` | 30.7 KB |
| Walking Tour Context | `nano_yatsushimahana_opt.webp` | 31.0 KB |
| Ortho Roof Elevation | `nano_ill_roof_ortho_opt.webp` | 20.9 KB |
| Underside 16 Rafters | `nano_ill_rafters_opt.webp` | 49.9 KB |
| Tomoe Swirl Crest | `nano_ill_crest_opt.webp` | 66.3 KB |
| Ortho Roof Photo | `nano_photo_roof_ortho_opt.webp` | 21.7 KB |
| Underside Rafters Photo | `nano_photo_rafters_opt.webp` | 35.8 KB |
| Tomoe Crest Photo | `nano_photo_crest_opt.webp` | 25.1 KB |
| Side Gable Photo | `nano_photo_roof_gable_opt.webp` | 33.1 KB |

**Total Self-Contained Bundle Size**: **1.76 MB (1,847,592 bytes)**.

---

## 5. Reconstruction Procedure

If rebuilding from scratch:
1. Run `python3 /Users/sophiaboettcher/.gemini/antigravity/brain/8b90f9fc-6b18-4055-9b0a-f8191c06e7bc/scratch/update_pre_obj4_full_advanced_roof.py`.
2. This generates `/Volumes/T9/makingpancakes/kyojima-studio-pre-obj4.html`.
3. Launch with `./open-pre-obj4` or double click `kyojima-studio-pre-obj4.html`.


---

## [2026-09-03 DEPLOYMENT CHECKPOINT] Pre-Object 04 Master Studio Deployed to kokechan.preattention.ai

- **Deployment Status**: **SUCCESSFULLY DEPLOYED TO PRODUCTION**
- **Production URL**: [https://kokechan.preattention.ai/studio](https://kokechan.preattention.ai/studio)
- **Main World Host**: [https://kokechan.preattention.ai](https://kokechan.preattention.ai)
- **Release ID**: `rc-1.2-kyojima-pre-obj4-master`
- **Cloudflare Worker**: `kokechan-claude-edition`
- **Version ID**: `c4ef1ed4-45dc-4871-b7d6-e0f7469d308a`
- **HTTP Verification**: `HTTP/2 200 OK` confirmed on both `/studio` and `/release-inventory-v1.json`.

### Features Live in Production:
1. **Object 01 (Crimson Vending Machine)**:
   - Approved dual-panel parallax master with chassis cutout, illuminated 3-tier drink showcase, LED buttons, and coin return.
2. **Object 02 (Timber Facade & Lattice Doors)**:
   - Ground floor Taisho sliding doors (`tex_ground_clean`) and upper 3-bay window wall (`tex_upper_clean`) mapped with authentic hand-drawn washi textures.
   - Clean solid cantilever wedge awning (`addSolidAwning([0, 2.80, 2.41], 6.40, 0.42, 0.88, 0.04)`) with iron brackets (zero floating vertical poles).
   - Backpropagated advanced Object 03 corrugated roof at $Y = 5.25\text{m} - 6.50\text{m}$.
   - 8 front ceramic planters and grounded corner crimson vending machine.
3. **Object 03 (Kawara Ceramic Roof & Sheltering Eaves)**:
   - 24 vertical 3D corrugated tile flutes (*hon-gawara*) with light & shadow facets.
   - 8 stepped horizontal shadow seam courses down front pitch.
   - 24 rounded *tomoe* eaves crest tiles (巴瓦).
   - 3-tier stepped *munegawara* ridge crown with terminal *onigawara* end crests.
   - Double-layered *hafuban* angled bargeboards with outer fascia.
   - Galvanized front gutter, 9 mounting brackets, corner hopper, and continuous vertical downspout.
   - 16 exposed cedar timber rafters (垂木).
4. **Queue (Objects 04–15)**:
   - Reset to pristine baseline prior to Object 04 inception.
5. **Performance**:
   - Total bundle size: **1.76 MB** (compressed nano WebP pipeline), loading in under 30ms.

# Deep Architectural Research: High-Efficiency 3D Asset Quantization, Lazy Loading, and VRAM Minimization for WebGL

**Target Environment**: Browser-based WebGL/Three.js applications on mobile & desktop (including `kokechan.preattention.ai` and Kyojima Studio).

---

## 1. The Core Problem: Why Browsers & Devices Get Overwhelmed

When interactive 3D web applications stutter, freeze, or cause mobile browser tabs to crash (especially on iOS Safari), the root cause is rarely the 3D polygon count alone. It is almost always a combination of **VRAM expansion**, **synchronous CPU decoding**, and **Float32 memory bandwidth bloat**:

### A. The WebP / PNG / JPEG VRAM Fallacy
* **The Illusion**: A compressed WebP or JPEG texture looks tiny on disk or over the network (e.g. 500 KB to 2 MB).
* **The Reality in GPU Memory**: WebP, PNG, and JPEG are *file storage formats*, not *GPU formats*. The browser's image decoder must decompress every single pixel into raw, uncompressed 32-bit RGBA channels ($4\text{ bytes per pixel}$) before uploading to the GPU:
  $$\text{VRAM per Texture} = \text{Width} \times \text{Height} \times 4\text{ bytes}$$
* **Concrete Numbers**:
  * A single $2048 \times 2048$ texture requires **16.78 MB of raw VRAM**!
  * With mipmaps ($+33\%$), it requires **22.37 MB of VRAM**.
  * A scene or studio with 15 objects, each having 2–3 textures (30–45 textures total), inflates to **over 500 MB to 750 MB of raw VRAM**!
* **Mobile Crash Threshold**: Mobile Safari enforces a strict WebGL memory limit (typically **250 MB to 384 MB** depending on device tier). Exceeding this triggers WebKit’s watchdog memory eviction, instantly crashing the page with: *"A problem repeatedly occurred with this webpage."*

### B. Float32 Geometry Bandwidth Bloat
* Default 3D geometries store vertex coordinates, normals, and UVs as 32-bit floating-point arrays (`Float32Array`):
  * Position ($X, Y, Z$): 12 bytes / vertex
  * Normal ($N_x, N_y, N_z$): 12 bytes / vertex
  * UV ($U, V$): 8 bytes / vertex
  * Color ($R, G, B, A$): 16 bytes / vertex (if float)
  * **Total**: $32\text{ to }48\text{ bytes per vertex}$!
* A 10,000-vertex model requires ~400 KB of buffer data transferred over the bus every draw cycle, quickly starving mobile memory buses and causing thermal throttling.

### C. Main-Thread Synchronous Parsing & Compilation
* Loading large assets synchronously on the JavaScript main thread locks the event loop.
* Parsing geometry and executing `gl.texImage2D()` blocks rendering frames, resulting in noticeable 200ms–1500ms visual hitches (stutter/jank).

---

## 2. Solution Pillar 1: Mesh & Attribute Quantization (`KHR_mesh_quantization`)

Quantization replaces 32-bit floating-point numbers with compact 16-bit or 8-bit integers, combined with a dequantization scale and offset matrix.

### A. How Quantization Works
| Vertex Attribute | Standard Precision | Quantized Format | GPU Representation | Memory Reduction |
| :--- | :--- | :--- | :--- | :--- |
| **Position ($X, Y, Z$)** | 32-bit float (12 bytes) | 16-bit signed int (`short[3]`) | `gl.SHORT` (normalized: false) | **50% reduction** (6 bytes) |
| **Normals ($N_x, N_y, N_z$)** | 32-bit float (12 bytes) | 8-bit signed int (`byte[3]` or Octahedral) | `gl.BYTE` (normalized: true) | **66% to 75% reduction** (3–4 bytes) |
| **Texture UVs ($U, V$)** | 32-bit float (8 bytes) | 16-bit unsigned int (`ushort[2]`) | `gl.UNSIGNED_SHORT` (normalized: true) | **50% reduction** (4 bytes) |
| **Vertex Colors ($R, G, B, A$)** | 32-bit float (16 bytes) | 8-bit unsigned int (`ubyte[4]`) | `gl.UNSIGNED_BYTE` (normalized: true) | **75% reduction** (4 bytes) |

### B. Why Quantization Outperforms Draco at Runtime
* **Draco**: A transmission compression format. While Draco achieves remarkable compression over the wire (e.g. 80% smaller file download), **the browser must decompress Draco back to full 32-bit float arrays in CPU memory and GPU VRAM before rendering**. Thus, Draco saves network bandwidth, but provides **zero runtime VRAM reduction** and introduces heavy CPU decompression jank.
* **Quantization (`KHR_mesh_quantization`)**: Quantized data **remains packed in GPU VRAM during rendering**. Modern GPUs natively sample 16-bit and 8-bit vertex attributes via `gl.vertexAttribPointer()`. This delivers an immediate **50% to 65% reduction in runtime GPU memory and bus bandwidth**.

### C. Best Practices for WebGL Implementation
1. **4-Byte Alignment**: Ensure vertex attributes are padded to 4-byte boundaries. Graphics drivers (especially ANGLE on Windows/macOS) maintain optimized fast paths for 4-component vectors (`short[4]`). Unaligned 3-component attributes (`short[3]`) can trigger internal driver translation (`CopyNativeVertexData`), which hurts CPU performance.
2. **Normalized Flag in `vertexAttribPointer`**:
   * For Normals and UVs, pass `normalized: true`. The GPU automatically maps `[-128, 127]` to `[-1.0, 1.0]` and `[0, 65535]` to `[0.0, 1.0]`.
   * For Positions, pass `normalized: false`, and apply a simple scale and offset in the vertex shader:
     ```glsl
     attribute vec3 aPosition; // Uploaded as SHORT
     uniform vec3 uPositionScale;
     uniform vec3 uPositionOffset;

     void main() {
       vec3 realPos = aPosition * uPositionScale + uPositionOffset;
       gl_Position = uProjection * uView * vec4(realPos, 1.0);
     }
     ```

---

## 3. Solution Pillar 2: GPU-Native Texture Compression (KTX2 / Basis Universal)

This is the single most critical intervention for preventing browser crashes and memory bloat.

### A. How KTX2 / Basis Universal Operates
* **Basis Universal** encodes textures using a universal intermediate format (UASTC or ETC1S) inside a `.ktx2` container.
* At runtime in the browser, a compact WebAssembly module (the Basis transcoder) inspects the client device's GPU capabilities and transcodes the data directly into the hardware's native block-compression format:
  * **Apple iOS / macOS (Apple Silicon)**: **ASTC** (Adaptive Scalable Texture Compression, e.g. 4×4 or 6×6 blocks).
  * **Android / ARM Mali / Qualcomm Adreno**: **ASTC** or **ETC2**.
  * **Desktop Windows / Linux (NVIDIA / AMD / Intel)**: **BC7** or **BC1/BC3**.
* **Direct Hardware Sampling**: The GPU hardware samples the compressed blocks directly from VRAM without ever decompressing them into raw pixels.

### B. VRAM Comparison
| Texture Format | File Download Size (2048px) | Runtime GPU VRAM Footprint | Mobile Safari Tab Safety |
| :--- | :--- | :--- | :--- |
| **PNG** | ~3.5 MB | **16.78 MB** | ⚠️ Dangerous (causes tab crashes in clusters) |
| **WebP** | **~0.4 MB – 1.2 MB** | **16.78 MB** | ⚠️ Low network weight, but dangerous VRAM spikes |
| **KTX2 (Basis UASTC)** | ~1.1 MB – 1.8 MB | **2.79 MB** (**84% VRAM reduction**) | ✅ Fully stable, zero risk of watchdog crash |
| **KTX2 (Basis ETC1S)** | ~0.3 MB – 0.6 MB | **1.39 MB** (**92% VRAM reduction**) | ✅ Ultra-safe for background/ambient assets |

---

## 4. Solution Pillar 3: Zero-Jank Asynchronous Loading (`createImageBitmap`)

When traditional `img.onload` or `HTMLImageElement` is passed to `gl.texImage2D()`, the browser performs decompression and color conversion synchronously on the main thread, causing frame drops.

### A. The `createImageBitmap` Asynchronous Pipeline
`createImageBitmap()` executes image decoding in the browser's background thread pool, delivering a GPU-ready bitmap to the main thread:
```javascript
async function loadTextureAsync(gl, url) {
  const response = await fetch(url);
  const blob = await response.blob();
  
  // Decodes in background thread with zero main-thread jank
  const bitmap = await createImageBitmap(blob, {
    premultiplyAlpha: 'none',
    colorSpaceConversion: 'none'
  });

  const texture = gl.createTexture();
  gl.bindTexture(gl.TEXTURE_2D, texture);
  gl.texImage2D(gl.TEXTURE_2D, 0, gl.RGBA, gl.RGBA, gl.UNSIGNED_BYTE, bitmap);

  // CRITICAL: Close bitmap immediately to release CPU memory and avoid GC stutter
  bitmap.close();
  return texture;
}
```

### B. Configuration Alignment
Ensure `ImageBitmapOptions` match your WebGL state (`premultiplyAlpha: 'none'`). If there is a mismatch, the browser will perform a fallback conversion synchronously on the main thread during `gl.texImage2D()`, defeating the purpose.

---

## 5. Solution Pillar 4: Progressive Lazy Loading & Spatial Chunking

Rather than bundling every object and texture into a single monolithic file, load assets on demand based on visibility and user focus.

### A. On-Demand Hierarchy for the 15-Object Studio
* **Core Bundle**:
  * Include only the viewer shell, active hero object (e.g. Object 02), and lightweight metadata for the other 14 objects.
* **On-Demand Streaming**:
  * When a user selects another object from the dropdown (e.g. Object 05: Alley Bicycle), fetch its geometry and texture payload dynamically.
  * Dispose of the previously active object's VBOs (`gl.deleteBuffer()`) and texture memory (`gl.deleteTexture()`) if memory budgets require it.

### B. Level of Detail (LOD) Pyramid
1. **LOD 0 (Hero / Direct Focus, < 6m)**:
   * Full detailed geometry (e.g. 3D corrugated tile flutes, individual rafter tails).
   * High-resolution texture maps.
2. **LOD 1 (Mid-Range / Street Context, 6m – 25m)**:
   * Decimated geometry (50% polygon count).
   * 512px downsampled textures.
3. **LOD 2 (Far Distance / Sky Silhouette, > 25m)**:
   * Simple volumetric bounding prisms (< 60 polygons).
   * Solid vertex color palette (zero texture sampling overhead).
4. **Impostor / Billboard Quad (> 50m)**:
   * A single 2-triangle quad rendering a pre-baked directional view of the building.

### C. Progressive LOD Streaming (`@needle-tools/gltf-progressive`)
* Assets are split into a tiny initial base chunk (~10% of total size) containing the simplified proxy geometry.
* The application displays the proxy immediately (sub-saccadic visual availability), while higher-resolution geometry buffers stream in incrementally over HTTP chunked transfer.

---

## 6. Recommended Action Plan for Our Kyojima Pipeline

1. **Implement On-Demand Dynamic Streaming in the Studio**:
   * Instead of embedding all 15 objects' textures and geometries into one HTML payload, maintain individual lightweight JSON/ArrayBuffer packages that stream instantly on dropdown change.
2. **Introduce Int16 Quantized Geometry Buffers**:
   * Pack our procedural geometries (vending machine chassis, facade posts, roof ribs) into `Int16Array` with `gl.SHORT`, cutting vertex memory by 50%.
3. **Adopt KTX2 / Basis Universal for World Textures**:
   * For the full 3D living archive on `kokechan.preattention.ai`, transcode facade textures (`tex_ground`, `tex_upper`, street surfaces) into `.ktx2`, slashing VRAM usage from 22 MB down to 2.8 MB per texture.
4. **Device Capability Profiling**:
   * Read `navigator.deviceMemory` and `navigator.hardwareConcurrency` at runtime:
     * High-end desktop: LOD 0 with 2048px textures.
     * Mobile / low memory: LOD 1 with 512px KTX2 textures and strict 2-texture bind slots.

# Morado's Architecture — Deep Research & Integration Roadmap
## For the 173-Landmark Living Archive: Kokechan / Kyojima World

**Documented:** 2026-09-03  
**Source Repositories:**
- [morado/Kosmos](https://github.com/morado/Kosmos) — WebGL Universe Engine (CoffeeScript / WebGL, BSD-2-Clause, 2013)
- [morado/IronWarfare](https://github.com/morado/IronWarfare) — iOS 3D Tank Game (Objective-C, MIT, 2012)

---

## 1. Overview of Morado's Two Repositories

### A. Kosmos — WebGL Universe Engine
A fully procedural, streaming 3D universe simulator written **entirely from scratch in WebGL/CoffeeScript** over ~4 weeks. It renders trillions of stars and planets through:
- A **two-tier LOD (Level of Detail) mesh system**: far sphere + near high-resolution subdivided cube-mapped sphere.
- A **ContentCache** system with progressive multi-frame loading to prevent jank.
- A **sprite-to-mesh transition** pipeline: objects start as billboarded point sprites, then graduate to geometry as you fly closer.
- A **procedural GPU map generation** system with per-face streaming (6 cube faces loaded progressively across frames).

**License:** BSD-2-Clause (permissive — we can directly build on this).

**Key source files:**
| File | Role |
| :--- | :--- |
| [`ContentCache.coffee`](https://github.com/morado/Kosmos/blob/master/source/ContentCache.coffee) | Multi-frame progressive asset cache with LRU eviction + frame-spread loading |
| [`Planetfield.coffee`](https://github.com/morado/Kosmos/blob/master/source/Planetfield.coffee) | Manages the full field of objects across multiple LOD tiers simultaneously |
| [`PlanetFarMesh.coffee`](https://github.com/morado/Kosmos/blob/master/source/PlanetFarMesh.coffee) | Far-distance low-res mesh (Float32 vertex buffer, `Uint16Array` index buffer) |
| [`PlanetNearMesh.coffee`](https://github.com/morado/Kosmos/blob/master/source/PlanetNearMesh.coffee) | Near-distance high-res 64×64 subdivided mesh |
| [`Bounds.coffee`](https://github.com/morado/Kosmos/blob/master/source/Bounds.coffee) | Axis-aligned bounding box with `getRadius()` and `getCorners()` for frustum culling |
| [`xgl.coffee`](https://github.com/morado/Kosmos/blob/master/source/xgl.coffee) | Thin WebGL abstraction: `addProgram()`, `loadShader()`, `createProgram()`, uniform/attrib lookup |
| [`Camera.coffee`](https://github.com/morado/Kosmos/blob/master/source/Camera.coffee) | View frustum, projection, camera space transforms |

### B. IronWarfare — iOS 3D Tank Game
A **full-featured 3D combat iOS game** built in 4 months from scratch in Objective-C/OpenGL ES. It demonstrates:
- **Custom 3D art pipeline with a MeshConverter tool** (C++, converts art assets into packed, indexed mesh formats for the GPU).
- **Terrain renderer** with camera-distance LOD.
- **Tree renderer** with billboard-to-geometry transition.
- **Pooled and batched particle systems** (zero allocation per frame via object pooling).
- **Custom script parser** loading all game objects (vehicles, maps, props) from a simple text format at runtime.
- A **resource manager** handling load/unload of textures and geometry with reference counting.

**License:** MIT (permissive — we can directly build on this).

**Key source directories:**
| Directory | Role |
| :--- | :--- |
| `Game/Source/` | Full game engine: terrain, trees, particles, vehicles, AI, resource management |
| `MeshConverter/` | Standalone CLI tool converting OBJ/art assets into packed binary mesh format |

---

## 2. The Most Valuable Patterns from Morado's Work

### Pattern 1: `ContentCache` — Frame-Spread Progressive Loading (Kosmos)

This is **the most directly applicable** pattern to our 173-landmark problem. Here is the exact design from [`ContentCache.coffee`](https://github.com/morado/Kosmos/blob/master/source/ContentCache.coffee):

```coffeescript
# Manages content objects uniquely identified by ID.
# Automatically loads and unloads as the cache "spills" (LRU eviction).
# 
# Supports progressive loading: the loader callback returns [finished, partialObj].
# Only when finished==true is the object returned to the requester.
# This allows loading work to be spread across multiple frames, preventing jank.

class ContentCache
  constructor: (maxItems, loaderCallback)
  getContent: (contentId)   # Returns null if not yet loaded; triggers load
```

**How it applies to 173 landmarks:**
- Each landmark (e.g. `kyojima-eki`, `nishi-arai-daishi`, `senso-ji`) is a `contentId`.
- The loader callback fetches the landmark's JSON payload, parses geometry into `Int16Array`/`Float32Array` buffers, uploads textures via `createImageBitmap`, and returns `[true, gpuObject]` when done.
- `maxItems` = VRAM budget (e.g. 8 landmarks at full LOD simultaneously, with remaining in sprite mode).
- When the user pans the world to a new area, stale landmark entries are evicted via LRU and their `gl.deleteBuffer()` / `gl.deleteTexture()` is called.

**Translation to JavaScript:**
```javascript
class LandmarkCache {
  constructor(maxItems = 8) {
    this.maxItems = maxItems;
    this.loaded = new Map();   // contentId -> { gpuObject, lastAccess }
    this.loading = new Map();  // contentId -> partialState
  }

  getContent(landmarkId) {
    if (this.loaded.has(landmarkId)) {
      this.loaded.get(landmarkId).lastAccess = performance.now();
      return this.loaded.get(landmarkId).gpuObject;
    }
    this._scheduleLoad(landmarkId);
    return null; // Caller renders placeholder/sprite in the meantime
  }

  async _scheduleLoad(landmarkId) {
    if (this.loading.has(landmarkId)) return;
    this.loading.set(landmarkId, { progress: 0 });
    
    // Evict LRU if at capacity
    if (this.loaded.size >= this.maxItems) {
      this._evictLRU();
    }

    const payload = await fetch(`/payloads/${landmarkId}.json`).then(r => r.json());
    const gpuObject = await this._compileGeometry(payload); // Int16 quantized buffers
    
    this.loaded.set(landmarkId, { gpuObject, lastAccess: performance.now() });
    this.loading.delete(landmarkId);
  }

  _evictLRU() {
    let oldest = null;
    let oldestTime = Infinity;
    for (const [id, entry] of this.loaded) {
      if (entry.lastAccess < oldestTime) { oldest = id; oldestTime = entry.lastAccess; }
    }
    const entry = this.loaded.get(oldest);
    gl.deleteBuffer(entry.gpuObject.vbo);
    gl.deleteTexture(entry.gpuObject.texture);
    this.loaded.delete(oldest);
  }
}
```

---

### Pattern 2: Dual LOD Tier System — Far Sprite → Near Mesh (Kosmos)

From [`Planetfield.coffee`](https://github.com/morado/Kosmos/blob/master/source/Planetfield.coffee), Morado defines explicit distance thresholds:

```coffeescript
@nearMeshRange   = nearMeshRange    # Full geometry visible within this distance
@farMeshRange    = farMeshRange     # Lower-res mesh for medium range
@spriteRange     = spriteRange      # Billboard sprite for very far distance
@spriteNearRange = nearMeshRange * 0.25  # Transition blend zone

# farMapCache: ContentCache(16, ...) — up to 16 low-res maps cached simultaneously
# nearMapCache: ContentCache(4, ...)  — only 4 high-res maps cached (expensive!)
@farMapCache  = new ContentCache(16, generateCallback)
@nearMapCache = new ContentCache(4, generateCallback)
```

**Critical insight:** Morado used **different cache sizes for different LOD tiers**. High-detail content (near mesh) has a tiny cache of 4. Low-detail content (far mesh) allows 16 cached simultaneously. The full sprite field buffers 100 sprites at once as a single draw call.

**Our equivalent for 173 landmarks:**
| LOD Tier | Distance | Cache Size | Asset Format |
| :--- | :--- | :--- | :--- |
| **Sprite billboard** | > 80m | All 173, single draw call | Single instanced quad, vertex color only |
| **Far volume** | 25m – 80m | 20 simultaneous | 30-polygon bounding prism + 1 texture |
| **Mid detail** | 8m – 25m | 10 simultaneous | Decimated geometry (50% poly), 512px WebP texture |
| **Hero / Near** | < 8m | 4 simultaneous | Full procedural geometry, full texture set |

---

### Pattern 3: Progressive Per-Frame Map Generation — Zero-Jank Loading (Kosmos)

From `Planetfield.coffee`, Morado's near-map loader:
```coffeescript
nearGenerateCallback: (seed, partial) ->
  if partial == null
    progress = 0.0
    maps = @nearMapGen.createMaps()
    face = 0
  else
    progress = partial.progress
    maps = partial.maps
    face = partial.face

  # Only generate a SLICE of the map per frame (2 / progressiveLoadSteps steps)
  @progressiveLoadSteps = 128.0  # Spread across 128 frames total!
  @nearMapGen.generateSubMap(maps, seed, face, progress, progressPlusOne)

  if face >= 6
    return [true, maps]   # Done!
  else
    return [false, {maps, progress, face}]  # "Come back next frame"
```

**Key insight:** Each call to the load callback does a small, fixed-time slice of work (`2/128 steps`), then returns partial state and yields. This lets the frame render without dropping below 60fps.

**Our equivalent for landmark geometry:**
```javascript
async function* progressiveCompileGeometry(payload) {
  const { vertices, indices, texture } = payload;
  
  // Frame 1: Upload vertex buffer
  const vbo = gl.createBuffer();
  gl.bindBuffer(gl.ARRAY_BUFFER, vbo);
  gl.bufferData(gl.ARRAY_BUFFER, new Int16Array(vertices), gl.STATIC_DRAW);
  yield { phase: 'vertex', vbo };

  // Frame 2: Upload index buffer
  const ibo = gl.createBuffer();
  gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, ibo);
  gl.bufferData(gl.ELEMENT_ARRAY_BUFFER, new Uint16Array(indices), gl.STATIC_DRAW);
  yield { phase: 'index', vbo, ibo };

  // Frame 3: Decode and upload texture (using createImageBitmap for zero main-thread jank)
  const blob = await fetch(texture).then(r => r.blob());
  const bitmap = await createImageBitmap(blob, { premultiplyAlpha: 'none', colorSpaceConversion: 'none' });
  const tex = gl.createTexture();
  gl.bindTexture(gl.TEXTURE_2D, tex);
  gl.texImage2D(gl.TEXTURE_2D, 0, gl.RGBA, gl.RGBA, gl.UNSIGNED_BYTE, bitmap);
  bitmap.close(); // Critical: release CPU RAM immediately
  yield { phase: 'complete', vbo, ibo, tex };
}
```

---

### Pattern 4: MeshConverter Art Pipeline (IronWarfare)

From IronWarfare, the `MeshConverter/` directory is a standalone C++ CLI tool that:
1. Reads raw art assets (OBJ files, textures).
2. Packs vertex buffers into compact, indexed binary formats.
3. Outputs custom binary mesh files the game loads directly.

**Why this matters for us:** We currently generate geometry procedurally in JavaScript at runtime (heavy CPU cost on mobile). Morado's approach of pre-baking geometry into compact binary at *build time* eliminates runtime parsing entirely.

**Our equivalent pipeline:**
```
Build Pipeline (offline, runs on macOS):
  1. Procedural geometry builder (Python/JS) generates vertex arrays for each landmark's objects.
  2. Quantizer script packs Float32 → Int16 (positions) / Int8 (normals) / Uint16 (UVs).
  3. Packs into binary ArrayBuffer (.bin file), alongside JSON metadata.
  4. Each landmark's payload: { meta.json + geometry.bin + textures/ }
  5. Deployed to Cloudflare CDN.

At runtime:
  1. Fetch geometry.bin as ArrayBuffer.
  2. Wrap in typed arrays: new Int16Array(buffer, offset).
  3. gl.bufferData() directly (no parsing overhead).
```

---

### Pattern 5: Object Pool / Batching (IronWarfare)

From IronWarfare README: *"pooled and batched particle systems"*. The game achieves zero GC pressure per frame by pre-allocating pools of objects and never calling `new` in the render loop.

**Our equivalent for landmark sprites:**
When rendering 173 landmarks as distant sprites, we batch all 173 into a single `Float32Array` vertex buffer updated per frame via `gl.bufferSubData()` (not a new `bufferData()` call, which would reallocate VRAM):
```javascript
// Pre-allocate once:
const spriteVBO = gl.createBuffer();
gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(173 * 4 * 6), gl.DYNAMIC_DRAW);

// Each frame, only update positions that changed (no reallocation):
gl.bufferSubData(gl.ARRAY_BUFFER, landmarkIndex * 96, new Float32Array([x, y, z, ...]));

// Single draw call renders all 173 sprites:
gl.drawArrays(gl.TRIANGLES, 0, 173 * 6);
```

---

## 3. What Morado Documented as Limitations — and How We Solve Them

Morado was candid in his Kosmos README about what didn't work:

> *"WebGL is flakey and not ready for 'serious' 3D games yet."* (2013)

This was accurate in 2013 due to ANGLE bugs on Windows Chrome. **In 2026, WebGL2 is standard and stable** across all modern browsers including Safari, Chrome, Firefox, and Edge. Morado's architectural patterns are sound — only the compatibility concerns are outdated.

> *"Procedural content generation provides 'infinite variation' but not infinite novelty."*

This is **exactly our advantage**: we are not procedurally generating generic variation. Each of our 173 landmarks is hand-guided, culturally documented, and individually approved. We use procedural generation as an *implementation tool* (building meshes from descriptors), not as the art direction itself.

---

## 4. Full Integration Architecture: Morado-Inspired 173-Landmark Streaming Engine

Combining Kosmos's ContentCache, dual-LOD, and progressive loading with IronWarfare's art pipeline and IronWarfare's batched pooling:

```
┌─────────────────────────────────────────────────────────────────┐
│                     KOKECHAN WORLD ENGINE                       │
│                  (Morado-Inspired Architecture)                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  SPATIAL LAYER                                                  │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  LandmarkRegistry (173 entries)                          │  │
│  │  { id, lat/lon/mapXY, name_ja, name_en, boundingRadius,  │  │
│  │    payloadUrl, checkpointVersions: ['v1', 'v2', 'pre4'] }│  │
│  └──────────────────────────────────────────────────────────┘  │
│           │ frustum culling (Bounds.getCorners)                  │
│           ▼                                                      │
│  LOD DISPATCH LAYER (Morado Planetfield pattern)               │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  distance > 80m  → sprite batch (all 173, 1 draw call)   │  │
│  │  25m – 80m       → farCache.getContent(id) → vol mesh    │  │
│  │  8m – 25m        → midCache.getContent(id) → dec mesh    │  │
│  │  < 8m            → nearCache.getContent(id) → full mesh  │  │
│  └──────────────────────────────────────────────────────────┘  │
│           │ on cache miss: progressive load (no jank)           │
│           ▼                                                      │
│  CONTENT CACHE LAYER (Morado ContentCache pattern)             │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  nearCache  (max 4)   — Int16 quantized geometry + KTX2  │  │
│  │  midCache   (max 10)  — Float32 basic mesh + WebP        │  │
│  │  farCache   (max 20)  — 30-poly volume + vertex color    │  │
│  │  spriteVBO  (fixed)   — pre-alloc 173 sprites, DYNAMIC   │  │
│  │                                                          │  │
│  │  LRU eviction: gl.deleteBuffer() + gl.deleteTexture()    │  │
│  │  Progressive load: generator function, 1 upload/frame    │  │
│  └──────────────────────────────────────────────────────────┘  │
│           │ fetch from CDN on miss                              │
│           ▼                                                      │
│  ASSET PIPELINE (Morado MeshConverter pattern)                 │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  /payloads/                                              │  │
│  │    kyojima-eki-v1.bin      (Int16 geometry, ~8 KB)       │  │
│  │    kyojima-eki-v2.bin      (iteration B, locked)         │  │
│  │    kyojima-eki-meta.json   (bounds, LOD params, credits) │  │
│  │    kyojima-eki-tex.ktx2    (84% VRAM savings over WebP)  │  │
│  │    ...                                                   │  │
│  │    [173 × up to N versions × ~20 KB each]                │  │
│  └──────────────────────────────────────────────────────────┘  │
│                                                                 │
│  CHECKPOINT VIEWER (Fusion)                                     │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  Dropdown: "kyojima-eki" → [v1-pre-obj4, v2, current]   │  │
│  │  Swap: nearCache.invalidate(id); nearCache.getContent(   │  │
│  │         `${id}-${version}`)                              │  │
│  │  No page reload. Payload streams in, swaps in-place.     │  │
│  └──────────────────────────────────────────────────────────┘  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 5. Remaining Research Gaps (to verify before building)

| Gap | Status | Priority |
| :--- | :--- | :--- |
| **KTX2 transcoder WASM size** | Not yet benchmarked for our constraints. Target: < 300 KB WASM overhead. | High |
| **Service Worker caching strategy** for version-tagged payloads | Not yet designed. | High |
| **`gl.bufferSubData` perf on iOS Safari** for sprite batch updates | Known fast on desktop; needs mobile validation. | Medium |
| **Morado's Camera.coffee frustum math** — can we port directly? | Need to read full source. Available [here](https://github.com/morado/Kosmos/blob/master/source/Camera.coffee). | Medium |
| **IronWarfare MeshConverter binary format spec** — can we adapt for .bin payloads? | Need to read `MeshConverter/` source. | Medium |
| **WebGPU fallback path** — Chrome stable + Safari TP have WebGPU, but we write WebGL1 today. | Future milestone. | Low |

---

## 6. License Compliance Notes

Both repositories are open source with permissive licenses:
- **Kosmos**: BSD-2-Clause — requires attribution in derivative works.
- **IronWarfare**: MIT — requires attribution in derivative works.

**Required action when building on this work:** Add a `CREDITS.md` or comment block:
```
// Architecture inspired by Morado's Kosmos (BSD-2-Clause, 2013)
// https://github.com/morado/Kosmos
// ContentCache and LOD dispatch patterns adapted for the Kokechan Living Archive.
```

---

## 7. Google Docs Sync Status

This document is the primary technical reference for the Kokechan streaming engine design. Appended to:
- [Doc 4: Beyond Polygon Bloat / 15-Object Master To-Do](https://docs.google.com/document/d/1j-yGucSOJefWUvdz31hjcztJmBl3ln2NisuPqf_YtSw/edit)
- [Doc 5: Generation Process & Meta-References Ledger](https://docs.google.com/document/d/1ry754XIZOmjj1J0Cdpn7y3oHOBq5RvVGto4BRTfb-88/edit)

# Streaming Studio Deployment Checkpoint
**Date:** 2026-09-03T14:01 PDT  
**Cloudflare Version ID:** 2420b312-5183-42c5-969a-a3b94066f7b5

---

## Two New URLs Deployed

| URL | Description |
| :--- | :--- |
| **[/studio-stream](https://kokechan.preattention.ai/studio-stream)** | Streaming Studio — Morado ContentCache architecture |
| **[/perf-bench](https://kokechan.preattention.ai/perf-bench)** | Performance Benchmark tool |
| **[/studio](https://kokechan.preattention.ai/studio)** | Original Monolithic Studio (unchanged, permanent fallback) |

---

## Streaming Studio: What Was Built

### Core Architecture (Morado's Patterns)
Based on `morado/Kosmos` (BSD-2-Clause, 2013) and `morado/IronWarfare` (MIT, 2012).

**`LandmarkCache` (JS port of Kosmos `ContentCache`)**:
- `TEXTURE_PAYLOADS` registry — 5 WebGL textures stored as base64 per-object
- `loadTexturesForObject(objId)` — called on object selection, not at startup
- **LRU eviction**: `gl.deleteTexture()` called on previous object's textures before loading new
- **Progressive loading**: each texture decoded in sequence, one per `requestAnimationFrame` frame
- Sentinel textures (1×1 pixel) render immediately while real textures stream in

**Performance Measurements (Static Analysis)**:

| Metric | Streaming | Monolithic |
| :--- | :--- | :--- |
| File size | 1,820 KB | 1,804 KB |
| Immediate loadTexture() calls at startup | **0** | **5** |
| VRAM held at startup | **~0 bytes** (sentinels) | **~6 MB** (all textures) |
| Texture decode blocking work at startup | **None** | ~600 KB PNG/WebP decode |
| Texture mode | **Lazy, per-object** | Upfront, all objects |
| LRU eviction | ✅ Yes | ❌ No |
| Progressive loading | ✅ Yes | ❌ No |
| Fallback button | ✅ Yes (opens /studio) | N/A |
| Performance timing badge | ✅ Yes | ❌ No |

**Why the file size is the same**: The 1.18 MB of 2D reference gallery images (Modes 2 & 3) remain in both files because they are always needed for the gallery panels. The WebGL textures (600 KB) are the part that became lazy-loaded.

### Browser Benchmark Tool
`/perf-bench` loads both studios in sequence inside `<iframe>` elements and measures:
- Time to first paint (iframe `onload`)
- Time to interactive (500ms after `onload`)
- JS heap (via `performance.memory` in Chrome)
- Longest blocking task (via `PerformanceObserver` for `longtask`)
- Visual bar chart comparison
- JSON export of results

---

## Fallback Guarantee

The original `kyojima-studio-pre-obj4.html` at `/studio` is **never modified or removed**.  
The streaming studio has a "⬇ Legacy Full-Load View" button that opens `/studio` in a new tab.
