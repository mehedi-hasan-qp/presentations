# Outline: Ask first, build cheap, ship clean

Backfilled from `index.html`, `context.md` and `transcript.md` on 2026-11-16. **Revision 2 (2026-11-16):** slides made self-explanatory for a first-time audience (one primer slide added, context moved from notes onto slides, terms defined on first use). Revision 2 approved; `## Slides` regenerated for the 31-slide deck. **Review fixes (2026-11-16):** user-approved content/design review fixes applied in `index.html`; Outline table and `## Slides` resynced to `index.html`.

**Revision 3 (2026-11-17, approved by the user 2026-11-17; `## Slides` finalized for the design-creator):** eqc-kit section only (old slides 4-12, 9 slides → new slides 4-10, 7 slides). Denser, self-explanatory slides; plain titles; first-person notes; a new "why I built it" slide; a comparison table (manual / ask AI / eqc-kit) with eqc-kit's cons; eqc-kit dev-branch features (code map, HTML report, baseline + `eqc guard`, optional `verify`, opt-in hooks) from `work/sources.md`; one combined demo (cached /eqc-check, HTML report, /eqc-fix ranked list); saved-plan demo dropped. Section time unchanged (12.25 min incl. 2 min Q&A), total still 40.0 min. Old slides 13-31 become 11-29 (-2), content unchanged except cross-references.

**Revision 4 (2026-11-17, approved by the user 2026-11-17; `## Slides` regenerated for the 26-slide deck):** /orchestrate section only (old slides 11-20, 10 slides → new slides 11-17, 7 slides). Same treatment as revision 3: the speaker's origin story, a comparison table (long prompt / plan mode / /goal / /orchestrate) with honest cons, a dense "what it is like" slide that folds in the 5 phases, scoring updated to the current skill (opus tier for security and unsplittable tasks), and one merged results + reveal + Q&A slide. Jokes dropped, plain titles. Section time unchanged (15.0 min incl. 2.5 min Q&A), total still 40.0 min. Old slides 21-29 become 18-26 (-3), content unchanged except cross-references. In the Outline table, **NEW** / **CHG** tags now mark revision 4 only. User decisions applied at approval: slide 13 `[TBD]` cells filled by the speaker; the /orchestrate "Interviews you first?" cell edited to "Yes (if needed), one question at a time"; slide 17 notes say the runs predate the opus tier; slide 16 PREP and fallback screenshot come from the current skill with one security task; slide 17 overflow rule ("~11 runs" moves to the notes first).

**Review fixes (2026-11-17, user-confirmed; applied in `index.html`, Outline table rows 11-17, Demo 2 and `## Slides` 11-17 resynced):** content-review findings 1-3, 5, 6, 8-13 (`work/reviews/content.md`). Slide 11 sub shortened (14). Slide 12 rows 02 and 03 merged, footer reworded (13). Slide 13 cells shortened, /goal OK cell "No, it starts working right away", /orchestrate OK cell "a hard gate: "just go" in your goal doesn't skip it", cons line lowercase models, one-line h2 (1, 3, 12). Slide 14 retitled "How /orchestrate runs a big task, phase by phase", lead and EXECUTE row no longer contradict (11, 2). Slide 15 retitled "How it picks a model for each task", header "Score or task type", guess-first now "add a config entry with exact steps" (10, 9, 8). Slide 16 demo puts "just go" into the goal and replies "ok, but drop task 3", then rejects (1). Slide 17 card title "Two "done" claims that weren't true", build line ends "(before the opus tier existed)" (5, 6). Finding 7: the "~11 runs" line left slide 17's left card and lives only in its notes. Findings 4 (context.md) fixed outside this file; finding 15 (timing) not applied, cues unchanged.

**Revision 5 (2026-11-18, approved by the user 2026-11-18 with final edits; `## Slides` finalized for the design-creator):** 27 slides (one added). EQC is spelled out ("Engineering Quality Checks") at first use, and the standard is always "the Mobile EQC" (React Native, Flutter, Android, iOS), never "the doc". QuestionPro is named on slides 1 and 2. Slide 4 sub reworded. Slide 6 is now one real rule (Mobile EQC folder structure, MEDIUM) checked by hand / in an AI chat / with eqc-kit. Slide 7 cells are one-liners. Slide 9 says "Compliance level: HARD_FAIL → MEDIUM" against the Mobile EQC. **NEW** slide 10 "Not tied to the Mobile EQC. Bring your own standard." (old 10-26 → 11-27, +1). Slide 14 (old 13) is one "forgot password" task run three ways (plan mode / /goal / /orchestrate); the long-prompt column is gone. Slide 15 (old 14) has one-line phases. Slide 18 (old 17) left card is now what I built with /orchestrate (48 finished runs, sources.md Revision 3 facts). Close is "Pick any one. Try it. Or build your own." (slides 25-27). Every slide trimmed. Timing: slide 6 2.25 → 1.5, slide 7 2 → 1.75, new slide 10 1.0; sections still 15 / 15 / 10, total 40.0 min. In the Outline table, **NEW** / **CHG** tags now mark revision 5 only. The "Revision 4: slide 13 table cells" section below is history (that slide is now 14, with 3 columns).

**Revision 5 final edits (user-approved 2026-11-18):** slide 10 is soft about scope: eqc-kit isn't tied to the Mobile EQC and is built to take your team's own written standard and its tiers; no "any project" / "any stack" claim, no stack list, no mention of what was or wasn't tested; the notes no longer point to an eqc-kit page on writing a standard. Slide 9's transition matches. Open questions 22-28 resolved as drafted: slide 4 sub "Checks every rule in your standard, one by one, and shows the file that proves it"; slide 14 tests stay in the notes only; slide 18 drops the two "done" catches, the CSS false alarm stays in its notes; slide 2 tier counts stay in the notes only; slide 6 AI-chat cells as drafted.

**Review fixes (2026-11-18, user-confirmed; `work/reviews/content.md` findings 1-5, 7-17, 19 partial, 21; Outline table and `## Slides` updated to match):** CUTTABLE notes on slides 6, 7, 9, 18 (1, 17); slide 17 → 18 transition (2); slide 14 header "/goal (runs until done)", footer reworded, "The same model" in both Who-checks cells, /goal defined in the notes, repeated "just go" sentence dropped (3, 13, 14); recap card "Ask first: check every rule, with proof, before you fix" plus "ask first / build cheap / ship clean" lines in the slide 4, 12, 19 notes (4); slide 9 row "One big sweep" (5); slide 2 notes open with the QuestionPro line (7); slide 5 notes trust line (8); slide 6 eqc-kit cells (9); slide 7 "Uses AI?" cell (10); slide 13 "slide 16" pointer (12); slide 15 first notes line (15); slide 18 attrs and notes wording (16); slide 26 notes "quickest win" (19; the "Too much hassle…" line stays as is). Minutes unchanged. Findings 6, 18, 20 (context.md) and 11 (transcript only) handled outside this file.

**Fix (2026-11-18, user-requested; Outline rows 1, 6, 9, 14, 18 and `## Slides` 1, 5 (transition), 6, 9, 14, 18 updated):** slide 6 table → two boxes (light red "AI prompting" vs light green "eqc-kit", vs-grid), short lines, by-hand path and catch line to the notes; slide 9 table → 3 positive highlights (card-grid), the rest to the notes, 58 reveal kept; slide 14 table → three boxes (light red plan mode and /goal, light green /orchestrate), footer detail to the notes; slide 18 right card is now presentation-builder (3 /orchestrate runs, 18 builder tasks 6 haiku / 10 sonnet / 2 opus, 0 escalations, opus dry-run 15 issues / 13 fixed), left card shortened; slide 1 footer "Built with presentation-builder". Same 27 slides, same order, same minutes (40.0).

**Review fixes round 2 (2026-11-18, user-confirmed; Outline rows 6, 9, 14, 18 and `## Slides` 1, 5, 6, 9, 14, 18 updated):** A slide 18 dry-run (opus tested the finished skill on a sample deck; 13 fixed after) · B slide 14 split "e.g. … auth → opus" · E slide 18 eqc-kit 0.1.0 paragraph CUTTABLE, "no task had to move to a bigger model" said once · G slide 18 left card (title = run stats, "Own tools" line; "most of my skills and agents" kept in the notes) · H slide 18 notes: the two opus tasks were asked for at approval · I "0 escalations" → "None moved up a model." · J slide 14 /goal line 2 "One model builds all." · K slide 6 title and notes say "AI prompting" (box label kept) · L slide 6 eqc-kit line 4 · M slide 6 rule line glosses god files · N, O slide 9 cards 1 and 3 · P slide 9 Platform.select and FlatList/Crashlytics lines CUTTABLE · S slide 1 footer line · T slide 5 notes. Layout F, Q, R recorded in the Builder notes on 6, 9, 14. Transcript-only C, D not in this file. Minutes unchanged (40.0).

## Brief

- **Topic:** "Ask first, build cheap, ship clean": my everyday AI workflow (eqc-kit, /orchestrate, the ship chain)
- **Speaker:** Mehedi Hasan, Mobile Team, QuestionPro
- **Audience:** fellow engineers, internal team session / brown-bag. First exposure: they have never seen eqc-kit, /orchestrate, reflect, /git-commit, /send-pr, release-notes or ci-pipeline. Every slide must make sense without the speaker.
- **Desired outcome:** each listener picks any tool or idea and tries it, or builds something of their own
- **Duration:** 40 min (3 sections: 15 / 15 / 10, each ending in a Q&A buffer of 2-2.5 min; cues sum to 40.0 min)
- **Slide count:** 27
- **Template:** default
- **Transcript:** yes (`transcript.md`: human, casual first person; no jokes in the revised sections)
- **Demos:** slide 8 (eqc-kit: cached /eqc-check scorecard, the HTML compliance report, /eqc-fix ranked list), slide 17 (/orchestrate preview gate), slide 23 (v1.9.4 release notes beside git log)

## Narrative arc

