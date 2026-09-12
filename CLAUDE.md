# Coffee Shop Analytics Dashboard

## Project overview
Power BI dashboard built from a single Kaggle CSV (raw data staged in
`public stg_cafe_transactions`), modeled into a star schema
(fact_transactions, dim_products, dim_stores). Built/maintained with
Claude via two MCP servers running side by side.

## MCP servers in use
- `powerbi-modeling-mcp` — semantic model (tables, measures, DAX).
  Connects live to the open Power BI Desktop instance.
- `powerbi-report-mcp` — report layer (pages, visuals). Reads/writes
  the .Report/.SemanticModel folders on disk, NOT the live connection.

## Hard rules
- NEVER modify or delete an existing measure without explicit confirmation first.
- Always confirm a plan before multi-file changes (use Plan Mode).
- After any semantic-model change, the user must save in Power BI
  Desktop (Ctrl+S) before report-mcp tools can see it — it reads from
  disk, not the live session.

See @.claude/rules/semantic-model.md and @.claude/rules/report-visuals.md
for detailed conventions.