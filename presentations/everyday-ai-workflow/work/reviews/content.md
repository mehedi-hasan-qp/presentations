Verdict: ready after fixes

Scope: focus on slides 11-17 (/orchestrate section), their transitions to slides 10 and 18, and cross-references to them in the rest of the deck, transcript.md, outline.md and context.md. Slides 1-10 and 18-26 were not judged. The speaker's stated preferences (dense self-explanatory slides, plain titles, no jokes, no invented numbers) override the best-practices density rule (≤6 lines / ~30 words). Every focus slide is over that limit on purpose, so density only appears below where it hurts readability.

1. [blocker] slide 16 (index.html:621-635), transcript.md:243-253, slide 13 (index.html:548) — The demo types "just go" at the "Approve, edit, or reject?" prompt and expects the same question back. The skill says the opposite. Only approval written *into the goal* is ignored (SKILL.md:45, quoted in sources.md:154; slide 14 states it correctly at index.html:573). A reply after the preview that is "an unconditional yes (ok, go, lgtm, …)" approves (SKILL.md:46, sources.md:155). Typed live, "just go" will most likely approve the plan and start a real run on stage, including a security task on opus. Slide 13's cell "\"just go\" doesn't count" has the same mistake. — Fix: put "just go" into the goal and show an "ok, but…" edit (this is a sources.md:244 demo candidate).
   - PREP: `/orchestrate <small goal with one security task>, just go`, answer GRILL, and stop at PREVIEW. The preview should print a line saying approval in the goal was ignored.
   - Step 01: "Paused at PREVIEW — I wrote \"just go\" into the goal. It still stopped, and says so. Every task has its score and model, and the opus row says why."
   - Step 02 (hi): "Reply \"ok, but drop task 3\" — That counts as an edit: it changes the plan and shows it again. Only a plain yes approves."
   - Watch for: "\"just go\" in the goal didn't skip the gate."
   - Notes and transcript step 4: reply with the "ok, but…" edit, show the re-preview, then reject. Add the line "Never type a bare 'go' or 'just go' at the prompt: that approves." Re-capture `orchestrate-preview.png`.
   - Slide 13 cell: "Yes, a hard gate: \"just go\" in your goal doesn't skip it".
   - Check the behaviour in rehearsal.
2. [major] slide 14 (index.html:568, 574) — The lead says "The orchestrator never writes the code itself", but the EXECUTE row says "Its only code change is one fix of 5 lines or less per task." So the slide contradicts itself, and "Its" reads as "the helpers'". A first-time reader can't resolve it. — Fix: Lead: "…The orchestrator doesn't write the code; helpers on haiku, sonnet or opus do." EXECUTE row: "Helpers build. A haiku verifier runs the checks; a sonnet reviewer reads the diff (an opus security reviewer for security tasks). The orchestrator may make one fix of 5 lines or less per task, only for a bug the verifier found."
3. [major] slide 13 (index.html:548) — In the "Stops for your OK before building?" row, /goal gets "No per-task approval gate". /orchestrate has no per-task gate either: it has one gate on the full plan. Also, the plan mode cell ("Yes, once, for the whole plan") and the /orchestrate cell read the same, so a reader sees no reason /orchestrate wins this row. — Fix: /goal cell "No, it starts working right away". /orchestrate cell as in finding 1, so the difference is "can't be skipped". If the speaker meant something else by the confirmed "/goal: no per-task approval gate" (sources.md:239), keep it in the notes, not the cell.
4. [major] context.md:15, 25, 28-29, 37-39, 72 (cross-references to slides 11-17) — context.md is still on the 31-slide numbering and has stale facts:
   - "Slides: 31".
   - The meta reveal on "slide 19" (now 17).
   - Cuttable "16/18/24" (now: notes paragraphs on 14 and 15, plus slide 21).
   - Fallback screenshot and pre-staging for "slide 15" (now 16), and the pre-staging line repeats the "only type 'just go'" flaw.
   - "Security ≥ sonnet" (now always opus).
   - "light humor… AI-slop jokes" (the speaker now wants no jokes).

   Slide 17's notes (index.html:666) tell the audience "If a slide is wrong, that file is the place to check", so readers who check it will find facts that contradict slide 15. — Fix: update these lines to the 26-slide numbering and the current scoring, and rewrite the checklist's pre-staging line to match finding 1. Optionally, change slide 17's notes to "a context file and a sources file in the same folder".
