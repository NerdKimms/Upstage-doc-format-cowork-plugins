# DOCX Template for Upstage Format

Use `docx-js` (npm package `docx`) to generate DOCX files matching Upstage's corporate format.

## Complete Template Code

```javascript
const fs = require("fs");
const { Document, Packer, Paragraph, TextRun, Table, TableRow, TableCell,
        ImageRun, Header, Footer, AlignmentType, LevelFormat,
        HeadingLevel, BorderStyle, WidthType, ShadingType,
        PageNumber, PageBreak, TabStopType, TabStopPosition } = require("docx");

// ============================================================
// DESIGN TOKENS
// ============================================================
const COLORS = {
  black: "000000",
  darkGrey: "434343",    // Heading 3
  midGrey: "666666",     // Heading 4/5/6
  gradientStart: "BFBFBF",
  gradientEnd: "D8C6F8",
  tableHeaderBg: "F3F3F3",
};

const FONT = {
  ascii: "Ups sans",
  eastAsia: "Ups sans",
  hAnsi: "Ups sans",
  cs: "Gothic A1",
};

const FONT_ALL = { font: "Ups sans" };

// ============================================================
// HELPER: Create styled run
// ============================================================
function upsRun(text, opts = {}) {
  return new TextRun({
    text,
    font: FONT.ascii,
    bold: opts.bold || false,
    italics: opts.italics || false,
    size: opts.size || 24, // 12pt default
    color: opts.color || COLORS.black,
    underline: opts.underline ? { type: "single" } : undefined,
  });
}

// ============================================================
// HELPER: Create table with Upstage styling
// ============================================================
function upsTable(headers, rows, columnWidths) {
  const totalWidth = columnWidths.reduce((a, b) => a + b, 0);
  const border = { style: BorderStyle.SINGLE, size: 4, color: COLORS.black };
  const borders = { top: border, bottom: border, left: border, right: border };
  const cellMargins = { top: 100, bottom: 100, left: 100, right: 100 };

  const headerRow = new TableRow({
    children: headers.map((text, i) =>
      new TableCell({
        width: { size: columnWidths[i], type: WidthType.DXA },
        borders,
        shading: { fill: COLORS.tableHeaderBg, type: ShadingType.CLEAR },
        margins: cellMargins,
        children: [new Paragraph({
          alignment: AlignmentType.CENTER,
          children: [upsRun(text, { bold: true })],
        })],
      })
    ),
  });

  const dataRows = rows.map(row =>
    new TableRow({
      children: row.map((text, i) =>
        new TableCell({
          width: { size: columnWidths[i], type: WidthType.DXA },
          borders,
          margins: cellMargins,
          children: [new Paragraph({
            children: [upsRun(typeof text === "string" ? text : String(text))],
          })],
        })
      ),
    })
  );

  return new Table({
    width: { size: totalWidth, type: WidthType.DXA },
    columnWidths,
    rows: [headerRow, ...dataRows],
  });
}

// ============================================================
// BUILD DOCUMENT
// ============================================================
function createUpstageDoc({ title, date, sections, logoPath }) {
  // Load logo
  const logoData = fs.readFileSync(logoPath);

  const doc = new Document({
    styles: {
      default: {
        document: {
          run: { font: FONT.ascii, size: 24 },
        },
      },
      paragraphStyles: [
        {
          id: "Heading1", name: "Heading 1",
          basedOn: "Normal", next: "Normal", quickFormat: true,
          run: { size: 40, bold: true, font: FONT.ascii },
          paragraph: { spacing: { before: 400, after: 120 }, outlineLevel: 0 },
        },
        {
          id: "Heading2", name: "Heading 2",
          basedOn: "Normal", next: "Normal", quickFormat: true,
          run: { size: 32, bold: true, font: FONT.ascii },
          paragraph: { spacing: { before: 360, after: 120 }, outlineLevel: 1 },
        },
        {
          id: "Heading3", name: "Heading 3",
          basedOn: "Normal", next: "Normal", quickFormat: true,
          run: { size: 28, bold: true, font: FONT.ascii, color: COLORS.darkGrey },
          paragraph: { spacing: { before: 320, after: 80 }, outlineLevel: 2 },
        },
        {
          id: "Heading4", name: "Heading 4",
          basedOn: "Normal", next: "Normal", quickFormat: true,
          run: { size: 24, font: FONT.ascii, color: COLORS.midGrey },
          paragraph: { spacing: { before: 280, after: 80 }, outlineLevel: 3 },
        },
      ],
    },
    numbering: {
      config: [
        {
          reference: "upsBullets",
          levels: [{
            level: 0, format: LevelFormat.BULLET, text: "\u2022",
            alignment: AlignmentType.LEFT,
            style: { paragraph: { indent: { left: 720, hanging: 360 } } },
          }, {
            level: 1, format: LevelFormat.BULLET, text: "\u25CB",
            alignment: AlignmentType.LEFT,
            style: { paragraph: { indent: { left: 1440, hanging: 360 } } },
          }],
        },
        {
          reference: "upsNumbers",
          levels: [{
            level: 0, format: LevelFormat.DECIMAL, text: "%1.",
            alignment: AlignmentType.LEFT,
            style: { paragraph: { indent: { left: 720, hanging: 360 } } },
          }, {
            level: 1, format: LevelFormat.LOWER_LETTER, text: "%2)",
            alignment: AlignmentType.LEFT,
            style: { paragraph: { indent: { left: 1440, hanging: 360 } } },
          }],
        },
      ],
    },
    sections: [{
      properties: {
        page: {
          size: { width: 12240, height: 15840 },
          margin: { top: 1440, right: 1440, bottom: 1440, left: 1440,
                    header: 720, footer: 720 },
        },
      },
      headers: {
        default: new Header({
          children: [
            // Logo in header
            new Paragraph({
              children: [
                new ImageRun({
                  type: "png",
                  data: logoData,
                  transformation: { width: 100, height: 33 },
                  floating: {
                    horizontalPosition: {
                      relative: "page",
                      offset: 914400,
                    },
                    verticalPosition: {
                      relative: "page",
                      offset: 352425,
                    },
                    wrap: { type: "none" },
                  },
                  altText: { title: "Upstage Logo", description: "Upstage company logo", name: "upstage-logo" },
                }),
              ],
            }),
          ],
        }),
      },
      footers: {
        default: new Footer({
          children: [
            new Paragraph({
              alignment: AlignmentType.RIGHT,
              children: [
                new TextRun({ children: [PageNumber.CURRENT], font: FONT.ascii }),
              ],
            }),
          ],
        }),
      },
      children: [
        // ---- COVER PAGE ----
        new Paragraph({ children: [] }), // spacer
        new Paragraph({ children: [] }),
        // Title
        new Paragraph({
          heading: HeadingLevel.TITLE,
          spacing: { line: 360, lineRule: "auto" },
          children: [upsRun(title, { bold: true, size: 58 })],
        }),
        // Spacers
        ...Array(6).fill(null).map(() =>
          new Paragraph({ spacing: { line: 360 }, children: [upsRun("")] })
        ),
        // Date
        new Paragraph({
          spacing: { line: 360 },
          children: [upsRun(date)],
        }),
        new Paragraph({ children: [] }),
        new Paragraph({ children: [] }),
        // Company seal
        new Paragraph({
          spacing: { line: 360 },
          children: [upsRun("업스테이지 직인 생략")],
        }),
        // Page break
        new Paragraph({ children: [new PageBreak()] }),

        // ---- BODY SECTIONS ----
        // Sections are added dynamically from the `sections` parameter
        ...buildSections(sections),
      ],
    }],
  });

  return doc;
}

// ============================================================
// BUILD SECTIONS
// ============================================================
function buildSections(sections) {
  const children = [];

  sections.forEach((section) => {
    // Section header (H3 style, bold)
    children.push(new Paragraph({
      heading: HeadingLevel.HEADING_3,
      spacing: { line: 276, lineRule: "auto" },
      children: [upsRun(section.title, { bold: true, size: 28, color: COLORS.darkGrey })],
    }));

    if (section.subsections) {
      section.subsections.forEach((sub) => {
        // Subsection header (H4)
        children.push(new Paragraph({
          heading: HeadingLevel.HEADING_4,
          children: [upsRun(sub.title, { color: COLORS.midGrey })],
        }));

        // Body paragraphs
        if (sub.paragraphs) {
          sub.paragraphs.forEach((text) => {
            children.push(new Paragraph({
              spacing: { before: 240, after: 240 },
              indent: { left: 270 },
              children: [upsRun(text)],
            }));
          });
        }

        // Bullet list
        if (sub.bullets) {
          sub.bullets.forEach((item, idx) => {
            children.push(new Paragraph({
              numbering: { reference: "upsBullets", level: 0 },
              spacing: idx === 0 ? { before: 240 } : {},
              children: [upsRun(item)],
            }));
          });
        }

        // Table
        if (sub.table) {
          children.push(upsTable(
            sub.table.headers,
            sub.table.rows,
            sub.table.columnWidths || sub.table.headers.map(() =>
              Math.floor(9360 / sub.table.headers.length)
            ),
          ));
        }
      });
    }
  });

  return children;
}

// ============================================================
// EXPORT & SAVE
// ============================================================
async function saveUpstageDoc(doc, outputPath) {
  const buffer = await Packer.toBuffer(doc);
  fs.writeFileSync(outputPath, buffer);
  console.log(`Document saved to ${outputPath}`);
}

module.exports = { createUpstageDoc, saveUpstageDoc, upsRun, upsTable };
```

