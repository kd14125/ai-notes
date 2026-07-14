---
name: scientific-figure-text-translation
description: Use when replacing or translating text labels in scientific and academic figures, especially English-to-Chinese or Chinese-to-English labels for papers, Visio/PPT/SVG/draw.io source diagrams, or requests to use image generation for figure text where terminology, spelling, fonts, and layout accuracy matter more than generative style.
---

# Scientific Figure Text Translation

## Workflow
1. Preserve the original figure. Never overwrite the source image; create a new file with a suffix such as `_en`, `_translated`, or `_labels_en`.
2. Find the highest-fidelity editable source before touching pixels: Visio `.vsdx`, PowerPoint, SVG, draw.io, PDF vector content, TikZ, or plotting code. Copy and edit that source when available, then export the replacement figure.
3. Extract the label map before editing. List each source label and target translation, using terminology from the paper, caption, and surrounding LaTeX/Word text. Keep correct abbreviations such as `FSO`, `RF`, `SNR`, `BER`, `RTK`, or `LoRa`.
4. Prefer deterministic text replacement for paper figures. Use the source editor, vector editing, SVG/canvas editing, Pillow overlays, or PDF tooling. Do not trust AI image generation for exact spelling, formulas, Chinese glyphs, or acronyms.
5. Use generative editing only for background repair when exact text can be overlaid afterward. If the user asks for GPT/image editing to translate labels, first check whether source files exist and explain that source/vector editing is the safer path for paper figures.
6. For Visio/PPT/Office sources, duplicate the original file, replace text boxes/shapes in the duplicate, export to PNG/PDF at the required resolution, and visually compare against the original for font drift, moved arrows, and clipped labels.
7. Segment raster-only figures by region. For flowcharts and boxes, clear text regions with local background color, redraw text, and repair any damaged lines. For photos or gradients, use small masks to avoid visible repair blocks.
8. Choose fonts that actually support the target script, such as Microsoft YaHei, SimSun, Source Han Sans, or Noto Sans CJK for Chinese labels. Avoid relying on generated text rasterization for CJK characters.
9. Wrap long labels manually so they fit inside boxes without shrinking the whole diagram. Keep equations and units exact.
10. Review visually in rounds. Check for remaining source-language text, duplicated labels, misspellings, bad Chinese glyphs, clipped text, broken arrows/lines, and excessive repair blocks.
11. If text accuracy and visual fidelity conflict, prioritize accuracy for paper figures and state any visual compromise.
12. If replacing a figure in LaTeX or Word, change only the relevant figure file/path unless the user asked for caption/label changes. Compile or render the document afterward using the project's expected chain.
13. Report the generated figure path, whether the original/source was preserved, the export method, and the compile/render result.

## Good Defaults
- Output next to the original figure unless the project has a dedicated generated-assets folder.
- For Chinese-to-English academic labels, prefer concise noun phrases over sentence-like labels.
- For English-to-Chinese labels, prefer concise academic/engineering terms from the surrounding paper instead of literal word-by-word translations.
- Use iterative visual checks instead of assuming the first edit succeeded.
- Keep a short verification note: no visible source-language residue, spelling/glyphs checked, source file preserved, and target document still builds or renders.
