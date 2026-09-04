# 3D Geometry & Material Demonstration & Approval Protocol

## Core Mandate
All 3D modeling, architectural revisions, material tuning, and geometry granularity adjustments MUST be **demonstrated and approved first** in the dedicated Object Studio viewer:
`file:///Users/sophiaboettcher/.gemini/antigravity/brain/8b90f9fc-6b18-4055-9b0a-f8191c06e7bc/kyojima_individual_object_viewer.html` (or `kyojima-studio.html`).

## Required Workflow
1. **Model in Studio First**: Implement and refine individual objects, micro-geometry, and PBR shaders inside the Object Studio workbench (`kyojima_individual_object_viewer.html`).
2. **Demonstrate & Request Review**: Present the changes in the viewer for user inspection (using the reference overlay, turntable isolation, wireframe, and dimension inspection).
3. **Explicit User Approval Required**: DO NOT deploy, push to production, or merge into the live engine (`WorldEngine` / `kokechan.preattention.ai`) until the user has explicitly reviewed and approved the demonstration in the viewer.
