# Markdown Template for Upstage Format

Since Markdown doesn't support visual styling (gradients, fonts, colors), the Upstage Markdown format focuses on consistent structure and numbering conventions that align with the branded format. This is best for Notion, Slack, GitHub, or lightweight document sharing.

## Template Structure

```markdown
# [Document Title]

**Date**: [Month. Year]
**Company**: Upstage AI, Inc.

---

## 1. [Section Title]

### 1.1 [Subsection Title]

[Body text with left alignment. Keep paragraphs concise and professional.]

### 1.2 [Subsection Title]

[Body text continues here.]

---

## 2. [Section Title]

### 2.1 [Subsection Title]

- Bullet item 1
  - Sub-item 1a
  - Sub-item 1b
- Bullet item 2
- Bullet item 3

| No. | 구분 | 요구사항 | 수용 여부 | 상세 설명 |
|-----|------|---------|----------|----------|
| 1   | GPU  | NVIDIA B200 | Pass | |
| 2   | 네트워크 | InfiniBand | Pass | |

### 2.2 [Subsection Title]

[Additional content.]

---

## 3. [Section Title]

### 3.1 [Subsection Title]

1. Numbered item 1
2. Numbered item 2
3. Numbered item 3

---

*업스테이지 직인 생략*
```

## Heading Hierarchy Mapping

| DOCX Style | Markdown | Usage |
|------------|----------|-------|
| Title | `# Title` | Document title (cover page equivalent) |
| Heading 3 (Section) | `## N. Title` | Main section headers |
| Heading 4 (Subsection) | `### N.N Title` | Subsection headers |
| Body text | Plain paragraph | Regular content |

## Conventions

1. **Section numbering**: Always use explicit numbers ("1.", "2.", "3.") in section headers rather than relying on auto-numbering. This matches the Upstage document convention.

2. **Horizontal rules**: Use `---` between major sections (before each `## N.` header) to visually separate sections, mimicking page breaks.

3. **Tables**: Always include a header row. Align columns for readability.

4. **Metadata block**: Start with title, date, and company name separated by `---` from the body.

5. **Korean/English mix**: Upstage documents frequently mix Korean and English. No special handling needed in Markdown.

6. **Company seal**: End with `*업스테이지 직인 생략*` in italics for formal documents.

## Notion-Specific Tips

When pasting into Notion:
- `# Title` becomes a "Heading 1" block
- `## Section` becomes "Heading 2"
- `### Subsection` becomes "Heading 3"
- Tables paste directly as Notion tables
- Horizontal rules become dividers

## Slack-Specific Tips

For Slack formatting, convert:
- `## N. Title` → `*N. Title*` (bold)
- `### N.N Title` → `_N.N Title_` (italic) or just bold text
- Tables → Code blocks with aligned columns
- Keep paragraphs short for readability in chat
