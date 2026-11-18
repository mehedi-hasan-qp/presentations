Verdict: ready after fixes

Scope: focus slides 1, 5, 6, 9, 14, 18, their transitions (1→2, 4→5→6→7, 8→9→10, 13→14→15, 17→18→19) and the matching transcript sections. I judged them against the speaker's intent: slides 6 and 14 are caveman-simple red/green boxes, slide 9 shows only the high points, and slide 18 credits presentation-builder and calls back slide 1. I found no blockers outside the focus.

## Findings

1. [major] slide 18 (index.html:680, :690; transcript.md:412) — The dry-run timing is wrong. The slide says "opus found 15 issues before any real work", and the notes and transcript say it "went through the plan… 13 got fixed before building started". The source says otherwise. In docs/plans/2026-11-16-presentation-skill.md:52, :66 and :69, task 2.2 ran after SKILL.md was built (it depends on 1.1 and 1.2): it used the finished skill to make a sample deck and found 15 skill issues, and wave 3 then applied 13 fixes. — Fix: on the slide, write `Dry-run: opus tested the new skill on a sample deck: 15 issues, 13 fixed`. In the notes and transcript, write "Then an opus dry run used the new skill to make a sample deck. It found fifteen issues, and thirteen got fixed."
2. [major] slide 14 (index.html:569) — "token → opus" is ambiguous. The previous slide says "Main reason: fewer tokens", so a first-time reader will think LLM tokens, not the reset token. The split is also only an example (the notes say so), but nothing on the slide marks it as one. — Fix: `Splits it, e.g. email → haiku · screen → sonnet · auth → opus.`
3. [major] slide 14 transcript (transcript.md:307) — The script still says "The last line is the honest part", but that footer line moved to the notes. It also repeats "Writing 'just go' in the goal does not skip the OK", which was already said at :303. The 2026-11-18 review fixes dropped this repeat from the notes but not from the transcript. — Fix: "One honest note. For a small task, this is too much overhead. Your main session must run on opus or sonnet. On haiku, it stops and asks you to switch. And you still read the report at the end."
4. [major] slide 6 transcript (transcript.md:116) — The script says "The last line is the honest part", but the slide's last line is now "Our app passes this rule." The catch line moved to the notes. — Fix: "One honest note. You need a written standard. The first full check is not cheap. And the agents can still be wrong, so read the evidence."
5. [major] slide 18 timing (transcript.md:400-423) — The non-cuttable speech is about 310 words, which is about 2.4 min against the 1.75 min content cue. That cuts the /orchestrate Q&A from 2.5 to about 1.85 min and pushes the "move on at 30 min" checkpoint. "No task had to move to a bigger model" is said twice (:404 and :410). — Fix: mark the eqc-kit 0.1.0 paragraph CUTTABLE (transcript :404, notes line 3). Drop the first "No task had to move to a bigger model" and keep it only on the presentation-builder line. (best-practices: Timing, "mark… cut if running late")
6. [minor] slide 18 left card (index.html:669-671) — The card title "My skills, agents, and eqc-kit's latest upgrade" sits above "Runs: 48 finished", so it reads as if all 48 runs built those tools. Only 13 did (sources.md, Revision 3 facts). "Mine: 13 of them" is unclear too, because all 48 runs are his. — Fix: title `48 finished runs · 8 projects · ~6 weeks`. Attrs: `Own tools: 13 runs (skills, agents, eqc-kit's latest upgrade)` · `Models: mostly haiku and sonnet`.
7. [minor] slide 18 notes and transcript (index.html:684; transcript.md:400) — "Same for most of my skills and agents" claims a share that no source backs. The sources list only presentation-builder with its agents, /update-presentation, /reflect, /send-pr and /orchestrate's own upgrades. — Fix: "I also built several of my skills and agents with it, like presentation-builder, /reflect and /send-pr."
8. [minor] slide 18 notes — The 2 opus builders in the presentation-builder runs look like they break slide 16's rule (opus only for security or unsplittable work), which invites a Q&A trap. The plan log says opus for 1.2 and 2.2 was set at approval (docs/plans/2026-11-16-presentation-skill.md:56). — Fix: add a notes line: "The 2 opus tasks were ones I asked for at approval; you saw on slide 16 that you can do that."
9. [minor] slide 18 (index.html:679) — "0 escalations" is jargon on the slide for first-timers; only the notes explain it. — Fix: `18 tasks: 6 haiku · 10 sonnet · 2 opus. None moved up a model.`
10. [minor] slide 14 (index.html:568) — In the /goal box, "Keeps going till done." repeats its label "(runs till done)", and the box never says "one model". That is the contrast the plan-mode box shows and the reason /orchestrate exists. — Fix: replace line 2 with `One model builds all.`
11. [minor] slide 6 (index.html:383) — The box label "AI prompting" doesn't match the title, notes and transcript, which all say "AI chat". — Fix: label `AI chat`.
12. [minor] slide 6 (index.html:384) — "Saved. Same answer next time." overclaims. A fresh re-audit is AI again and can differ (the notes admit "agents can still be wrong"). What the sources support is that the saved result is read back (no-arg /eqc-check) and guard flags changes. — Fix: `Saved. Read back next time, not re-guessed.` This matches the notes.
13. [minor] slide 6 (index.html:381) — "god files" is defined only in the notes, which breaks the self-explanatory rule for this audience. — Fix: `The rule (MEDIUM): Folder structure — feature-first, no god files (one huge file that does everything).`
14. [minor] slide 9 (index.html:465) — Card 1 repeats the title word for word ("HARD_FAIL → MEDIUM", "against the Mobile EQC"). — Fix: card `~5 days` / `From HARD_FAIL to MEDIUM` / `27 recorded fixes` (27 milestones, context.md).
15. [minor] slide 9 (index.html:467) — "after the biggest sweep" means nothing on its own, and "sweep" is jargon. — Fix: sub `after one ~85-file fix`.
16. [minor] slide 9 transcript (transcript.md:206-210) — There are about 14 numbers in 40 seconds of speech: hard to follow by ear and hard to say. — Fix: mark the FlatList/Crashlytics line (:208) and the Platform.select sentence CUTTABLE. Keep the ESLint → LOW line and "33 pass, 2 partial, 4 fail".
17. [minor] slide 1 (index.html:290; transcript.md:19) — "Please ignore the small footer for now" works against the plant that slide 18 pays off ("Remember the footer on slide 1?"). — Fix: "Keep this small footer in mind: 'Built with presentation-builder'. I will come back to it on slide eighteen."
18. [minor] slide 5 (index.html:358, :368; transcript.md:85) — The slide says "I didn't trust the answers", but the transcript says "I did not fully trust the answers". The notes say "I was using AI", but the slide says "Then I used AI". — Fix: transcript "Then I used AI. It helped, but it was still too much work, and I did not trust the answers." Notes "Then I used AI. It helped, but…".

