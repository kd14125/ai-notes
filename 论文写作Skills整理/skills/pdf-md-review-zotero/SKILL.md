---
name: pdf-md-review-zotero
description: Convert academic PDFs to Markdown with MinerU, preserve images, write concise reading summaries, organize PDF/MD/summary files, and index all three as Zotero attachments under one parent item. Use for batch paper整理、PDF转MD、MinerU解析、阅读总结、Zotero索引、修复Zotero中Markdown图片不显示等任务。
---

# PDF 转 MD 并简要阅读，最终索引到 Zotero

## When to Use

Use this skill when the user wants to:

- Batch organize academic PDF papers into a clean local folder structure.
- Convert PDFs to Markdown, preferably with MinerU.
- Preserve Markdown image folders so `![](images/...)` references work.
- Write per-paper reading summaries.
- Import or repair Zotero entries so PDF, MinerU Markdown, and summary Markdown are indexed under one parent item.
- Fix Zotero Markdown attachments whose images do not render.
- Repair MinerU Markdown where image placeholders such as `<!-- image-->` were emitted without actual image files or Markdown image references.

This skill is domain-neutral. If the user provides a research direction, make summaries focus on that direction. If not, write a general research-oriented summary.

## Required Inputs

Confirm or discover these before mutating files or Zotero:

- Source/project folder.
- Target Zotero collection name or collection key.
- Paper count target, if any.
- Naming rule, defaulting to `年份_中文标题名`.
- User research direction for summary relevance, if any.
- Zotero data directory before database-level repair.

On Windows, before PowerShell output or inline Python involving Chinese paths, use UTF-8 setup:

```powershell
$OutputEncoding = [Console]::OutputEncoding = [Text.UTF8Encoding]::new($false)
$env:PYTHONIOENCODING = 'utf-8'
$env:PYTHONUTF8 = '1'
```

## Recommended Directory Layout

Use this layout unless the user specifies another:

```text
<project>/
  pdf版本/
    年份_中文标题名.pdf
  md版本/
    年份_中文标题名/
      年份_中文标题名.md
      阅读总结.md
      images/
```

Keep the PDF, MinerU Markdown, summary Markdown, and `images/` aligned by the same paper folder name.

## Workflow

### 1. Collect and Normalize PDFs

- Gather papers from the requested sources, such as IEEE Xplore, Google Scholar, publisher pages, arXiv, or user-provided files.
- Prefer recent papers if the user gives a time range.
- Rename PDFs as `年份_中文标题名.pdf` unless the user gives another rule.
- Skip obvious duplicates such as `- 副本.pdf`, unless the user explicitly asks to keep them.
- Put final PDFs under `pdf版本/`.

### 2. Convert PDFs to Markdown with MinerU

- Use MinerU for PDF-to-Markdown text extraction whenever requested or available.
- For each PDF, create one folder under `md版本/<论文中文名>/`.
- Save the main Markdown as `<论文中文名>.md`.
- Preserve MinerU output images under `md版本/<论文中文名>/images/`.
- If MinerU text extraction works but image extraction needs local help, local image extraction is acceptable only for images; the final `images/` folder must still live beside the Markdown.

### 3. Preserve Images for Markdown

- Markdown image paths should remain relative, normally `![](images/xxx.png)` or equivalent.
- Do not move `images/` away from the Markdown folder.
- Do not treat `images/` as a separate document attachment when the goal is Markdown rendering.
- Before claiming completion, verify every Markdown folder has an `images/` directory when the Markdown references `images/`.
- An `images/` directory being non-empty is not enough. Verify the main Markdown actually contains image references and each referenced image file exists.
- If MinerU emits placeholders such as `<!-- image-->`, replace them with real image references or remove them after Figure images are inserted. Do not leave visible empty placeholders in final Markdown.

### 3.1 Local Figure Extraction Fallback

Use this fallback when MinerU returns Markdown text but omits images, creates empty `images/` folders, or leaves `<!-- image-->` placeholders.

