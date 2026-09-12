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