## Usage Example

```javascript
const { createUpstageDoc, saveUpstageDoc } = require("./upstage-docx-template");

const doc = createUpstageDoc({
  title: "Upstage NVIDIA B200 GPU 기반 클러스터 구성 제안 요청서",
  date: "Jan. 2026",
  logoPath: "<skill-dir>/assets/upstage-logo.png",
  sections: [
    {
      title: "1. 제안 개요",
      subsections: [
        {
          title: "1.1 배경 및 목적",
          paragraphs: [
            "Upstage는 대규모 언어모델 및 멀티모달 모델을 자체 개발·운영하는 AI 전문 기업으로..."
          ],
        },
        {
          title: "1.2 제안 요청",
          paragraphs: ["귀사의 기술적·상업적 제안서를 본 RFP의 작성 지침에 따라 제출해 주시기 바랍니다."],
        },
      ],
    },
    {
      title: "2. 요구 사항",
      subsections: [
        {
          title: "2.1 구매 일반 사항",
          bullets: [
            "GPU 사양: NVIDIA B200 GPU만 제안 가능",
            "규모: 80노드 ~ 160노드",
          ],
          table: {
            headers: ["No.", "구분", "요구사항", "수용 여부", "상세 설명"],
            columnWidths: [555, 1215, 3885, 2250, 1455],
            rows: [
              ["1", "GPU", "NVIDIA B200", "Pass", ""],
            ],
          },
        },
      ],
    },
  ],
});

saveUpstageDoc(doc, "output.docx");
```

