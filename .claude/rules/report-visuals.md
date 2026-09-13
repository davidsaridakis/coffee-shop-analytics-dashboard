# Report / visual conventions

## Two distinct page types — do not conflate them

### 1. Component pages (single-chart tabs)
Examples: "avg hourly transactions", "avg hourly revenue", "revenue by
category", TEST_VISUAL, TEST_PAGE_RECREATE_1.
- Exactly ONE visual per page, no KPI row, no insight panel.
- Do NOT apply the inverted pyramid layout here — that's a dashboard
  page pattern only (see below). A component page is just the chart,
  full canvas, nothing else, unless told otherwise.
- These are working/exploratory tabs, not final deliverables — treat
  requests for a specific test color scheme literally and exactly
  (see Color rules below), since the whole point may be visually
  distinguishing a test from the real dashboard style.

### 2. Dashboard / report pages (assembled, presentation-ready)
Examples: "Report page 1/2/3" (matching assets/bi_report_p*.png).
- Follow the inverted pyramid layout: header band → KPI row → main
  visual(s) → "What the Data Tells Us" insight panel. See structure
  details below.
- Multiple visuals per page, assembled from measures already proven
  on component pages.
- Confirmed: these use Power BI's DEFAULT built-in theme — there is
  no custom theme file and no per-visual color overrides anywhere in
  this project (verified via pbir_get_report_theme and
  pbir_audit_theme_compliance). Do NOT invent or apply a custom
  palette to these pages unless explicitly told to — leave default
  styling untouched by default.

## Color rules (applies to BOTH page types when a specific scheme is requested)

If the user names colors explicitly (e.g. "yellow and blue"), APPLY
them immediately via dataColors / pbir_set_datapoint_colors using a
reasonable hex approximation — never skip or fall back to default
because an exact hex wasn't given. Ambiguity is not a reason to do
nothing; pick the most reasonable interpretation and apply it.

Reasonable defaults for common names, unless the user gives an exact hex:
- Yellow: #FFC300
- Orange: #FF8C00
- Blue (bright/primary): #1F5FCE
- Navy/dark blue: #1B2A6B
- Green: #2E8B57
- Red: #CD191C

## Chart type defaults
- Clustered column chart is the default choice for component pages.
- Horizontal bar chart: used specifically for day-of-week ranking.
- Multi-series line chart: used specifically for hourly trends across
  several product categories.
- Don't introduce a new chart type (pie, donut, gauge, etc.) without
  checking it fits this existing style first.

## Inverted pyramid layout (dashboard pages only)
Each dashboard page follows a broad-to-narrow structure, top to bottom:
1. **Header (broadest):** page title + one-sentence context/purpose.
2. **KPI row:** the 2-4 most important summary metrics for this page.
3. **Main visual(s):** the chart(s) supporting the KPI row above.
4. **Insight panel (narrowest):** "What the Data Tells Us" panel with
   bold "Insight:" / "Business implication:" lead-ins.