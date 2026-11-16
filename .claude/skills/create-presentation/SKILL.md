---
name: create-presentation
description: Interviews the user, previews an outline, then builds a single-file HTML/CSS/JS slide deck (with speaker notes and optional spoken transcript) from a bundled template, and runs content + technical review agents. Use whenever the user wants to make, draft, or build a presentation, deck, slides, talk, keynote, pitch, or demo walkthrough, even if they don't say "HTML".
---

# Create presentation

Turn a topic into a polished, self-contained HTML deck through a gated conversation. The user steers every content decision; you do the drafting, building, and checking.

The run has three **gates** where you stop and wait for the user: each interview question (step 1), outline approval (step 4), and fix selection (step 9). At a gate, end your turn. Moving past a gate on assumed consent costs the user a rebuild, so wait for an explicit answer.

Paths below are relative to this skill's folder.

## 1. Interview — GATE: one question per turn

Ask these in order, **one question per message**, each with a recommended default the user can accept with "yes". Skip any question the user's request already answers (say which answers you took from it). If the request answers every question, list the answers back in one message and go straight to step 2 (no extra confirmation turn). Otherwise end your turn after each question and wait for the reply.

1. **Topic** — what the talk is about, in one sentence.
2. **Audience & context** — who is in the room, where (meetup, all-hands, client call, conference), and what they should do or feel afterwards. This drives tone and density; see the audience tuning in [references/best-practices.md](references/best-practices.md).
3. **Duration** in minutes.
4. **Slide count** — suggest one from duration: about 1 content slide per minute, plus title, section dividers, and closing. The user decides; duration then only drives pacing.
5. **Template** — list the folders under `templates/` (each holds `template.html` + `DESIGN.md`); recommend `default`.
6. **Details & source material** — notes, file paths, links, data. Read every file or link given before outlining; the deck should carry their facts, not generic filler.
7. **Live-demo segments** — where in the talk, and how long each. For each demo, follow up: what is demoed (tool/app) and the fallback (recording/screenshot location, or "none").
8. **Spoken transcript?** — yes/no (default: no). Yes means a `transcript.md` with a word-for-word script per slide.

Done when every question has an answer (given or defaulted).

## 2. Outline preview (no HTML yet)

Read `templates/<template>/DESIGN.md` now so every slide maps to a real component. Then present:

- A table, one row per slide: **#**, **type/component** (e.g. `divider`, `steps-list`, `vs-grid`, `dtable`, `flow`, `code-block`, `card-grid`, `demo`), **title**, **key points** (≤3 short phrases), **speaker-note gist** (one line), **minutes**.
- **Narrative flow**: hook → sections → climax → close/CTA, in 3–5 lines, naming the slides that carry each beat.
- **Timing**: total minutes vs agreed duration; flag any gap over 10%.

Slide count must equal the agreed count; if the material does not fit, say so and propose a new count instead of silently changing it.

## 3. Engagement & best-practice suggestions

Read [references/best-practices.md](references/best-practices.md) and audit the outline against it. Present **numbered** proposals, each with:

- **What** — the concrete change (e.g. "open with the 3 a.m. outage story instead of the agenda").
- **Why** — the practice it serves, one line.
- **Where** — slide number(s) affected.

Always check the title/topic against the stated outcome and propose a retitle if they conflict. Aim for the few changes with the most impact (typically 3–8), not every rule.

## 4. Approval — GATE: wait for the user

Ask the user to accept or reject each suggestion by number and to edit the outline freely. End your turn.

Change nothing the user has not confirmed. Apply accepted suggestions and edits, then show the revised outline (step 2 format) and any new suggestions (step 3); loop until the user explicitly approves the outline. Approval of suggestions alone is not approval of the outline.

## 5. Build

1. **Slug**: kebab-case of the approved deck title, ≤5 words counted after splitting on hyphens.
2. **Output path**: the output root is the repo root (git top-level, or the CWD if not a repo). If it contains `presentations/` or a CLAUDE.md naming it, write `presentations/<slug>/index.html`; otherwise `./<slug>/index.html`. Create directories if missing. Ask before overwriting an existing folder.
3. Copy `templates/<template>/template.html` to the output path.
4. Replace `{{TITLE}}` with the talk title.
5. Replace everything between `<!-- SLIDES:START -->` and `<!-- SLIDES:END -->` with the approved slides. Build each from the matching `<!-- SAMPLE: <type> -->` markup and the component docs in `DESIGN.md`. The first slide keeps class `active` (the script also sets it on load). Leave the chrome (CSS, nav JS, markers themselves) untouched: navigation, notes, and print all depend on it.
6. Give **every** slide an `<aside class="notes">…</aside>` as its last child: what to say, the transition to the next slide, and a timing cue (e.g. `~2 min`). Demo slides add the demo steps and a fallback (screenshot/recording) if the demo fails. The notes panel preserves line breaks (`white-space: pre-line`), so put demo steps and `FALLBACK:` on separate lines.
7. Keep on-slide text within the density limits in best-practices; the detail goes in the notes.

Done when the file has the approved slides in the approved order, no `SAMPLE` slides remain, and no `{{` placeholder remains.

## 6. Transcript (when asked)

Write it if the user said yes in step 1 or asks at any later point. Create `transcript.md` beside `index.html`:

```markdown
# <Title>

## 1 · <Slide title>
_~X min_

<Spoken script, in the presenter's voice, as it would be said aloud.>

## 2 · <Slide title>
...
```

Expand the speaker notes into speech; keep the two consistent (same points, same order, same timing). Word budget ≈130 wpm × speaking minutes only: live-demo time and audience pauses count toward slide time cues but not the word budget. Total words should land within ±10% of that budget. If the transcript is requested after review, re-run the content audit (step 8a) on it.

## 7. Self-check

Run these and fix failures before review:

- Slide count: `grep -cE '<div class="slide[ "]' <index.html>` (the pattern skips the `slides` wrapper) equals the agreed count.
- Leftovers: `grep -n '{{\|SAMPLE:' <index.html>` returns nothing.
- Notes: every slide has exactly one `<aside class="notes">`.
- Tag balance: `grep -o '<div' <index.html> | wc -l` equals `grep -o '</div>' <index.html> | wc -l`.
- Headless render (skip if Chrome is absent; macOS path): `"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --dump-dom file://<abs path> | grep -o 'id="counter">[^<]*'` shows `id="counter">1 / <slide count>`.
- Transcript (if any): one `##` section per slide, minutes sum ≈ duration.

## 8. Independent reviews

Launch **two** review agents **in parallel**: one message, two Agent calls, `subagent_type: general-purpose`. They are read-only and neither sees the other's output, so each review stays unanchored. Fill the briefs from [references/review-agents.md](references/review-agents.md):

- **(a) Content audit** — `model: opus`.
- **(b) Technical check** — `model: sonnet`.

Wait for both to return.

## 9. Report & fixes — GATE: wait for the user

Merge both reports into one numbered list, de-duplicated, grouped by **severity** (blocker / should fix / nice to have), each item tagged with its source (content/technical), slide number or `file:line`, and the proposed fix. End your turn and ask which fixes to apply.

Apply only the fixes the user confirms, then re-run step 7. Finish by giving the output path(s) and how to present: open `index.html` in a browser; ←/→/Space to move, Home/End to jump, `N` for notes, swipe on touch, print to PDF for one slide per page.