- **Hook (slide 2, not an agenda):** "At QuestionPro we take engineering quality seriously", then a show of hands: who has read the whole Mobile EQC (Engineering Quality Checks, 39 rules), and who checked their code against every rule. Slide 1's footer ("Built with presentation-builder") is planted for a later payoff. Slide 3 then gives first-timers the four terms the rest of the talk uses.
- **Problem:** checking 39 Mobile EQC rules by hand never happens (slide 2); I was asked if my projects were compliant and checking by hand, even with AI, was too much (slide 5); I kept typing the same plan-mode instructions (phases, tiered sub-agents, interview me first) for every big task (slide 13).
- **Stakes:** HARD_FAIL compliance; even one rule (folder structure) checked with AI prompting gives "pass" with no proof and can break again later (slide 6); one model builds all of a "forgot password" flow, auth included, and checks its own work (slide 14).
- **Insight:** AI checks each rule with proof, a plain script works out the level, and the guard remembers what passed (slides 6-7); eqc-kit isn't tied to the Mobile EQC: it takes your team's own written standard and uses its tiers (slide 10); a score per task picks the model, security always goes to opus, and the lower tier wins when unsure (slides 14, 16); one piece of writing has four audiences (slide 21).
- **Solution:** eqc-kit (slides 4-10), /orchestrate (slides 12-18), the ship chain (slides 19-24).
- **Proof:** compliance level HARD_FAIL → MEDIUM against the Mobile EQC in about 5 days (slide 9); 48 finished /orchestrate runs across 8 projects, 13 of them on my own skills, agents and eqc-kit's latest upgrade, mostly on haiku / sonnet; presentation-builder in 3 runs, 18 builder tasks, none moved up a model (slide 18); demos on slides 8, 17, 23.
- **Climax:** slide 18, the reveal (this deck was built with presentation-builder, a plugin /orchestrate built), at ~25.75-27.5 min (~64-69% of runtime).
- **Close / CTA (slide 26):** "Pick any one. Try it. Or build your own." (EQC compliance hassle → eqc-kit · big ticket → `/orchestrate` · vague commits → `/git-commit`), each paired with the pain it fixes. Commands stay on screen through the final Q&A (slide 27).

## Outline

| # | Component | Title | Key points | Notes gist | Min |
|---|---|---|---|---|---|
| 1 | title | Ask first, build cheap, ship clean | **CHG** kicker "Mehedi Hasan · Mobile Team · QuestionPro"; subtitle: three tools for checking, planning and shipping code; footer: built with presentation-builder | Intro; **CHG** goal: try one thing or build your own; footer comes back on slide 18 | 0.5 |
| 2 | center | **CHG** 39 rules. Nobody wants to check them by hand. | "At QuestionPro we take engineering quality seriously"; Mobile EQC (Engineering Quality Checks): 39 rules, 3 tiers, React Native / Flutter / Android / iOS; "eqc-kit checks · /orchestrate plans · the ship chain ships" | Opens with the QuestionPro line; show of hands; EQC spelled out; tier counts (9 / 13 / 17) in notes | 1.25 |
| 3 | dtable | A skill is a playbook. Sub-agents are its helpers. | Claude Code: AI coding agent in your terminal; skill (`/name`) = saved playbook, sub-agent = helper given one task; haiku → sonnet → opus = cheapest → priciest model | Primer for first-timers; every tool today is a skill or uses sub-agents | 1 |
| 4 | divider | 01 · eqc-kit | **CHG** sub: "Checks every rule in your standard, one by one, and shows the file that proves it" | ~10 min then Q&A; "ask first" signpost | 0.25 |
| 5 | steps-list | How I ended up building eqc-kit | **CHG** 4 short rows: handed the Mobile EQC → checked by hand → AI, still too much → automated it (hi); install line + 5 tools | Speaker's story; "not tied to the Mobile EQC" saved for slide 10; one-command install | 1.25 |
| 6 | vs-grid | **CHG** One Mobile EQC rule: AI prompting vs eqc-kit | Rule: MEDIUM, folder structure, "feature-first, no god files (one huge file that does everything)"; light red box "AI prompting": says pass, no proof, new answer each time · light green box (hi) "eqc-kit": checks the folders, pass + the files, saved and read back next time; "our app passes" | By hand, RN folder list (cuttable), my AI-prompting pains and the honest catch in the notes | 1.5 |
| 7 | dtable | What you run, and where AI is used | **CHG** one-line "What it does" per command: `/eqc-check` · `/eqc-fix` · `eqc guard` · `verify` + hooks; short "Uses AI?" column ("Yes (a plain script sets the level)" for `/eqc-check`) | Detail (code map, level script, HTML report, baseline) in the notes; code-map, second half of verify and hooks paragraphs cuttable | 1.75 |
| 8 | demo | Demo: check, report, and what to fix next | **CHG** shorter step-descs: 01 cached `/eqc-check` (hi) · 02 `COMPLIANCE.html` · 03 `/eqc-fix` ranked list | 3-part demo; FALLBACK per part; guess-first on Logger file count | 2.75 |
| 9 | card-grid | **CHG** Our mobile app against the Mobile EQC: Compliance level: HARD_FAIL → MEDIUM | 3 positive cards: ~5 days (from HARD_FAIL to MEDIUM, 27 recorded fixes) · 58 files to our Logger (hi) · 2,912 / 2,912 tests passing (after one ~85-file fix); one-line level definitions | Reveal 58; ESLint, `Platform.select()` (cuttable), FlatList / Crashlytics (cuttable), today 33 / 2 / 4, the 4 still failing, i18n story (cuttable) and the secret in the notes | 1.75 |
| 10 | steps-list | **NEW** Not tied to the Mobile EQC. Bring your own standard. | Bring your team's written standard → eqc-kit reads it and lists every rule in your tiers (LOW/MEDIUM/HIGH, Bronze/Silver/Gold) → same check, report and fixes (hi) | eqc-kit is the tool, the standard is yours; built to adapt to your standard and tiers; it needs a written standard | 1 |
| 11 | center | Questions? (eqc-kit) | Q&A buffer | Seeds; move on at 15 min | 2 |
| 12 | divider | 02 · /orchestrate | sub: "Plans big work with you, then sends each task to the cheapest model that can do it" | Separate tool, ~12 min then questions; "build cheap" signpost | 0.25 |
| 13 | steps-list | Why I built /orchestrate | **CHG** 3 shorter rows: kept going back to plan mode → typed the same asks every time → made it a skill (hi); footer: main reason, fewer tokens | Speaker's origin story; no token number | 1.5 |
| 14 | vs-grid | **CHG** One "forgot password" task, three ways to run it | Lead: endpoint, reset email, reset screen, tests; it touches auth; light red boxes "Plan mode" and "/goal (runs till done)": one model builds all, checks itself · light green box (hi) "/orchestrate": asks first, splits (e.g. email → haiku · screen → sonnet · auth → opus), waits for your OK, another agent checks | /goal defined in one line; the split is an example, not a captured run; security is always opus; "just go" doesn't skip the OK, the catch, and "next big task" in the notes | 2.75 |
| 15 | dtable | How /orchestrate runs a big task, phase by phase | **CHG** lead: the orchestrator plans and checks, helpers write the code; 5 one-line rows: GRILL · PLAN · PREVIEW (the gate) · EXECUTE / VERIFY · CLOSE | Detail (fast lane, 3 helpers, file owners, "ok, but…", ≤5-line fix, reviewers, resume) in the notes; shortcuts paragraph cuttable | 2.5 |
| 16 | dtable | How it picks a model for each task | **CHG** shorter lead; 0–2 haiku · 3–4 sonnet · 5–6 split first, opus if it can't be split · security always opus; pick-lower quote; one-line "if a task fails" | Guess-first "add a config entry with exact steps" → haiku; ties back to slide 14; opus requests and retry ladder in the notes | 2 |
| 17 | demo | Demo: the preview gate | 01 paused at PREVIEW, "just go" written into the goal · 02 reply "ok, but drop task 3" (hi); watch-for: "just go" in the goal didn't skip the gate | Pre-staged run with one security task; reject at the end; never type a bare "go" / "just go" at the prompt | 1.75 |
| 18 | vs-grid | **CHG** What I've built with /orchestrate | **CHG** left (short): title "48 finished runs · 8 projects · ~6 weeks"; own tools: 13 runs (skills, agents, eqc-kit's latest upgrade); mostly haiku / sonnet · right (hi, same shape) "This deck · built with /orchestrate": title "presentation-builder, a Claude Code plugin"; 2 skills (new deck · change one); 6 agents, one job each; closing line "Questions?" | Slide 1 payoff (footer callback spoken); what the plugin is; build facts in notes only (3 runs, 18 tasks, none moved up a model, dry-run 15 issues / 13 fixed); the 2 opus tasks were asked for at approval; eqc-kit 0.1.0 predates /orchestrate (cuttable); verifier false alarm (honest limit); context-file line cuttable; Q&A seed; content ~1.75 + Q&A 2.5 | 4.25 |
| 19 | divider | 03 · The ship chain | sub: "After the code works: commit, PR, release notes, build" | Lighter section; value is in the connection; "ship clean" signpost | 0.25 |
| 20 | steps-list | Each skill feeds the next | 01-05: /reflect, /git-commit (hi, "start here"), /send-pr, /release-notes, ci-pipeline | What each step does; /git-commit is the cheapest start | 1.5 |
| 21 | dtable | One change, four write-ups, four readers | Commit: devs + testers; PR: reviewers; Release notes: managers; Store note: users; "Written by" column | Guess-first: who reads your commits; cut-path refs → slides 22/23 | 1.5 |
| 22 | code-block | Commits are written for the release notes | git-commit: "raw material for release notes"; release-notes: "don't trust commit messages alone" | Cuttable; two halves of a contract | 0.75 |
| 23 | demo | Demo: v1.9.4 notes beside their commits | Step-descs; code block "One change, three write-ups"; watch-for line | Match a commit to its sentence; read the store note | 1.5 |
| 24 | center | No release notes, no build | CI fails if `RELEASE_NOTES_v<version>.md` is missing; staging and production copy the store note from it | Enforced, not recommended | 1 |
| 25 | card-grid | Ask first, build cheap, ship clean (recap) | eqc-kit (Ask first: check every rule, with proof, before you fix; sub "checks your code, keeps passing rules passing"); /orchestrate (Build cheap); ship chain (hi, Ship clean) | One sentence per section; **CHG** "Pick any one" | 0.75 |
| 26 | closing | **CHG** Pick any one. Try it. Or build your own. | **CHG** pain + command: EQC compliance hassle → eqc-kit · big ticket → `/orchestrate` · vague commits → `/git-commit`; install line | Match a tool to your pain, or build your own; install line is a prompt | 0.75 |
| 27 | center | Questions? (final) | **CHG** mirrors slide 26 (pain + command) + install line on screen | Open floor; "Which one are you trying first?" | 2 |

