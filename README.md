# Kyojima Eki Living Archive Studio
### 京島駅 生きた記録 スタジオ

An interactive WebGL viewer for 173 cultural landmarks in the Kyojima / Koganecho neighborhoods of Yokohama. Built as a single-file HTML application — no frameworks, no bundlers, no build step. Runs entirely in the browser.

---

## Live URLs

| Studio | URL | Description |
|--------|-----|-------------|
| Monolithic Studio | https://kokechan.preattention.ai/studio | All textures pre-loaded at startup |
| Streaming Studio | https://kokechan.preattention.ai/studio-stream | Lazy LRU streaming, 0ms first paint |
| Performance Benchmark | https://kokechan.preattention.ai/perf-bench | Side-by-side benchmark with live HUD |

---

## What This Is

Kyojima Eki Living Archive Studio is a real-time 3D reconstruction tool for neighborhood-scale cultural documentation. Each of the 173 landmarks in the Kyojima / Koganecho corridor is broken into up to 15 individually modeled objects — street furniture, building facades, roofing, utility infrastructure, plants, and signage — all rendered in WebGL 1.0 with cel shading and sumi ink outlines.

The project is designed for **zero-shot reconstruction**: any developer with this repository and a Cloudflare account can rebuild the full archive from scratch using the documentation here.

---

## Technology Stack

| Layer | Choice | Why |
|-------|--------|-----|
| Rendering | Vanilla WebGL 1.0 | No Three.js overhead; full control over every shader uniform and buffer |
| File format | Single HTML file | Offline-capable, no install, trivial versioning, easy handover |
| Textures | Base64-inline | No CDN dependency; textures travel with the file |
| Hosting | Cloudflare Workers Assets | Global edge delivery, zero cold-start, free tier covers the scale |
| Deployment | npx wrangler@4.127.1 deploy | Single command, no CI required |

---

## Repository Layout

    makingpancakes/
    ├── kyojima-studio-pre-obj4.html   # 1,862 KB — monolithic studio (all textures pre-loaded)
    ├── kyojima-studio-stream.html     # 2,760 KB — streaming studio (lazy LRU, sentinel textures)
    ├── kyojima-perf-bench.html        # 11.8 KB — performance benchmark tool
    ├── docs/
    │   └── meta-references/           # Authoritative Google Docs archive (Docs 1–5 exported)
    ├── finalized-assets/              # Approved, locked geometry exports
    ├── AGENTS.md                      # Inclusive languaging protocol (all copy must comply)
    ├── GEMINI.md                      # Same protocol — Gemini agent reference copy
    ├── README.md                      # This file
    ├── ARCHITECTURE.md                # Technical architecture deep-dive
    ├── OBJECTS.md                     # 15-object queue with specs, camera, texture info
    ├── RECONSTRUCTION.md              # Step-by-step guide: rebuild from zero
    ├── LANGUAGING.md                  # Languaging policy summary
    ├── *.json / *.webp                # Sample and test landmark data files
    └── context/                       # (gitignored) Cloudflare build artifacts

---

## Authoritative Google Docs Registry & Meta-References

The conceptual, editorial, and architectural authority for this archive is synchronized with Google Drive via `gdoc.py`. For complete offline access and zero-shot reproducibility, full verbatim exports are preserved in [`docs/meta-references/`](./docs/meta-references/):

