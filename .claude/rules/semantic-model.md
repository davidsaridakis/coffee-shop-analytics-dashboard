# Semantic model conventions

## Table naming
Tables carry a `public` schema prefix inherited from the source
(e.g. `public fact_transactions`, `public dim_products`). Reference
tables with this exact prefix in DAX/tool calls.

## Measures table
All measures live in `_Medidas`, not scattered across data tables.
New measures should go here too, unless told otherwise.

## Display folders (confirmed as of Sept 2026)
- Totals
- Ratios
- Time Averages\Hourly
- Time Averages\Daily
- Segments\Morning

New measures should be placed in one of these if they clearly fit,
otherwise ask before inventing a new folder.

## Hard rule
Never modify, rename, or delete an existing measure's expression
without explicit confirmation first — this applies even to measures
that look redundant or misnamed.

## Open / unconfirmed
- No naming convention has been set for future measures beyond
  matching the existing plain-English style (e.g. "Total Units Sold").
  Ask if unsure rather than assuming a pattern.

  ## Table relationships (confirmed, as of Sept 2026)

The star schema:
- fact_transactions[product_id] → dim_products[product_id] (Many:1, one-direction, active)
- fact_transactions[store_id] → dim_stores[store_id] (Many:1, one-direction, active)
- fact_transactions[transaction_date] → auto date table (Many:1, one-direction, active)

Isolated table:
- stg_cafe_transactions[transaction_date] → its own SEPARATE auto date
  table. This table has NO relationship to fact_transactions,
  dim_products, or dim_stores — it's fully disconnected from the star
  schema, confirming it's raw staging data, not part of the active
  model.

## Hard rule
Do not create a new relationship between stg_cafe_transactions and
the star schema without explicit confirmation — its isolation is
intentional (raw staging vs. transformed model), not an oversight to
"fix".

## Open / unconfirmed
No naming convention has been set for relationships beyond Power BI's
auto-generated GUID names. If creating a new relationship, ask
whether a descriptive name is wanted, or if the default is fine.