# HTML Template for Upstage Format

Use this template to generate self-contained HTML documents matching Upstage's corporate design.

## Complete HTML Template

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{{DOCUMENT_TITLE}}</title>
  <style>
    /* ============================================================
       UPSTAGE DESIGN TOKENS
       ============================================================ */
    :root {
      --ups-black: #000000;
      --ups-dark-grey: #434343;
      --ups-mid-grey: #666666;
      --ups-gradient-start: #BFBFBF;
      --ups-gradient-end: #D8C6F8;
      --ups-table-header-bg: #F3F3F3;
      --ups-white: #FFFFFF;
      --ups-font: 'Ups sans', 'Gothic A1', 'Pretendard', 'Apple SD Gothic Neo', 'Noto Sans KR', sans-serif;
      --ups-page-width: 8.5in;
      --ups-margin: 1in;
      --ups-content-width: 6.5in;
    }

    /* ============================================================
       PAGE SETUP
       ============================================================ */
    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      font-family: var(--ups-font);
      font-size: 12pt;
      line-height: 1.5;
      color: var(--ups-black);
      background: #f5f5f5;
    }

    .document {
      max-width: var(--ups-page-width);
      margin: 20px auto;
      background: var(--ups-white);
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .page {
      padding: var(--ups-margin);
      padding-top: 80px;
      min-height: 11in;
      position: relative;
    }

    /* ============================================================
       HEADER
       ============================================================ */
    .header {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
    }

    .gradient-bar {
      height: 18px;
      background: linear-gradient(to right, var(--ups-gradient-start), var(--ups-gradient-end));
    }

    .logo-area {
      padding: 10px 0 0 var(--ups-margin);
    }

    .logo-area img {
      height: 26px;
      width: auto;
    }

    /* ============================================================
       FOOTER
       ============================================================ */
    .footer {
      text-align: right;
      padding: 20px var(--ups-margin);
      font-size: 10pt;
      color: var(--ups-black);
    }

    /* ============================================================
       COVER PAGE
       ============================================================ */
    .cover-page {
      display: flex;
      flex-direction: column;
      min-height: calc(11in - 2 * var(--ups-margin) - 80px);
      padding-top: 40px;
    }

    .cover-title {
      font-family: var(--ups-font);
      font-size: 29pt;
      font-weight: 700;
      line-height: 1.5;
      color: var(--ups-black);
      margin-bottom: 0;
    }

    .cover-spacer { flex: 1; }

    .cover-date {
      font-family: var(--ups-font);
      font-size: 12pt;
      color: var(--ups-black);
      margin-bottom: 40px;
    }

    .cover-seal {
      font-family: var(--ups-font);
      font-size: 12pt;
      color: var(--ups-black);
    }

    /* ============================================================
       TYPOGRAPHY
       ============================================================ */
    h3.section-header {
      font-family: var(--ups-font);
      font-size: 14pt;
      font-weight: 700;
      color: var(--ups-dark-grey);
      margin-top: 24px;
      margin-bottom: 8px;
      line-height: 1.15;
    }

    h4.subsection-header {
      font-family: var(--ups-font);
      font-size: 12pt;
      font-weight: 400;
      color: var(--ups-mid-grey);
      margin-top: 20px;
      margin-bottom: 8px;
    }

    .body-text {
      font-family: var(--ups-font);
      font-size: 12pt;
      color: var(--ups-black);
      margin: 12pt 0;
      padding-left: 0.19in;
      line-height: 1.5;
    }

    /* ============================================================
       LISTS
       ============================================================ */
    ul.ups-list, ol.ups-list {
      padding-left: 0.5in;
      margin: 12pt 0;
    }

    ul.ups-list li, ol.ups-list li {
      font-family: var(--ups-font);
      font-size: 12pt;
      margin-bottom: 4pt;
    }

    ul.ups-list li:first-child {
      margin-top: 12pt;
    }

    ul.ups-list ul, ol.ups-list ol {
      padding-left: 0.5in;
    }

    /* ============================================================
       TABLES
       ============================================================ */
    table.ups-table {
      width: 100%;
      border-collapse: collapse;
      margin: 16pt 0;
      font-family: var(--ups-font);
      font-size: 12pt;
    }

    table.ups-table th {
      background-color: var(--ups-table-header-bg);
      font-weight: 700;
      text-align: center;
      border: 1px solid var(--ups-black);
      padding: 7pt;
    }

    table.ups-table td {
      border: 1px solid var(--ups-black);
      padding: 7pt;
      vertical-align: top;
    }

    /* ============================================================
       PRINT STYLES
       ============================================================ */
    @media print {
      body { background: none; }
      .document { box-shadow: none; margin: 0; max-width: none; }
      .page { min-height: auto; page-break-after: always; }
      .page:last-child { page-break-after: auto; }
    }

    @page {
      size: letter;
      margin: 1in;
    }
  </style>
</head>
<body>
  <div class="document">
    <!-- COVER PAGE -->
    <div class="page">
      <div class="header">
        <div class="gradient-bar"></div>
        <div class="logo-area">
          <img src="{{LOGO_PATH_OR_BASE64}}" alt="Upstage">
        </div>
      </div>
      <div class="cover-page">
        <h1 class="cover-title">{{DOCUMENT_TITLE}}</h1>
        <div class="cover-spacer"></div>
        <div class="cover-date">{{DATE}}</div>
        <div class="cover-seal">업스테이지 직인 생략</div>
      </div>
    </div>

    <!-- BODY PAGES -->
    <div class="page">
      <div class="header">
        <div class="gradient-bar"></div>
        <div class="logo-area">
          <img src="{{LOGO_PATH_OR_BASE64}}" alt="Upstage">
        </div>
      </div>

      <!-- Example section structure -->
      <h3 class="section-header">1. 제안 개요</h3>
      <h4 class="subsection-header">1.1 배경 및 목적</h4>
      <p class="body-text">본문 내용을 여기에 작성합니다.</p>

      <h4 class="subsection-header">1.2 제안 요청</h4>
      <p class="body-text">제안 관련 내용을 작성합니다.</p>

      <h3 class="section-header">2. 요구 사항</h3>
      <h4 class="subsection-header">2.1 구매 일반 사항</h4>
      <ul class="ups-list">
        <li>항목 1</li>
        <li>항목 2</li>
      </ul>

      <table class="ups-table">
        <thead>
          <tr>
            <th>No.</th>
            <th>구분</th>
            <th>요구사항</th>
            <th>수용 여부</th>
            <th>상세 설명</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>1</td>
            <td>GPU</td>
            <td>NVIDIA B200</td>
            <td>Pass</td>
            <td></td>
          </tr>
        </tbody>
      </table>

      <div class="footer">1</div>
    </div>
  </div>
</body>
</html>
```

## Embedding the Logo as Base64

For a fully self-contained HTML file, convert the logo to base64:

```javascript
const fs = require('fs');
const logo = fs.readFileSync('<skill-dir>/assets/upstage-logo.png');
const base64 = `data:image/png;base64,${logo.toString('base64')}`;
// Use as: <img src="${base64}" alt="Upstage">
```

Or in Python:
```python
import base64
with open('<skill-dir>/assets/upstage-logo.png', 'rb') as f:
    b64 = base64.b64encode(f.read()).decode()
logo_src = f'data:image/png;base64,{b64}'
```

## Template Variables

Replace these placeholders when generating:

| Placeholder | Description |
|-------------|-------------|
| `{{DOCUMENT_TITLE}}` | Document title text |
| `{{DATE}}` | Date string (e.g., "Mar. 2026") |
| `{{LOGO_PATH_OR_BASE64}}` | Path to logo image or base64 data URI |

## CSS Variable Customization

All colors and fonts are controlled via CSS variables in `:root`. This makes it easy to adjust if the brand evolves while maintaining the same structure.
