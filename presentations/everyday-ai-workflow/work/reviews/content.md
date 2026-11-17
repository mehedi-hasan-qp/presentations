Verdict: ready after fixes

Scope: slides 1-21 and 23-31 (slide 22 excluded per focus; its 2.5 min is still counted in the timing total). The review judges whether each slide makes sense to a first-time reader flipping through without the speaker, plus story, density, timing, notes, transcript and outline fidelity. No blockers. Story arc, hooks, Q&A buffers, demo fallbacks, cut markers and cross-slide references in the notes all check out. The main gaps are two demo slides that never show their result, a primer title that contradicts its own table, a few cards that repeat or contradict themselves, and a CTA install line that only makes sense if you heard the talk.

## Findings

1. [major] slide 3 — The title "A skill is a playbook. Sub-agents run it." contradicts the table on the same slide. The table says the main session runs the skill and hands single tasks to sub-agents, and the example skill (`/git-commit`) uses no sub-agents at all. This primer is what first-timers learn from, so it has to be right. — Retitle to "A skill is a playbook. / Sub-agents are its helpers." Leave the table as it is.
2. [minor] slide 2 — The second line ("Today: one tool each for checking, planning and shipping.") repeats slide 1's subtitle almost word for word. The tool names also never appear together on one slide before the section dividers, so a reader gets no map. — Replace the line with a named signpost: "Today: eqc-kit checks · /orchestrate plans · the ship chain ships." This also keeps the hook from turning into an agenda (best-practices: "Open with a hook, not an agenda"; the line stays secondary to the 39-rules headline).
3. [minor] slide 5 — "works in Claude Code + 4 other AI coding tools" leaves the reader asking which ones. The names are only in the notes. The slide also has about 47 words (rule: ~30). — Footer: "`npx eqc-kit init` · Claude Code, Codex, Cursor, Copilot, Gemini CLI". To pay for it, cut the lead to "Open-source npm package: AI agents audit your code against your own written standard."
4. [minor] slide 6 — Row 04 says "Level = highest tier with no fails." That is wrong as written: a clean HIGH tier with a LOW fail is still HARD_FAIL. Slide 10's definition is correct, so the two slides disagree. — Change the step-desc to "Plain script, no AI. Level = highest tier where it and every tier below have no fails."
5. [minor] slide 7 — The lead "No arguments = re-read the last audit" never names the command, so a reader skimming the deck has to guess. The kicker and the watch-for line also both say "no tokens". — Lead: "`/eqc-check` with no arguments re-reads the last audit: level per tier, every open fail with its evidence." Kicker: "Demo · /eqc-check, cached".
6. [minor] slide 8 — About 68 words, the densest eqc-kit slide (rule: ≤6 lines / ~30 words). The card titles "Goes straight" and "Gets a plan" repeat the headline. — Delete both `.vs-card-title` lines and merge the medium/large attributes into "**First:** opus writes a read-only plan; you approve it". Keep the "Then:" line.
7. [major] slide 9 — The demo slide tells the room what to watch for but never says what happened. A reader without the speaker learns nothing about which model got which chunk or where it stopped, which is the whole point of the demo (best-practices: "Return slide … restating what was just shown"). — Replace the watch-for line with an outcome line that still works as a watch-for: "Each chunk names its model: haiku for mechanical edits, sonnet for judgment calls. It stops before anything touching CI, packages or architecture." Once `screenshots/eqc-fix-plan.png` exists, consider embedding it.
8. [major] slide 11 — The cards contradict each other. Card 1 says "4 fails" and card 2 is TypeScript, which is one of those 4, so a reader counts 5. Card 3 ("no LLM / Not in pre-commit") is a design choice of the tool, not a fail of the app, and on its own it is cryptic. That makes two ideas on one slide (best-practices: "One idea per slide"). — Card 1: slash "3 big moves", name "Architecture, not quick wins", sub "state migration (123 files), data-fetching library, cert pinning". Card 2 (hi): slash "TypeScript", name "Recorded as a fail, not faked", sub "project mandates JavaScript". Card 3: slash "By design", name "No LLM in pre-commit", sub "too slow, costly and nondeterministic for every commit".
9. [minor] slide 15 — The title promises "two hard stops", but only PREVIEW is highlighted. The reader has to work out that GRILL is the other one. "Reports the model mix" is unexplained jargon. — Step-titles "GRILL · stop 1" and "PREVIEW gate · stop 2" (keep hi on PREVIEW). CLOSE desc: "Reports which models did the work; never commits".
10. [minor] slide 18 — In the right column, "Delegate it" doesn't say who it gets delegated to. — Change it to "Hand it to a sub-agent".
11. [minor] slide 19 — The left card reads "**Audit:** test-coverage audit: done" and "**E2E:** E2E (end-to-end) test: line 143 covered". Each label repeats itself. The `<strong>` prefixes were added in the build; they are not in the outline's copy (outline fidelity). — Change it to "**Coverage audit:** "done"" and "**E2E (end-to-end) test:** "line 143 covered"". Mirror the right card: "**Coverage audit:** ~65 identifiers missing → retry with exact list → 0 missing" and "**E2E test:** line 143 still uncovered".
12. [major] slide 20 — Every card says the same thing twice: name and sub repeat each other, e.g. "Skill issues found by one dry-run" / "Issues one opus dry-run (a trial run) found in a new skill", and "One wave stopped by a full disk" / "Disk full: one wave, 3 agents, zero bytes". The slide has about 75 words, the densest in the deck. The dry-run and ENOSPC cards also don't support the title "cheap models did most of the work". — Retitle to "~11 real runs: / mostly cheap models, a few surprises" and keep one line per card. haiku / sonnet: "Did most of the work" · retries: "Retried on the same model, rarely moved up" · 15: "Issues an opus trial run caught before real work" · ENOSPC: "Disk full: 3 agents, zero bytes written".
13. [minor] slide 21 — The meta reveal is the climax, but it lands at 26.25-27.5 min (66-69%), just before the 70-80% window. It is also a fun reveal rather than the strongest proof; slide 10 is the stronger proof, at ~28%. That's acceptable for three independent tools. — No change needed. If rehearsal runs short, let slide 21's notes recall slide 10 in one line ("a skill built this deck; the same habits took our app from HARD_FAIL to MEDIUM").
14. [major] transcript.md:278 (slide 21) — The transcript reads the cut-condition aloud as real speech: "If we skipped that slide: an opus dry-run found fifteen issues…". In the normal run it repeats the 15-issues fact straight after "That opus dry-run with fifteen issues? This skill." — Wrap it as a stage direction the way slides 17, 19 and 25 already do: "[IF SLIDE 20 WAS CUT, say instead: "An opus dry-run of this skill found fifteen issues before any real work; thirteen got fixed."]". Delete the spoken sentence.
15. [minor] slide 24 — CLAUDE.md appears with no gloss; it isn't in the slide 3 primer. Slide 3 also defines a skill as "`/name`", but reflect and release-notes have no slash here, so a reader can't tell whether they are skills. — reflect desc: "Session end: updates CLAUDE.md (the agent's project notes) and docs". Add a short line under the list: "No slash = the agent runs it when asked, e.g. "write the release notes"". Confirm this is how reflect and release-notes are actually triggered before stating it.
16. [minor] slide 25 — The title "One piece of writing, four audiences" contradicts the table, which lists four different pieces of writing. "Store note" is never defined on a slide. — Retitle to "One change, / four write-ups, four readers". Change row 4 to "**Store note** (App/Play Store "What's new")".
17. [major] slide 27 — Same gap as slide 9: the ship-chain section promises a commit turning into a sentence a manager or user can read, but no slide ever shows one. A reader flipping the deck never sees the payoff. The slide also doesn't say whose v1.9.4 this is. — After the talk prep, add a `code-block` (≤4 lines) with one real commit line from `git log` and its matching sentence and store-note line from `docs/RELEASE_NOTES_v1.9.4.md`, or embed `screenshots/release-notes-v1.9.4.png`. Don't invent the text. Kicker: "Demo · our mobile app v1.9.4".
18. [minor] slide 27 — The demo runs at ~34.0-35.5 min (85-89%), past the rule "no later than ~80% of runtime". — Accept, since the section is short by design. If rehearsal runs long, cut slide 26 first; that pulls the demo to ~83%.
19. [minor] slide 29 — The talk's tagline "Ask first, build cheap, ship clean" is the recap title, but no slide ever explains it, and the three cards don't map onto its three verbs. — Card-names: eqc-kit → "Ask first: big fixes wait for your OK" (sub "LLM judges, a script counts"); /orchestrate → "Build cheap: score the task, then pick the model" (sub "plans, then cheaper models build"); ship chain → "Ship clean: write the commit for its next reader" (sub unchanged). The word count stays the same.
20. [major] slides 30, 31 — The CTA's install line ("Skills: "Fetch and follow https://…INSTALL.md"") only makes sense if you heard the notes. A reader can't tell it's a prompt to paste into the agent, or that it is how you get `/orchestrate` and `/git-commit`. This is the mechanism behind the desired outcome. — Change it on both slides to: "Get /orchestrate and /git-commit: paste into Claude Code → "Fetch and follow https://raw.githubusercontent.com/mehedibangladeshi/ai-skills/master/INSTALL.md"".
21. [minor] density, deck-wide — These slides are over ~30 words, with approximate word counts: 3 (~63), 5 (~47), 6 (~57), 8 (~68), 10 (~58), 16 (~50), 18 (~56), 19 (~57), 20 (~75), 24 (~51), 27 (~46), 29 (~47). Slides 2, 7, 9, 11, 14, 15, 17, 21, 25, 26 are at 35-45. Most of this is the intended trade-off of the self-explanatory revision: glossary and table slides earn their rows. — Apply the trims in findings 3, 6, 11 and 12. Accept the rest as table/steps slides, and don't add any more on-slide text beyond the fixes above.
22. [minor] transcript per-slide pacing — At ~130 wpm the spoken text runs over its cue on slide 2 (~140 words + pause ≈ 1.25 vs 1.0), slide 3 (~150 ≈ 1.15 vs 1.0), slide 21 (~175 ≈ 1.35 vs 1.25), slide 30 (~90 ≈ 0.7 vs 0.5) and dividers 4 and 13 (~45 ≈ 0.35 vs 0.25). Slides 10, 15, 20 and 29 run under their cues, so the total still fits. — Either move 0.25 min each from slides 10 and 29 to slides 2 and 30, or trim the slide 3 transcript's recipe aside and the slide 21 duplicate (fixed by finding 14).

