# CONTEXT

## Project Goal
Create interview-ready Mermaid diagrams that explain movement across the income statement, cash flow statement, and balance sheet for core finance interview topics.

## Current Phase
Added a standalone browser HTML viewer for the finance interview diagram pack and validated that all Mermaid diagrams render in-browser.

## Implemented Features
- Added a standalone diagram pack at `three-statement-interview-diagrams.md`.
- Added a browser-viewable export at `three-statement-interview-diagrams.html` with a wider study layout and section navigation.
- Covered topics A-H with a short explanation, one Mermaid flowchart, and a compact interview script per topic.
- Added a dedicated scope section explaining what typically counts inside operating NWC and CapEx in interview settings.
- Added explicit definitions for accounts receivable and accounts payable in the scope notes and working-capital section.
- Added explicit one-line definitions for prepaids, accrued expenses, and deferred revenue.
- Applied consistent sign conventions for working capital sources and uses of cash.
- Added color-coded Mermaid node styling by statement type and cash impact.
- Added a vertical three-statement reference diagram to make the statement structure easier to scan visually.
- Increased Mermaid font size and spacing across the file so diagrams render larger in Markdown preview.
- Simplified the overview diagram cross-links so it stays vertical instead of spreading wide.
- Removed HTML line breaks from Mermaid labels and normalized node labels into quoted form for broader renderer compatibility.
- Expanded Topics A, B, C, and E with more explicit CapEx and operating NWC definitions and interview traps.
- Verified all 10 Mermaid blocks compile by rendering them through Mermaid CLI in `/tmp/mermaid-check`.
- Validated the HTML export in a real browser and confirmed all 10 Mermaid blocks render successfully.
- Added lean project-memory files for continuity in this workspace.

## Constraints
- Diagrams must use valid Mermaid flowchart syntax and render in Markdown.
- Explanations must stay interview-oriented, technically correct, and easy to say out loud.
- Working capital examples must show both up and down cases for each required line item.

## Decisions Log
- 2026-03-09T17:47:54Z: Chose a single Markdown deliverable instead of scattering content across multiple files.
- 2026-03-09T17:47:54Z: Used one main Mermaid diagram per topic with short labels and statement tags inside nodes.
- 2026-03-09T17:47:54Z: Included both the EBITDA bridge and the equivalent net income bridge for levered free cash flow.
- 2026-03-09T18:44:12Z: Added a visual legend and statement-based color system to improve scanability.
- 2026-03-09T18:44:12Z: Added a vertical three-statement reference map so the statements read more like stacked financial statements.
- 2026-03-09T18:47:15Z: Increased Mermaid font size and spacing to improve readability in the preview pane.
- 2026-03-09T18:47:15Z: Rebuilt the overview diagram as a true top-to-bottom flow to avoid the landscape layout.
- 2026-03-09T18:55:54Z: Replaced Mermaid HTML line breaks with plain text and quoted node labels to eliminate parser failures.
- 2026-03-09T18:55:54Z: Verified the full file by rendering all Mermaid blocks with Mermaid CLI rather than relying on visual inspection.
- 2026-03-09T18:58:34Z: Added a dedicated CapEx and operating NWC scope diagram so the bridge assumptions are explicit before the topic sections.
- 2026-03-09T18:58:34Z: Expanded Topics A, B, C, and E to spell out what CapEx and operating NWC usually include and exclude.
- 2026-03-09T19:05:56Z: Added explicit AR and AP definitions so the working-capital abbreviations are self-contained for study use.
- 2026-03-09T19:10:56Z: Added matching plain-English definitions for prepaids, accrued expenses, and deferred revenue.
- 2026-03-11T22:42:52Z: Added a standalone HTML viewer so the diagram pack can be reviewed in a browser instead of Markdown preview.
- 2026-03-11T22:42:52Z: Kept the ESM Mermaid loader because it rendered all 10 diagrams cleanly in browser validation, while the non-module fallback regressed the overview diagram.

## Open Risks
- Some firms define levered free cash flow slightly differently around mandatory debt amortization; the file notes the interview convention explicitly.
- Companies and modeling tests may define operating NWC and CapEx differently, so the file now teaches the usual interview convention but still requires scope confirmation in edge cases.

## Next Immediate Task
Let the user review the HTML export in a browser; if any section still feels cramped, split the densest topics into separate zoomed-in HTML pages or add print styling.

## Last Updated
2026-03-11T22:42:52Z
