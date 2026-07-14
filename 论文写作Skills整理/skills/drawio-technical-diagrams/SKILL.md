---
name: drawio-technical-diagrams
description: Create or edit editable `.drawio` / diagrams.net technical diagrams from source documents, screenshots, templates, or user plans. Use when Codex needs to generate draw.io XML, update an existing `.drawio`, draw technical route diagrams, project proposal flowcharts, system/block diagrams, research-content diagrams, or convert Word/PPT/project materials into editable diagrams, especially when the draw.io CLI is unavailable and XML must be authored and validated manually.
---

# Drawio Technical Diagrams

## Workflow

1. Confirm the source and target:
   - Read source documents, existing `.drawio` files, screenshots, or PPT templates before drawing.
   - Use the user-specified output folder exactly. If several artifacts are created, keep them together.
   - If the user supplies an implementation plan, treat it as the contract unless it conflicts with source facts.

2. Choose the artifact form:
   - Prefer editable `.drawio` XML over raster images.
   - If `draw.io`, `diagrams.net`, or a CLI exporter is not installed, generate standard uncompressed `mxfile` XML and tell the user it can be opened in draw.io for preview/export.
   - If the user asks for PPT, do not paste the diagram as one flat image unless they explicitly ask. Recreate the diagram as editable PPT shapes or hand off to a PowerPoint skill.

3. Map content before placing boxes:
   - Extract the real title, module names, data inputs, methods, outputs, and final capability statement from source material.
   - For technical-route or proposal diagrams, use a stable structure: top title, 2-4 major module bands, inner lanes for input / processing / validation / output, and a bottom convergence or deliverable box.
   - Keep labels short enough for boxes. Move long explanations to notes or companion text, not cramped diagram nodes.

4. Match the reference style:
   - Inspect reference images or diagrams for canvas size, background, border radius, title color, dashed frames, fill colors, arrow style, line width, font, and spacing.
   - Reuse existing project `.drawio` style conventions when present.
   - For dynamic tracking antenna diagrams, distinguish the axes correctly: azimuth is the horizontal yaw/base rotation; elevation is the upper pitch/tilt assembly. Do not draw both axes as horizontal yaw rings.

5. Author XML defensively:
   - Use unique IDs, explicit `mxGeometry`, stable coordinates, and enough canvas height for Chinese labels.
   - XML-escape text values (`&`, `<`, `>`, quotes) instead of relying on draw.io to repair them.
   - Make repeated node sizes consistent; avoid overlapping arrows and text.
   - Prefer larger grouped module frames over dense card grids when the diagram is meant for project proposal material.

6. Validate before reporting completion:
   - Parse the `.drawio` as XML.
   - Verify the output file exists and has nonzero length.
   - Check that required headings and key labels are present exactly once where appropriate.
   - Count major module frames and key cells against the plan.
   - If a renderer/exporter is available, export a preview image and inspect it for overflow, clipping, and missing characters. If not available, say that validation was structural only.

7. Iterate from user corrections:
   - Edit the existing `.drawio` when possible; do not recreate from scratch if the user only asks to replace one module or fix wording.
   - Preserve user-provided module order and template style unless the user asks for a redesign.
   - When a user marks an image issue, translate that visual correction into a concrete diagram rule before regenerating.
