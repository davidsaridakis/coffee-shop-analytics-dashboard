# MCP workflow gotchas

- pbir_add_visual's binding validator can have a stale cache and wrongly
  report a real, saved measure as "not found". Before assuming a real
  error: cross-check with `pbir_model_usage` (reads fresh from disk).
  If that confirms the field exists, it's safe to retry with
  `strictBindings: false`.
- If a modeling-mcp write hangs with no response, check for a pending
  approval popup in Claude Desktop before retrying.
- Both MCP servers drop their connection on app restart — always
  reconnect (list local instances → connect) before the first tool
  call of a new session.
  

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