Total: 40.0 min (40 min slot). Sections: eqc-kit 15.0 (slides 1-11) · /orchestrate 15.0 (12-18: content 12.5 + Q&A 2.5 inside slide 18) · ship chain 10.0 (19-27). Rows: 27 (matches slide count).

**REMOVED / MOVED (revision 5, old numbers):** old 6's 5-row table (trust "pass" · every rule covered · same answer twice · stays fixed · cost) → new 6 one-rule table, the AI-chat pains move to its notes · old 2's tier counts (9 / 13 / 17) → slide 2 notes · old 7's long cells (code map, level script, MD + HTML report, baseline) → slide 7 notes · old 9's architecture details (123-file state migration, data-fetching library, certificate pinning) → slide 9 notes · old 13's "Long prompt every time" column and 6-row table → new 14, 3 columns × 4 rows on one example task · old 14's long phase cells → slide 15 notes · old 15's opus-request line → slide 16 notes · old 17's left card "Two "done" claims that weren't true" (~65 identifiers, line 143) and the "~11 runs" notes line → dropped, replaced by the 48-run stats; the CSS false alarm stays in the slide 18 notes as the honest limit.

**REMOVED (revision 4, old numbers):** 12 center "One expensive model. One long session. Nobody checked." (→ new 12 origin story + new 13 comparison) · 13 steps-list "Five phases, two hard stops" (→ new 14 lead + rows) · 16 dtable "Every reasonable-sounding shortcut is banned" (→ new 14 notes) · 18 card-grid "~11 real runs…" (→ new 17 left card; disk-full joke dropped; 15-issue dry-run → notes) · 20 center "Questions? (/orchestrate)" (→ new 17 closing line + notes). Old 19 "This deck was built by a skill…" → new 17 right card. Old 21-29 → new 18-26 (-3), content unchanged except cross-references. Corrected against the current skill (sources.md, 2026-11-17): security is now always opus (was "≥ sonnet"); 5-6 is split first, opus if unsplittable; escalation ladder wording updated.

### Revision 4: slide 13 table cells (approved 2026-11-17)

Long prompt, plan mode and /goal cells are the speaker's confirmed gaps (sources.md, speaker interview; the former `[TBD]` cells were filled by the speaker at approval). The /orchestrate "Interviews you first?" cell is the speaker's edit (the fast lane skips the interview for tiny goals).

| Question | Long prompt every time | Plan mode | /goal | /orchestrate (acc) |
|---|---|---|---|---|
| Remembers the instructions? | No, you retype or paste them | No, you retype the phase, sub-agent, model and interview asks | No, it keeps the goal, not your method | Yes, it's a skill |
| Interviews you first? | Only if you type that in | Only if you ask, every time | No, it just starts working | Yes (if needed), one question at a time |
| Stops for your OK before building? | No, it starts editing | Yes, once, for the whole plan | No per-task approval gate | Yes, a hard gate on the full plan; "just go" doesn't count |
| Picks a model per task? | No, same model for everything | No, one model builds it all | No | Yes, by score: haiku, sonnet or opus |
| Who checks the work? | Nothing enforces the rules | The same model that built it | It checks itself | A separate haiku verifier, plus sonnet or opus reviewers |
| Picks up after a break? | No, forgets between sessions | No, the plan lives in the chat | Only within the session | Yes, from the plan file (`/orchestrate resume`) |

Cons line under the table: "The catch: the planning and checking add overhead that isn't worth it on small tasks, the orchestrator itself has to run on Opus or Sonnet, and you still read the report."

Superseded by the 2026-11-17 review fixes (findings 1, 3, 12): plan mode row 1 "No, you retype your asks"; /goal OK cell "No, it starts working right away"; /orchestrate OK cell "Yes, a hard gate: "just go" in your goal doesn't skip it"; long prompt "Who checks" "Nobody, unless you do"; cons line "…it has to run on opus or sonnet (it stops on haiku)…". `## Slides` slide 13 is current.

**REMOVED (revision 3, old numbers):** 5 flow "Bring your standard, get a compliance level" (install + tools → new 5; flow → new 7) · 6 steps-list "/eqc-check: agents judge, the engine counts" (→ new 7) · 7 demo "the free scorecard" (→ new 8, step 01) · 8 vs-grid "/eqc-fix: small fixes go straight…" (→ new 7 row + notes) · 9 demo "ranked fixes and a chunked plan" (ranked list → new 8 step 03; MEDIUM-10 saved-plan demo dropped) · 11 card-grid "4 fails left…" (fails → new 9 row; guardrails → new 7; unsourced "40 seconds" line dropped; "gate" → `guard`; "each rule gets a verify command" corrected).

### Revision 2: on-slide changes

Historical record of the revision 2 proposal, in pre-revision-3 numbering. Items 4-12 are superseded by revision 3. Where the 2026-11-16 review fixes differ, `## Slides` (synced to `index.html`) wins. Proposed on-slide copy for every revision 2 **NEW** / **CHG** row (old number in brackets). Unchanged: slide 22. Facts come only from `context.md`, the deck and the transcript; general glosses (Claude Code, skill, sub-agent, Conventional Commit, E2E) are definitions, not claims.

- **1 [1] CHG:** subtitle "My everyday AI workflow: three tools for checking, planning and shipping code."
- **2 [2] CHG:** body "Our quality standard: 39 rules in 3 tiers (9 LOW, 13 MEDIUM, 17 HIGH)." New second line: "Today: one tool each for checking, planning and shipping."
- **3 [new] NEW (dtable):** kicker "Before we start · 4 terms". Title "A skill is a playbook. / Sub-agents run it." Table `Term | What it means`: Claude Code | An AI coding agent that runs in your terminal · Skill (`/name`) | A saved playbook you run by name, e.g. `/git-commit` · Sub-agent | A helper the main session hands one task to · haiku · sonnet · opus | Claude models: cheap and fast → mid → biggest and priciest. Notes: everything today is a skill or a set of sub-agents; eqc-kit also works in 4 other tools.
- **4 [3] CHG:** sub "Checks your code against your team's own quality standard".
- **5 [4] CHG:** lead "An open-source (MIT) npm package: AI agents audit your code against your own written standard." Flow: Your standard → Rule list → Code audit → Level (on, badge "Output") → Fixes. Footer "`npx eqc-kit init` · works in Claude Code + 4 other AI coding tools". 1.5 → 1.25 min.
- **6 [5] CHG:** step-descs: 01 Index agent — Reads your doc, lists every rule by tier · 02 Audit agents — One per tier, in parallel, reading your code · 03 Verdict + evidence — pass / partial / fail / n/a, each with file proof · 04 Engine does the maths (hi) — Plain script, no AI. Level = highest tier with no fails.
- **7 [6] CHG:** lead "No arguments = re-read the last audit: level per tier, every open fail with its evidence." Watch-for line kept.
- **8 [7] CHG:** lead "Starts with the 10 easiest fails. Never commits for you." Small card: Who: one fixer agent, one pass · Then: re-audit, log a milestone (one recorded fix). Medium / large (hi): First: opus writes a plan, read-only · You: approve the plan · Then: chunks (small steps) run on haiku or sonnet. 1.5 → 1.25 min (model gloss now on slide 3).
- **9 [8] CHG:** 01 Run /eqc-fix (hi) — The top 10, easiest first · 02 Open a saved plan — Rule MEDIUM-10: 34 `Platform.OS` checks → `Platform.select()`, in chunks. Add "Watch for: which model each chunk gets, and where it stops to ask."
- **10 [9] CHG:** lead "Our mobile app, ~5 days. HARD_FAIL = a lowest-tier rule fails. MEDIUM = no fails in LOW or MEDIUM." Table unchanged.
- **11 [10] CHG:** cards (slash / name / sub): 4 fails / Big architectural moves / e.g. a 123-file state migration · TypeScript (hi) / Honest "can't pass" / project mandates JavaScript · no LLM / Not in pre-commit / slow, costly, nondeterministic.
- **12 [11] CHG:** copy unchanged; Q&A buffer 2.5 → 2 min.
- **13 [12] CHG:** sub "For work too big for one prompt: you plan and approve, cheaper models build".
- **14 [13] CHG:** first line trimmed to "It guesses at scope, edits as it goes, then says it's done." New second line: "/orchestrate: a skill that plans first, waits for your OK, then hands each task to a cheaper model."
- **15 [14] CHG (flow → steps-list):** 01 GRILL — Questions one at a time; you lock the answers · 02 PLAN — Goal split into tasks, each scored · 03 PREVIEW gate (hi) — Nothing runs until you approve · 04 EXECUTE / VERIFY — Sub-agents build, a verifier checks · 05 CLOSE — Reports the model mix; never commits. 1.5 → 1.75 min.
- **16 [15] CHG:** lead "Each task scores 0–2 on Ambiguity (how unclear), Breadth (how wide), Reasoning (how hard). The total picks the model." Row 5–6 → "Too big: split it first". Notes: guess-first asks "which model".
- **17 [16] CHG:** 01 Paused at PREVIEW — Every task with its score and model; nothing has run · 02 Type "just go" (hi) — Only approve, edit or reject count. Watch-for kept.
- **18 [17] CHG:** lead "Rules the orchestrator must follow, even when a shortcut sounds fine." Headers "Tempting thought | What it does instead"; right column: Delegate it · Show the preview · Let the verifier run them.
- **19 [18] CHG:** lead "Verifier: a separate cheap agent that re-checks every 'done' claim." Left labels "Test-coverage audit: done" · "E2E (end-to-end) test: line 143 covered". Right side unchanged.
- **20 [19] CHG:** card-subs: retries — Failures retried on the same model, rarely moved up · 15 — Issues one opus dry-run (a trial run) found in a new skill · ENOSPC — Disk full: one wave, 3 agents, zero bytes. haiku / sonnet card unchanged.
- **21 [20] CHG:** line "/create-presentation is the skill that built these slides. /orchestrate built it: 5 tasks + 2 fixes, 0 escalations (no task needed a bigger model)."
- **23 [22] CHG:** sub "After the code works: commit, PR, release notes, build".
- **24 [23] CHG (flow → steps-list, kicker "Ship chain · 4 skills + our CI"):** 01 reflect — Session end: updates CLAUDE.md and docs · 02 /git-commit · start here (hi) — Conventional Commit (`type(scope): summary`); you confirm · 03 /send-pr — Writes the PR title and body · 04 release-notes — Commits + diffs → release notes file · 05 ci-pipeline — Our CI: builds and ships from that file. 1.25 → 1.5 min.
- **25 [24] CHG:** add column "Written by": /git-commit · /send-pr · release-notes · release-notes (CI copies it). Commit row "Developers + testers (dev-build tester note)".
- **26 [25] CHG:** code head "Quoted from each skill's instruction file (SKILL.md)". 1 → 0.75 min.
- **27 [26] CHG:** 01 Open RELEASE_NOTES_v1.9.4.md (hi) — Written by release-notes; ends with the store note · 02 Put `git log` beside it — Match one commit to its sentence. Add "Watch for: one commit line becoming a sentence a manager or user can read."
- **28 [27] CHG:** add line "Staging and production builds copy the store note from this file."
- **29 [28] CHG:** card-subs: eqc-kit — checks code against your standard · /orchestrate — plans, then cheaper models build · ship chain — commit → PR → notes → build.
- **30 [29] CHG:** commands line becomes "Quality doc nobody checks? `npx eqc-kit init` · Big ticket? `/orchestrate` · Vague commits? `/git-commit` today". Install line unchanged.
- **31 [30] CHG:** mirror slide 30's two lines.