5. [minor] slide 17 (index.html:647, 649) — The card title "The verifier caught two false \"done\"s" overclaims: the source for line 143 says "a coverage refresh showed it wasn't" (context.md:77) and doesn't name the verifier. — Fix: title "Two \"done\" claims that weren't true", or confirm the verifier caught it.
6. [minor] slide 17 (index.html:655) — The note that the runs predate the opus tier is only in the speaker notes. A reader who saw "security: always opus" on slide 15 sees "0 escalations" with no context. — Fix: "The build: /orchestrate built it in 5 tasks + 2 fixes, 0 escalations (before the opus tier existed)."
7. [minor] slide 17 (outline fidelity) — The outline's third left-card line "~11 runs: most of the work went to haiku and sonnet." is not in the deck. The builder note allows this if the slide overflows, and the line is in the notes. — Fix: none needed. Record in the outline that it moved to the notes.
8. [minor] slide 15 (index.html:601), transcript.md:222-226 — The guess-first answer "write CLAUDE.md → haiku, it's narrow" is debatable. Writing a CLAUDE.md means reading across the repo, and the skill sends "cross-module synthesis" to sonnet (sources.md:189), so an engineer in the room can argue. — Fix: use the skill's own haiku example: "Which model gets 'add a config entry with exact steps'?" (planning.md:30). Answer: haiku, because it's clear, touches one file and needs little thinking.
9. [minor] slide 15 (index.html:594, 598) — The header "Total" doesn't fit the "Security work" row, which isn't a score. — Fix: header "Score or task type".
10. [minor] slide 15 title — "How it picks a model, and why that saves tokens" has two ideas (best-practices: "If the title needs 'and', split it"). The saving is never shown, and slide 13's cons line admits overhead. — Fix: "How it picks a model for each task". Keep the token point in the "Its rule" line and the notes.
11. [minor] slide 14 title — "What /orchestrate is like" is vague. — Fix, still plain: "How /orchestrate runs a big task, phase by phase".
12. [minor] slide 13 (index.html:545-553) — There are about 190 words at 0.76rem across 6 rows and 5 columns. This is the one slide likely to be unreadable when projected. — Fix: shorten the cells without losing rows:
    - Plan mode, row 1: "No, you retype your asks".
    - Long prompt, "Who checks": "Nobody, unless you do".
    - Cons line: "…has to run on opus or sonnet (it stops on haiku)…". This also matches the lowercase model names on slides 3 and 15.
13. [minor] slide 12 (index.html:519-524) — Rows 02 and 03 are the same idea ("I asked for the same things" / "Same prompt, over and over"). The footer states "it saves tokens" as a fact, but no number is ever given. — Fix: merge 02 and 03 into "I typed the same asks every time — Split into phases, a sub-agent per phase on a model that fits, interview me first. Same prompt, every big task." Footer: "Why I built it: to spend fewer tokens by sending each piece to the cheapest model that can do it."
14. [minor] slide 11 (index.html:500) — The divider sub has 22 words, which is long for a one-line promise (best-practices: divider "+ .sub for the one-line promise"). — Fix: "Plans big work with you, then sends each task to the cheapest model that can do it."
15. [minor] slides 12, 13 (timing) — The transcript runs about 130 words on slide 12 (≈1.0 min, cue 1.5) and about 230 words on slide 13 (≈1.75 min, cue 2.75). Slide 17 runs about 270 words (≈2.1 min) against a 1.75-min content cue. — Fix: move 0.5 min from 12 to 17's content cue, or leave it as spare time. If running late, cut in this order: slide 14's CUTTABLE paragraph (~0.6 min), slide 15's ladder (~0.5 min), then slide 17's notes on the dry-run and the context file (~0.4 min).

Slide 11: no issues beyond finding 14. Notes, transition from slide 10 and time cue are fine.
Slide 16: findings 1 only. Otherwise fine: it's after the concept (slides 14-15), has a watch-for line, a scripted fallback, and a return line into slide 17.
Notes on slides 11-17: present on every slide, say more than the slide, and include a transition and a time cue. All cross-references check out: "slide 17" (1), "slide 15" (17), "next two slides" (13), "next slide" (14), "in a minute" (14 → 16).
Transcript 11-17: same points and order as the notes, natural speech, no jokes. It inherits the "just go" error at lines 243 and 251.
Arc and engagement: the reveal (slide 17, right card) lands at ~26.5-27.5 min (66-69%), just before the 70-80% window, which is acceptable. Audience moments in this section: guess-first (15, ~22 min), demo (16), Q&A (17).

## Timing

| Slide | Planned min | Est. min |
|---|---|---|
| 1-10 (not in focus) | 15.0 | 15.0 |
| 11 | 0.25 | 0.25 |
| 12 | 1.5 | 1.0 |
| 13 | 2.75 | 2.25 (1.75 speech + table reading) |
| 14 | 2.5 | 2.0 (1.4 without CUTTABLE) |
| 15 | 2.0 | 2.0 (incl. guess pause) |
| 16 | 1.75 | 1.75 (live demo) |
| 17 | 4.25 | 4.6 (2.1 content + 2.5 Q&A) |
| 18-26 (not in focus) | 10.0 | 10.0 |
| **Total** | **40.0** | **≈38.9** vs. 40-min slot (within ±10%) |
