---
name: mineru
description: "Parse PDFs, Word docs, PPTs, images, or public document URLs into clean Markdown using MinerU's VLM engine or the MinerU MCP. Use when: (1) the user asks for MinerU/MinerU MCP/cloud parsing, (2) converting PDF/Word/PPT/image to Markdown, (3) extracting text/tables/formulas/images, (4) batch paper conversion while preserving Markdown plus image folders, (5) saving parsed content to Obsidian or local output directories, or (6) retrying MinerU timeout/SSL failures."
homepage: https://mineru.net
metadata:
  openclaw:
    emoji: "📄"
    requires:
      bins: ["python3"]
      env:
        - name: MINERU_TOKEN
          description: "MinerU API key — get free token at https://mineru.net/user-center/api-token (2000 pages/day, 200MB/file)"
    install:
      - id: pip
        kind: pip
        packages: ["requests", "aiohttp"]
        label: "Install Python dependencies (pip)"
---

# MinerU Document Parser

Convert PDF, Word, PPT, and images to clean Markdown using MinerU's VLM engine — LaTeX formulas, tables, and images all preserved.

## MCP-First Workflow

1. If the user says MinerU, MinerU MCP, cloud parsing, or explicitly rejects local PDF extraction, use the MinerU MCP `parse_documents` tool. Do not fall back to `pdfplumber`, `pypdf`, OCR scripts, or local text extraction unless the user explicitly allows it.
2. Set `output_dir` when the user provides a target folder or when batch output may be too large for inline return. Prefer an output folder next to the source PDFs, such as `md版本`, `markdown`, or the user-specified directory.
3. Omit `enable_ocr` unless the user mentions scanned or poor-quality documents. Set `language` only when it is clear from the document or request.
4. For batch PDFs, process in small groups. Use one file per call for large papers, many-image papers, or after any timeout. For page-specific requests, pass a `{"source": "...", "pages": "N-M"}` object instead of parsing the whole PDF.

## Preserving Images

- Treat each parsed Markdown file and its companion image/assets folder as one unit. Do not move only the `.md` file if MinerU emitted images.
- After parsing, verify the output folder contains the expected Markdown count and inspect whether each parsed document has an images/assets directory or referenced image files.
- If the user asks to keep image folders, report both Markdown and image-folder counts. If MinerU returns inline-only Markdown or omits images, state that explicitly instead of claiming the images were preserved.

## Timeout and SSL Recovery

- If `parse_documents` times out around 120 seconds, retry the failed file alone with an explicit `output_dir`. If it was already a single large file, retry a smaller page range when useful.
- If MinerU/CDN download fails with SSL/EOF errors, wait briefly and retry once. If the same file fails again, record it in a failed-files list and continue with the rest of the batch.
- When the user says the network changed or asks whether MinerU recovered, test with one small representative document first before restarting a large batch.
- Do not report the batch complete until failed files are either successfully parsed or clearly listed as failed MinerU items.

## Verification

- Count source PDFs/documents and generated `.md` files.
- Check for missing Markdown outputs, zero-byte files, and missing image/assets folders when images are expected.
- Summarize results as: parsed count, failed count, output folder, and any files that need retry.

## Setup

1. Get free API token at https://mineru.net/user-center/api-token

```bash
export MINERU_TOKEN="your-token-here"
```

**Limits:** 2000 pages/day · 200 MB per file · 600 pages per file

## Supported File Types

| Type | Formats |
|------|---------|
| 📕 PDF | `.pdf` — papers, textbooks, scanned docs |
| 📝 Word | `.docx` — reports, manuscripts |
| 📊 PPT | `.pptx` — slides, presentations |
| 🖼️ Image | `.jpg`, `.jpeg`, `.png` — OCR extraction |

## Commands

### Single File

```bash
python3 scripts/mineru_v2.py --file ./document.pdf --output ./output/
```

### Batch Directory with Resume

```bash
python3 scripts/mineru_v2.py \
  --dir ./docs/ \
  --output ./output/ \
  --workers 10 \
  --resume
```

### Direct to Obsidian

```bash
python3 scripts/mineru_v2.py \
  --dir ./pdfs/ \
  --output "~/Library/Mobile Documents/com~apple~CloudDocs/Obsidian/VaultName/" \
  --resume
```

### Chinese Documents

```bash
python3 scripts/mineru_v2.py --dir ./papers/ --output ./output/ --language ch
```

### Complex Layouts (Slow but Most Accurate)

```bash
python3 scripts/mineru_v2.py --file ./paper.pdf --output ./output/ --model vlm
```

## CLI Options

```
--dir PATH          Input directory (PDF/Word/PPT/images)
--file PATH         Single file
--output PATH       Output directory (default: ./output/)
--workers N         Concurrent workers (default: 5, max: 15)
--resume            Skip already processed files
--model MODEL       Model version: pipeline | vlm | MinerU-HTML (default: vlm)
--language LANG     Document language: auto | en | ch (default: auto)
--no-formula        Disable formula recognition
--no-table          Disable table extraction
--token TOKEN       API token (overrides MINERU_TOKEN env var)
```

## Model Version Guide

| Model | Speed | Accuracy | Best For |
|-------|-------|----------|----------|
| `pipeline` | ⚡ Fast | High | Standard docs, most use cases |
| `vlm` | 🐢 Slow | Highest | Complex layouts, multi-column, mixed text+figures |
| `MinerU-HTML` | ⚡ Fast | High | Web-style output, HTML-ready content |

## Script Selection

| Script | Use When |
|--------|----------|
| `mineru_v2.py` | Default — async parallel (up to 15 workers) |
| `mineru_async.py` | Fast network, need maximum throughput |
| `mineru_stable.py` | Unstable network — sequential, max retry |

## Output Structure

```
output/
├── document-name/
│   ├── document-name.md    # Main Markdown
│   ├── images/             # Extracted images
│   └── content.json        # Metadata
```

## Performance

| Workers | Speed |
|---------|-------|
| 1 (sequential) | 1.2 files/min |
| 5 | 3.1 files/min |
| 15 | 5.6 files/min |

## Error Handling

- 5x auto-retry with exponential backoff
- Use `--resume` to continue interrupted batches
- Failed files listed at end of run

## API Reference

For detailed API documentation, see [references/api_reference.md](references/api_reference.md).
