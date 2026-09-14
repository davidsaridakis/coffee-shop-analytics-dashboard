# MCP workflow gotchas

These are things that don't behave the way the tool names imply — noted
here so we don't waste time (and tokens) rediscovering them each session.

- **`pbir_add_visual`'s binding validator can be wrong.** It sometimes has
  a stale cache and reports a real, saved measure as "not found" even
  though it exists. Before assuming it's a real error: cross-check with
  `pbir_model_usage`, which always reads fresh from disk. If that confirms
  the field exists, it's safe to retry with `strictBindings: false`.
- **`pbir_add_visual`'s x/y land correctly, but width/height can silently
  reset to a default.** Visuals added in a batch call can come back at
  280×280 regardless of what `width`/`height` were passed — position
  works, size doesn't. Worse, the tool's own `layoutWarnings` response
  echoes that wrong 280×280 back as "actual," so it looks like a harmless
  validator quirk rather than a real problem. Always double-check real
  sizes with `pbir_list_visuals` after adding visuals, and fix any that
  drifted with `pbir_move_visual`.
- **`pbir_list_visuals` with `slim:false` crashes if the page has
  textboxes.** Textboxes have no title, and `slim:false` fails schema
  validation on that null value. Stick with `slim:true` (the default) on
  any page that includes textboxes.
- **If a modeling-mcp write hangs with no response,** check for a pending
  approval popup in Claude Desktop before retrying — it's usually just
  waiting on you, not actually stuck.
- **If a DAX query (`dax_query_operations` `Execute`) hangs or keeps
  getting declined even after approving it, stop retrying.** That's a
  stuck approval-gate, not a query problem — even a trivial one-row query
  fails the exact same way, which rules out query complexity as the
  cause. Fall back to reasoning from the visuals/model directly instead of
  blocking on a live query.
- **Both MCP servers drop their connection on app restart — reconnect
  both before the first tool call of a new session, not just one:**
  - `powerbi-modeling-mcp`: list local instances → connect.
  - `powerbi-report-mcp`: call `pbir_set_report` with the path to
    `coffee_shop_analytics_dashboard.Report` (the project's report
    folder) — it has no memory of the last session's connection either,
    and every report-mcp tool call fails with "No report connected" until
    this is done.

## Mandatory pause between model and report changes
Whenever a task involves BOTH creating/changing a measure (modeling MCP)
AND using it in a visual (report MCP) in the same request:
1. Create/change the measure first.
2. STOP. Explicitly ask the user to save in Power BI Desktop (Ctrl+S)
   and confirm before continuing.
3. Only proceed to building the visual after the user confirms.
Do not attempt to build the visual in the same turn as creating the
measure, even if asked to do both at once — this pause is required
every time, not just the first time.