Preferred approach:

1. Use a local PDF parser/renderer such as PyMuPDF (`fitz`) to parse each PDF page.
2. Locate figure captions using patterns such as `Fig. 1`, `Fig. 2`, `Figure 1`, and `Figure 2`.
3. For each caption, crop the actual figure region:
   - Prefer the closest image block above the caption on the same page.
   - If the figure is vector-drawn and no image block exists, crop the bounded region above the caption rather than rendering an arbitrary full page.
   - Avoid logos, publisher badges, copyright blocks, page headers, footers, and unrelated page screenshots.
4. Save cropped figures under:

```text
md版本/<论文中文名>/images/figures/figure_XX_page_YYY.png
```

5. Insert each cropped figure directly before its matching caption in the main Markdown:

```markdown
![](images/figures/figure_01_page_003.png)

Fig. 1. ...
```

6. Generate an optional local index:

```text
md版本/<论文中文名>/images/figure_index.md
```

The index is only a navigation aid. It does not replace inserting the images into the main Markdown.

Validation requirements for this fallback:

- No `<!-- image-->` placeholders remain in the final main Markdown.
- Every `![](images/...)` path in the main Markdown resolves to an existing local file.
- Each detected figure caption has the corresponding cropped figure immediately above it when possible.
- If a paper has subfigures or repeated textual references such as “Figure 1 illustrates...”, insert images only before real captions, not before every textual mention.

### 4. Write Reading Summaries

For each paper, create:

```text
md版本/<论文中文名>/阅读总结.md
```

Default summary structure:

```markdown
# 中文论文名阅读总结

## 论文基本信息

## 论文解决的问题与采用的方法

## 主要创新点

## 与用户研究方向的相关性

## 可借鉴的具体思路

## 代码公开情况

## 关键图示与阅读提示
```

Code availability rules:

- Mark code as public only when the paper explicitly provides GitHub, GitLab, Zenodo, repository URL, or phrases such as `source code is available`, `code available at`, or `implementation is available`.
- Do not mark code as public just because the paper mentions datasets, simulation software, pseudocode, channel coding, or toolboxes.
- If no clear evidence is found, write: `未在转换出的论文正文中发现明确的代码公开说明。`

For figures:

- Prefer 2-4 high-value images: system model, algorithm flow, link/beam/positioning diagram, and key performance curves.
- Reference images using relative paths, for example `![](images/xxx.jpg)`.
- If summaries refer to figures, ensure those figures are embedded in the main Markdown or available through `images/figure_index.md`.

### 5. Organize Files by Paper

For each valid paper, final local assets should be:

- `pdf版本/<论文中文名>.pdf`
- `md版本/<论文中文名>/<论文中文名>.md`
- `md版本/<论文中文名>/阅读总结.md`
- `md版本/<论文中文名>/images/`

Run a count check: number of non-duplicate PDFs, Markdown paper folders, main Markdown files, summaries, and image folders should match unless the user explicitly chose otherwise.

For batch jobs that include source code, place the matching repository inside the paper folder, for example:

```text
md版本/<论文中文名>/开源代码/
```

Keep a mapping file such as `open_source_paper_mapping.json` when the source folder names differ from the normalized paper names.

### 6. Import and Index in Zotero

Target shape in Zotero:

- One parent item per paper.
- Parent title should use the Chinese paper name unless the user requests another naming style.
- Attach exactly these three main attachments under the parent item:
  - `PDF原文 - <论文中文名>`
  - `MinerU MD原文 - <论文中文名>`
  - `中文阅读总结MD - <论文中文名>`

Do not add `images/` as a visible Zotero child attachment merely to make Markdown images work. That does not fix relative Markdown rendering.

If Zotero attachment titles become mojibake, repair titles using UTF-8-safe scripts and the paper folder names as the source of truth.

### 7. Fix Zotero Markdown Image Display

Zotero stores imported or linked file attachments under directories like:

```text
<Zotero data dir>/storage/<attachmentKey>/
```

