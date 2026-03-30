# upstage-doc-format

Claude Code plugin for generating professional documents in **Upstage's official corporate format**.

## Supported Output Formats

| Format | Use Case |
|--------|----------|
| **DOCX** | Formal business documents (RFP, proposals, reports) |
| **HTML** | Web preview, interactive documents |
| **Markdown** | Notion, Slack, GitHub, lightweight sharing |

## Installation

### Claude Code CLI

```bash
claude plugin add upstage-doc-format --from github:UpstageAI/upstage-doc-format
```

### Claude Desktop (Cowork)

Add this plugin from the Cowork plugin marketplace, or install manually by adding to your Claude configuration.

## Trigger Keywords

The skill automatically activates when you ask for:

- Business documents: RFP, proposal, report, whitepaper, memo, one-pager
- Korean terms: 제안서, 보고서, 기획서, 문서 작성
- Format references: "Upstage format", "Upstage template", "Upstage 양식"
- Casual: "우리 양식으로 만들어줘", "make it look like our docs"

## Design System

- **Font**: Ups sans (fallback: Gothic A1, Pretendard, Apple SD Gothic Neo)
- **Header**: Gradient bar (#BFBFBF -> #D8C6F8) with Upstage logo
- **Page**: US Letter (8.5" x 11"), 1" margins
- **Tables**: #F3F3F3 header background, 1px black borders

## Directory Structure

```
upstage-doc-format/
├── plugin.json
├── README.md
└── skills/
    └── upstage-doc-format/
        ├── SKILL.md                    # Skill definition
        ├── assets/
        │   └── upstage-logo.png        # Official Upstage logo
        └── references/
            ├── design-tokens.md        # Colors, fonts, spacing specs
            ├── docx-template.md        # DOCX generation template (docx-js)
            ├── html-template.md        # HTML/CSS template
            └── markdown-template.md    # Markdown conventions
```

## License

MIT
