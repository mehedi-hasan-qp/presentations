Verdict: ready after fixes

Scope: focus slides 1, 2, 4, 5, 6, 7, 9, 10, 13, 14, 15, 16, 18, 25, 26, 27 (27-slide numbering), their transitions, and cross-references in transcript.md, context.md and outline.md. Other slides were not judged and have no blockers. The speaker's preferences (dense but self-explanatory, plain titles, casual first-person notes, no jokes, no invented numbers, "the Mobile EQC", QuestionPro on slides 1-2 only, soft scope for eqc-kit) override the generic density rule, so density is flagged only where it hurts a first-time reader. Word counts are estimated from transcript.md at ~130 wpm.

1. [major] slides 6, 7, 9 (index.html:388-396, 410-421, 473-482; transcript.md:97-214): section 1 runs long. The spoken text is about 250 words on slide 6 (~1.9 min against a 1.5 cue), ~375 words on slide 7 (~2.9 min against 1.75, ~3.4 with the hooks paragraph) and ~280 words on slide 9 (~2.2 min against 1.75). Section 1 ends ~1.8 min late, which leaves almost nothing of the 2-minute eqc-kit Q&A (best-practices: Timing, keep each section within its slot). Fix: mark these as CUTTABLE in the notes and the transcript. Slide 7: the code-map paragraph ("If you already have a code map…") and the second half of verify ("Not every rule gets one…"). Slide 6: the folder-list paragraph ("The rule lists the folders per stack…"). Slide 9: the "Not on the slide" line and the i18n story. Saying none of them recovers ~1.5 min.
2. [major] slide 17→18 transition (index.html:662; transcript.md:383): the line "Here's what the checking after looked like on real runs" is left over from the old slide 17 (verifier catches), which was dropped in revision 5. Slide 18 now shows what was built and the run stats. Fix: Transition: "That's the check before anything runs. Here's what I've actually built with it." Use the same line in the transcript.
3. [major] slide 14 (index.html:567-569), plus slide 13's transition (index.html:559): /goal is never defined on any slide, including the slide 3 primer, but it gets a whole column. A first-time reader can't follow it, which breaks the "self-explanatory" requirement. Fix: change the lead to "The task: an API endpoint, a reset email, a reset screen, tests. It touches auth. (/goal: Claude Code keeps working until a goal is met.)", or the header to "/goal (runs until done)".
4. [major] slides 4, 25 (index.html:333-334, 837): the three title phrases appear only on slides 1 and 25. No section is signposted as "Ask first", "Build cheap" or "Ship clean". On the recap, "Ask first: big fixes wait for your OK" is a weak fit for eqc-kit, because asking first and waiting for an OK is what /orchestrate does (GRILL + PREVIEW). Fix: slide 25 card-name "Ask first: check every rule, with proof, before you fix". Slide 4 notes: add "This is the 'ask first' part: ask the standard before you change code." Add the matching one-liners "build cheap" to the slide 12 notes and "ship clean" to the slide 19 notes.
5. [major] slide 9 (index.html:470; transcript.md:204): the transcript says "The tests stayed green all the way. We touched about eighty-five test files." The sources only say "13-chunk sweep across ~85 files, suite 2912/2912 green (MEDIUM-8)" (context.md:58). Nothing says they were test files, or that tests stayed green across every fix. Fix the transcript: "One big sweep touched about eighty-five files, and all 2,912 tests still pass." Fix the slide row: "One big sweep | ~85 files, 2,912 / 2,912 tests passing".
6. [major] slides 5, 6, 7, 26, 27 (index.html:363, 385, 405-408, 853, 868): guard, verify, hooks, the HTML report and the code map are all "[Unreleased]" (sources.md:1-5). The published eqc-kit is 0.1.0. The CTA `npx eqc-kit init` only gives people what slides 6-7 promise once the dev branch is published. Outline open question 11 is still open, and the context.md checklist has no publish step. Fix: add a checklist line to context.md: "Publish eqc-kit with guard / verify / hooks / HTML report; confirm `npx eqc-kit init` installs it." If it isn't out by the talk, add "(next release)" to the slide 7 rows for `eqc guard` and `verify` + git hooks.
7. [minor] slide 2 (index.html:301; transcript.md:29-33): the transcript opens with "At QuestionPro, we take engineering quality seriously" and the notes don't. The transcript also scripts "Yes. Very few hands." as a fact. Fix: make that line the first notes line. Change the transcript to "If few hands: Yes. Very few hands. That's the point. If many: Great, then you know how long it takes."
8. [minor] slide 5 (index.html:356, 364-367; transcript.md:81): the slide says "I didn't trust the answers" and the notes skip it. "Tedious" is hard to say for a non-native speaker. Fix: notes line 3 "I was using AI, but it was still too much work, and I didn't trust the answers." Transcript: "It was slow, boring work."
9. [minor] slide 6 (index.html:383, 385): "A MEDIUM-tier agent" and `eqc guard` appear before slide 7 explains them. Fix: "An agent for the MEDIUM rules checks the folders" and "Saved; a guard flags it if it stops passing".
10. [minor] slide 7 (index.html:405): the "Uses AI?" cell "Yes to check, no to count" is cryptic for first-timers. Fix: "Yes (a plain script sets the level)".
11. [minor] slide 10 (transcript.md:220): "It does not." is a stronger claim than the notes' "It isn't tied to it." and pushes against the soft scope. Fix: "You may think eqc-kit only works with the Mobile EQC. It isn't tied to it."
12. [minor] slide 13 (index.html:558; transcript.md:272): the notes say "in a couple of slides" and the transcript says "in a few slides". The payoff is slide 16, three slides on. Fix both: "I'll come back to it on slide 16."
13. [minor] slide 14 (index.html:572, 575): in the footer, "its OK" and "it has to run on opus or sonnet" are unclear. In the table, "The same model" and "Itself" mean the same thing. Fix: footer 'Writing "just go" in the goal doesn't skip the OK. The catch: too much overhead for small tasks, and your main session must run on opus or sonnet.' Use "The same model" in both Who-checks cells.
14. [minor] slides 14, 15 (index.html:583, 605): "just go" comes up four times before the demo (slide 14 footer + notes, slide 15 notes, slide 17). That spoils the slide 17 watch-for and costs time. Fix: drop the sentence "Even if I write 'just go' into the goal, it still stops and waits." from the slide 14 notes and transcript.md:296. Keep the footer.
15. [minor] slide 15 (index.html:602; transcript.md:308): spoken aloud, "The detail is here, not on the slide" makes no sense to the room. Fix: "Five phases. The slide keeps it short; I'll add the detail as I go."
16. [minor] slide 18 (index.html:675, 682, 686; transcript.md:391, 395): "13 of them" could be read as 13 tools. "0 escalations" is jargon. The code map and guard weren't shown, only talked about. Fix: "On my own tools: 13 of the 48 runs (skills, agents, eqc-kit)". "0 escalations (no task needed a bigger model)". Notes: "the guard you heard about earlier". Transcript: "No task had to move to a bigger model."
17. [minor] slide 18 timing (index.html:691-693): ~290 spoken words of content (~2.2 min against the 1.75 content cue), taken out of the 2.5-minute Q&A. Fix: mark the opus dry-run line and the "facts come from a context file" line as CUTTABLE.
18. [minor] slide 18 ↔ context.md:77-83: the notes say "if a slide is wrong, that file is the place to check". But context.md's /orchestrate research still says "Real runs (~11 plan files)" and lacks the 48-run, 8-project, 60/60 and upgrade model-mix facts. Fix: replace context.md:77 with the sources.md:271-275 facts, and keep the ~11-run items labelled as the older sample.
19. [minor] slides 26, 27 (index.html:853, 856, 868; outline.md:669, 685; transcript.md:538): "Too much hassle to check and keep up EQC compliance?" is awkward, drops "Mobile", and ties eqc-kit to EQC right after slide 10 said to bring your own standard. "Five-minute win" reads like an invented number. Fix: "Checking the Mobile EQC, or your own standard, by hand? Try eqc-kit: `npx eqc-kit init`" on both slides and in the outline. Notes and transcript: "/git-commit is the quickest win: start today."
20. [minor] context.md:10, 31: the outcome is stale ("picks 2–3 skills or habits … this week"), and item 9 says "five phases now live in slide 14" and "ship-chain slide (now 19)". Fix: outcome "each listener picks any one tool or idea and tries it, or builds their own". Item 9: "(revision 5: slides 15 and 20)".
21. [minor] outline.md:720 (open question 29): it still says transcript.md needs a 27-slide resync. That's done; only the context.md items in findings 18 and 20 remain. Fix: mark it resolved for the transcript and point it at findings 18 and 20. Point open question 11 at finding 6.

