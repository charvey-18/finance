# HANDOFF

## Snapshot
Workspace now contains both the Markdown study pack and a standalone HTML viewer; the browser export has been validated and all 10 Mermaid diagrams render successfully.

## Latest Prompt Sync
User asked for interview-ready Mermaid diagrams covering three-statement flow topics A-H, starting with EBITDA to levered free cash flow and then continuing through working capital, depreciation, CapEx, debt, interest, and taxes.
Follow-up asked whether these could be created as workflow diagrams in Mermaid; deliverable already exists in the workspace.
Latest follow-up asked for more color coding and a more vertical statement-style visual; the main file was updated accordingly.
Newest follow-up said the overview was still too small and too wide; the file was updated with larger Mermaid settings and a true top-to-bottom overview.
Newest follow-up reported that the EBITDA-to-FCF block was not loading; the Mermaid file was normalized and all diagrams were compile-tested successfully.
Newest follow-up asked for more teaching detail on what CapEx and NWC actually consist of before using the file for study; the file was expanded and revalidated.
Latest follow-up asked for definitions of payables and receivables; those were added directly into the scope notes and working-capital section.
Current follow-up asked for the same treatment for prepaids, accrued expenses, and deferred revenue; those definitions were added.
Newest follow-up asked for an easier browser-viewable format; a standalone HTML export was created and validated in-browser.
Latest follow-up asked how to access the browser viewer on a phone; no file changes were needed, only local network access instructions.

## Active Engineering Notes
- Main deliverable: `three-statement-interview-diagrams.md`
- Browser viewer: `three-statement-interview-diagrams.html`
- Sign conventions are consistent across sections: operating asset up = use, operating liability up = source.
- File now includes a color legend and a vertical reference diagram before the topical sections.
- All Mermaid blocks now include larger init settings for font size and spacing.
- HTML `<br/>` tags were removed from Mermaid labels because they were causing renderer/parser incompatibilities.
- File now includes a dedicated scope section for `operating NWC` and `CapEx`.
- File now explicitly defines `AR` and `AP` in plain English for study use.
- File now explicitly defines `prepaids`, `accrued expenses`, and `deferred revenue` in the same section.
- Topics A, B, C, and E now state what usually sits inside or outside those buckets.
- All 10 Mermaid blocks rendered successfully via Mermaid CLI from `/tmp/mermaid-check/blocks`.
- All 10 Mermaid blocks also rendered successfully in browser validation through the HTML export.
- The HTML viewer uses a Mermaid ESM CDN loader because that variant rendered all diagrams reliably; a non-module fallback was tested and rejected after it regressed the overview diagram.

## Immediate Next Actions
- Run the project-memory validator.
- Point the user to the HTML file path and local browser URL.
- If needed later, split dense topic diagrams into separate zoomed-in views or add print-friendly styling.
