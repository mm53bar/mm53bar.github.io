---
tags:
  - meta
  - evergreen
sources:
  - "[[Evergreen notes should be concept-oriented]]"
publish: true
similar:
  - README (0.80)
  - Evergreen notes should be concept-oriented (0.80)
  - Evergreen notes should fit on an index card (0.80)
  - Note titles should match how you'll search for them (0.80)
  - tags (0.80)
compiled: 2026-04-06
---

Atomic notes factored by concept (not by source or project) can connect across unexpected domains, revealing insights invisible in context-specific notes.

When you write "deleted_at columns create query complexity" instead of "soft deletion problems," you create space for the note to connect beyond soft deletion. It might link to:
- Rails default scopes hiding complexity
- GraphQL N+1 queries from implicit filters
- Security issues from forgotten access control checks

These connections wouldn't emerge from a note titled "Problems with soft deletion" because that title locks the concept into one domain.

The key is recognizing when a concept is actually a specific instance of a broader pattern. "deleted_at creates query complexity" is really about "implicit filters that must be remembered everywhere." That broader framing enables cross-domain insight.

**Practice**: When writing atomic notes from source material, ask "What's the underlying concept here that might appear in other contexts?" Extract that concept, not just the surface-level topic.

**Tradeoff**: This makes note-taking harder—you must think abstractly while reading. But [[Evergreen notes should be concept-oriented|the harder thinking is the point]]—it forces deeper understanding.

**Related:** This is why [[Synthesis notes connect atomic notes into actionable strategies|synthesis notes]] exist—they keep the practical, searchable context while atomic notes explore conceptual connections.
