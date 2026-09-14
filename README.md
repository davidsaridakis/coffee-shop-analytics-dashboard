# ☕ Operational Analytics for Small Hospitality Businesses

## Can transaction data improve operational decisions traditionally driven by intuition?

### Project Overview

This project started as a business case study using a public Kaggle coffee shop dataset to explore whether transaction data could validate, challenge, or improve the kind of operational decisions hospitality managers often make on instinct in areas like staffing, product focus and daily rhythm.


This second phase takes the finished Power BI dashboard and extends it with **AI-assisted development**, using Claude connected directly to the live project via MCP, to maintain, extend, and rebuild parts of the dashboard, all governed by an explicit rulebook rather than open-ended access.

---

# Why This Phase Exists

This phase asks the question:

**Can an AI agent reliably maintain and extend an existing BI project, the same way a human developer would?**

The goal is not for AI to generate a dashboard from scratch. Instead I went for something I believe to be a bit closer to real BI enhancement. That is, reading an existing model, understanding its conventions, and building within them.

---

# Architecture

Two MCP servers give Claude direct, governed access to the project, one per layer:

| Server | Layer | Purpose |
|---|---|---|
| `powerbi-modeling-mcp` | Semantic model | Tables, relationships, DAX measures — live connection to Power BI Desktop |
| `powerbi-report-mcp` | Report | Pages, visuals, layout, theming — reads/writes the PBIP project files on disk |

**The governance layer.** Claude doesn't operate on open-ended access, it works under an explicit, version-controlled rulebook:

```
CLAUDE.md                    — project brief, hard rules, architecture notes
.claude/
├── settings.json            — explicit permission allow/deny rules
└── rules/
    ├── semantic-model.md    — measure conventions, confirmed relationships
    ├── report-visuals.md    — layout patterns, color rules, canvas budgeting
    └── mcp-workflow.md       — known integration gotchas, required save/pause steps
```

Development happens through **Plan Mode**: Claude proposes a plan — which measures it's reusing, what it's building, what layout — before touching a single file. I review and approve before anything executes.

---

# Workflow

```
Business/design request
        ↓
Plan Mode: propose approach
        ↓
Human review & approval
        ↓
Execute via MCP (model + report)
        ↓
Validate (bindings, layout)
        ↓
Version control (git)
```

---

# Project Status

- ✅ Two MCP servers connected and governed by explicit rules
- ✅ Existing measures reviewed, organized, and safely extended
- ✅ Single-chart and full-page recreation tested via Plan Mode
- ✅ Version-controlled with a clean, reviewable commit history
- 🔄 Flagship dashboard pages — in progress

---

# What I Learned

Good AI collaboration turned out to need the same thing good operational decisions need which are rules grounded in how the business actually works, not assumptions about how it should.

The rulebook wasn't written upfront and left alone. It was a recursive process. Claude was asked for suggested edits to the rulebook after each iteration in order to improve efficiency and reduce the amount of tokens needed to do the work. It got tighter every time a real test exposed a gap — a layout conflict, a missing safety pause, etc. This was an invaluable resource and greatly improved the overall result.
