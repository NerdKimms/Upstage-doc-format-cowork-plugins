# Upstage Design Tokens

## Colors

| Token | Hex | Usage |
|-------|-----|-------|
| `--ups-black` | #000000 | Body text, table borders, title |
| `--ups-dark-grey` | #434343 | Heading 3 (section headers) |
| `--ups-mid-grey` | #666666 | Heading 4, 5, 6 (subsections) |
| `--ups-gradient-start` | #BFBFBF | Header gradient bar left |
| `--ups-gradient-end` | #D8C6F8 | Header gradient bar right (light purple) |
| `--ups-table-header-bg` | #F3F3F3 | Table header row background |
| `--ups-white` | #FFFFFF | Page background |

## Typography

### Font Stack
- **Primary**: `Ups sans`
- **Korean fallback (cs)**: `Gothic A1`
- **Special characters**: `Batang` (for 『 』 etc.)
- **HTML fallback stack**: `'Ups sans', 'Gothic A1', 'Pretendard', 'Apple SD Gothic Neo', 'Noto Sans KR', sans-serif`

### Type Scale (in half-points for DOCX / pt for CSS)

| Element | DOCX w:sz | Actual pt | Weight | Color |
|---------|-----------|-----------|--------|-------|
| Title | 58 | 29pt | Bold | #000000 |
| Heading 1 | 40 | 20pt | Normal | #000000 |
| Heading 2 | 32 | 16pt | Normal | #000000 |
| Heading 3 (Section) | 28 | 14pt | **Bold** | #434343 |
| Heading 4 (Subsection) | 24 | 12pt | Normal | #666666 |
| Body text | 24 | 12pt | Normal | #000000 |
| List item (level 0) | 24 | 12pt | Normal | #000000 |
| List item text (level 1) | 22 | 11pt | Normal | #000000 |

## Page Layout (DXA units: 1440 = 1 inch)

| Property | Value (DXA) | Value (inches) |
|----------|-------------|----------------|
| Page width | 12,240 | 8.5" |
| Page height | 15,840 | 11" |
| Margin top | 1,440 | 1" |
| Margin right | 1,440 | 1" |
| Margin bottom | 1,440 | 1" |
| Margin left | 1,440 | 1" |
| Header from top | 720 | 0.5" |
| Footer from bottom | 720 | 0.5" |
| Content width | 9,360 | 6.5" |

## Spacing

| Element | Before (DXA) | After (DXA) | Line spacing |
|---------|-------------|-------------|-------------|
| Title | 0 | 60 | 360/auto (1.5x) |
| Heading 3 | 320 | 80 | 276/auto (1.15x) |
| Heading 4 | 280 | 80 | default |
| Body paragraph | 240 | 240 | default |
| List item L0 | 240 | 0 | default |
| List item L1 | 0 | 0 | default |
| Cover page lines | 0 | 0 | 360/auto |

## Body Text Indentation

| Context | Left indent (DXA) |
|---------|-------------------|
| Body paragraphs under section | 270 |
| List level 0 | defined by numbering |
| List level 1 | defined by numbering |

## Header Design

The header consists of two elements:

### 1. Gradient Bar
- **Position**: Full page width, top of page
- **Size**: ~7821000 EMU wide × 223200 EMU tall (~8.15" × 0.23")
- **Gradient**: Linear, angle 10800025 (left to right)
  - Start: #BFBFBF (grey)
  - End: #D8C6F8 (light purple/lavender)
- **Border**: None (noFill on line)

### 2. Logo
- **Image**: `assets/upstage-logo.png` (1000×324 px)
- **Position**: Anchored to page
  - Horizontal: 914400 EMU from page edge (1 inch / left margin)
  - Vertical: 352425 EMU from page top (~0.37")
- **Display size**: 944166 × 309563 EMU (~0.99" × 0.32")

## Footer Design

- Page number field, right-aligned
- Tab stops at center (4680) and right (9360)
- Text color: #000000

## Table Styling

### Header Row
- **Background**: #F3F3F3 (light grey)
- **Font**: Ups sans, Bold
- **Alignment**: Center (both horizontal)
- **Cell borders**: Single, size 4, color #000000
- **Cell margins**: 100 DXA all sides (top/right/bottom/left)

### Body Rows
- **Background**: None (white)
- **Font**: Ups sans, Normal
- **Alignment**: Left (default)
- **Cell borders**: Single, size 4, color #000000
- **Cell margins**: 100 DXA all sides
- **Row height**: ~800 DXA minimum for data rows

### Common Column Widths (from RFP table)
Total table width matches content width (9360 DXA):
- No. column: 555 DXA
- Category column: 1215 DXA
- Requirements column: 3885 DXA
- Status column: 2250 DXA
- Notes column: 1455 DXA

## Cover Page Structure

1. Empty paragraph (Title style, with spacing)
2. Empty paragraph
3. Title text: Bold, 29pt, Ups sans, Title style, line-spacing 1.5x
4. Several empty paragraphs (spacers, ~5-6 lines)
5. Date line (e.g., "Jan. 2026")
6. Two empty paragraphs
7. Company seal note ("업스테이지 직인 생략")
8. Empty paragraphs to fill page

## Section Numbering Convention

- Main sections: "1. 제안 개요", "2. 요구 사항", "3. ..."
  - Style: Heading 3, Bold
- Subsections: "1.1 배경 및 목적", "2.1 구매 일반 사항"
  - Style: Heading 4
- Sub-subsections: Bullet lists or numbered lists under subsections
