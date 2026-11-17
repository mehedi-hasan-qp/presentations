# Outline: Ask first, build cheap, ship clean

Backfilled from `index.html`, `context.md` and `transcript.md` on 2026-11-16. **Revision 2 (2026-11-16):** slides made self-explanatory for a first-time audience (one primer slide added, context moved from notes onto slides, terms defined on first use). Revision 2 approved; `## Slides` regenerated for the 31-slide deck. **Review fixes (2026-11-16):** user-approved content/design review fixes applied in `index.html`; Outline table and `## Slides` resynced to `index.html`.

**Revision 3 (2026-11-17, approved by the user 2026-11-17; `## Slides` finalized for the design-creator):** eqc-kit section only (old slides 4-12, 9 slides → new slides 4-10, 7 slides). Denser, self-explanatory slides; plain titles; first-person notes; a new "why I built it" slide; a comparison table (manual / ask AI / eqc-kit) with eqc-kit's cons; eqc-kit dev-branch features (code map, HTML report, baseline + `eqc guard`, optional `verify`, opt-in hooks) from `work/sources.md`; one combined demo (cached /eqc-check, HTML report, /eqc-fix ranked list); saved-plan demo dropped. Section time unchanged (12.25 min incl. 2 min Q&A), total still 40.0 min. Old slides 13-31 become 11-29 (-2), content unchanged except cross-references.

**Revision 4 (2026-11-17, approved by the user 2026-11-17; `## Slides` regenerated for the 26-slide deck):** /orchestrate section only (old slides 11-20, 10 slides → new slides 11-17, 7 slides). Same treatment as revision 3: the speaker's origin story, a comparison table (long prompt / plan mode / /goal / /orchestrate) with honest cons, a dense "what it is like" slide that folds in the 5 phases, scoring updated to the current skill (opus tier for security and unsplittable tasks), and one merged results + reveal + Q&A slide. Jokes dropped, plain titles. Section time unchanged (15.0 min incl. 2.5 min Q&A), total still 40.0 min. Old slides 21-29 become 18-26 (-3), content unchanged except cross-references. In the Outline table, **NEW** / **CHG** tags now mark revision 4 only. User decisions applied at approval: slide 13 `[TBD]` cells filled by the speaker; the /orchestrate "Interviews you first?" cell edited to "Yes (if needed), one question at a time"; slide 17 notes say the runs predate the opus tier; slide 16 PREP and fallback screenshot come from the current skill with one security task; slide 17 overflow rule ("~11 runs" moves to the notes first).

**Review fixes (2026-11-17, user-confirmed; applied in `index.html`, Outline table rows 11-17, Demo 2 and `## Slides` 11-17 resynced):** content-review findings 1-3, 5, 6, 8-13 (`work/reviews/content.md`). Slide 11 sub shortened (14). Slide 12 rows 02 and 03 merged, footer reworded (13). Slide 13 cells shortened, /goal OK cell "No, it starts working right away", /orchestrate OK cell "a hard gate: "just go" in your goal doesn't skip it", cons line lowercase models, one-line h2 (1, 3, 12). Slide 14 retitled "How /orchestrate runs a big task, phase by phase", lead and EXECUTE row no longer contradict (11, 2). Slide 15 retitled "How it picks a model for each task", header "Score or task type", guess-first now "add a config entry with exact steps" (10, 9, 8). Slide 16 demo puts "just go" into the goal and replies "ok, but drop task 3", then rejects (1). Slide 17 card title "Two "done" claims that weren't true", build line ends "(before the opus tier existed)" (5, 6). Finding 7: the "~11 runs" line left slide 17's left card and lives only in its notes. Findings 4 (context.md) fixed outside this file; finding 15 (timing) not applied, cues unchanged.

## Brief

- **Topic:** "Ask first, build cheap, ship clean": my everyday AI workflow (eqc-kit, /orchestrate, the ship chain)
- **Speaker:** Mehedi Hasan, Mobile Team
- **Audience:** fellow engineers, internal team session / brown-bag. First exposure: they have never seen eqc-kit, /orchestrate, reflect, /git-commit, /send-pr, release-notes or ci-pipeline. Every slide must make sense without the speaker.
- **Desired outcome:** each listener picks 2-3 skills or habits and tries them on their own work this week
- **Duration:** 40 min (3 sections: 15 / 15 / 10, each ending in a Q&A buffer of 2-2.5 min; cues sum to 40.0 min)
- **Slide count:** 26
- **Template:** default
- **Transcript:** yes (`transcript.md`: human, casual first person; no jokes in the revised sections)
- **Demos:** slide 8 (eqc-kit: cached /eqc-check scorecard, the HTML compliance report, /eqc-fix ranked list), slide 16 (/orchestrate preview gate), slide 22 (v1.9.4 release notes beside git log)

## Narrative arc

- **Hook (slide 2, not an agenda):** show of hands: who has read the whole 39-rule quality standard, and who checked their code against every rule. Slide 1's footer ("Built with /create-presentation") is planted for a later payoff. Slide 3 then gives first-timers the four terms the rest of the talk uses.
- **Problem:** checking 39 rules by hand never happens (slide 2); I was asked if my projects were compliant and checking by hand, even with AI, was too much (slide 5); I kept typing the same plan-mode instructions (phases, tiered sub-agents, interview me first) for every big task (slide 12).
- **Stakes:** HARD_FAIL compliance; AI that says "pass" when it isn't and breaks fixed rules again on the next feature (slide 6); one model builds everything, nothing stops it before edits, and it checks its own work (slide 13); "done" claims that are not true (slide 17).
- **Insight:** AI checks each rule with proof, a plain script works out the level, and the guard remembers what passed (slides 6-7); a score per task picks the model, and the lower tier wins when unsure (slide 15); one piece of writing has four audiences (slide 20).
- **Solution:** eqc-kit (slides 4-9), /orchestrate (slides 11-17), the ship chain (slides 18-23).
- **Proof:** HARD_FAIL to MEDIUM in about 5 days (slide 9); two "done" claims that weren't true, and ~11 runs ran mostly on haiku / sonnet (slide 17, the runs line in the notes); demos on slides 8, 16, 22.
- **Climax:** slide 17, the reveal (this deck was built by a skill that /orchestrate built), at ~26.5-27.5 min (~66-69% of runtime).
- **Close / CTA (slide 25):** "Pick two. Try them this week." (`npx eqc-kit init` · `/orchestrate` on your next ticket · `/git-commit` today), each paired with the pain it fixes. Commands stay on screen through the final Q&A (slide 26).

