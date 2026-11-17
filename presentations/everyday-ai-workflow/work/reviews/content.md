Verdict: ready after fixes

Scope: focus slides 4-10, plus cross-references from slides 1 and 27-29. The deck matches `work/outline.md` (revision 3) word for word on slides 4-10. Because the speaker asked for it, density in slides 5-9 is not flagged as a problem (best-practices "Density limit" waived for this section).

## Findings

1. [major] context.md:33-38 (before-the-talk checklist) — The checklist still uses the pre-revision-3 slide numbers ("slide 7/10 numbers", "slide 9 (`/eqc-fix` top-10 + `MEDIUM-10` plan)", "slide 11's guardrails paragraph"). It lists the dropped MEDIUM-10 plan demo and leaves out the new `eqc-compliance-report.png` fallback. The speaker could prep the wrong things. — Renumber the checklist to: re-run `/eqc-check` so slides 8 and 9 agree; capture `eqc-check-scorecard.png`, `eqc-compliance-report.png` and `eqc-fix-ranked.png` for slide 8; mark slide 7's hooks paragraph as cuttable. Drop the MEDIUM-10 item.
2. [major] Slides 5, 6, 7, 8, 28, 29 (release dependency) — According to sources.md:1-5, the code map, the HTML report, `eqc guard`, `verify` and hooks exist only on the unreleased dev branch, and the published package is still 0.1.0. The CTA `npx eqc-kit init` on slides 5, 28 and 29 installs 0.1.0, which has none of what slides 6-8 show. Nothing in the checklist covers publishing. — Add a checklist item: "Publish eqc-kit with the [Unreleased] changes and confirm `npx eqc-kit init` installs them". Also add one fallback line to slide 7's notes: "If the release slips: guard, verify, hooks and the HTML page are in the next version; check and fix work today."
3. [minor] Slide 6, row "Same answer next time?", eqc-kit cell — "same answers always give the same level" is true, but read on its own the slide suggests a fresh re-check is deterministic. The agents can still give different answers on a re-run, and the cons line admits that. The row overstates the guarantee. — Change the cell to: "Saved results are re-read, not re-guessed; a plain script turns the same answers into the same level every time."
4. [minor] Slides 6-7 — "level" and "code map" appear on the slides with no definition. For first-time readers without the speaker, "level" is only defined on slide 9 and "code map" never is. — Slide 7, `/eqc-check` cell: change "A plain script works out the level" to "A plain script works out the level (the highest tier with no fails at or below it)". Change "using a code map first" to "using a code map, e.g. a graphify graph, first".
5. [minor] Slide 6, first column header — The header says "Problem", but every row is a question ("Can I trust a 'pass'?"). — Rename the header to "Question".
6. [minor] Slide 7 → 8 transition — "Let me show you three of these on our app" is inaccurate: the demo runs two of the four commands plus the report file. — Change it to: "Enough talking. Let me show you two of these, and the report it writes, on our app."
7. [minor] Slide 8 → 9 ("hold that number" payoff) — The slide 9 title shows MEDIUM as soon as you flip. The transcript's later line "And that number you were holding: MEDIUM" (transcript.md:144) comes after the audience has already read it, so the payoff falls flat. — Move the line to the top of slide 9, right after the Logger reveal: "Fifty-eight. And the level you saw in the terminal: MEDIUM, right there in the title." Delete transcript.md:144.
8. [minor] Slide 8 notes — /eqc-fix uses AI (per slide 7), and the notes give no time limit for part 3. On a slow run the 2.75 min slot overruns. — Add to step 5: "If the ranked list hasn't appeared in ~30 s, cancel and show FALLBACK (part 3)."
9. [minor] Slide 9, table — The header reads "What we fixed", but the "Tests kept green the whole way" and "Still failing (4)" rows are not fixes. — Change the header to "What changed".

Slide 4: no issues. The divider sub and notes are fine. "About 10 minutes" is consistent with 10.25 min of content before Q&A.
Slide 5: no issues beyond #2. The first-person story fits the requested voice, and the transcript follows the notes.
Slide 10: no issues. The seeds fit the section, and the "move on at 15 minutes" cue matches the cumulative time (15.0).
Cross-references: slide 1's notes ("comes back on slide 19") are correct. Slide 27's eqc-kit card ("Ask first: big fixes wait for your OK"; "keeps passing rules passing") matches slide 7's /eqc-fix and guard rows. Slides 28-29 are consistent with slide 5's install line (subject to #2).

## Timing (focus slides)

| Slide | Planned min | Est. min |
|---|---|---|
| 4 | 0.25 | 0.25 |
| 5 | 1.25 | 1.25 (~170 spoken words) |
| 6 | 2.25 | 2.0-2.25 (~260 words) |
| 7 | 2.0 | 2.0 (~260 words; hooks paragraph cuttable, ~0.3 min) |
| 8 | 2.75 | 2.75-3.25 (demo; risk is /eqc-fix latency, see #8) |
| 9 | 1.75 | 1.75 (~230 words) |
| 10 | 2.0 | 2.0 (Q&A buffer) |
| **Total 4-10** | **12.25** | **12.0-12.75** |

Slides 1-3 add 2.75 min, so section one ends at 15.0 min as planned. The full deck sums to 40.0 min against the 40 min slot (from the outline; slides outside the focus were not re-timed). If running late, cut the hooks paragraph on slide 7, then shorten Q&A on slide 10.