To make images render when opening MD attachments from Zotero:

1. Locate the `attachmentKey` for each `MinerU MD原文` and `中文阅读总结MD` attachment.
2. Copy the paper's local `md版本/<论文中文名>/images/` folder into both MD attachment storage folders:

```text
<Zotero data dir>/storage/<MinerU MD attachmentKey>/images/
<Zotero data dir>/storage/<summary MD attachmentKey>/images/
```

3. Verify the copied image file count matches the source `images/` count.
4. Keep the Zotero item itself at three visible attachments: PDF, MinerU MD, summary MD.

If database-level Zotero repair is needed:

- Close Zotero first.
- Back up `zotero.sqlite` with a timestamp.
- Make the minimal change.
- Reopen Zotero and verify through the Local API or UI.

### 8. Verification Checklist

Before final response, verify:

- PDF count matches intended paper count after excluding duplicates.
- Each paper has a folder under `md版本/`.
- Each paper folder contains the main Markdown and `阅读总结.md`.
- `images/` exists for Markdown files that reference `images/`.
- Main Markdown files contain real `![](images/...)` references when figures were extracted.
- Every image reference in main Markdown resolves to an existing file.
- No `<!-- image-->` placeholders remain after local Figure repair.
- Figure crops are based on PDF Figure/Fig. captions and not arbitrary page screenshots, except when a vector figure requires caption-bounded region cropping.
- Zotero collection contains one parent item per paper.
- Each parent item has exactly three visible main attachments: PDF, MinerU MD, summary MD.
- Zotero Markdown attachment storage folders contain copied `images/` folders.
- No attachment titles are mojibake.
- No original PDF, Markdown, summary, or image folder was deleted.

For local Figure repair, write a summary CSV when practical:

```text
open_source_figure_patch_summary.csv
```

Recommended columns: `Name`, `FigureFiles`, `MdImageRefs`, `MissingRefs`, `PlaceholdersLeft`, `FigureCaptions`, `CaptionsWithPrevImage`.

## Naming Rules

- Default paper file/folder name: `年份_中文标题名`.
- Attachment titles:
  - `PDF原文 - <论文中文名>`
  - `MinerU MD原文 - <论文中文名>`
  - `中文阅读总结MD - <论文中文名>`
- Keep names stable across PDF, Markdown folder, summary, and Zotero parent item.
- If the user provides a different naming scheme, follow it consistently and document the choice in the final response.

## Common Failure Modes

- **Mistake:** Adding `images/` as a visible Zotero child attachment.
  **Fix:** Copy `images/` into each MD attachment's Zotero storage folder instead.

- **Mistake:** Markdown opens but images are broken.
  **Fix:** Confirm the opened MD file's directory contains an `images/` folder with matching filenames.

- **Mistake:** `images/` is non-empty, but the main Markdown still shows `<!-- image-->` or no inline images.
  **Fix:** Insert `![](images/...)` references into the main Markdown, preferably immediately before matching `Fig.`/`Figure` captions. Then remove stale placeholders.

- **Mistake:** Local extraction saved random page screenshots instead of the paper's actual Figure images.
  **Fix:** Re-extract using Figure/Fig. caption detection. Crop the nearest image block above each caption, or crop the caption-bounded vector figure region if no image block exists.

- **Mistake:** Figure files were regenerated, but Markdown still references old filenames.
  **Fix:** Remove stale `![](images/figures/figure_*.png)` lines and rebuild image references from the files that currently exist in `images/figures/`.

- **Mistake:** Chinese titles become mojibake in Zotero.
  **Fix:** Re-run title repair with PowerShell and Python UTF-8 settings; use folder names as authoritative titles.

- **Mistake:** MinerU output is incomplete.
  **Fix:** Re-run MinerU for text. Use local tools only for supplementary image extraction if the user allows it, then place results in `images/`.

- **Mistake:** Duplicate PDFs inflate paper count.
  **Fix:** Exclude obvious duplicates such as `- 副本.pdf` unless the user says otherwise.
