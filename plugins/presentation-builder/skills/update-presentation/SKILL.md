---
name: update-presentation
description: Updates an existing HTML slide deck from the user's instructions, using the plugin agents to rewrite, rebuild, resync the transcript, and review. Use whenever the user wants to change, edit, update, revise, or fix an existing presentation, deck, or slides (wording, styling, add/remove/reorder slides, new material). Not for new decks; use create-presentation for those.
---

# Update presentation

Apply the user's change to an existing deck in `presentations/<slug>/`. You run the conversation and every user interaction; plugin agents do the research, writing, building, and reviewing.

**Gates** where you stop and wait for the user: deck choice (step 1), a clarifying question (step 2, only if asked), outline approval (step 5), and fix selection (step 7). At a gate, end your turn. Moving past a gate on assumed consent costs the user a rebuild, so wait for an explicit answer.

`S` = `${CLAUDE_PLUGIN_ROOT}/skills/create-presentation/` (templates and `references/best-practices.md` live there; do not copy them). If ${CLAUDE_PLUGIN_ROOT} is not substituted, use this skill's base directory + `/../create-presentation/`. Template = the one named in the `work/outline.md` Brief, else `default`.

## Agents

Call with the Agent tool: `subagent_type: presentation-builder:<name>`, and always pass `model` explicitly.

| agent | model | job |
|---|---|---|
| `presentation-builder:knowledge-explorer` | haiku | reads user files/links → `work/sources.md` |
| `presentation-builder:content-writer` | opus | backfill / outline / slides / fix → `work/outline.md` |
| `presentation-builder:transcript-writer` | sonnet | write / fix (`resync`) → `transcript.md` |
| `presentation-builder:design-creator` | sonnet | build / fix `index.html`, runs the self-check |
| `presentation-builder:content-reviewer` | opus | read-only audit → `work/reviews/content.md` |
| `presentation-builder:design-reviewer` | sonnet | read-only HTML/CSS/JS check → `work/reviews/design.md` |

Rules:
- Only this skill or the user (@-mention) invokes them. Never pass `isolation`. Agents never call agents.
- Agents cannot talk to the user. Every task prompt includes: the **mode**, absolute paths (deck dir, work dir, `S/templates/<template>/template.html`, `S/templates/<template>/DESIGN.md`, `S/references/best-practices.md`), and the instruction details the agent needs. Content-writer and reviewer prompts also pass the talk facts (title, audience, desired outcome, duration, slide count, template, demos) copied from the `work/outline.md` Brief.
- Agents reply in ≤10 lines. Read their output files only to show them to the user.
- Review files: a `Verdict: ...` line, then numbered `[blocker|major|minor] <slide|file:line> — problem — fix`.

## 1. Pick the deck — GATE

If the skill argument is a slug under `presentations/`, use it. Otherwise list the folders under `presentations/`; if only one exists, propose it. Ask the user to confirm the deck and end your turn. If `presentations/` has no decks, tell the user (suggest `/create-presentation`) and stop. If the slug does not exist, list the existing decks and ask which one.

## 2. Understand the change

Restate the instruction and classify it, saying which class you picked:
- **small**: no slide added, removed, or reordered, and no narrative or timing change (wording, typos, styling on existing slides).
- **structural**: everything else.

Note any new sources (files/links). If the class is ambiguous, ask one question — GATE: end your turn and wait. Otherwise continue.

## 3. Research

If there are new sources: `knowledge-explorer` (haiku) → `work/sources.md` (create `work/` if missing). The prompt states `web search: no` unless the user asked for web research.

## 4. Small change

1. `design-creator` mode `fix` (sonnet), `structural: no`, slide count N = `grep -cE '<div class="slide[ "]' index.html`, findings = the user's instruction.
2. If `work/outline.md` exists, `content-writer` mode `fix` (opus) with the same wording changes so `## Slides` stays in sync. No backfill for small changes.

Then go to step 6.

## 5. Structural change — GATE: outline approval

1. If `work/outline.md` is missing, run `content-writer` mode `backfill` (opus) first, naming the absolute paths of `index.html`, `context.md`, `transcript.md` and `work/sources.md` (those that exist).
2. Run `content-writer` mode `outline` (opus) with `requested changes` = the instruction (it revises `work/outline.md` in place).
3. Show the changed, added, and removed rows (columns: **#**, **type/component**, **title**, **key points** ≤3 short phrases, **speaker-note gist**, **minutes**), the new slide count N (read from the revised outline's row count), and timing vs duration (flag a gap over 10%; if duration or minutes are `unknown`, skip this check and say "duration unknown").
4. Ask the user to approve or edit. End your turn. Loop revisions (run `outline` again with their edits as `requested changes`, show, ask) until the user explicitly approves.
5. Then `content-writer` mode `slides` (opus), then `design-creator` mode `fix` (sonnet) with `structural: yes` and the new N.

## 6. Transcript

If `transcript.md` exists and slide copy, notes, or order changed: `transcript-writer` mode `fix` with `resync` (sonnet).

## 7. Review — GATE: fix selection

Only if the change was structural or touched more than 3 slides. In **one message**, two Agent calls in parallel, unanchored (do not pass either one your opinion or the other's output): `content-reviewer` (opus; pass the transcript path if present) and `design-reviewer` (sonnet), each with `focus: slides <changed list>` using the new numbering. If `work/outline.md` is missing (small changes never backfill; do not backfill just for review), pass talk facts from `context.md` where available, else `unknown`. If duration or per-slide minutes are `unknown`, tell both reviewers to skip timing checks and not flag timing. Wait for both.

Read `work/reviews/content.md` and `work/reviews/design.md`. Merge into one numbered list, de-duplicated, grouped by severity, each item tagged with source, slide or `file:line`, and proposed fix. Ask which fixes to apply and end your turn. If the reviewers found nothing or the user declines all fixes, go to step 8. Apply only confirmed findings, routed:
- Structural or narrative → `content-writer` mode `fix`, then `design-creator` mode `fix` with `structural: yes`.
- HTML/CSS/JS or on-slide wording → `design-creator` mode `fix` with `structural: no`, then `content-writer` mode `fix` with the same wording changes.
- Transcript → `transcript-writer` mode `fix`; after any content or structural fix, resync it if a transcript exists.
- Always pass the current slide count N to `design-creator`.

## 8. Report

List the changed slides and files written, and how to view: open `presentations/<slug>/index.html` in a browser; ←/→/Space to move, Home/End to jump, `N` for notes.