## Outline

| # | Component | Title | Key points | Notes gist | Min |
|---|---|---|---|---|---|
| 1 | title | Ask first, build cheap, ship clean | subtitle: "three tools for checking, planning and shipping code"; footer: built with /create-presentation | Intro, goal: leave with 2-3 things to try; **CHG** footer comes back on slide 17 | 0.5 |
| 2 | center | 39 rules. One long doc. Nobody wants to check them by hand. | "39 rules in 3 tiers (9 LOW, 13 MEDIUM, 17 HIGH)"; "eqc-kit checks · /orchestrate plans · the ship chain ships" | Show of hands; checking 39 rules by hand never happens | 1.25 |
| 3 | dtable | A skill is a playbook. Sub-agents are its helpers. | Claude Code: AI coding agent in your terminal; skill (`/name`) = saved playbook, sub-agent = helper given one task; haiku → sonnet → opus = cheapest → priciest model | Primer for first-timers; every tool today is a skill or uses sub-agents | 1 |
| 4 | divider | 01 · eqc-kit | sub: "Checks your code against your team's own quality standard" | ~10 min then Q&A; open MIT npm package | 0.25 |
| 5 | steps-list | How I ended up building eqc-kit | 4 first-person rows: handed the standard + "are your projects compliant?" → checked rule by rule by hand → AI helped, still too much → automated it (hi): eqc-kit, MIT npm package; install line + 5 supported tools | Speaker's own story, close to his words; tiers come from your doc; one-command install | 1.25 |
| 6 | dtable | Three ways to check a project against the standard | Table Question \| Manual review \| Ask AI directly \| eqc-kit (acc), 5 rows: trust "pass" · every rule covered · same answer twice · stays fixed later · cost every time; cons line: needs a written standard, first audit costs time + tokens, agents can misjudge | Speaker's pains with asking AI directly; what eqc-kit does about each; honest cons | 2.25 |
| 7 | dtable | What you run, and where AI is used | Table Command \| What it does (acc) \| Uses AI?: `/eqc-check` (code map, verdict + proof, script counts, MD + HTML report) · `/eqc-fix` (low effort, high gain first; big fixes need your OK; never commits) · `eqc guard` (baseline, fails only on regressions) · `verify` + hooks (optional, mechanical rules only, opt-in, no AI) | Plain-language walk-through | 2 |
| 8 | demo | Demo: check, report, and what to fix next | 01 `/eqc-check` cached (hi): instant, no agents · 02 open `docs/eqc/COMPLIANCE.html` · 03 `/eqc-fix`: ranked list, cancel before fixing | 3-part demo with numbered steps; ~30 s cut-over to FALLBACK on part 3; FALLBACK screenshot per part; guess-first on Logger file count | 2.75 |
| 9 | dtable | Our mobile app went from HARD_FAIL to MEDIUM in about 5 days | Lead defines HARD_FAIL / MEDIUM + today's 33 / 2 / 4; rows: ESLint 54 errors / 30 files · Logger 58 files · `Platform.select()` 34 places · tests ~85 files, 2912/2912 green · still failing (4), TypeScript recorded as a fail | Reveal 58; i18n took 7 audits; hardcoded secret handled | 1.75 |
| 10 | center | Questions? (eqc-kit) | Q&A buffer | Seeds; move on at 15 min | 2 |
| 11 | divider | 02 · /orchestrate | **CHG** sub: "Plans big work with you, then sends each task to the cheapest model that can do it" | **CHG** separate tool, ~12 min then questions; drop the "manager who reads the PR" line | 0.25 |
| 12 | steps-list | **NEW** Why I built /orchestrate | 3 first-person rows: kept going back to plan mode → typed the same asks every time (split into phases, a sub-agent per phase on a model that fits, interview me first; same prompt, every big task) → made it a skill (hi); footer: why I built it, to spend fewer tokens by sending each piece to the cheapest model that can do it | Speaker's origin story in his words; replaces old 12 (problem); no token number, come back to it on slide 15 | 1.5 |
| 13 | dtable | **NEW** Four ways to run a big task with AI | Table Question \| Long prompt every time \| Plan mode \| /goal \| /orchestrate (acc); 6 rows: remembers the instructions · interviews you first · stops for your OK before building (/goal: starts right away; /orchestrate: hard gate, "just go" in your goal doesn't skip it) · picks a model per task · who checks the work · picks up after a break; cons line: overhead not worth it on small tasks, has to run on opus or sonnet (stops on haiku), you still read the report | Speaker-confirmed gaps per column; the OK row's difference is "can't be skipped"; /orchestrate cells point to slides 14-15; honest cons; fast lane softens the small-task con | 2.75 |
| 14 | dtable | **NEW** How /orchestrate runs a big task, phase by phase | Lead: 5 phases GRILL → PLAN → PREVIEW → EXECUTE / VERIFY → CLOSE; the orchestrator doesn't write the code, helpers on haiku / sonnet / opus do; table Phase \| What it does (acc), 5 rows: GRILL (one question at a time, recommended answer; code map before grep; fast lane skips it for tiny goals) · PLAN (scored tasks; max 3 helpers at once, one owner per file) · PREVIEW · the gate ("just go" in the goal ignored, "ok, but…" is an edit) · EXECUTE / VERIFY (helpers build; haiku verifier, sonnet reviewer or opus security reviewer; orchestrator may make one ≤5-line fix per task, only for a verifier-found bug) · CLOSE (reports the model mix; plan file for stop / resume / reject; never commits on its own) | Walk the phases; banned shortcuts and the 2 files × 100 lines read cap live in the CUTTABLE notes paragraph | 2.5 |
| 15 | dtable | **CHG** How it picks a model for each task | Lead glosses Ambiguity / Breadth / Reasoning 0-2; table Score or task type \| Goes to (acc): 0-2 haiku · 3-4 sonnet · 5-6 split first, opus if it can't be split · security work: always opus + an opus security reviewer; footer lines: you can ask for opus; more than 2 opus tasks → it asks you to confirm; quote "When unsure, pick the lower tier: escalating costs less than over-provisioning."; ladder: haiku retry → sonnet retry → one opus try or the orchestrator re-scopes → pauses and tells you | Guess-first "add a config entry with exact steps" → haiku; token saving stays in the rule line and the notes, qualitative, no numbers ("look at the model mix at CLOSE") | 2 |
| 16 | demo | **CHG** Demo: the preview gate | 01 paused at PREVIEW: "just go" written into the goal, it still stopped and says so; each task with score and model, the opus row says why · 02 reply "ok, but drop task 3" (hi): an edit, plan changes and shows again; only a plain yes approves; watch-for: "just go" in the goal didn't skip the gate | Pre-staged `/orchestrate <goal>, just go` with one security task, paused at PREVIEW; reply the edit, show the re-preview, then reject; never type a bare "go" / "just go" at the prompt | 1.75 |
| 17 | vs-grid | **CHG** What happened when I used it | Left card: two "done" claims that weren't true (coverage audit ~65 identifiers missing → 0 after retry; E2E line 143 wasn't covered); right card (hi): this deck was built by /create-presentation, which /orchestrate built: 5 tasks + 2 fixes, 0 escalations (before the opus tier existed); closing line "Questions?" | Merges old 17, 18, 19, 20; slide 1 payoff; verifiers fail too (CSS false alarm); "~11 runs, mostly haiku / sonnet" is in the notes only (finding 7); runs predate the opus tier; Q&A seed; transition to the ship chain; content ~1.75 + Q&A 2.5 | 4.25 |
| 18 | divider | 03 · The ship chain | sub: "After the code works: commit, PR, release notes, build" | Lighter section; value is in the connection | 0.25 |
| 19 | steps-list | Each skill feeds the next | 01-05: /reflect, /git-commit (hi, "start here"), /send-pr, /release-notes, ci-pipeline | What each step does; /git-commit is the cheapest start | 1.5 |
| 20 | dtable | One change, four write-ups, four readers | Commit: devs + testers; PR: reviewers; Release notes: managers; Store note: users; "Written by" column | Guess-first: who reads your commits; **CHG** cut-path refs → slides 21/22 | 1.5 |
| 21 | code-block | Commits are written for the release notes | git-commit: "raw material for release notes"; release-notes: "don't trust commit messages alone" | Cuttable; two halves of a contract | 0.75 |
| 22 | demo | Demo: v1.9.4 notes beside their commits | Step-descs; code block "One change, three write-ups"; watch-for line | Match a commit to its sentence; read the store note | 1.5 |
| 23 | center | No release notes, no build | CI fails if `RELEASE_NOTES_v<version>.md` is missing; staging and production copy the store note from it | Enforced, not recommended | 1 |
| 24 | card-grid | Ask first, build cheap, ship clean (recap) | eqc-kit (Ask first: big fixes wait for your OK; sub "checks your code, keeps passing rules passing"); /orchestrate (Build cheap); ship chain (hi, Ship clean) | One sentence per section; "Pick two" | 0.75 |
| 25 | closing | Pick two. Try them this week. | Each command paired with its pain; install line | Match tools to pain; install line is a prompt | 0.75 |
| 26 | center | Questions? (final) | **CHG** mirrors slide 25 (pain + command) + install line on screen | Open floor; "Which two are you trying first?" | 2 |

