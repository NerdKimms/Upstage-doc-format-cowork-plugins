---
name: upstage-doc-format
description: "Generate documents in Upstage's official vertical document format. Supports DOCX, HTML, and Markdown output. Use this skill whenever the user asks to create any business document (RFP, proposal, report, whitepaper, memo, one-pager, internal doc, external doc, 제안서, 보고서, 기획서, 문서 작성) in Upstage's branded design format. Also trigger when the user mentions 'Upstage format', 'Upstage template', 'Upstage 양식', 'Upstage 디자인', '업스테이지 문서', '업스테이지 양식', '업스테이지 포맷', or asks for any document that should match Upstage's corporate identity. Even if the user just says 'make it look like our docs' or '우리 양식으로 만들어줘', use this skill."
---

# Upstage Document Format Skill

This skill generates professional documents that exactly match Upstage's official corporate document design.

## When to Use

Any time a document needs to follow Upstage's branded format, whether the output is DOCX, HTML, or Markdown.

## Design System Overview

Before creating any document, read the detailed design tokens and templates in `references/design-tokens.md`. That file contains the exact fonts, colors, sizes, spacing, header/footer specs, table styling, and gradient bar details extracted from Upstage's official RFP template.

### Quick Reference

| Element | Spec |
|---------|------|
| **Primary Font** | "Ups sans" (fallback: Gothic A1 for Korean, Arial for Latin) |
| **Page Size** | US Letter (8.5" x 11"), 1" margins |
| **Title** | Ups sans, Bold, 29pt (#000000) |
| **Section Header (H3)** | Ups sans, Bold, 14pt (#434343) |
| **Subsection Header (H4)** | Ups sans, 12pt (#666666) |
| **Body Text** | Ups sans, 12pt (#000000), line-spacing 1.15 |
| **Header Bar** | Full-width gradient: #BFBFBF → #D8C6F8 (left to right) |
| **Header Logo** | Upstage logo, top-left, below gradient bar |
| **Footer** | Page number, right-aligned |
| **Table Header** | Background #F3F3F3, bold, centered, 1px black borders |
| **Table Body** | No fill, 1px black borders, 100 DXA cell padding |

## Output Format Selection

The user may request one of three formats:

### 1. DOCX (default for formal documents)
Use `docx-js` (npm package `docx`) to generate. Read `references/docx-template.md` for the complete JavaScript template code that reproduces the exact Upstage format including:
- Gradient header bar as a shape
- Logo image in header
- Styled headings, body text, lists, tables
- Page numbering in footer

### 2. HTML (for web/preview/interactive)
Read `references/html-template.md` for the complete HTML/CSS template. The HTML version uses:
- CSS gradient for header bar
- Embedded logo (base64 or path)
- CSS variables matching the design tokens
- Print-friendly styling

### 3. Markdown (for Notion/Slack/lightweight use)
Read `references/markdown-template.md` for the Markdown conventions. Since Markdown can't reproduce all visual styling, it uses:
- Heading hierarchy matching the Upstage numbering scheme
- Table formatting with proper alignment
- Clear section numbering

## Document Structure

All Upstage documents follow this structure:

1. **Cover Page** (DOCX/HTML only)
   - Title (bold, large)
   - Several blank lines for spacing
   - Date
   - Additional blank lines
   - Company seal note ("업스테이지 직인 생략")

2. **Body Pages** (all formats)
   - Section headers: "1. 제안 개요", "2. 요구 사항", etc.
   - Subsection headers: "1.1 배경 및 목적", etc.
   - Body paragraphs with left indent (270 DXA / ~0.19")
   - Bullet/numbered lists with proper indentation
   - Tables with header row styling

3. **Header** (DOCX/HTML only)
   - Gradient bar across full page width
   - Upstage logo positioned below bar, left-aligned

4. **Footer** (DOCX/HTML only)
   - Page number, right-aligned

## Creating a Document

### Step 1: Read the relevant template reference
Based on the requested format, read the appropriate reference file:
- DOCX → `references/docx-template.md`
- HTML → `references/html-template.md`
- Markdown → `references/markdown-template.md`

### Step 2: Adapt content to the template
Fill in the user's content using the exact styling from the template. Maintain the heading hierarchy, spacing, and formatting conventions.

### Step 3: Generate the file
- For DOCX: Run the JavaScript generation script, then validate with `python scripts/office/validate.py`
- For HTML: Write a single self-contained HTML file
- For Markdown: Write a .md file following the convention

### Step 4: Verify
Always preview or validate the output before delivering to the user.

## Important Notes

- "Ups sans" is a custom Upstage font. For DOCX, it's specified in the font properties and will render correctly if installed. For HTML, use a font stack: `'Ups sans', 'Gothic A1', 'Pretendard', 'Apple SD Gothic Neo', sans-serif`
- The gradient bar colors are #BFBFBF (grey, left) → #D8C6F8 (light purple, right)
- Korean text should use the same "Ups sans" font
- Table header background is always #F3F3F3 with bold centered text
- Body text paragraphs have 240 DXA (12pt) spacing before and after
- The logo asset is available at `assets/upstage-logo.png` (1000x324px)
