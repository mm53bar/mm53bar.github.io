---
tags:
  - meta
  - evergreen
sources:
  - "[[Clippings/Evergreen notes]]"
  - "[[Evergreen notes should be concept-oriented]]"
publish: true
similar:
  - Evergreen notes should fit on an index card (0.81)
  - Atomic notes can transcend their original context (0.80)
  - Synthesis notes connect atomic notes into actionable strategies (0.80)
  - Evergreen notes should be concept-oriented (0.80)
  - README (0.79)
compiled: 2026-04-06
---

Note titles should balance concept-orientation with practical discoverability—you need to find them when making decisions.

Pure concept-orientation can hurt discoverability. If you title notes "Archive tables separate deleted data" and "PostgreSQL triggers automate archival," you won't find them when searching "soft delete"—the term you'll actually use when facing the problem.

The solution: [[Synthesis notes connect atomic notes into actionable strategies|synthesis notes]] use searchable decision-language titles ("Soft deletes should use archive tables with triggers"), while atomic notes use concept-language titles ("deleted_at columns create query complexity").

This creates two paths to knowledge:
1. **Decision path**: Search "soft delete" → find synthesis note → get strategy
2. **Concept path**: Follow links to atomic notes → discover cross-domain connections

Example: "deleted_at columns create query complexity" might link to a future note about Rails default scopes creating similar problems—a connection you wouldn't see if everything was titled with "soft delete."

**Tradeoff**: You need both types of notes. Pure concept-orientation optimizes for serendipitous discovery but hurts practical retrieval. Pure searchability makes notes action-oriented but limits their reusability across contexts.

**Related:** [[Atomic notes can transcend their original context]] - concept-oriented titles enable this.