Total: 40.0 min (40 min slot). Sections: eqc-kit 15.0 (slides 1-10) · /orchestrate 15.0 (11-17: content 12.5 + Q&A 2.5 inside slide 17) · ship chain 10.0 (18-26). Rows: 26 (matches slide count).

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

Revision 4 numbering. The eqc-kit section has one combined demo (slide 8); the /orchestrate demo moves to slide 16, the release-notes demo to slide 22.

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

### Demo 2 (slide 16): the preview gate, ~1.75 min
PREP: before the talk, on the current skill (with the opus tier), run `/orchestrate <small goal with one security task>, just go` on opus or sonnet, answer GRILL, and stop at PREVIEW. The preview should print a line saying approval in the goal was ignored. Leave that terminal paused at "Approve, edit, or reject?". Don't approve. Capture ./screenshots/orchestrate-preview.png from this run. Check the behaviour in rehearsal.
Watch for: "just go" in the goal didn't skip the gate.
1. Switch to the pre-staged terminal.
2. Walk the task table (task, score, tier) and point at the Tier column: the opus row carries its reason, e.g. `opus (security: <surface>)`. Read the "Mix" line.
3. Point at the line saying "just go" in the goal was ignored, then at the prompt: "Approve, edit, or reject?"
4. Reply "ok, but drop task 3". That counts as an edit: show the re-preview with the plan changed. Never type a bare "go" or "just go" at the prompt: that approves.
5. Reject, and switch back to the slides.
FALLBACK: screenshot ./screenshots/orchestrate-preview.png, recaptured from the PREP run on the current skill (not the README's illustrative preview) — "Here's the preview from a real run; the bit to notice is that 'just go' in the goal didn't skip the gate."

### Demo 3 (slide 22): v1.9.4 notes beside their commits, ~1.5 min
The code block on screen is the example: one real change in three write-ups. The live demo shows it side by side.
Watch for: one commit line turning into a sentence a manager or a user can read.
1. Open docs/RELEASE_NOTES_v1.9.4.md in the editor, left pane.
2. In the right pane, run git log for the v1.9.4 range.
3. Pick one commit and find where it shows up in the notes.
4. Scroll to the App Store / Play Store release-note block and read it out loud.
5. Switch back to the slides.
FALLBACK: screenshot ./screenshots/release-notes-v1.9.4.png — "Here are the two side by side; same commit, two very different audiences."

## Engagement suggestions

Items 1-7 already applied in the deck (accepted suggestions recorded in `context.md`). Slide numbers updated for revision 4. Item 8 now also covers revision 4.

1. **What:** retitle to "Ask first, build cheap, ship clean". **Why:** title matches the three-part workflow and the "pick two" outcome. **Where:** 1, 24.
2. **What:** keep company/internal names off slides ("our mobile app", "our quality standard"). **Why:** internal names only in notes. **Where:** all, esp. 5, 9.
3. **What:** a "guess first" audience moment per section. **Why:** interaction every ~8-10 min. **Where:** 8→9 (Logger file count), 15 ("add a config entry with exact steps" model), 20 (who reads commits); plus show of hands on 2.
4. **What:** demo prep: re-run /eqc-check and capture a screenshot fallback for every demo part. **Why:** slides 8 and 9 must agree; demos can break. **Where:** 8, 9, 16, 22.
5. **What:** intentional honest limits. **Why:** engineers trust stated failure modes. **Where:** 6 (eqc-kit cons line), 9 ("still failing" row), 13 (/orchestrate cons line), 17 (verifiers fail too, in notes).
6. **What:** slide 1 footer foreshadows the reveal. **Why:** setup and payoff. **Where:** 1, 17.
7. **What:** mark cuttable content in notes. **Why:** recover time if running late. **Where:** 21, the hooks paragraph in slide 7's notes, the banned-shortcuts paragraph in slide 14's notes, the escalation-ladder paragraph in slide 15's notes.
8. **What:** self-explanatory slides for a first-time audience: a 4-term primer, a "what it is" line on each divider and intro slide, terms defined on first use; in eqc-kit and /orchestrate, denser slides (tables with context, comparison, pros/cons) so a slide read without the speaker still makes sense, plain titles, no jokes, and casual first-person notes. **Why:** nobody has seen these tools; the speaker wants the deck to work without narration. **Where:** 3, 4-9, 11-17, 18, 19.

## Slides

Revision 4, 26 slides (regenerated 2026-11-17). Slides 11-17 are new copy (revision 4, approved); slides 4-10 are revision 3 copy; slides 1-3 and 18-26 are revision 2 copy (18-26 = old 21-29), changed only in renumbering and cross-references. `(hi)` = `.hi` / `.on` emphasis; ` / ` (with spaces) in a title = line break before the `.accent` part; a slash command keeps its slash. Notes lines are separate lines in `<aside class="notes">`. dtable has no row highlight: its one emphasis is `th.acc`. A "Builder note" is for the design-creator, not for `<aside class="notes">`.

### Slide 1 — Ask first, build cheap, ship clean (title)
On-slide copy:
- Kicker: Mehedi Hasan · Mobile Team
- Ask first, build cheap, / ship clean
- My everyday AI workflow: three tools for checking, planning and shipping code.
- Built with /create-presentation — more on that later.

Speaker notes:
Hi, I'm Mehedi, from the Mobile Team. This is the AI workflow I actually use every day, not the conference-poster version.
Three tools: one checks code, one plans work, one chain ships it. Each stands on its own.
Goal: you leave with two or three things to try this week.
Ignore that footer for now. It comes back on slide 17.
Transition: "Let's start with a document most of us have never read to the end."
~0.5 min

### Slide 2 — 39 rules. One long doc. Nobody wants to check them by hand. (center)
On-slide copy:
- Kicker: The problem
- 39 rules. One long doc. / Nobody wants to check them by hand.
- Our quality standard: 39 rules in 3 tiers (9 LOW, 13 MEDIUM, 17 HIGH).
- Today: eqc-kit checks · /orchestrate plans · the ship chain ships.

Speaker notes:
Show of hands: who has read the whole quality standard, end to end? Keep your hand up if you checked your own code against every rule.
(Expect very few hands. That's the point.)
The standard is fine. The problem is that checking 39 rules across a whole app by hand is a week of nobody's favourite work, so it doesn't happen.
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
- Checks your code against your team's own quality standard

Speaker notes:
Section one: eqc-kit. About 10 minutes, then questions.
This is the one I built myself, so I'll start with how that happened.
Transition: "It started with one question."
~0.25 min

### Slide 5 — How I ended up building eqc-kit (steps-list)
On-slide copy:
- Kicker: eqc-kit · Why I built it
- How I ended up / building eqc-kit
- 01 I was handed our quality standard — and one question: are your projects compliant?
- 02 So I checked it by hand — Read a rule, looked through the project, wrote it down, next rule. Tedious.
- 03 Then I used AI — It helped, but it was still too much work, and I didn't fully trust the answers.
- 04 So I automated it (hi) — One thing led to another. Now it's eqc-kit: an open-source (MIT) npm package that checks your code against your own written standard.
- `npx eqc-kit init` · works in Claude Code, Codex, Cursor, Copilot and Gemini CLI

Speaker notes:
So, quick story. I was given the EQC docs and asked if my projects were compliant.
I went through the doc and checked it one by one against the project. It was a tedious job.
I was using AI, but it was still too much.
So I started to make the process automated. And one thing led to another, and now I have this entire eqc-kit.
It's not tied to our doc. You bring any written standard, and the tiers come from it: LOW/MEDIUM/HIGH, Bronze/Silver/Gold, whatever your doc uses.
Install is one command. The setup asks a few questions, and they all have defaults, so you can just keep pressing Enter. No dependencies, Node 18 or newer.
In Claude Code you get slash commands. In the other tools it adds a block to AGENTS.md, so you just say "eqc check".
Transition: "Before I built it, I tried the two obvious ways. Here's how they compare."
~1.25 min

### Slide 6 — Three ways to check a project against the standard (dtable)
On-slide copy:
- Kicker: eqc-kit · Why not just ask AI?
- Three ways to check a project / against the standard
- Table Question | Manual review (read the doc, check each rule by hand) | Ask AI directly (paste the doc, ask "is my project compliant?") | eqc-kit (acc):
  - Can I trust a "pass"? | Yes, if I was careful | It said pass when it wasn't | Every rule's answer points at the file that proves it; a plain script, not the AI, works out the level
  - Is every rule checked? | Easy to skip one when you're tired | Lost track halfway | First it lists every rule; then one agent per tier checks them
  - Same answer next time? | Depends who checks | Different answer every time | Saved results are re-read, not re-guessed; a plain script turns the same answers into the same level every time.
  - Does it stay fixed? | One-off check | Fixed today, broken again by the next feature | Remembers every rule that passed; `eqc guard` and optional git hooks catch it slipping back
  - What does each run cost? | Your time, every time | Same exploring, same tokens, every time | Re-reading saved results costs nothing; uses your code map if it's up to date
- The catch: you need a written standard, the first full check takes time and tokens, and agents can still get it wrong, so read the evidence.

Speaker notes:
Manual review is where I started. It works if you're careful, but it's slow and it's a one-off. Nobody does it twice.
Then I tried the obvious thing: paste the doc into the AI and ask "is my project compliant?" Here's what actually happened to me.
It said pass when it wasn't.
It lost track halfway through. Thirty-nine rules is a lot to hold in one go.
Ask twice, get a different answer.
It fixed things for now, and later, while working on a new feature, the AI would break the same rule again.
And every time, it burned tokens and time doing the same exploring from scratch.
The right column is what eqc-kit does about each one. By "answer" I mean pass, partial, fail or not applicable, plus the file that shows it. You can open the file and argue with it.
Bottom line on the slide is the honest part. You need a written standard first. The first full check isn't cheap. And the agents can still be wrong, which is exactly why every answer comes with evidence you can read.
Transition: "So what do you actually run?"
~2.25 min

### Slide 7 — What you run, and where AI is used (dtable)
On-slide copy:
- Kicker: eqc-kit · The commands
- What you run, / and where AI is used
- Table Command | What it does (acc) | Uses AI?:
  - `/eqc-check` | Turns your doc into a rule list, then one agent per tier checks the code (using a code map, e.g. a graphify graph, first, if yours is up to date). Each rule gets pass / partial / fail / n/a with the file as proof. A plain script works out the level (the highest tier with no fails at or below it). Writes `COMPLIANCE.md` and a `COMPLIANCE.html` page. | Yes, to check rules. No, to count.
  - `/eqc-fix` | Suggests what to fix first: low effort, high gain. Small fixes go straight to one helper; big ones get a plan you approve first. Never commits for you. | Yes
  - `eqc guard` | Compares the latest results with the baseline (every rule that has passed). Fails only if one of those stops passing, or the level drops. Known fails don't block you. | No
  - `verify` + git hooks | An optional shell check (e.g. `npm run lint`), only for rules a command can test. Runs on commit and push once you opt in with `npx eqc-kit hooks`. | No: too slow, costly and unpredictable for every commit

Speaker notes:
Four things you run. The top two use AI, the bottom two don't.
/eqc-check: the first time, one agent reads your doc and lists every rule by tier. Then one agent per tier goes through the code, in parallel.
If you already have a code map, like a graphify graph, it looks there first, but only if the map is newer than your last commit and your uncommitted changes. It never builds or refreshes the map for you, and anything it finds there it confirms in the real code.
Then a plain script, no AI, works out the level: the highest tier where that tier and every tier below it have no fails. A fail in the lowest tier is HARD_FAIL. The script never reads your code; it just counts the answers.
New: next to the Markdown report you also get an HTML page. One file, no JavaScript, you just open it in the browser.
/eqc-fix: it ranks what to fix, low effort and high gain first. Small stuff goes to one fixer. Bigger stuff: opus writes a plan, you approve it, and cheaper models do the typing. It asks before touching CI, packages, architecture or the top tier, and it only runs one fixer at a time.
guard: this is the answer to "AI fixed it, then broke it again". Every time results are saved, it remembers which rules passed. That's the baseline, and it only goes up. Guard checks against it. A rule that was already failing won't block you; only something that used to pass and now doesn't.
verify: some rules a plain command can check, like "lint is clean". Those rules carry a command, like npm run lint. Not every rule gets one, only the ones a command can check without judgment. The script runs them only for rules that are passing, so a known fail never blocks a commit; only a regression does.
CUTTABLE if running late — hooks: opt-in, one command per clone, npx eqc-kit hooks. Commit runs verify; push runs verify, then guard. It won't override hooks you already have, like Husky; it prints the lines to add instead. Anyone can skip hooks with --no-verify, so put the same two commands in CI.
Why no AI in the hooks? Too slow, costs money on every commit, and you'd get a different answer each time.
Transition: "Enough talking. Let me show you two of these, and the report it writes, on our app."
~2 min

### Slide 8 — Demo: check, report, and what to fix next (demo)
On-slide copy:
- Badge: Live demo
- Kicker: Demo · /eqc-check · the report · /eqc-fix
- Demo: check, report, / and what to fix next
- 01 `/eqc-check` with no arguments (hi) — Re-reads the last saved results: level per tier, every open fail with its evidence. Instant, no agents running.
- 02 Open `docs/eqc/COMPLIANCE.html` — The same results as one page in the browser: level, progress per tier, what needs attention, every rule.
- 03 Run `/eqc-fix` — A ranked list of what to fix next, low effort and high gain first. I'll cancel before it changes anything.

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

### Slide 9 — Our mobile app went from HARD_FAIL to MEDIUM in about 5 days (dtable)
On-slide copy:
- Kicker: eqc-kit · Our mobile app
- Our mobile app went from HARD_FAIL / to MEDIUM in about 5 days
- HARD_FAIL = a rule in the lowest tier fails. MEDIUM = no fails in LOW or MEDIUM. Today: MEDIUM, 33 pass, 2 partial, 4 fail.
- Table What changed | How much (acc):
  - ESLint errors | 54 errors in 30 files. This alone took us from HARD_FAIL to LOW.
  - `console.*` → our Logger | 58 files
  - `Platform.OS` checks → `Platform.select()` | 34 places
  - Tests kept green the whole way | ~85 test files touched, 2,912 of 2,912 passing
  - Still failing (4) | 3 big architecture jobs (state migration across 123 files, a data-fetching library, certificate pinning) + TypeScript, recorded as a fail because the project has to stay JavaScript

Speaker notes:
The guess: 58 files for the Logger sweep.
Fifty-eight. And the level you saw in the terminal: MEDIUM, right there in the title.
We started at HARD_FAIL. Fixing the ESLint errors alone got us to LOW. All in, 27 recorded fixes in about five days: 25 done, 2 partial.
Not on the slide: FlatList windowSize on 33 lists, and Crashlytics error handling in 17 files.
My favourite one: the i18n rule took 7 audits and 6 rounds of fixes, because every audit found more hardcoded English. In the end I added a custom ESLint rule so it can't come back.
The four still failing are honest. Three are big architecture moves, not quick wins. TypeScript can't pass because the project has to stay JavaScript, so the kit records it as a fail and says why it doesn't apply, instead of pretending. I'd rather have an honest fail than a fake pass.
Also, the audit found a hardcoded secret in the codebase. I'm not naming it. It's handled.
(The "today" numbers come from the cached check. Re-run before the talk and update if they moved.)
Transition: "That's eqc-kit. Questions before we move on?"
~1.75 min

### Slide 10 — Questions? (eqc-kit) (center)
On-slide copy:
- Kicker: Q&A
- Questions?
- eqc-kit

Speaker notes:
Open the floor.
If it's quiet, seed one: "Which tier would your project land in today?" or "Which of your rules could a plain command check, like lint?"
Watch the clock: this buffer is 2 minutes. Move on at 15 minutes into the talk.
Transition: "eqc-kit checks code against a standard. Next is how I get bigger work done without burning my best model."
~2 min — Q&A buffer

### Slide 11 — 02 · /orchestrate (divider)
On-slide copy:
- 02 · /orchestrate
- Plans big work with you, then sends each task to the cheapest model that can do it

Speaker notes:
Section two: /orchestrate. It's a separate tool, you can use it without eqc-kit.
About 12 minutes, then questions.
Same as before, I'll start with why I built it.
Transition: "It came out of a habit I had with plan mode."
~0.25 min

### Slide 12 — Why I built /orchestrate (steps-list)
On-slide copy:
- Kicker: /orchestrate · Why I built it
- Why I built /orchestrate (accent on "/orchestrate", no line break)
- 01 I kept going back to plan mode — Plan mode: Claude Code writes a plan and waits for your OK before it edits. I used it for every long task.
- 02 I typed the same asks every time — Split into phases, a sub-agent per phase on a model that fits, interview me first. Same prompt, every big task.
- 03 So I made it a skill (hi) — Now it's /orchestrate. One command, and the instructions are already there.
- Why I built it: to spend fewer tokens by sending each piece to the cheapest model that can do it.

Speaker notes:
This one comes straight out of my day-to-day work.
I was doing my usual work and kept going back to plan mode. Every time, I asked Claude to split the long work into phases, hand each phase to a sub-agent on a model that matches how hard that piece is, and interview me before starting.
It was the same prompt and the same instructions over and over again, every big task. So I started building this skill.
The main reason I built it is tokens. Most pieces of a big task don't need the biggest model. If each piece goes to the cheapest model that can do it, you spend fewer.
I don't have a number for that, and I'll come back to it in a couple of slides.
Transition: "Before the skill, I used three other ways. Here's how they compare."
~1.5 min

### Slide 13 — Four ways to run a big task with AI (dtable)
On-slide copy:
- Kicker: /orchestrate · Why not plan mode or /goal?
- Four ways to run a big task with AI (accent on "a big task with AI", one line, smaller h2)
- Table Question | Long prompt every time | Plan mode | /goal (keeps working until the goal is met) | /orchestrate (acc):
  - Remembers the instructions? | No, you retype or paste them | No, you retype your asks | No, it keeps the goal, not your method | Yes, it's a skill
  - Interviews you first? | Only if you type that in | Only if you ask, every time | No, it just starts working | Yes (if needed), one question at a time
  - Stops for your OK before building? | No, it starts editing | Yes, once, for the whole plan | No, it starts working right away | Yes, a hard gate: "just go" in your goal doesn't skip it
  - Picks a model per task? | No, same model for everything | No, one model builds it all | No | Yes, by score: haiku, sonnet or opus
  - Who checks the work? | Nobody, unless you do | The same model that built it | It checks itself | A separate haiku verifier, plus sonnet or opus reviewers
  - Picks up after a break? | No, forgets between sessions | No, the plan lives in the chat | Only within the session | Yes, from the plan file (`/orchestrate resume`)
- The catch: the planning and checking add overhead that isn't worth it on small tasks, it has to run on opus or sonnet (it stops on haiku), and you still read the report.

Speaker notes:
These are the three things I used before. The first three columns are how each one worked for me day to day, not a feature list from the docs.
Long prompt: it works, but I pasted it every time, one model did everything, and nothing stopped it before it started editing. Next session, it was gone.
Plan mode is good at planning. But I still typed the phases, the sub-agents, the models and the "interview me" part every time. Once I approved, one model built the whole thing and checked its own work, and the plan only lived in that chat.
/goal keeps going until the goal is met. It doesn't ask me anything first, it starts working right away, there's no model choice, and it checks itself.
The /orchestrate column is what the next two slides explain. On the OK row, the difference is that its gate can't be skipped: even "just go" written into the goal doesn't skip it. "If needed" on the interview: for tiny goals it takes a fast lane and skips the questions. The verifier still runs.
The bottom line is the honest part. On a small task, all that planning and checking is overhead you don't need. It has to run on opus or sonnet; on haiku it stops and asks you to switch. And you still read the report at the end.
Transition: "So what's it actually like to use?"
~2.75 min

### Slide 14 — How /orchestrate runs a big task, phase by phase (dtable)
On-slide copy:
- Kicker: /orchestrate · How it works
- How /orchestrate runs a big task, / phase by phase
- Lead: Five phases: GRILL → PLAN → PREVIEW → EXECUTE / VERIFY → CLOSE. The orchestrator doesn't write the code; helpers on haiku, sonnet or opus do.
- Table Phase | What it does (acc):
  - GRILL | Asks you questions one at a time, each with a recommended answer. If you have a code map, its helpers search that before grepping. Tiny goals skip this step (fast lane).
  - PLAN | Splits the goal into tasks and scores each one (next slide). At most 3 helpers run at once, and each file has one owner.
  - PREVIEW · the gate | Shows every task with its score and model, then stops. Only your reply counts: "just go" written into the goal is ignored, and "ok, but…" is an edit.
  - EXECUTE / VERIFY | Helpers build. A haiku verifier runs the checks; a sonnet reviewer reads the diff (an opus security reviewer for security tasks). The orchestrator may make one fix of 5 lines or less per task, only for a bug the verifier found.
  - CLOSE | Reports which models did the work. Everything is in a plan file, so you can stop, resume or reject. Never commits on its own.

Speaker notes:
This is the whole thing in one table. I'll go through it quickly.
GRILL is the interview I used to ask for by hand. One question at a time, and it gives you its recommended answer, so most of the time I just say yes. If the goal is tiny, it skips this.
PLAN: it splits the goal into tasks and scores each one. Scoring is the next slide. It also decides up front who owns which file, so three helpers working at the same time don't step on each other.
PREVIEW is the part I care about most. It shows the full plan and stops. I'll show you that live in a minute.
EXECUTE: the orchestrator doesn't write the code, the helpers do. The one exception is a fix of 5 lines or less per task, and only for a bug the verifier found. Then a cheap haiku verifier re-runs the checks, and a separate reviewer reads the diff.
CLOSE tells me which models actually did the work. Everything lives in a plan file under docs/plans, so I can stop, close the laptop, and run /orchestrate resume the next day. It suggests a commit; it never makes one.
CUTTABLE if running late — the shortcuts it isn't allowed to take. Each one sounds reasonable in the moment. "I'll do this quick fix myself": hand it to a helper. "Approval was given in advance": show the preview anyway. "Small repo, I'll just read it": it reads at most 2 files of 100 lines per phase itself and sends a scout for the rest. "I'll run the tests to be sure": the verifier does that. "This agent sets its own model": pass the model anyway.
Transition: "The part of PLAN I want to show you is how it picks the model."
~2.5 min

### Slide 15 — How it picks a model for each task (dtable)
On-slide copy:
- Kicker: /orchestrate · Picking a model
- How it picks a model / for each task
- Lead: Each task scores 0–2 on Ambiguity (how unclear it is), Breadth (how much it touches) and Reasoning (how hard it is to think through). The total picks the model.
- Table Score or task type | Goes to (acc):
  - 0–2 | haiku
  - 3–4 | sonnet
  - 5–6 | Split into smaller tasks first; opus only if it can't be split
  - Security work (auth, secrets, crypto, permissions…) | Always opus, plus an opus security reviewer
- You can ask for opus yourself. If a plan has more than 2 opus tasks, it asks you to confirm.
- Its rule: "When unsure, pick the lower tier: escalating costs less than over-provisioning."
- If a task fails: haiku retries → sonnet retries → one opus try, or the orchestrator re-scopes it → still failing? It pauses and tells you.

Speaker notes:
GUESS-FIRST: which model gets "add a config entry with exact steps"? Take a few answers. (Answer: haiku. It's clear, it's one file, and it doesn't need much thinking.)
Three questions per task: how unclear is it, how much does it touch, how hard is it to think through. Zero to two each, add them up.
Big tasks get split first. Opus only gets a task that really can't be split, or anything that touches security, like auth, secrets, crypto or permissions. Those always go to opus, and a fresh opus reviewer goes through the diff looking for vulnerabilities.
The rule I like most is the one on screen. When it's unsure, it picks the cheaper model. If that was wrong, the task fails and moves up. That still costs less than sending everything to the big model just in case.
That's where the token saving comes from. I can't give you a number. Try it on one real task and look at the model mix it reports at CLOSE.
CUTTABLE if running late — the retry ladder: a failed haiku task retries once on haiku with the exact error and the current diff, then moves to sonnet. Sonnet retries once, then the orchestrator either tries opus once or works out the problem itself and re-scopes or splits the task. If that still fails, it pauses and reports to me. Every retry is logged in the plan file.
Transition: "Now the gate itself, live."
~2 min

### Slide 16 — Demo: the preview gate (demo)
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
Transition: "That's the check before anything runs. Here's what the checking after looked like on real runs."
~1.75 min

### Slide 17 — What happened when I used it (vs-grid)
On-slide copy:
- Kicker: /orchestrate · In practice
- What happened / when I used it
- Left vs-card: label "My runs" · title "Two "done" claims that weren't true"
  - Coverage audit: the agent said "done", but ~65 identifiers were missing. Retried with the exact list: 0 missing.
  - E2E (end-to-end) test: the agent said line 143 was covered. It wasn't.
- Right vs-card (hi): label "This deck" · title "Built by a skill that /orchestrate built"
  - The skill: /create-presentation made these slides.
  - The build: /orchestrate built it in 5 tasks + 2 fixes, 0 escalations (before the opus tier existed).
- Closing line: Questions?

Speaker notes:
Two real catches from my own runs. In a test-coverage audit, a sonnet helper wrote from memory and said it was done. The verifier found about 65 identifiers missing. The retry got the exact list and came back with zero missing.
Another time, a helper said line 143 of an end-to-end test was covered. A coverage refresh said it wasn't.
Verifiers get it wrong too. On one run the final verifier raised a false alarm because its search matched numbers in CSS. So I still read the report.
Across about 11 runs, most of the work went to haiku and sonnet.
One thing to be clear on: the ~11 runs and the 0-escalation build all happened before I added the opus tier you saw on slide 15.
Now the right side. Remember the footer on slide 1? /create-presentation is the skill that built this deck, and /orchestrate built that skill. 5 tasks plus 2 fixes, nothing had to move to a bigger model, and one 1-line fix during VERIFY.
Before any real work, an opus dry-run found 15 issues in that skill; 13 got fixed. And the CSS false alarm I just mentioned was this same build.
The facts in this deck come from a context file in the same folder, so it doesn't make numbers up. If a slide is wrong, that file is the place to check.
Q&A: open the floor on /orchestrate. Seed if quiet: "What's a ticket on your board right now that would score 0–2?" Move on at about 30 minutes in.
Transition: "Last section is lighter: what happens after the code is written."
~4.25 min (~1.75 content + 2.5 Q&A buffer)

Builder note: applied (review finding 7). The "~11 runs" line is no longer on the left card; it lives only in the notes ("Across about 11 runs…"). Keep the right card whole.

### Slide 18 — 03 · The ship chain (divider)
On-slide copy:
- 03 · The ship chain
- After the code works: commit, PR, release notes, build

Speaker notes:
Section three, lighter coverage. Each skill is small on its own; the value is that they connect.
Transition: "Here's the chain."
~0.25 min

### Slide 19 — Each skill feeds the next (steps-list)
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

### Slide 20 — One change, four write-ups, four readers (dtable)
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
Transition: "Which means commits get written with the next step in mind." (If slide 21 is cut: "Here's a real one." and go to slide 22.)
~1.5 min

### Slide 21 — Commits are written for the release notes (code-block)
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

### Slide 22 — Demo: v1.9.4 notes beside their commits (demo)
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

### Slide 23 — No release notes, no build (center)
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

### Slide 24 — Ask first, build cheap, ship clean (card-grid)
On-slide copy:
- Kicker: Recap
- Ask first, build cheap, / ship clean
- eqc-kit: Ask first: big fixes wait for your OK · checks your code, keeps passing rules passing
- /orchestrate: Build cheap: score the task, then pick the model · plans, then cheaper models build
- ship chain (hi): Ship clean: write the commit for its next reader · commit → PR → notes → build

Speaker notes:
One sentence each.
eqc-kit: agents check your code against your own standard, a plain script works out the level, big fixes wait for your OK, and the guard stops passing rules from slipping back.
/orchestrate: every task gets a score before it gets a model; you approve the plan, cheaper models build and a verifier checks.
Ship chain: write the commit for whoever reads it next, and it becomes the PR, the release notes and the store note, with CI making sure.
Transition: "You don't need all three. Pick two."
~0.75 min

### Slide 25 — Pick two. Try them this week. (closing)
On-slide copy:
- Kicker: Your move
- Pick two. / Try them this week.
- Quality doc nobody checks? `npx eqc-kit init` · Big ticket? `/orchestrate` · Vague commits? `/git-commit` today
- Get /orchestrate and /git-commit: paste into Claude Code → "Fetch and follow https://raw.githubusercontent.com/mehedibangladeshi/ai-skills/master/INSTALL.md"

Speaker notes:
Pick the two that match your pain. If your commit messages say "fix", /git-commit is the five-minute win: start today.
The install line is a prompt: paste it into your agent and it sets up the skills.
It's my repo — read INSTALL.md first if you like.
The same lines stay on the next slide through Q&A, so no rush to copy.
Transition: "Thanks. Last round of questions."
~0.75 min

### Slide 26 — Questions? (final) (center)
On-slide copy:
- Kicker: Q&A
- Questions?
- Quality doc nobody checks? `npx eqc-kit init` · Big ticket? `/orchestrate` · Vague commits? `/git-commit` today
- Get /orchestrate and /git-commit: paste into Claude Code → "Fetch and follow https://raw.githubusercontent.com/mehedibangladeshi/ai-skills/master/INSTALL.md"

Speaker notes:
Thank everyone. Open the floor for anything across the three sections.
Seed if quiet: "Which two are you trying first?"
Leave this slide up through Q&A: the commands and the install line stay on screen.
Transition: none, this is the end.
~2 min — Q&A buffer

## Open questions

Items 5-7 and 9 are resolved history and keep pre-revision-3 slide numbers. Items 1-4, 8, 10-12 use revision 3 numbers unless marked; items 13-18 are revision 4 (26-slide numbering). Revision 4 renumbering for items 2-4: demo 15 → 16, demo 25 → 22; slides 16/18/24 cut list → 21 plus the notes paragraphs in engagement item 7.

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
11. Dev eqc-kit: presented as available. Confirm it is published before the talk and give the version, or the slides stay version-free [TBD]. Known dev wording bug: `npx eqc-kit hooks` output still says "verify + gate" though the pre-push hook runs `guard` (sources.md, Contradictions); avoid running `hooks` live or fix it before publishing.
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