## Demo plan

Revision 5 numbering. The eqc-kit section has one combined demo (slide 8); the /orchestrate demo is slide 17, the release-notes demo slide 23. Demo content unchanged from revision 4.

### Demo 1 (slide 8): check, report, and what to fix next, ~2.75 min
PREP: dev eqc-kit installed in our mobile app repo; full /eqc-check re-run before the talk so `docs/eqc/COMPLIANCE.html` exists and the numbers match slide 9; browser tab with the HTML page already open.
Watch for: the first part is instant (no agents); the report is one page you just open; the fix list starts with the cheap wins.
1. Switch to the terminal in our mobile app repo.
2. Type /eqc-check with no arguments and press Enter.
3. Point at the level: "hold that number, it's on the next slide". Read one fail's evidence line out loud.
4. Switch to the browser tab with docs/eqc/COMPLIANCE.html. Scroll once: level and tier progress at the top, then what needs attention, then every rule by tier.
5. Back in the terminal, run /eqc-fix. If the ranked list hasn't appeared in ~30 s, cancel and show FALLBACK (part 3).
6. Read the top three suggestions and why they're low effort, high gain. Cancel at the prompt. No fixes live today.
7. Switch back to the slides.
FALLBACK (part 1): screenshot ./screenshots/eqc-check-scorecard.png — "Here's the same scorecard from this morning; the live one says the same thing."
FALLBACK (part 2): screenshot ./screenshots/eqc-compliance-report.png — "This is the page it writes next to the Markdown report; it's just a file, no setup."
FALLBACK (part 3): screenshot ./screenshots/eqc-fix-ranked.png — "Here's the ranked list from my last run; same output, no waiting."

