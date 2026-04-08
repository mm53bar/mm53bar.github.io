---
sources:
  - "[[Clippings/Why are big tech companies so slow?|Why are big tech companies so slow?]]"
publish: true
tags: [evergreen]
similar:
  - Developers spend most of their time figuring out systems (0.79)
  - Role of a product manager at a small startup (0.79)
  - Investopedia (0.79)
  - Technical debt reflects incomplete understanding (0.79)
  - you-need-to-try-these-open-source-ai-projects-right-now (0.79)
compiled: 2026-04-06
---
The real difficulty in large systems isn’t writing new code—it’s discovering all the implicit contracts your feature must honour with existing ones. When Google Docs adds emoji reactions, the effort goes into edge cases: Will this break offline mode’s conflict resolution? Does comment history need to track reaction edits? These aren’t coordination problems but emergent interface negotiations, where every existing feature owns undocumented rules.

This is why [[Stable teams compound institutional knowledge]]. Teams that ship multiple features in a domain develop intuition for these hidden contracts—they know where the landmines are buried. New teams, meanwhile, waste months relearning why the cursor behaves oddly during collaborative undo ([[The hidden cost of institutional amnesia]]).