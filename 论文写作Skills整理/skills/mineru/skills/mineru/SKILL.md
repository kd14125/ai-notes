---
name: mineru
description: Parse PDFs into Markdown/JSON/DOCX using MinerU API or MinerU MCP. Extract text, tables, formulas, and images with OCR support. Use when converting PDF documents, preserving Markdown plus image folders, extracting content from scanned papers, batch processing PDF files, or retrying MinerU timeout/SSL failures.
metadata:
  author: Nebutra
  version: "2.0.0"
  argument-hint: <pdf-file-or-url>
---

# MinerU PDF Parser

Parse PDF documents into structured Markdown using the MinerU API.

## MCP-First Workflow

- If the user explicitly asks for MinerU MCP, cloud parsing, or says not to use local PDF extraction, use the MinerU MCP `parse_documents` tool instead of local scripts.
- Set `output_dir` when the user provides a target folder, especially for batch conversion or image-heavy papers.
- Process large or failure-prone batches in small groups. After a timeout, retry the failed file alone or with a smaller page range.

## Preserve Markdown And Images

- Treat each Markdown output and its companion image/assets folder as one unit.
- Do not move only `.md` files when MinerU emitted referenced images.
- Verify generated Markdown count, missing files, zero-byte outputs, and expected image/assets folders before reporting completion.

## Quick Start

```bash
# Set API token
export MINERU_TOKEN="your-jwt-token"

# Parse single PDF
python mineru_api.py --file ./document.pdf --output ./output/
```

## Features

- **Multi-format Output**: Markdown, JSON, DOCX
- **Formula Recognition**: LaTeX formula extraction
- **Table Extraction**: Structured table parsing
- **OCR Support**: Scanned PDF processing
- **Batch Processing**: Parallel processing with async

## Authentication

Get your free token at: https://open.walab.ai/

```bash
export MINERU_TOKEN="your-token-here"
```