### Demo 2 (slide 17): the preview gate, ~1.75 min
PREP: before the talk, on the current skill (with the opus tier), run `/orchestrate <small goal with one security task>, just go` on opus or sonnet, answer GRILL, and stop at PREVIEW. The preview should print a line saying approval in the goal was ignored. Leave that terminal paused at "Approve, edit, or reject?". Don't approve. Capture ./screenshots/orchestrate-preview.png from this run. Check the behaviour in rehearsal.
Watch for: "just go" in the goal didn't skip the gate.
1. Switch to the pre-staged terminal.
2. Walk the task table (task, score, tier) and point at the Tier column: the opus row carries its reason, e.g. `opus (security: <surface>)`. Read the "Mix" line.
3. Point at the line saying "just go" in the goal was ignored, then at the prompt: "Approve, edit, or reject?"
4. Reply "ok, but drop task 3". That counts as an edit: show the re-preview with the plan changed. Never type a bare "go" or "just go" at the prompt: that approves.
5. Reject, and switch back to the slides.
FALLBACK: screenshot ./screenshots/orchestrate-preview.png, recaptured from the PREP run on the current skill (not the README's illustrative preview) — "Here's the preview from a real run; the bit to notice is that 'just go' in the goal didn't skip the gate."

### Demo 3 (slide 23): v1.9.4 notes beside their commits, ~1.5 min
The code block on screen is the example: one real change in three write-ups. The live demo shows it side by side.
Watch for: one commit line turning into a sentence a manager or a user can read.
1. Open docs/RELEASE_NOTES_v1.9.4.md in the editor, left pane.
2. In the right pane, run git log for the v1.9.4 range.
3. Pick one commit and find where it shows up in the notes.
4. Scroll to the App Store / Play Store release-note block and read it out loud.
5. Switch back to the slides.
FALLBACK: screenshot ./screenshots/release-notes-v1.9.4.png — "Here are the two side by side; same commit, two very different audiences."

## Engagement suggestions

Items 1-7 already applied in the deck (accepted suggestions recorded in `context.md`). Slide numbers updated for revision 5 (27 slides). Items 2 and 8 updated for revision 5.

1. **What:** retitle to "Ask first, build cheap, ship clean". **Why:** title matches the three-part workflow; the close now asks for "pick any one, or build your own", which the title doesn't contradict. **Where:** 1, 25.
2. **What:** keep internal names off slides ("our mobile app"), except QuestionPro on slides 1-2 and the Mobile EQC by name (speaker decision, revision 5); no project or repo names on slide 18. **Why:** internal detail lives in the notes. **Where:** all, esp. 5, 9, 18.
3. **What:** a "guess first" audience moment per section. **Why:** interaction every ~8-10 min. **Where:** 8→9 (Logger file count), 16 ("add a config entry with exact steps" model), 21 (who reads commits); plus show of hands on 2.
4. **What:** demo prep: re-run /eqc-check and capture a screenshot fallback for every demo part. **Why:** slides 8 and 9 must agree; demos can break. **Where:** 8, 9, 17, 23.
5. **What:** intentional honest limits. **Why:** engineers trust stated failure modes. **Where:** 6 (eqc-kit catch, in notes), 9 (the 4 still failing, in notes), 14 (/orchestrate catch, in notes), 18 (verifiers fail too, in notes).
6. **What:** slide 1 footer foreshadows the reveal. **Why:** setup and payoff. **Where:** 1, 18.
7. **What:** mark cuttable content in notes. **Why:** recover time if running late. **Where:** 22, the folder-list paragraph in slide 6's notes, the code-map, second-half-of-verify and hooks paragraphs in slide 7's notes, the i18n story in slide 9's notes, the context-file line in slide 18's notes, the banned-shortcuts paragraph in slide 15's notes, the retry-ladder paragraph in slide 16's notes.
8. **What:** self-explanatory slides for a first-time audience: a 4-term primer, a "what it is" line on each divider and intro slide, terms defined on first use (EQC = Engineering Quality Checks); one real example per comparison (one Mobile EQC rule on 6, one "forgot password" task on 14); short one-line cells, detail in the notes, plain titles, no jokes, casual first-person notes. **Why:** nobody has seen these tools; the speaker wants the deck to work without narration and to be easy to read at a glance. **Where:** 2, 3, 4-10, 12-18, 19, 20.

## Slides

Revision 5, 27 slides (2026-11-18, approved with final edits; slide 10 and slide 9's transition refreshed). Changed in revision 5: 1, 2, 4-10 (10 is new), 13-16, 18, 25-27; the rest (3, 11, 12, 17, 19-24) keep their copy and change only in numbering and cross-references. `(hi)` = `.hi` / `.on` emphasis; ` / ` (with spaces) in a title = line break before the `.accent` part; a slash command keeps its slash. Notes lines are separate lines in `<aside class="notes">`. dtable has no row highlight: its one emphasis is `th.acc`. A "Builder note" is for the design-creator, not for `<aside class="notes">`.

### Slide 1 — Ask first, build cheap, ship clean (title)
On-slide copy:
- Kicker: Mehedi Hasan · Mobile Team · QuestionPro
- Ask first, build cheap, / ship clean
- My everyday AI workflow: three tools for checking, planning and shipping code.
- Built with presentation-builder — more on that later.

Speaker notes:
Hi, I'm Mehedi, from the Mobile Team here at QuestionPro. This is the AI workflow I actually use every day.
Three tools: one checks code, one plans work, one chain ships it. Each one stands on its own.
Goal: you leave with one thing to try, or an idea for something of your own.
Keep this small footer in mind: 'Built with presentation-builder'. I'll come back to it on slide eighteen.
Transition: "Let's start with a standard most of us have never read to the end."
~0.5 min

### Slide 2 — 39 rules. Nobody wants to check them by hand. (center)
On-slide copy:
- Kicker: The problem
- 39 rules. / Nobody wants to check them by hand.
- At QuestionPro we take engineering quality seriously. Our Mobile EQC (Engineering Quality Checks) has 39 rules in 3 tiers, for React Native, Flutter, Android and iOS.
- Today: eqc-kit checks · /orchestrate plans · the ship chain ships.

Speaker notes:
At QuestionPro, we take engineering quality seriously.
Show of hands: who has read the whole Mobile EQC, end to end? Keep your hand up if you checked your own code against every rule.
(Expect very few hands. That's the point.)
EQC stands for Engineering Quality Checks. The Mobile EQC is our standard for mobile apps: React Native, Flutter, Android and iOS. 39 rules in three tiers: 9 LOW, 13 MEDIUM, 17 HIGH.
The standard is good. The problem is that checking 39 rules across a whole app by hand is slow, boring work, so it doesn't happen.
Each part today is something I used to skip: checking, planning, writing it up.
Transition: "Before the tools, four words you'll hear all talk."
~1.25 min

### Slide 3 — A skill is a playbook. Sub-agents are its helpers. (dtable)
On-slide copy:
- Kicker: Before we start · 4 terms
- A skill is a playbook. / Sub-agents are its helpers.
- Table Term | What it means:
  - Claude Code | An AI coding agent that runs in your terminal
  - Skill (`/name`) | A saved playbook you run by name, e.g. `/git-commit`
  - Sub-agent | A helper the main session hands one task to
  - haiku · sonnet · opus | Claude models: cheap and fast → mid → biggest and priciest

Speaker notes:
Quick primer, because none of these tools have come up here before.
Claude Code is where I run all of this: an AI coding agent in the terminal.
A skill is a saved set of instructions. You type its name with a slash and it follows the playbook, the same way every time.
A sub-agent is a helper: the main session hands it one task and gets a short report back.
haiku, sonnet, opus: three model sizes. Keep the order in mind; a lot of today is about sending work to the cheapest one that can do it.
Everything you'll see is a skill, a set of sub-agents, or both. eqc-kit also works in four other AI coding tools, so you don't need Claude Code for that one.
Transition: "With those four words, section one."
~1 min

### Slide 4 — 01 · eqc-kit (divider)
On-slide copy:
- 01 · eqc-kit
- Checks every rule in your standard, one by one, and shows the file that proves it

Speaker notes:
Section one: eqc-kit. About 10 minutes, then questions.
This is the "ask first" part: ask the standard before you change code.
This is the one I built myself, so I'll start with how that happened.
Transition: "It started with one question."
~0.25 min

### Slide 5 — How I ended up building eqc-kit (steps-list)
On-slide copy:
- Kicker: eqc-kit · Why I built it
- How I ended up / building eqc-kit
- 01 I was handed the Mobile EQC — And one question: are your projects compliant?
- 02 I checked it by hand — Rule by rule, through the whole project. Slow, boring work.
- 03 Then I used AI — It helped, but it was still too much work, and I didn't trust the answers.
- 04 So I automated it (hi) — Now it's eqc-kit: an open-source (MIT) npm package.
- `npx eqc-kit init` · works in Claude Code, Codex, Cursor, Copilot and Gemini CLI

Speaker notes:
Quick story. I was given our Mobile EQC and asked if my projects were compliant.
I went through the standard and checked it rule by rule against the project. It was slow, boring work.
Then I used AI. It helped, but it was still too much work, and I didn't trust the answers.
So I started to automate the process. One thing led to another, and now I have eqc-kit.
It's not tied to the Mobile EQC. I'll come back to that just before questions.
Install is one command. The setup asks a few questions, and they all have defaults, so you can just keep pressing Enter. No dependencies, Node 18 or newer.
In Claude Code you get slash commands. In the other tools it adds a block to AGENTS.md, so you just say "eqc check".
Transition: "Here's what checking one rule looks like: with AI prompting, and with eqc-kit."
~1.25 min

### Slide 6 — One Mobile EQC rule: AI prompting vs eqc-kit (vs-grid)
On-slide copy:
- Kicker: eqc-kit · One rule, two ways
- One Mobile EQC rule: / AI prompting vs eqc-kit
- Lead: The rule (MEDIUM): Folder structure — feature-first, no god files (one huge file that does everything).
- Left box (light red): label "AI prompting" (paste the standard into an AI chat, ask)
  - Ask AI.
  - AI says pass.
  - No proof.
  - Ask again: new answer.
- Right box (light green, hi): label "eqc-kit"
  - Reads the rule.
  - Checks the folders.
  - Says pass + shows the files.
  - Saved. Read back next time, not re-guessed.
- Our app passes this rule.

Builder note: two vs-card style boxes, light red fill for the "without" box (AI prompting) and light green for the eqc-kit box. Label + 4 short lines each (plain `.vs-attr` lines, no `<strong>` attribute names); no `.vs-card-title` needed. The fills and `.vs-card-label` at 0.95rem are inline styles in this deck only; template unchanged (Open question 30).

Speaker notes:
Let's make it concrete with one real rule from the Mobile EQC. MEDIUM tier: folder structure, feature-first, no god files. No single huge file that does everything.
CUTTABLE if running late — The rule lists the folders per stack. For React Native that's src/screens, src/features, src/components and src/navigation. Flutter, Android and iOS each get their own layout.
By hand you'd find the rule, walk every folder, look for huge files. It works if you're careful. Then you do it again next time, plus the other 38 rules.
The red box is AI prompting, what I tried next: paste the standard into the AI and ask. Here's what actually happened to me. It explored from scratch every time, it lost track, it said pass when it wasn't, and asking twice gave a different answer. And later, while working on a new feature, the AI would break the same rule again.
The green box is eqc-kit. The rule is already on its list, a MEDIUM-tier agent checks the folders, and "pass" comes with the files that prove it. You can open them and argue with it. It's saved, so next time it's re-read, not re-guessed, and guard warns you if the rule stops passing.
Our app passes this one.
The honest part: eqc-kit needs a written standard, the first full check costs time and tokens, and the agents can still be wrong, so read the evidence.
Transition: "So what do you actually run?"
~1.5 min

### Slide 7 — What you run, and where AI is used (dtable)
On-slide copy:
- Kicker: eqc-kit · The commands
- What you run, / and where AI is used
- Table Command | What it does (acc) | Uses AI?:
  - `/eqc-check` | Checks every rule, with the file as proof | Yes (a plain script sets the level)
  - `/eqc-fix` | Suggests fixes, easiest wins first | Yes
  - `eqc guard` | Fails if a rule that passed stops passing | No
  - `verify` + git hooks | Optional: runs a command like `npm run lint` on commit | No

Speaker notes:
Four things you run. The top two use AI, the bottom two don't.
/eqc-check: the first time, one agent reads your standard and lists every rule by tier. Then one agent per tier goes through the code, in parallel. Each rule gets pass, partial, fail or not applicable, with the file as proof.
CUTTABLE: If you already have a code map, like a graphify graph, it looks there first, but only if the map is newer than your last commit and your uncommitted changes. It never builds or refreshes the map for you, and anything it finds there it confirms in the real code.
Then a plain script, no AI, works out the level: the highest tier where that tier and every tier below it have no fails. A fail in the lowest tier is HARD_FAIL. The script never reads your code; it just counts the answers.
It writes the report as Markdown, and next to it an HTML page. One file, no JavaScript, you just open it in the browser.
/eqc-fix: it ranks what to fix, low effort and high gain first. Small stuff goes to one fixer. Bigger stuff: opus writes a plan, you approve it, and cheaper models do the typing. It asks before touching CI, packages, architecture or the top tier, it only runs one fixer at a time, and it never commits for you.
guard: this is the answer to "AI fixed it, then broke it again". Every time results are saved, it remembers which rules passed. That's the baseline, and it only goes up. Guard fails if one of those rules stops passing, or the level drops. A rule that was already failing won't block you.
verify: some rules a plain command can check, like "lint is clean". Those rules carry a command, like npm run lint.
CUTTABLE: Not every rule gets one, only the ones a command can check without judgment. The script runs them only for rules that are passing, so a known fail never blocks a commit; only a regression does.
CUTTABLE if running late — hooks: opt-in, one command per clone, npx eqc-kit hooks. Commit runs verify; push runs verify, then guard. It won't override hooks you already have, like Husky; it prints the lines to add instead. Anyone can skip hooks with --no-verify, so put the same two commands in CI.
Why no AI in the hooks? Too slow, costs money on every commit, and you'd get a different answer each time.
Transition: "Let me show you two of these, and the report it writes, on our app."
~1.75 min

### Slide 8 — Demo: check, report, and what to fix next (demo)
On-slide copy:
- Badge: Live demo
- Kicker: Demo · /eqc-check · the report · /eqc-fix
- Demo: check, report, / and what to fix next
- 01 `/eqc-check` with no arguments (hi) — Re-reads the last results. Instant, no agents.
- 02 Open `docs/eqc/COMPLIANCE.html` — The same results as one page in the browser.
- 03 Run `/eqc-fix` — What to fix next, easiest wins first. I'll cancel before it changes anything.

Speaker notes:
Watch for: the first part is instant (no agents, no tokens); the report is just a file; the fix list starts with the cheap wins.
PREP: dev eqc-kit installed in the app repo, full check re-run this morning, browser tab with COMPLIANCE.html already open.
1. Switch to the terminal in our mobile app repo.
2. Type /eqc-check with no arguments and press Enter.
3. Point at the level: "hold that number, it's on the next slide". Read one fail's evidence line out loud.
4. Switch to the browser tab with docs/eqc/COMPLIANCE.html. Scroll once: level and tier progress at the top, then what needs attention, then every rule by tier.
5. Back in the terminal, run /eqc-fix. If the ranked list hasn't appeared in ~30 s, cancel and show FALLBACK (part 3).
6. Read the top three suggestions and why they're low effort, high gain. Cancel at the prompt. No fixes live today.
7. Switch back to the slides.
FALLBACK (part 1): screenshot ./screenshots/eqc-check-scorecard.png — "Here's the same scorecard from this morning; the live one says the same thing."
FALLBACK (part 2): screenshot ./screenshots/eqc-compliance-report.png — "This is the page it writes next to the Markdown report; it's just a file, no setup."
FALLBACK (part 3): screenshot ./screenshots/eqc-fix-ranked.png — "Here's the ranked list from my last run; same output, no waiting."
Transition (GUESS-FIRST, take a few numbers before flipping to slide 9): "Before I flip: one of the fixes moved all our console logs to our Logger. How many files did that touch?"
Watch for: how fast the first one is, and which fixes it puts at the top.
~2.75 min

### Slide 9 — Our mobile app against the Mobile EQC: Compliance level: HARD_FAIL → MEDIUM (card-grid)
On-slide copy:
- Kicker: eqc-kit · Our mobile app
- Our mobile app against the Mobile EQC / Compliance level: HARD_FAIL → MEDIUM
- Cards (card-slash / card-name / card-sub):
  - ~5 days / From HARD_FAIL to MEDIUM / 27 recorded fixes
  - 58 files (hi) / Console logs moved to our Logger / in one fix
  - 2,912 / 2,912 / Tests passing / after one ~85-file fix
- HARD_FAIL = a LOW-tier rule fails. MEDIUM = nothing fails in LOW or MEDIUM.

Builder note: three cards only; `.hi` on the 58 card (the slide 8 guess-first reveal). The level-definition line is a short `p` under the grid. Larger card text as inline styles in this deck only (template unchanged): `.card-slash` 2.2rem, `.card-name` 1.2rem, `.card-sub` 0.95rem.

Speaker notes:
The guess: 58 files for the Logger sweep.
Fifty-eight. And the level you saw in the terminal: against the Mobile EQC, our compliance level went from HARD_FAIL to MEDIUM, in about five days. And after one fix that touched about 85 files, all 2,912 tests still passed.
Some detail behind it. Fixing the ESLint errors alone, 54 errors in 30 files, got us from HARD_FAIL to LOW. Of the 27 recorded fixes, 25 are done and 2 partial.
CUTTABLE if running late — 34 Platform.OS checks became Platform.select().
CUTTABLE if running late — Also: FlatList windowSize on 33 lists, and Crashlytics error handling in 17 files.
Today it's 33 pass, 2 partial, 4 fail.
CUTTABLE if running late — My favourite one: the i18n rule took 7 audits and 6 rounds of fixes, because every audit found more hardcoded English. In the end I added a custom ESLint rule so it can't come back.
The four still failing are honest. Three are big architecture moves, not quick wins: a state migration across 123 files, a data-fetching library, and certificate pinning. TypeScript can't pass because the project has to stay JavaScript, so the kit records it as a fail and says why it doesn't apply, instead of pretending. I'd rather have an honest fail than a fake pass.
Also, the audit found a hardcoded secret in the codebase. I'm not naming it. It's handled.
(The "today" numbers come from the cached check. Re-run before the talk and update if they moved.)
Transition: "One more thing before questions: eqc-kit isn't tied to the Mobile EQC."
~1.75 min

### Slide 10 — Not tied to the Mobile EQC. Bring your own standard. (steps-list)
On-slide copy:
- Kicker: eqc-kit · Your standard
- Not tied to the Mobile EQC. / Bring your own standard.
- 01 Bring your team's written standard — The rules your team already wrote down.
- 02 eqc-kit reads it and lists every rule — In your tiers: LOW / MEDIUM / HIGH, Bronze / Silver / Gold, whatever yours uses.
- 03 Same check, report and fixes (hi) — Everything you just saw, on your own rules.
- The Mobile EQC is just the standard I use it with.

Speaker notes:
You might think eqc-kit only works with the Mobile EQC. It isn't tied to it. eqc-kit is the tool; the standard is yours.
It's built to take your team's own written standard and adapt to it.
It reads the standard, lists every rule, and takes the tiers from it. Ours are LOW, MEDIUM and HIGH. Yours might be Bronze, Silver and Gold. It uses whatever yours has.
After that it's the same flow: the check, the report, the fixes and the guard.
The one thing it needs is a written standard.
Transition: "That's eqc-kit. Questions before we move on?"
~1 min

### Slide 11 — Questions? (eqc-kit) (center)
On-slide copy:
- Kicker: Q&A
- Questions?
- eqc-kit

Speaker notes:
Open the floor.
If it's quiet, seed one: "Which standard would your team bring?" or "Which tier would your project land in today?"
Watch the clock: this buffer is 2 minutes. Move on at 15 minutes into the talk.
Transition: "eqc-kit checks code against a standard. Next is how I get bigger work done without burning my best model."
~2 min — Q&A buffer

### Slide 12 — 02 · /orchestrate (divider)
On-slide copy:
- 02 · /orchestrate
- Plans big work with you, then sends each task to the cheapest model that can do it

Speaker notes:
Section two: /orchestrate. It's a separate tool, you can use it without eqc-kit.
About 12 minutes, then questions.
This is the "build cheap" part: score each task, then send it to the cheapest model that can do it.
Same as before, I'll start with why I built it.
Transition: "It came out of a habit I had with plan mode."
~0.25 min

### Slide 13 — Why I built /orchestrate (steps-list)
On-slide copy:
- Kicker: /orchestrate · Why I built it
- Why I built /orchestrate (accent on "/orchestrate", no line break)
- 01 I kept going back to plan mode — Claude Code writes a plan and waits for your OK. I used it for every long task.
- 02 I typed the same asks every time — Split into phases, a sub-agent per phase on the right model, interview me first.
- 03 So I made it a skill (hi) — Now it's /orchestrate. One command, instructions built in.
- Main reason: fewer tokens. Each piece goes to the cheapest model that can do it.

Speaker notes:
This one comes straight out of my day-to-day work.
I was doing my usual work and kept going back to plan mode. Every time, I asked Claude to split the long work into phases, hand each phase to a sub-agent on a model that matches how hard that piece is, and interview me before starting.
It was the same prompt and the same instructions over and over again, every big task. So I started building this skill.
The main reason I built it is tokens. Most pieces of a big task don't need the biggest model. If each piece goes to the cheapest model that can do it, you spend fewer.
I don't have a number for that. I'll come back to it on slide 16.
Transition: "Here's how it compares with plan mode and /goal, on one task."
~1.5 min

### Slide 14 — One "forgot password" task, three ways to run it (vs-grid)
On-slide copy:
- Kicker: /orchestrate · Why not plan mode or /goal?
- One "forgot password" task, / three ways to run it
- Lead: The task: an API endpoint, a reset email, a reset screen, tests. It touches auth.
- Box 1 (light red): label "Plan mode"
  - Makes a plan.
  - You OK it.
  - One model builds all.
  - It checks itself.
- Box 2 (light red): label "/goal (runs till done)"
  - Starts right away.
  - One model builds all.
  - No questions.
  - It checks itself.
- Box 3 (light green, hi): label "/orchestrate"
  - Asks you first.
  - Splits it, e.g. email → haiku · screen → sonnet · auth → opus.
  - Waits for your OK.
  - Another agent checks.

Builder note: three vs-card style boxes, light red fill for the two "without" boxes (plan mode, /goal) and light green for the /orchestrate box. Label + 4 short lines each (plain `.vs-attr` lines, no `<strong>` attribute names); no `.vs-card-title` needed. Auto-fit grid (`grid-template-columns: repeat(auto-fit, minmax(240px, 1fr))`, 3 columns at full width), the fills and `.vs-card-label` at 0.95rem are inline styles in this deck only; template unchanged (Open question 30).

Speaker notes:
One task every stack has: forgot password. An API endpoint, a reset email, a reset screen, and tests. It touches auth, which matters in a second.
The two red boxes are how plan mode and /goal worked for me day to day, not a feature list from the docs.
Plan mode writes a plan and waits for my OK, which is good. But I type the phases, sub-agents, models and "interview me" part myself, every time. After I approve, one model builds all four parts and checks its own work.
/goal tells Claude Code to keep working until a goal is met. It starts right away, no questions, one model, and it checks itself.
The green box is /orchestrate. It asks me a few questions first, one at a time. Then it splits the work and scores each piece. The email template is simple, so haiku. The reset screen is real UI logic, so sonnet. The reset token and the endpoint touch auth, and anything on the security surface always goes to opus. The tests get scored the same way.
That split is an example to show the rules, not a captured run.
Checking: a cheap haiku verifier re-runs the checks. The reset screen gets a sonnet reviewer, and because the auth part is security, a fresh opus security reviewer reads that diff looking for vulnerabilities.
And nothing gets built until I say yes. Writing "just go" in the goal doesn't skip that OK; I'll show you that live in a few minutes.
Next big task: with plan mode or /goal I type my asks again. With /orchestrate it's the same skill, one command.
The honest part. On a small task, all that planning and checking is overhead you don't need. It has to run on opus or sonnet; on haiku it stops and asks you to switch. And you still read the report at the end.
Transition: "Here are the phases it goes through."
~2.75 min

### Slide 15 — How /orchestrate runs a big task, phase by phase (dtable)
On-slide copy:
- Kicker: /orchestrate · How it works
- How /orchestrate runs a big task, / phase by phase
- Lead: The orchestrator plans and checks. Helpers on haiku, sonnet or opus write the code.
- Table Phase | What it does (acc):
  - GRILL | Asks you questions, one at a time
  - PLAN | Splits the goal into scored tasks
  - PREVIEW · the gate | Shows the plan, waits for your OK
  - EXECUTE / VERIFY | Helpers build; a separate verifier checks
  - CLOSE | Reports which models did the work; never commits

Speaker notes:
Five phases. The slide keeps it short; I'll add the detail as I go.
GRILL is the interview I used to ask for by hand. One question at a time, each with a recommended answer, so most of the time I just say yes. If you have a code map, its helpers search that before grepping. Tiny goals take a fast lane and skip this.
PLAN: it splits the goal into tasks and scores each one. Scoring is the next slide. At most 3 helpers run at once, and each file has one owner, so they don't step on each other.
PREVIEW is the part I care about most. It shows every task with its score and model, then stops. Only my reply counts: "just go" written into the goal is ignored, and "ok, but…" counts as an edit. I'll show you that live in a minute.
EXECUTE / VERIFY: the orchestrator doesn't write the code, the helpers do. The one exception is a fix of 5 lines or less per task, and only for a bug the verifier found. A cheap haiku verifier re-runs the checks; a sonnet reviewer reads the diff, or an opus security reviewer for security tasks.
CLOSE tells me which models actually did the work. Everything lives in a plan file under docs/plans, so I can stop, close the laptop, and run /orchestrate resume the next day. It suggests a commit; it never makes one.
CUTTABLE if running late — the shortcuts it isn't allowed to take. Each one sounds reasonable in the moment. "I'll do this quick fix myself": hand it to a helper. "Approval was given in advance": show the preview anyway. "Small repo, I'll just read it": it reads at most 2 files of 100 lines per phase itself and sends a scout for the rest. "I'll run the tests to be sure": the verifier does that. "This agent sets its own model": pass the model anyway.
Transition: "The part of PLAN I want to show you is how it picks the model."
~2.5 min

### Slide 16 — How it picks a model for each task (dtable)
On-slide copy:
- Kicker: /orchestrate · Picking a model
- How it picks a model / for each task
- Lead: Each task scores 0–2 on Ambiguity (how unclear), Breadth (how wide) and Reasoning (how hard). Add them up.
- Table Score or task type | Goes to (acc):
  - 0–2 | haiku
  - 3–4 | sonnet
  - 5–6 | Split first; opus only if it can't be split
  - Security work (auth, secrets, crypto, permissions…) | Always opus, plus an opus security reviewer
- Its rule: "When unsure, pick the lower tier: escalating costs less than over-provisioning."
- A task fails? It retries, then moves up or re-scopes. Still failing: it pauses and tells you.

Speaker notes:
GUESS-FIRST: which model gets "add a config entry with exact steps"? Take a few answers. (Answer: haiku. It's clear, it's one file, and it doesn't need much thinking.)
Three questions per task: how unclear is it, how much does it touch, how hard is it to think through. Zero to two each, add them up.
Big tasks get split first. Opus only gets a task that really can't be split, or anything that touches security, like auth, secrets, crypto or permissions. Those always go to opus, and a fresh opus reviewer goes through the diff looking for vulnerabilities. That's why the auth part of the forgot-password task went to opus: because it's security, not because of its score.
You can also ask for opus yourself. If a plan has more than 2 opus tasks, it asks you to confirm.
The rule I like most is the one on screen. When it's unsure, it picks the cheaper model. If that was wrong, the task fails and moves up. That still costs less than sending everything to the big model just in case.
That's where the token saving comes from. I can't give you a number. Try it on one real task and look at the model mix it reports at CLOSE.
CUTTABLE if running late — the retry ladder: a failed haiku task retries once on haiku with the exact error and the current diff, then moves to sonnet. Sonnet retries once, then the orchestrator either tries opus once or works out the problem itself and re-scopes or splits the task. If that still fails, it pauses and reports to me. Every retry is logged in the plan file.
Transition: "Now the gate itself, live."
~2 min

### Slide 17 — Demo: the preview gate (demo)
On-slide copy:
- Badge: Live demo
- Kicker: Demo · the preview gate
- Demo: / the preview gate
- 01 Paused at PREVIEW — I wrote "just go" into the goal. It still stopped, and says so. Every task has its score and model; the opus row says why.
- 02 Reply "ok, but drop task 3" (hi) — That counts as an edit: it changes the plan and shows it again. Only a plain yes approves.
- Watch for: "just go" in the goal didn't skip the gate.

Speaker notes:
Watch for: "just go" in the goal didn't skip the gate.
PREP: before the talk, use the current skill (the one with the opus tier). Run /orchestrate on opus or sonnet with a small goal that includes one security-touching task, and end the goal with "just go": /orchestrate <goal>, just go. An opus row with its reason tag should show up. Answer GRILL and stop at PREVIEW. The preview should print a line saying approval in the goal was ignored. Leave the terminal paused at "Approve, edit, or reject?". Don't approve.
PREP: capture ./screenshots/orchestrate-preview.png from that same run. Don't use the README preview; it's marked illustrative.
1. Switch to the pre-staged terminal.
2. Walk the task table (task, score, tier). Point at the Tier column: the opus row carries its reason, e.g. opus (security: <surface>). Read the "Mix" line.
3. Point at the line saying "just go" in the goal was ignored, then at the prompt: "Approve, edit, or reject?"
4. Reply "ok, but drop task 3". That counts as an edit: show the re-preview with the plan changed. Never type a bare 'go' or 'just go' at the prompt: that approves.
5. Reject, and switch back to the slides.
FALLBACK: screenshot ./screenshots/orchestrate-preview.png — "Here's the preview from a real run; the bit to notice is that 'just go' in the goal didn't skip the gate."
Transition: "That's the check before anything runs. Here's what I've actually built with it."
~1.75 min

### Slide 18 — What I've built with /orchestrate (vs-grid)
On-slide copy:
- Kicker: /orchestrate · In practice
- What I've built / with /orchestrate
- Left vs-card: label "Built with it" · title "48 finished runs · 8 projects · ~6 weeks"
  - Own tools: 13 runs (skills, agents, eqc-kit's latest upgrade)
  - Models: mostly haiku and sonnet
- Right vs-card (hi): label "This deck · built with /orchestrate" · title "presentation-builder, a Claude Code plugin"
  - 2 skills: /create-presentation (new deck) · /update-presentation (change one)
  - 6 agents, one job each: research · outline · script · build · content review · design review
- Closing line: Questions?

Speaker notes:
I built eqc-kit's latest upgrade with /orchestrate: the code map, the HTML report and the guard you heard about earlier. Same for most of my skills and agents.
I only counted runs that finished: 48, across 8 projects, in about 6 weeks. 13 of them were on my own tools.
CUTTABLE if running late — eqc-kit itself, version 0.1.0, I built before /orchestrate existed. Only the latest upgrade went through it: 1 opus, 2 sonnet and 1 haiku builder, 60 of 60 tests passing.
Across those runs, most of the building went to haiku and sonnet. Opus shows up in a few.
Now the right side. Remember the footer on slide 1? This deck was built with presentation-builder, and /orchestrate built presentation-builder.
It's a Claude Code plugin with two skills: one makes a new deck, one changes a deck. And six agents, each with one job: one reads my sources, one writes the outline and slide text, one writes the script, one builds the HTML, and two review it, one for content and one for design.
Building it took 3 runs and 18 tasks, and none moved up a model. The two opus tasks were ones I asked for at approval; you saw on slide 16 that you can do that.
Then opus tried the finished skill on a sample deck, a dry-run. It found 15 issues, and 13 got fixed after.
Verifiers get it wrong too: on one of those builds, the final verifier raised a false alarm because its search matched numbers in CSS. So I still read the report.
CUTTABLE if running late — The facts in this deck come from a context file in the same folder, so it doesn't make numbers up. If a slide is wrong, that file is the place to check.
Q&A: open the floor on /orchestrate. Seed if quiet: "What's a ticket on your board right now that would score 0–2?" Move on at about 30 minutes in.
Transition: "Last section is lighter: what happens after the code is written."
~4.25 min (~1.75 content + 2.5 Q&A buffer)

Builder note: no project or repo names on this slide (presentation-builder is the plugin name, it stays). The two cards are symmetrical: label, one-line title, exactly 2 attr lines each. The right card keeps class `vs-card hi` and uses the same inline title size as the left card. Its attrs start with `<strong>2 skills:</strong>` and `<strong>6 agents, one job each:</strong>`. No build stats on the slide (runs, builders, dry-run live in the notes).

### Slide 19 — 03 · The ship chain (divider)
On-slide copy:
- 03 · The ship chain
- After the code works: commit, PR, release notes, build

Speaker notes:
Section three, lighter coverage. Each skill is small on its own; the value is that they connect.
This is the "ship clean" part: write each change up for whoever reads it next.
Transition: "Here's the chain."
~0.25 min

### Slide 20 — Each skill feeds the next (steps-list)
On-slide copy:
- Kicker: Ship chain · 4 skills + our CI
- Each skill feeds the next (accent on "feeds the next", no line break)
- 01 /reflect — Session end: updates CLAUDE.md (the agent's project notes) and docs
- 02 /git-commit · start here (hi) — Conventional Commit (`type(scope): summary`); you confirm
- 03 /send-pr — Writes the PR title and body
- 04 /release-notes — Commits + diffs → release notes file
- 05 ci-pipeline — Our CI: builds and ships from that file

Speaker notes:
The first four are skills in the install repo; the last is our CI.
/reflect keeps CLAUDE.md, CONTEXT.md and docs/ in line with what changed, so the why is written down.
/git-commit previews the message and waits for you. No AI attribution trailer.
/send-pr: a PR title and body that actually say something.
/release-notes also reads the doc changes, not just commits and diffs.
/git-commit is highlighted because it's the cheapest one to start with today.
Transition: "The trick is that it's one piece of writing with several readers."
~1.5 min

### Slide 21 — One change, four write-ups, four readers (dtable)
On-slide copy:
- Kicker: Ship chain · Audiences
- One change, / four write-ups, four readers
- Table Writing | Read by (acc) | Written by:
  - Commit message | Developers + testers (dev-build tester note) | `/git-commit`
  - Pull request | Reviewers | `/send-pr`
  - Release notes | Managers | `/release-notes`
  - Store note (App/Play Store "What's new") | Users | `/release-notes` (CI copies it)

Speaker notes:
GUESS-FIRST: who reads your commit messages? Take answers. "Nobody" is the usual one.
Answer: more people than you think. On our dev builds, the last commit message becomes the tester note. So "wip fix stuff" is what QA sees.
Same facts, rewritten for each reader as they move down the chain.
Transition: "Which means commits get written with the next step in mind." (If slide 22 is cut: "Here's a real one." and go to slide 23.)
~1.5 min

### Slide 22 — Commits are written for the release notes (code-block)
On-slide copy:
- Kicker: Ship chain · Under the hood
- Commits are written / for the release notes
- Code head: Quoted from each skill's instruction file (SKILL.md) · markdown
- `# git-commit` (tok-dim) / "each line doubles as raw material for release notes later" (tok-ok)
- `# release-notes` (tok-dim) / "don't trust commit messages alone" (tok-warn) / → also reads code diffs and doc changes (tok-dim)

Speaker notes:
CUTTABLE if running late.
Two halves of a contract: the commit skill writes each line to be reused, technical and product-facing; the /release-notes skill trusts but verifies.
The why comes from /reflect: /release-notes reads CLAUDE.md and CONTEXT.md because they often explain WHY a change happened.
Transition: "Here's a real one."
~0.75 min

### Slide 23 — Demo: v1.9.4 notes beside their commits (demo)
On-slide copy:
- Badge: Live demo
- Kicker: Demo · our mobile app v1.9.4
- Demo: v1.9.4 notes / beside their commits
- 01 Open RELEASE_NOTES_v1.9.4.md (hi) — Written by /release-notes; ends with the store note
- 02 Put `git log` beside it — Match one commit to its sentence
- Code block, head "One change, three write-ups" · "real":
  - `# commit` (tok-dim) / fix(android): restore hardware back button navigation on SDK 36
  - `# release notes` (tok-dim) / Android Back Button Fixed (Android 16 / SDK 36)
  - `# store note` (tok-dim) / Fixed the Android back button and improved app stability
- Watch for: one commit line becoming a sentence a manager or user can read.

Speaker notes:
The code block on screen is the example: one real change in three write-ups. The live demo shows it side by side.
Watch for: one commit line turning into a sentence a manager or a user can read.
1. Open docs/RELEASE_NOTES_v1.9.4.md in the editor, left pane.
2. In the right pane, run git log for the v1.9.4 range.
3. Pick one commit and find where it shows up in the notes.
4. Scroll to the App Store / Play Store release-note block and read it out loud.
5. Switch back to the slides.
FALLBACK: screenshot ./screenshots/release-notes-v1.9.4.png — "Here are the two side by side; same commit, two very different audiences."
Transition: "And this file isn't optional."
~1.5 min

### Slide 24 — No release notes, no build (center)
On-slide copy:
- Kicker: Enforced, not recommended
- No release notes, / no build
- CI fails if `RELEASE_NOTES_v<version>.md` is missing.
- Staging and production builds copy the store note from this file.

Speaker notes:
No file, failed build.
The pipeline: dev builds go to Firebase, staging to TestFlight and Play internal testing, prod gets promoted to the stores.
This is the difference between a habit and a process: the chain is enforced by CI, not just recommended in a wiki nobody opens.
Transition: "Let's pull the three sections together."
~1 min

### Slide 25 — Ask first, build cheap, ship clean (card-grid)
On-slide copy:
- Kicker: Recap
- Ask first, build cheap, / ship clean
- eqc-kit: Ask first: check every rule, with proof, before you fix · checks your code, keeps passing rules passing
- /orchestrate: Build cheap: score the task, then pick the model · plans, then cheaper models build
- ship chain (hi): Ship clean: write the commit for its next reader · commit → PR → notes → build

Speaker notes:
One sentence each.
eqc-kit: agents check your code against your team's written standard, like our Mobile EQC, a plain script works out the level, big fixes wait for your OK, and the guard stops passing rules from slipping back.
/orchestrate: every task gets a score before it gets a model; you approve the plan, cheaper models build and a verifier checks.
Ship chain: write the commit for whoever reads it next, and it becomes the PR, the release notes and the store note, with CI making sure.
Transition: "You don't need all three. Pick any one."
~0.75 min

### Slide 26 — Pick any one. Try it. Or build your own. (closing)
On-slide copy:
- Kicker: Your move
- Pick any one. Try it. / Or build your own.
- Too much hassle to check and keep up EQC compliance? Try eqc-kit: `npx eqc-kit init` · Big ticket? Try `/orchestrate` · Vague commits? Try `/git-commit`
- Get /orchestrate and /git-commit: paste into Claude Code → "Fetch and follow https://raw.githubusercontent.com/mehedibangladeshi/ai-skills/master/INSTALL.md"

Speaker notes:
Pick whichever one matches your pain. You don't need all three.
If your commit messages say "fix", /git-commit is the quickest win: start today.
Or take one idea and build your own. Every tool today started as something I kept doing by hand.
The install line is a prompt: paste it into your agent and it sets up the skills. It's my repo, so read INSTALL.md first if you like.
The same lines stay on the next slide through Q&A, so no rush to copy.
Transition: "Thanks. Last round of questions."
~0.75 min

### Slide 27 — Questions? (final) (center)
On-slide copy:
- Kicker: Q&A
- Questions?
- Too much hassle to check and keep up EQC compliance? Try eqc-kit: `npx eqc-kit init` · Big ticket? Try `/orchestrate` · Vague commits? Try `/git-commit`
- Get /orchestrate and /git-commit: paste into Claude Code → "Fetch and follow https://raw.githubusercontent.com/mehedibangladeshi/ai-skills/master/INSTALL.md"

Speaker notes:
Thank everyone. Open the floor for anything across the three sections.
Seed if quiet: "Which one are you trying first, or what would you build?"
Leave this slide up through Q&A: the commands and the install line stay on screen.
Transition: none, this is the end.
~2 min — Q&A buffer

## Open questions

Items 5-7 and 9 are resolved history and keep pre-revision-3 slide numbers. Items 1-4, 8, 10-12 use revision 3 numbers unless marked; items 13-21 are revision 4 (26-slide numbering); item 29 is revision 5 (27-slide numbering); revision 5 items 22-28 were resolved at approval (2026-11-18, see the "Revision 5 final edits" line at the top) and removed. Revision 4 renumbering for items 2-4: demo 15 → 16, demo 25 → 22; slides 16/18/24 cut list → 21 plus the notes paragraphs in engagement item 7.

1. eqc-kit numbers: slide 9 uses the cached `compliance.json` (2026-10-02: 33 pass / 2 partial / 4 fail); `docs/eqc/COMPLIANCE.md` (2026-09-28) says 30 / 5 / 4. Re-run /eqc-check (with the dev eqc-kit) before the talk so slides 8 and 9 agree and `docs/eqc/COMPLIANCE.html` exists.
2. Demo fallbacks: five screenshots in `./screenshots/`, all still to capture: `eqc-check-scorecard.png`, `eqc-compliance-report.png` (NEW), `eqc-fix-ranked.png` (replaces `eqc-fix-plan.png`; the saved-plan part is dropped), `orchestrate-preview.png`, `release-notes-v1.9.4.png`. (`context.md` checklist: **resolved**, renumbered 2026-11-17.)
3. Slide 15 needs a pre-staged /orchestrate run paused at PREVIEW before the talk.
4. Timing observation (no change made): the slide 25 demo runs at ~34.0-35.5 min (~85-89% of runtime), past the ~80% demo guideline. Within the light ship-chain section this is by design; flag only if rehearsal runs long (cut slides 16/18/24 first).
5. **Resolved:** time funding kept as proposed (eqc-kit Q&A 2.5 → 2 min; slides 5 and 8 1.5 → 1.25; slide 26 1 → 0.75).
6. **Resolved:** if slides 6, 8, 15 or 24 overflow one screen, trim the step-descs, not the definitions. Slides section keeps the approved copy as written; each step-desc is one short line, so height is set by row count (4-5 rows). Design-creator trims only if the self-check shows overflow.
7. **Resolved:** slides 15 and 24 converted from `flow` to `steps-list`; "lock", "gate" and "start here" now live in the step text, emphasis via `.step-row.hi` on PREVIEW (15) and /git-commit (24).
8. Outside this file (**checklist part resolved:** `context.md` checklist renumbered 2026-11-17): `context.md` (accepted-suggestion slide numbers, and the stale "`gate --min TIER`" line → `eqc guard [--min TIER]`) and `transcript.md` (eqc-kit section rewritten for slides 4-10; all later headings shift by -2; drop the "forty seconds" line) need a resync now that revision 3 is approved.
9. **Resolved (2026-11-16):** content and design review fixes applied (user-approved) in `index.html`; still 31 slides, cues sum to 40.0 min (sections 15 / 15 / 10).
10. Density (by the speaker's request): slides 6, 7 and 9 go well past the ~30-word guideline, and slide 6 / slide 9 have 5 dtable rows (DESIGN.md says "about four"). Design-creator must check each fits one screen (print clips overflow). If one overflows, which to trim first: slide 6's "cost" row (it repeats slide 7's code-map and cached-check points) or slide 7's cell text?
11. Dev eqc-kit: presented as available. Confirm it is published before the talk and give the version, or the slides stay version-free [TBD]. Known dev wording bug: `npx eqc-kit hooks` output still says "verify + gate" though the pre-push hook runs `guard` (sources.md, Contradictions); avoid running `hooks` live or fix it before publishing. Tracked in the `context.md` checklist (review finding 6, 2026-11-18): "Publish eqc-kit (guard, verify, hooks, HTML report); confirm `npx eqc-kit init` installs it".
12. /eqc-fix ranking: "low effort, high gain" is from your interview; the old deck said "top 10 easiest fails first". Confirm the wording /eqc-fix prints, so the slide matches what the audience sees.
13. **Resolved (2026-11-17):** slide 13 `[TBD]` cells filled by the speaker; /orchestrate "Interviews you first?" edited to "Yes (if needed), one question at a time"; table keeps 6 rows. Plan mode and /goal behaviour still come only from the speaker, not checked against Claude Code docs (the slide 13 notes say "how each one worked for me").
14. **Resolved (2026-11-17):** slides 13-15 fit one 1280x720 screen after the review fixes (slide 13: one-line h2, 0.9rem cells, all 6 rows kept). Print preview not yet checked. Original note: slide 13 is 6 rows × 5 columns and slide 14 is 5 rows with long cells, both well past DESIGN.md's ~4 rows / ~30 words. Design-creator must check each fits one screen (print clips overflow). If one overflows, trim first: slide 14's GRILL/CLOSE extras (code map, stop/resume/reject) into the notes, then shorten slide 13's plan mode cells?
15. **Resolved (2026-11-17):** slide 17 keeps the approved density; if the design-creator reports overflow, the "~11 runs" line moves to the notes first (Builder note on slide 17).
16. **Resolved (2026-11-17):** slide 17 notes say the ~11 runs and the 0-escalation build happened before the opus tier existed.
17. **Resolved in the notes (2026-11-17):** slide 16 PREP uses the current skill with one security-touching task; `./screenshots/orchestrate-preview.png` must be recaptured from that run (still to capture, see item 2).
18. **Resolved (2026-11-17):** `transcript.md` resynced to the 26-slide deck after the review fixes (jokes removed throughout). Original note: `transcript.md` (/orchestrate section rewritten for slides 11-17, jokes dropped; ship-chain headings shift by -3) and `context.md` (accepted-suggestion and checklist slide numbers) need a resync once revision 4 is approved. (**`context.md` resolved 2026-11-17** per review finding 4: 26-slide numbering, security always opus, no jokes, new demo pre-staging line.)
19. **Resolved (2026-11-17, review finding 7):** the "~11 runs: most of the work went to haiku and sonnet" line moved from slide 17's left card to its notes only.
20. Slide 16 demo (review finding 1): confirm in rehearsal that `/orchestrate <goal>, just go` still stops at PREVIEW and prints that approval in the goal was ignored, and that "ok, but drop task 3" re-previews. Recapture `./screenshots/orchestrate-preview.png` from that run.
21. **Resolved (2026-11-17):** slide 12 merged to 3 rows in `index.html` (01 plan mode · 02 "I typed the same asks every time" · 03 "So I made it a skill"). Original note: `index.html` slide 12 did not yet match review finding 13 as recorded here: it still has the old row 03 "Same prompt, over and over" and the old row 02 text, and the last row is numbered "03" too (two "03"s, 4 rows). The outline records the confirmed merge (3 rows). Fix the deck to match, or confirm the 4-row version.
29. **Resolved (2026-11-18):** `transcript.md` resynced to 27 slides; the remaining `context.md` items (review findings 18 and 20: slide 18 run facts, stale outcome and slide numbers) were updated by the orchestrating session. Original note (pending resync, outside this file): `transcript.md` and `context.md` need a resync to 27 slides (new slide 10 "Not tied to the Mobile EQC", no "any project / any stack" wording; old 10-26 → 11-27; slide 1 footer payoff → 18; demos 17 and 23; "pick any one" close; EQC spelled out, "the Mobile EQC" wording; slide 18's new runs card).
30. Fix 2026-11-18 (slides 6, 9, 14, 18): resolved. Red/green boxes are inline styles on `.vs-card` inside this deck only (template unchanged, by decision of the orchestrating session); presentation-builder = 3 runs (the 4th ETH plan is an eqc-kit review, not a build); facts added to sources.md; transcript resynced.
