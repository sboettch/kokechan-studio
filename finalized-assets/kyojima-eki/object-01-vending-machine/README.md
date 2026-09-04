# Finalized Asset: Object 01 — Crimson Vending Machine (Kyojima Eki)

## Status: FINALIZED & APPROVED FOR METAVERSE INTEGRATION

### Asset Package Files:
- `panel-1-window-display.jpg`: Full resolution 2D reference master for the showcase window.
- `panel-1-window-panel.jpg`: Tight crop texture mapped to the recessed interior 3D quad (z = 0.380m).
- `panel-2-chassis-body.jpg`: Full resolution 2D reference master for the crimson sheet-metal chassis.
- `panel-2-chassis-cutout.png`: RGBA texture with transparent window aperture cutout mapped to the front door quad (z = 0.428m).
- `hero-portrait.jpg`: Washi-paper front-on portrait illustration.
- `dusk-alley-scene.jpg`: Shitamachi dusk environmental illustration.
- `object-spec.json`: Machine-readable metadata, geometric constraints, and metaverse room placement coordinates.

### How to Import into Online Metaverse Rooms:
1. Copy this entire folder into your client dist (`dist/assets/finalized/kyojima-eki/object-01-vending-machine`).
2. The runtime engine reads `object-spec.json` to instantiate the Two-Panel WebGL composite mesh at world anchor `kyojima-eki` with offset `[3.4, 0.0, 1.8]`.