## Notes on the Gradient Header Bar

The original document has a gradient bar as a WordprocessingShape in the header. `docx-js` doesn't natively support gradient-filled shapes. Two approaches:

### Approach A: Skip the gradient bar in DOCX
The logo alone provides sufficient branding. The gradient bar is more impactful in HTML output.

### Approach B: Use a colored paragraph border (approximation)
Add a paragraph with a bottom border in purple as a visual separator:
```javascript
new Paragraph({
  border: { bottom: { style: BorderStyle.SINGLE, size: 12, color: "D8C6F8", space: 1 } },
  children: [],
})
```

### Approach C: Post-process the DOCX XML
After generating with docx-js, unpack the DOCX and manually inject the gradient shape XML into the header. This is the most faithful approach but requires XML manipulation. The gradient shape XML is:

```xml
<wps:wsp>
  <wps:cNvSpPr/>
  <wps:spPr>
    <a:xfrm>
      <a:off x="0" y="0"/>
      <a:ext cx="7821000" cy="223200"/>
    </a:xfrm>
    <a:prstGeom prst="rect"><a:avLst/></a:prstGeom>
    <a:gradFill>
      <a:gsLst>
        <a:gs pos="0"><a:srgbClr val="BFBFBF"/></a:gs>
        <a:gs pos="100000"><a:srgbClr val="D8C6F8"/></a:gs>
      </a:gsLst>
      <a:lin ang="10800025" scaled="0"/>
    </a:gradFill>
    <a:ln><a:noFill/></a:ln>
  </wps:spPr>
</wps:wsp>
```