Slide 1: no issues.
Slide 4: no issues.
Slide 12: no issues.
Slide 13: no issues.
Slide 14: no issues.
Slide 16: no issues beyond density (finding 21). The lead's gloss of Ambiguity / Breadth / Reasoning makes the table self-explanatory.
Slide 17: no issues. The watch-for line already states the outcome.
Slide 23: no issues.
Slide 26: no issues.
Slide 28: no issues.

Notes: every in-focus slide has notes that add to the slide, a transition and a time cue. All cross-references (slide 1→21, 7→10, 8→3, 9→10, and the cut paths 17→19, 19→21, 25→27) resolve. Demo slides 7, 9, 17 and 27 all have scripted steps and a FALLBACK. The screenshots in `./screenshots/` still have to be captured (context.md checklist). Audience moments come at about 1, 11.5, 19 and 32 min, plus three Q&A buffers, which meets "every 8-10 min". Outline fidelity: the deck matches the 31-slide outline in order and copy, except finding 11.

## Timing

Est. = transcript words at ~130 wpm, plus live-demo action and guess pauses. Word counts are approximate (±10%).

| Slide | Planned min | Est. min |
|---|---|---|
| 1 | 0.5 | 0.6 |
| 2 | 1.0 | 1.25 |
| 3 | 1.0 | 1.15 |
| 4 | 0.25 | 0.35 |
| 5 | 1.25 | 1.1 |
| 6 | 1.25 | 1.0 |
| 7 (demo) | 1.5 | 1.45 |
| 8 | 1.25 | 1.15 |
| 9 (demo + guess) | 1.75 | 2.0 |
| 10 | 1.75 | 1.3 |
| 11 | 1.5 | 1.3 |
| 12 (Q&A) | 2.0 | 2.0 |
| 13 | 0.25 | 0.35 |
| 14 | 1.25 | 1.15 |
| 15 | 1.75 | 1.45 |
| 16 (guess) | 1.75 | 1.55 |
| 17 (demo) | 1.5 | 1.35 |
| 18 (cuttable) | 1.5 | 1.45 |
| 19 | 1.75 | 1.55 |
| 20 (cuttable) | 1.5 | 1.15 |
| 21 | 1.25 | 1.35 |
| 22 (Q&A, out of focus) | 2.5 | 2.5 |
| 23 | 0.25 | 0.25 |
| 24 | 1.5 | 1.3 |
| 25 (guess) | 1.5 | 1.55 |
| 26 (cuttable) | 0.75 | 0.7 |
| 27 (demo) | 1.5 | 1.35 |
| 28 | 1.0 | 0.85 |
| 29 | 1.0 | 0.7 |
| 30 | 0.5 | 0.7 |
| 31 (Q&A) | 2.0 | 2.0 |
| **Total** | **40.0** | **~37.9** |

Planned 40.0 min = the 40 min slot (sections 15.0 / 15.0 / 10.0). The estimate of ~37.9 min is within ±10%. The ~2 min of slack absorbs live-demo friction; the biggest risk is slide 9 (demo plus guess, est. 2.0 vs 1.75). The transcript has ~3,750 spoken words ≈ 29 min. Add 6.5 min of Q&A buffers, ~3 min of live-demo action and ~1 min of guess pauses and you get ≈ 39-40 min. If running late, cut in this order: 18 (−1.5), 20 (−1.5), 26 (−0.75), slide 11's guardrails paragraph (−0.3), about 4 min in all.
