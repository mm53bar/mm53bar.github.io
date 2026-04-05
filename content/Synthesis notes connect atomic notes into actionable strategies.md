---
tags:
  - meta
  - evergreen
sources:
  - "[[Clippings/Evergreen notes]]"
publish: true
similar:
  - Note titles should match how you'll search for them (0.81)
  - README (0.80)
  - AGENTS (0.80)
  - Evergreen notes should fit on an index card (0.80)
  - Atomic notes can transcend their original context (0.80)
---

While [[Atomic notes can transcend their original context|atomic notes]] capture individual concepts, synthesis notes combine them into actionable strategies for making decisions.

Synthesis notes answer questions like "How should I handle soft deletes?" or "How should I organize teams?" They're your entry point when you need to apply knowledge, not just explore connections.

A synthesis note:
- States a clear strategy or approach
- Links to atomic notes that explain the reasoning
- Includes just enough practical detail (code snippets, examples) to be actionable
- References source materials in frontmatter

Example: [[Soft deletes should use archive tables with triggers]] links to three atomic notes explaining why `deleted_at` fails, why archive tables work, and how triggers automate it. When making an architectural decision, you search "soft delete" and find the synthesis note—your distilled strategy ready to use.

Atomic notes live at the concept level ([[deleted_at columns create query complexity]]). Synthesis notes live at the decision level ("use archive tables with triggers").

**Related:** Similar to how [[Learning as a Business Strategy]] synthesizes insights from multiple sources into a single actionable principle.
