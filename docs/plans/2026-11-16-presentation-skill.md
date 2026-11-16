# Plan: Presentation-builder skill + repo init
Status: Executing (wave 1)

## Goal / Done when / Non-goals
Goal: a project-local skill that interviews the user (duration, template, topic, details, context) and emits one self-contained HTML/CSS presentation; plus CLAUDE.md for this repo and a DESIGN.md derived from the user's prior deck.
Source template: /Users/mehedihasan/dev/questionpro/pipeline_setup/presentation/pipeline-presentation.html (39 KB, single file).

## Open questions
- [x] Skill location / name → `.claude/skills/create-presentation/` (project skill)
- [x] Output location → `presentations/<slug>/index.html`; CWD fallback when run outside this repo
- Scout facts: 26 slides, `.slide`/.active, inline nav JS (←→ Space Home End), Fira Sans via Google Fonts @import (only external dep), oklch blue accent, components: vs-grid, steps-list, dtable+badge, hook-block (code; rename), pipeline, sum-grid, demo-badge, divider. Chrome = lines 1-227 + 711-746; content 229-709. No speaker notes, no responsive, no touch.
- [x] Template mechanism → `templates/default/template.html` skeleton (chrome + one sample slide per component, content stripped) + DESIGN.md; new templates = new folders
- [x] Pacing → user picks slide count; duration only suggests a count and drives pacing notes
- [x] Questions: topic, audience/context, duration, slide count, template, details/source material, demo segments
- [x] Extras (all): speaker notes (N toggle), demo cues, touch/swipe + responsive, print/PDF
- Skill-writing refs: ~/.claude/skills/writing-for-agents/SKILL.md, ~/.claude/plugins/marketplaces/claude-plugins-official/plugins/skill-creator/skills/skill-creator/SKILL.md, ~/.claude/plugins/cache/claude-plugins-official/superpowers/7.0.2/skills/writing-skills/SKILL.md

## Rough split (pre-grill)
| # | Task | A | B | R | Tier |
|---|---|---|---|---|---|
| 0 | Scout template structure | 0 | 0 | 0 | haiku |
| 1 | DESIGN.md + default template asset | 1 | 1 | 1 | sonnet |
| 2 | SKILL.md + references | 2 | 1 | 1 | sonnet |
| 3 | CLAUDE.md (/init) | 0 | 0 | 0 | haiku |

## Contracts
MAP: none
Files:
- `.claude/skills/create-presentation/SKILL.md`
- `.claude/skills/create-presentation/templates/default/template.html`
- `.claude/skills/create-presentation/templates/default/DESIGN.md` (travels with the template; CLAUDE.md links it)
- `CLAUDE.md` (repo root)
Template conventions:
- `<title>{{TITLE}}</title>`; slides are `<div class="slide …">` inside `<div class="slides">`, between `<!-- SLIDES:START -->` and `<!-- SLIDES:END -->`; each sample slide preceded by `<!-- SAMPLE: <type> -->`.
- Speaker notes: `<aside class="notes">…</aside>` as last child of a slide; hidden by default; `N` toggles a notes panel for the active slide.
- Nav: ←/→/Space, Home/End, N, touch swipe; prev/next buttons; progress bar; counter computed from DOM slide count.
- Print: `@media print` → every slide visible, one per page, chrome + notes hidden, animations off.
- Responsive: fluid type/padding (clamp), grids collapse under ~900px.
- Component classes (generic renames of source): `title-slide`, `center`, `divider`(+`.sub`), `kicker`(+`.demo`), `vs-grid/vs-card(.hi)/vs-card-label/vs-card-title/vs-attr`, `steps-list/step-row(.hi)/step-num(.demo)/step-title/step-desc`, `dtable(.acc)/badge/badge-same/badge-diff`, `code-block/code-head/code-lang/code-body` + `tok-warn/tok-ok/tok-dim`, inline `code`, `flow/flow-step(.on)/flow-badge/flow-arr/flow-step-name`, `card-grid/card/card-slash/card-name/card-sub`, `demo-badge`.
Skill flow (user edit, 2026-11-16): interview → outline preview (per-slide content + narrative flow + timing) → engagement/best-practice suggestions as numbered proposals → WAIT for user to accept/reject each → build HTML → launch 2 independent parallel agents: (a) content audit (opus): report + suggested fixes; (b) HTML/CSS/JS check (sonnet): report. Fixes from reports applied only after user confirms.
Transcript (user edit): interview asks "want a spoken transcript?"; if yes (or user asks any time) write `presentations/<slug>/transcript.md` beside index.html — per-slide `## n · Title` + spoken script + timing, consistent with speaker notes; content-audit agent also reviews it.
Model override: user asked for opus where warranted (1.2, 2.2, content-audit agent).
Output: `presentations/<slug>/index.html` in this repo; `./<slug>/index.html` elsewhere.

## Waves
| # | Task | Tier | Own | Depends |
|---|---|---|---|---|
| 1.1 | Template skeleton + extras | sonnet | templates/default/template.html | — |
| 1.2 | SKILL.md + references/best-practices.md + references/review-agents.md | opus | SKILL.md, references/* | contract |
| 1.3 | CLAUDE.md | haiku | CLAUDE.md | contract |
| 2.1 | DESIGN.md from finished template | haiku | templates/default/DESIGN.md | 1.1 |
| 2.2 | Dry-run: follow SKILL.md with canned answers → sample deck in scratchpad | opus | scratchpad only | 1.1, 1.2 |

## Log
- MAP: none (empty dir, not a git repo)
- Approved 2026-11-16 (opus for 1.2/2.2; transcript.md; outline preview + suggestions gate; 2 post-build review agents)
- git init; local author Mehedi Hasan; baseline porcelain: `?? docs/`
- Wave 1 launched: 1.1 sonnet · 1.2 opus · 1.3 haiku
- 1.3 haiku done: CLAUDE.md 50 lines
