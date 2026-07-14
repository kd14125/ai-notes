---
name: docx-red-yellow-revision
description: Apply visible revision-style edits to `.docx` files using red old text, yellow new text, minimal-diff highlights, paired red/yellow paragraph cleanup, and PDF spot checks. Use when the user asks for "红色旧内容", "黄色新内容", "最小改动标注", deleting superseded paragraphs while keeping the new text, or Word revisions without true tracked changes.
---

# DOCX Red Yellow Revision

## Setup
1. If available, apply `ps-utf8-io` first for Windows shell and inline Python commands.
2. Use `python-docx` for the document edits.
3. When page placement matters, export the edited file to PDF and spot-check the relevant pages.

## Choose the edit mode
- Full paragraph replacement: keep old paragraph text in red and new paragraph text in yellow.
- Phrase replacement: keep unchanged context, mark the removed phrase red, and mark the replacement yellow.
- Minimal-diff update: highlight only inserted or replaced spans in yellow rather than whole paragraphs.
- Pair cleanup: detect adjacent red-old and yellow-new paragraph pairs and remove the old red paragraph after rebuilding the kept paragraph.

## Editing rules
1. Resolve the exact target paragraph range before editing.
2. Preserve formatting by capturing paragraph style and a template run's font properties before clearing and rebuilding runs.
3. Use `WD_COLOR_INDEX.RED` for removed text and `WD_COLOR_INDEX.YELLOW` for kept or new text.
4. When the user wants "minimum change" markup, compute a diff and highlight only insert or replace spans, not equal spans.
5. When cleaning red/yellow paragraph pairs, delete from back to front so paragraph indices do not drift.
6. If the source file is open or overwrite fails, save a sibling `*_revision.docx` or `*_最小改动标注.docx` file and explain why.

## Pair cleanup heuristic
- Look for adjacent paragraphs where the first contains red-highlighted runs and the second contains yellow-highlighted runs.
- Compare paragraph text similarity before treating them as a pair.
- Rebuild the kept paragraph before deleting the old paragraph.
- Recount remaining red and yellow runs in the target segment after cleanup.

## Validation
1. Print the output path and a compact summary of what changed.
2. Re-open the saved DOCX and verify target paragraphs, highlight counts, or key phrases.
3. If layout matters, export to PDF and search anchor phrases on the expected pages.
4. If the result still has unexpected red spans or over-highlighted yellow text, iterate once more instead of returning the first draft.

## Windows PDF spot-check options
- Prefer Word COM export (`SaveAs(..., FileFormat=17)`) when Microsoft Word is available.
- Otherwise fall back to LibreOffice or the generic DOCX rendering helper.