Slide 1: no issues. The hook lands at ~0.5 min, the footer pays off on slide 18, and the transcript matches.
Slide 4: no issues beyond the signposting line in finding 4. The section promise of ~10 min matches the cues on slides 5-10 (10.0).
Slide 16: no issues. The guess-first is placed well, it ties back to slide 14, and the retry ladder is already CUTTABLE.
Slide 25: only finding 4.
Story check: the hook, arc, dividers, recap and single "pick any one" CTA all work. There is an audience moment about every 8-10 minutes (slides 2, 8→9, 16, 21 plus three Q&A buffers). The climax (slide 18) lands at ~64-69% of runtime, a little ahead of the 70-80% guidance. That's fine because the slide also carries Q&A, so no change is needed.

## Timing

| Slide | Planned min | Est. min |
|---|---|---|
| 1 | 0.5 | 0.6 |
| 2 | 1.25 | 1.3 |
| 3 | 1 | 1 (not judged) |
| 4 | 0.25 | 0.25 |
| 5 | 1.25 | 1.25 |
| 6 | 1.5 | 1.9 |
| 7 | 1.75 | 2.9 (3.4 with hooks) |
| 8 | 2.75 | 2.75 (not judged) |
| 9 | 1.75 | 2.2 |
| 10 | 1 | 0.8 |
| 11 | 2 | 2 (Q&A) |
| 12 | 0.25 | 0.3 |
| 13 | 1.5 | 1.1 |
| 14 | 2.75 | 2.6 |
| 15 | 2.5 | 2.1 (2.8 with CUTTABLE) |
| 16 | 2 | 2.1 (2.6 with CUTTABLE) |
| 17 | 1.75 | 1.75 (not judged) |
| 18 | 4.25 | 4.7 (2.2 content + 2.5 Q&A) |
| 19 | 0.25 | 0.25 (not judged) |
| 20 | 1.5 | 1.5 (not judged) |
| 21 | 1.5 | 1.5 (not judged) |
| 22 | 0.75 | 0.75 (not judged) |
| 23 | 1.5 | 1.5 (not judged) |
| 24 | 1 | 1 (not judged) |
| 25 | 0.75 | 0.75 |
| 26 | 0.75 | 0.95 |
| 27 | 2 | 2 (Q&A) |
| **Total** | **40.0** | **~41.7 (~42.9 with every CUTTABLE said)** vs 40-min slot |

Sections: eqc-kit 15.0 planned → ~16.8 est.; /orchestrate 15.0 → ~14.7; ship chain 10.0 → ~10.2. The overall total is within ±10%. The section 1 overrun eats its Q&A buffer, so cut there first (finding 1). If you're still late, cut slide 22 and the slide 15/16 CUTTABLE paragraphs.
