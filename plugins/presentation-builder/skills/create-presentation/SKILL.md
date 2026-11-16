---
name: create-presentation
description: Interviews the user, previews an outline, then builds a single-file HTML/CSS/JS slide deck (with speaker notes and optional spoken transcript) from a bundled template, using plugin agents for research, writing, design, and independent content + design review. Use whenever the user wants to make, draft, or build a presentation, deck, slides, talk, keynote, pitch, or demo walkthrough, even if they don't say "HTML".
---

# Create presentation

Turn a topic into a polished, self-contained HTML deck through a gated conversation. You run the conversation and every user interaction; plugin agents do the research, writing, building, and reviewing.

Three **gates** where you stop and wait for the user: each interview question (step 1), outline approval (step 4), and fix selection (step 8). At a gate, end your turn. Moving past a gate on assumed consent costs the user a rebuild, so wait for an explicit answer.

Skill files live under `${CLAUDE_PLUGIN_ROOT}/skills/create-presentation/` (`S` below). If ${CLAUDE_PLUGIN_ROOT} is not substituted, use this skill's base directory.

## Agents

Call with the Agent tool: `subagent_type: presentation-builder:<name>`, and always pass `model` explicitly.

| agent | model | job |
|---|---|---|
| `presentation-builder:knowledge-explorer` | haiku | reads user files/links → `work/sources.md` |
| `presentation-builder:content-writer` | opus | outline / slides / fix → `work/outline.md` |
| `presentation-builder:transcript-writer` | sonnet | write / fix → `transcript.md` |
| `presentation-builder:design-creator` | sonnet | build / fix `index.html`, runs the self-check |
| `presentation-builder:content-reviewer` | opus | read-only audit → `work/reviews/content.md` |
| `presentation-builder:design-reviewer` | sonnet | read-only HTML/CSS/JS check → `work/reviews/design.md` |

Rules:
- Only this skill or the user (@-mention) invokes them. Never pass `isolation`. Agents never call agents.
- Agents cannot talk to the user. Every task prompt includes: the **mode**, absolute paths (deck dir, work dir, `S/templates/<template>/template.html`, `S/templates/<template>/DESIGN.md`, `S/references/best-practices.md`), and the interview answers the agent needs.
- Agents reply in ≤10 lines. Read their output files only to show them to the user.
- Review files: a `Verdict: ...` line, then numbered `[blocker|major|minor] <slide|file:line> — problem — fix`.

## 1. Interview — GATE: one question per turn

Ask in order, **one question per message**, each with a recommended default the user can accept with "yes". Skip any question the request already answers (say which answers you took). If the request answers every question, list the answers back in one message and go straight to step 2 (no extra confirmation turn). Otherwise end your turn after each question and wait.

1. **Topic** — what the talk is about, in one sentence.
2. **Audience & context** — who is in the room, where (meetup, all-hands, client call, conference), and what they should do or feel afterwards. Drives tone and density; see the audience tuning in `S/references/best-practices.md`.
3. **Duration** in minutes.
4. **Template** — list the folders under `S/templates/` (each holds `template.html` + `DESIGN.md`); recommend `default`.
5. **Details & source material** — notes, file paths, links, data. The deck should carry their facts, not generic filler.
6. **Live-demo segments** — where in the talk, and how long each. For each demo: what is demoed (tool/app) and the fallback (recording/screenshot location, or "none").
7. **Spoken transcript?** — yes/no (default: no). Yes means a `transcript.md` with a word-for-word script per slide.
8. **Slide count** — asked last; suggest one from duration, demo time, and material: about 1 content slide per minute, plus title, section dividers, and closing. The user decides; duration then only drives pacing.

Done when every question has an answer (given or defaulted).

Then set up the output:
- **Slug**: kebab-case of the interview topic (not the deck title, so a later retitle keeps the folder name), ≤5 words counted after splitting on hyphens.
- **Output path**: output root is the repo root (git top-level, or the CWD if not a repo). If it contains `presentations/` or a CLAUDE.md naming it, deck dir = `presentations/<slug>/`; otherwise `./<slug>/`. Ask before overwriting an existing folder.
- Create `<deck dir>/work/`.

## 2. Research

If the user gave files or links: run `knowledge-explorer` (haiku) → `work/sources.md`. Skip otherwise. The prompt states `web search: no` unless the user asked for web research in the interview.

## 3. Outline

Run `content-writer` mode `outline` (opus) → `work/outline.md`. Read it and show the user:

- A table, one row per slide: **#**, **type/component**, **title**, **key points** (≤3 short phrases), **speaker-note gist**, **minutes**.
- **Narrative flow**: 3–5 lines, hook → sections → climax → close/CTA, naming the slides that carry each beat.
- **Timing**: total vs agreed duration; flag any gap over 10%.
- **Demo plan** and numbered **engagement suggestions** (what / why / where), from the file.

Slide count must equal the agreed count; if the material does not fit, say so and propose a new count instead of silently changing it.

## 4. Approval — GATE: wait for the user

Ask the user to accept or reject each suggestion by number and to edit the outline freely. End your turn.

Change nothing the user has not confirmed. Approval of suggestions alone is not approval of the outline. When the user accepts suggestions or requests changes, run `content-writer` mode `outline` again with them as `requested changes` (it revises `work/outline.md` in place), show the revised outline (step 3 format), then ask for approval. Loop until the user explicitly approves the outline.

## 5. Build

1. `content-writer` mode `slides` (opus): the outline is final; it adds slide content and speaker notes to `work/outline.md`.
2. `design-creator` mode `build` (sonnet): builds `<deck dir>/index.html` from the template and runs its self-check.

## 6. Transcript (only if yes in step 1, or asked later)

Run `transcript-writer` mode `write` (sonnet) → `<deck dir>/transcript.md`. If a transcript is added after review, re-run `content-reviewer` on it.

## 7. Review

In **one message**, two Agent calls in parallel, unanchored (do not pass either one your own opinion or the other's output): `content-reviewer` (opus; pass the transcript path if `transcript.md` exists) and `design-reviewer` (sonnet). Wait for both.

## 8. Report & fixes — GATE: wait for the user

Read `work/reviews/content.md` and `work/reviews/design.md`. Merge into one numbered list, de-duplicated, grouped by severity (blocker / major / minor), each item tagged with its source, slide or `file:line`, and the proposed fix. End your turn and ask which fixes to apply.

Apply only confirmed findings, routed:
- Structural or narrative → `content-writer` mode `fix`, then `design-creator` mode `fix` with `structural: yes`.
- HTML/CSS/JS or on-slide wording → `design-creator` mode `fix` with `structural: no`, then `content-writer` mode `fix` with the same wording changes so `## Slides` stays in sync.
- Transcript → `transcript-writer` mode `fix`. After any content or structural fix, if a transcript exists, run `transcript-writer` mode `fix` to resync it.
- Always pass the current slide count N to `design-creator`.

`design-creator` reruns its self-check after fixes. Finish by giving the output path(s) and how to present: open `index.html` in a browser; ←/→/Space to move, Home/End to jump, `N` for notes, swipe on touch, Cmd+P to print to PDF for one slide per page.