| # | Title | Live Google Drive Link | Local Markdown File | Role & Scope |
|---|---|---|---|---|
| **Doc 1** | Landmark Production To-Do Queue | [1GSGC_yeOueCsB-5k5rKaZn1sg4MfdMvpWGzxZ653p6U](https://docs.google.com/document/d/1GSGC_yeOueCsB-5k5rKaZn1sg4MfdMvpWGzxZ653p6U/edit) | [`01_LANDMARK_PRODUCTION_QUEUE.md`](./docs/meta-references/01_LANDMARK_PRODUCTION_QUEUE.md) | 168 editorial landmark prompts, spatial coordinates & master production queue |
| **Doc 2** | 173 Cultural Sites Registry | [1JGM_XJZMs8TTLqxF21yKM5Y0KMOH3fMgyjbCshc5c78](https://docs.google.com/document/d/1JGM_XJZMs8TTLqxF21yKM5Y0KMOH3fMgyjbCshc5c78/edit) | [`02_173_CULTURAL_SITES_REGISTRY.md`](./docs/meta-references/02_173_CULTURAL_SITES_REGISTRY.md) | Comprehensive cross-verified directory of all 173 physical sites across Kyojima & Koganecho |
| **Doc 3** | Kyojima Eki Architectural Dossier | [1JF2p7R4DecQz1VihR8aK9a8QbSkPMXrJ6gLugyEN4Fs](https://docs.google.com/document/d/1JF2p7R4DecQz1VihR8aK9a8QbSkPMXrJ6gLugyEN4Fs/edit) | [`03_KYOJIMA_EKI_ARCHITECTURAL_DOSSIER.md`](./docs/meta-references/03_KYOJIMA_EKI_ARCHITECTURAL_DOSSIER.md) | Comprehensive architectural survey, cultural history, and 15-object sequence |
| **Doc 4** | Beyond Polygon Bloat: Shader Architecture | [1j-yGucSOJefWUvdz31hjcztJmBl3ln2NisuPqf_YtSw](https://docs.google.com/document/d/1j-yGucSOJefWUvdz31hjcztJmBl3ln2NisuPqf_YtSw/edit) | [`04_BEYOND_POLYGON_BLOAT_SHADER_ARCHITECTURE.md`](./docs/meta-references/04_BEYOND_POLYGON_BLOAT_SHADER_ARCHITECTURE.md) | Technical shading manifesto, Half-Lambert lighting, Morado proxy textures & 15-object master to-do |
| **Doc 5** | Generation Process & Meta-References Ledger | [1ry754XIZOmjj1J0Cdpn7y3oHOBq5RvVGto4BRTfb-88](https://docs.google.com/document/d/1ry754XIZOmjj1J0Cdpn7y3oHOBq5RvVGto4BRTfb-88/edit) | [`05_GENERATION_PROCESS_AND_META_REFERENCES_LEDGER.md`](./docs/meta-references/05_GENERATION_PROCESS_AND_META_REFERENCES_LEDGER.md) | Object 02, 03 & 04 generation process, reference image bibles, math, and Z-fighting resolutions |


---

## Two Studio Variants

### Monolithic Studio (kyojima-studio-pre-obj4.html)
All textures for all objects are decoded and uploaded to GPU at startup. Object switching is instant (no load delay). Startup cost is proportional to total texture data (~several seconds on first load). Best for desktop review sessions and documentation work.

### Streaming Studio (kyojima-studio-stream.html)
Uses an LRU texture cache. At startup, each object gets a 1×1 sentinel texture (zero decode cost). When the user switches to an object, textures for that object are loaded one per animation frame (progressive, never blocking the render loop). The result is **0ms time-to-first-paint** — the studio is interactive immediately. The performance HUD shows whether each load fell within the saccadic mask threshold (150ms), indicating whether texture pop-in is perceptible to a user.

---

## Scale Goals

    173 landmarks × 15 objects each ≈ 2,500 geometry assets

Objects 01–03 are currently approved and locked. Objects 04–15 are queued. Object 16 is a manually triggered scene composite (baked merge of all finalized objects).

See [OBJECTS.md](./OBJECTS.md) for the full queue.

---

## Object 16: Scene Composite Bake

Object 16 is not a standalone object — it is the merged output of all finalized scene objects rendered together. The bake is triggered manually via the **🍳 Bake Obj 16** button in the studio UI. This calls window.bakeSceneComposite(), which performs a mergeFrom() sweep across all finalized geometry buffers and uploads a single fused VBO to the GPU.

The bake is guarded: if already baked, it switches the view without re-baking. If a bake is in progress, it returns early. A 16ms setTimeout gives the UI time to update before the blocking merge operation runs.

---

## Inclusive Languaging

All copy in this project — UI labels, documentation, tooltips, metadata — must comply with the inclusive languaging protocol defined in [AGENTS.md](./AGENTS.md) and [GEMINI.md](./GEMINI.md).

Key rules:
- No AI ingroup jargon (spine, gate, pass, leverage, cadence, etc.)
- Write for everyday visitors, local shopkeepers, and neighborhood residents
- Japanese and English copy carry equal warmth and dignity
- No filler words: delve, tapestry, testament, beacon, nexus, paradigm

---

## Deployment

The studio is hosted on Cloudflare Workers Assets under the worker name kokechan-claude-edition.

**Deploy from:**

    context/kyojimakokogarden/claude-world/kokechan/

**Command:**

    npx wrangler@4.127.1 deploy

**Route:** kokechan.preattention.ai (custom domain)

The dist/ directory inside the deploy folder maps:
- studio.html → /studio
- studio-stream.html → /studio-stream
- perf-bench.html → /perf-bench

See [RECONSTRUCTION.md](./RECONSTRUCTION.md) for full setup instructions.

---

## Contributing

This is a living archive — not a static snapshot. To propose a new object or correction:

1. Review the object queue in [OBJECTS.md](./OBJECTS.md)
2. Read the geometry construction guidelines in [RECONSTRUCTION.md](./RECONSTRUCTION.md)
3. Follow all languaging rules in [AGENTS.md](./AGENTS.md)
4. Export geometry as JSON using the ⬇ Save Obj button in the studio
5. Open a pull request with the exported JSON and a description of the landmark

---

*Kyojima Eki Living Archive Studio is a community documentation project rooted in the Kyojima / Koganecho neighborhoods of Yokohama. All reconstructions are interpretive illustrations, not field-verified architectural surveys.*
