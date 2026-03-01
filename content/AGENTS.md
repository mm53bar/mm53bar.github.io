# AGENTS.md

Instructions for AI agents (OpenClaw and others) working with this Obsidian vault.

## Vault Overview

- Owner: Mike
- Purpose: Personal knowledge management using Andy Matuschak's evergreen notes approach
- Public website: Built from notes with `publish: true` using Quartz + GitHub Pages

## Directories

| Directory | Purpose | Process? |
|-----------|---------|----------|
| `Clippings/` | Web clipper inbox — raw saved articles | Yes — extract claims, propose evergreen notes |
| Root `*.md` | Personal notes of all kinds + evergreen notes | Yes — tag untagged notes, propose evergreens |
| `Projects/` | Active personal projects (prefixed with `+`) | No |
| `Vertical City/` | Work notes for current employer | No |
| `_ARCHIVE/` | Daily notes, weekly reviews, old job notes | No |
| `_ATTACHMENTS/` | Images and PDFs | No |
| `_TEMPLATES/` | Obsidian templates | No |

## Tag Vocabulary

Always use tags from this list. Do not invent new tags. If a new category is genuinely needed, propose it here first.

| Tag | Use for |
|-----|---------|
| `evergreen` | Atomic concept notes suitable for publishing |
| `clippings` | Web clippings (applied automatically by conversion script) |
| `homelab` | Self-hosted services, networking, Docker, Proxmox, Synology, Raspberry Pi |
| `gear` | Products, purchases, appliances, vehicles, specs, research |
| `dev` | Software development patterns, tools, Rails, coding concepts |
| `management` | Leadership, 1:1s, team strategy, engineering management |
| `camping` | Outdoor trips, trails, camping gear, teardrop trailer |
| `health` | Medical notes, fitness, medications |
| `people` | Notes about specific individuals |
| `career` | Job applications, interviews, previous employers, career planning |
| `garden` | Plants, landscaping, aquarium, yard projects |
| `media` | Games, books, movies, TV, music |
| `personal` | Life admin, household, miscellaneous personal notes |
| `meta` | Notes about this note-taking system |

## Frontmatter Conventions

```yaml
---
title: Optional explicit title
sources: "[[source note or clipping]]"     # evergreen notes only; can be a list
tags: [evergreen, dev]                      # from vocabulary above
publish: true                               # only on evergreen notes ready for website
---
```

- `sources:` — links an evergreen note back to its source clipping(s). Can be a single wikilink string or a YAML list.
- `publish: true` — opt-in for website publication. Never add to personal notes, people notes, career notes, or anything private.
- `tags:` — use YAML flow style `[tag1, tag2]` for consistency.

## Recurring Cleanup Tasks

When asked to run a cleanup pass, do the following in order:

### 1. Tag untagged notes
- Find root-level notes with no `tags:` in frontmatter (or no frontmatter at all)
- Propose tags from the vocabulary based on content and title
- Apply tags by adding or updating frontmatter
- Skip: `README.md`, `AGENTS.md`, files in excluded directories

### 2. Process clippings
- Scan `Clippings/` for unprocessed articles (no corresponding evergreen note linking back to them)
- Extract 1-3 atomic claims from each clipping
- For each claim: check whether an existing evergreen note covers it
  - If yes: propose adding a `reference:` link to that clipping
  - If no: propose a new evergreen note with a concept-oriented title

### 3. Propose evergreen notes
- When proposing a new evergreen note:
  - Title should be a complete, searchable claim (not a vague topic)
  - Include `reference:` linking to source clipping(s)
  - Include `tags: [evergreen]`
  - Include `publish: true` only if the concept is well-developed and non-personal
  - Keep content to 3-4 paragraphs maximum
  - Link to related existing notes using wikilinks `[[note title]]`

### 4. Flag duplicates
- Identify notes that appear to cover the same concept
- Report them for human review — do not merge automatically

## What Not To Do

- Do not reorganize notes into new subdirectories
- Do not delete notes — flag for human review instead
- Do not add `publish: true` to: people notes, personal life admin, career/job notes, health notes, homelab how-tos, gear research
- Do not invent tags outside the vocabulary
- Do not modify notes in `_ARCHIVE/`, `Projects/`, or `Vertical City/`
- Do not modify clippings already in `Clippings/` — treat them as read-only source material