Accepted as intended, no change needed:
- Density: slides 5 (~75 words), 9 (~45) and 18 (~85) are over the ~30-word limit, but this fits the speaker's dense, self-explanatory style.
- Slides 6 and 14 are caveman-simple.

Verified against sources:
- Mobile EQC: 39 rules (9/13/17); the folder-structure rule is MEDIUM; our app passes it.
- Our app: ~5 days, 58 Logger files, 2,912/2,912 tests, 54 errors / 30 files, 34 Platform.select, 27 fixes (25/2), 33/2/4, the 4 remaining fails, i18n 7/6.
- Install: MIT, Node 18, 5 tools.
- /orchestrate: security always opus, plus a haiku verifier and a sonnet/opus reviewer; must run on opus or sonnet.
- Run history: 48 runs / 8 projects / ~6 weeks / 13 own; eqc-kit upgrade 1/2/1, 60/60; presentation-builder 3 runs, 18 tasks 6/10/2, 0 escalations; CSS false alarm.

Naming: "eqc-kit" and "the Mobile EQC" are used correctly throughout. Scope stays soft and nothing claims "any project". There are no jokes.

Slide 1: no issues beyond finding 17. The hook lands on slide 2 at ~0.5 min, and the 1→2 transition works.
Slide 5: no issues beyond finding 18. The 4→5 and 5→6 transitions work.
Slide 6: the 6→7 transition works.
Slide 9: the 8→9 guess-first reveal and the 9→10 transition work.
Slide 14: the 13→14 and 14→15 transitions work.
Slide 18: the 17→18 and 18→19 transitions work.

## Timing (focus slides; transcript at ~130 wpm, CUTTABLE excluded)

| Slide | Planned min | Est. min |
|---|---|---|
| 1 | 0.5 | 0.65 |
| 5 | 1.25 | 1.3 |
| 6 | 1.5 | 1.6 |
| 9 | 1.75 | 1.8 |
| 14 | 2.75 | 2.8 (2.6 after finding 3) |
| 18 | 4.25 (1.75 + 2.5 Q&A) | 4.9 (2.4 + 2.5 Q&A), or Q&A shrinks to ~1.85 |
| Focus total | 12.0 | ~13.05 (+1.05) |

The whole deck's planned cues sum to 40.0 min for the 40 min slot. Left as is, the focus slides add about 1 min, mostly on slide 18. Findings 3 and 5 recover about 0.8 min. If the talk is running late, cut the CUTTABLE note blocks on slides 6, 9 and 18 first.
