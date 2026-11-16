# Plan: /update-presentation skill
Status: Complete

## Goal / Done when / Non-goals
Goal: Add a `/update-presentation` skill to the presentation-builder plugin that takes the user's instructions and uses the six existing agents to update an existing deck.
Done when: P/skills/update-presentation/SKILL.md exists; agents updated (backfill, focus, guards); `claude plugin validate plugins/presentation-builder` passes; CLAUDE.md + README document the command.
Non-goals: template chrome refresh, template switching, new decks, undo (git covers it).

## Open questions
- Facts: only deck is presentations/everyday-ai-workflow (index.html, transcript.md, context.md; NO work/ dir — built before the plugin). All 6 agent descriptions say "Invoked only by /create-presentation" → must widen. content-writer modes: outline | slides | fix.
- [x] Deck without work/outline.md → backfill on demand: small edits → design-creator fix on index.html; structural → content-writer rebuilds outline.md from index.html first (user, 2026-11-16)
- [x] Approval gate → only for structural: content-writer revises outline, user approves changed rows, then design-creator rebuilds; small edits apply directly (user, 2026-11-16)
- [x] Routing (default): small = no slide added/removed/reordered, no narrative/timing change → design-creator fix structural:no (+ content-writer fix to sync outline only if outline.md exists); structural → backfill if needed → content-writer outline w/ requested changes → gate → content-writer slides → design-creator fix structural:yes; new sources → knowledge-explorer first; transcript exists + copy changed → transcript-writer fix resync. Reviewers when structural or >3 slides changed, with `focus: slides …`.
- [x] Missing agent capabilities (default): content-writer mode `backfill` (index.html + context.md + transcript.md → outline.md incl. Brief); reviewers accept optional `focus`; all 6 guards name both skills.
- [x] Review → scale with change: small = self-check only; structural/multi-slide = both reviewers focused on changed slides + confirm-before-fix gate (user, 2026-11-16)
- [x] Deck selection (default): arg slug; else list presentations/; one deck → propose it and confirm
- [x] Chrome refresh → non-goal (lock confirmed "go", 2026-11-16)

## Contracts
MAP: none
Baseline `git status --porcelain`: `?? docs/plans/2026-11-16-update-presentation.md`
P = plugins/presentation-builder

- Guard sentence (all 6 agents, replaces the old one): `Invoked only by /create-presentation, /update-presentation or an explicit @-mention; never delegate to it otherwise.`
- content-writer mode `backfill`: inputs index.html (read-only), context.md + transcript.md if present, work/sources.md if present. Writes work/outline.md in the SAME format as outline+slides modes (Brief, arc, `## Outline` table, timing, demo plan, `## Slides` with `### Slide N — <title> (<component>)`, on-slide copy, speaker notes). Describes the deck as it is: no improvements, no invented facts; Brief fields not derivable → `unknown`. Row count = slide count in index.html.
- Reviewers (content-reviewer, design-reviewer): optional input `focus: slides <list>` (e.g. `3, 5-7`). With focus: judge only those slides + their transitions to neighbours (design: plus whole-file checks like slide count/tag balance); findings outside focus only if blocker.
- update-presentation SKILL.md (P/skills/update-presentation/SKILL.md): frontmatter name `update-presentation`, description triggers on change/edit/update/revise an existing deck/presentation/slides. Uses `S` = `${CLAUDE_PLUGIN_ROOT}/skills/create-presentation/` for templates/best-practices (no duplication). Template = the one named in outline.md Brief, else `default`. Flow:
  1 pick deck (arg slug | list presentations/ | single deck → confirm) — GATE
  2 restate instruction + classify: small (no add/remove/reorder, no narrative/timing change) | structural; note new sources. Ambiguous instruction → ask one question — GATE
  3 new sources → knowledge-explorer (haiku) appends/creates work/sources.md
  4 small → design-creator fix (sonnet, structural: no, N = current count, findings = the user's instruction) → if outline.md exists content-writer fix (opus) same wording
  5 structural → no outline.md → content-writer backfill (opus) → content-writer outline with `requested changes` = instruction (opus) → show changed rows (step-3 table format of create) + new N + timing → GATE approve (loop) → content-writer slides (opus) → design-creator fix structural: yes, new N (sonnet)
  6 transcript.md exists and copy/structure changed → transcript-writer fix `resync` (sonnet)
  7 structural or >3 slides changed → content-reviewer (opus) ∥ design-reviewer (sonnet) with `focus: slides …` → merged list → GATE confirm → route fixes exactly as create-presentation step 8
  8 report: changed slides, files, how to view
  Agents table + rules same as create SKILL.md (subagent_type presentation-builder:<name>, explicit model, agents never call agents, ≤10-line replies). ≤100 lines.

## Waves (scores A/B/R)
| # | Task | Tier | Own | Deps | Scores |
|---|------|------|-----|------|--------|
| 1.1 | Write update-presentation SKILL.md per contract | sonnet | P/skills/update-presentation/SKILL.md | — | 2/1/1 |
| 1.2 | Agents: backfill mode, reviewer focus, guard sentence ×6 | sonnet | P/agents/*.md (6) | — | 1/2/1 |
| 2.1 | Docs: CLAUDE.md (layout, Updating a deck, agent invoker line), README usage line | haiku | CLAUDE.md, README.md | 1.1, 1.2 | 0/1/0 |

## Log
- GRILL started; MAP: none
- Lock confirmed ("go"); Baseline: `?? docs/plans/2026-11-16-update-presentation.md`
- PREVIEW approved ("go"), 2026-11-16
- Wave 1 launched: 1.1 (sonnet, general-purpose) ∥ 1.2 (sonnet, general-purpose)
- 1.2 done (6 agents; validate pass; content-writer 64 lines)
- 1.1 done (SKILL.md 80 lines; validate pass)
- Wave-1 verifier (haiku) + reviewer (sonnet) launched
- Wave-1 verifier: OUTSIDE-OWN none; all checks pass (validate notes LICENSE/ICON = pre-existing deferred follow-up)
- Wave-1 reviewer (sonnet): no blockers; 3 minors accepted (talk facts from Brief + backfill paths; skip timing if duration unknown; Brief slide count updates on add/remove) → new task 1.3 (sonnet; Own SKILL.md, content-writer.md); 1.2 minor (Open questions in backfill) accepted as-is
- 1.1, 1.2 VERIFIED
- Wave 2 launched: 1.3 (sonnet) ∥ 2.1 (haiku)
- 1.3 done (SKILL.md 80, content-writer 64; validate pass)
- 2.1 done (CLAUDE.md layout/section/agents line, README sentence)
- Final verifier (haiku) + reviewer (sonnet) launched
- Final verifier: OUTSIDE-OWN none; checks a–f pass
- Final reviewer (sonnet): no blockers; 6 minors accepted (review talk facts w/o outline; reviewers skip timing if unknown; outline-mode unknown minutes; step-1 no-deck exit; step-7 no-fix exit; CLAUDE.md transcript bullet) → task 1.4 (sonnet; Own SKILL.md, content-writer.md, CLAUDE.md) launched
- 1.4 done; orchestrator spot-check: validate pass, 6 findings present (SKILL.md:35,70,72; content-writer.md:25; CLAUDE.md item 4) → VERIFIED
- CLOSE: tier mix 4 sonnet builders (1.1, 1.2, 1.3, 1.4) · 1 haiku builder (2.1) · verifiers haiku · reviewers sonnet. Escalations: none. Retries: none. Added 1.3 and 1.4 from review minors.
