# Report / visual conventions

## Confirmed house style (observed from existing dashboard pages)

### Page layout
- Header: light gray band containing a bold title, with a smaller,
  lighter-weight descriptive subtitle directly below it.
- KPI callouts: label above a large bold number, no box/border —
  separated by a thin vertical rule between adjacent KPIs.
- Every page includes a "What the Data Tells Us" side panel: light
  gray background, containing one or more bullet points, each led by
  a bold "Insight:" or "Business implication:" label.


### Layout pattern: inverted pyramid
Each page follows a broad-to-narrow structure, top to bottom:

1. **Header (broadest):** page title + one-sentence context/purpose —
   what question this page answers.
2. **KPI row (headline numbers):** the 2-4 most important summary
   metrics for this page, given first, before any chart detail.
3. **Main visual(s) (the detail):** the chart(s) that support and
   explain the KPI row above them.
4. **Insight panel (narrowest — the "so what"):** "What the Data
   Tells Us" panel with the specific interpretation and business
   implication drawn from the visual(s) on this page.

New pages should follow this same top-to-bottom narrowing, rather
than leading with a chart and adding numbers/insights as an
afterthought.


### Color palette
- Primary two-way comparisons (e.g. weekday vs weekend, morning vs
  afternoon, revenue share vs volume share) use a light-blue /
  dark-navy pair.
- A third category (when unavoidable) adds an orange/amber accent —
  used sparingly, not as a default third color.
- Multi-category trend lines (4+ series) use a wider distinct color
  set — this is the one exception to the two-tone rule, used only
  when comparing many categories on one line chart.
- Exact hex values have not been confirmed from a theme file — ask
  before assuming precise colors; visually approximate as a medium
  sky-blue and a dark navy blue.

### Chart type defaults
- Clustered column chart is the default choice.
- Horizontal bar chart: used specifically for day-of-week ranking.
- Multi-series line chart: used specifically for hourly trends across
  several product categories.
- Don't introduce a new chart type (pie, donut, gauge, etc.) without
  checking it fits this existing style first.

## Before applying a color scheme or layout style
For NEW pages, default to the confirmed style above rather than
inventing a new one, unless told otherwise. The TEST_MCP and
TEST_VISUAL pages used one-off schemes for testing purposes only —
don't treat those as the house style.