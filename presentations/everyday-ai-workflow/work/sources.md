## eqc-kit dev branch changes (unreleased until talk; will be published by the talk)

Base dir for citations (all paths below are relative to it): `/private/tmp/claude-501/-Users-mehedihasan-dev-questionpro-ETH/411b776d-d60e-4877-aa0f-8d72383b4e98/scratchpad/eqc-dev/`. `engine/eqc.mjs` and `bin/cli.mjs` are NOT in the export, so engine and CLI facts cite `DIFF-main-to-dev.patch` line numbers (patch lines, not source lines).

- Released version is 0.1.0, dated 2026-09-29; everything below is under "[Unreleased]" [CHANGELOG.md:7, 22]
- Dev has three merged PRs on top of main, all dated 2026-11-17: #3 `feat/visual-report`, #2 `feat/guardrails`, #1 `feat/guardrails` [LOG-main-to-dev.txt:1, 11, 13]
- Earlier dev commit dated 2026-10-30, titled "guardrails: keep agents and commits from breaking passing Rules between audits" [LOG-main-to-dev.txt:31]
- Plan log: "npm test 60/60" and "selftest ok" at the final verifier step [docs/plans/2026-11-16-codemap-report-guardrails.md:42]

### Feature 1: code map (exploration aid)
- Problem: explore a code map before reading files, but only when it is fresh. Definition: "A pre-built index of the project's code (symbols, calls, dependencies), such as a graphify graph, used to explore before reading files. Used only when fresh: not older than the latest commit or uncommitted changes." [CONTEXT.md:68-69]
- Detected maps: `graphify-out/graph.json`, `.codegraph/`, `.gitnexus/`, `.serena/` [prompts/codemap.md:8]
- Freshness: map file mtime compared with `git log -1 --format=%ct` and with each file in `git status --porcelain` [prompts/codemap.md:10]
- "The agent never builds or refreshes the map itself." [docs/concepts.md:144]
- "Never build, install, refresh or update a map, even if an update command exists." [prompts/codemap.md:11]
- Stale map: skipped with a one-line hint, e.g. `graphify update .` [docs/concepts.md:144; prompts/codemap.md:11]
- Map facts must be confirmed in source: "The map is never sole evidence." [prompts/codemap.md:17]
- Prompt-only feature: `MAP: none (<reason>)` or `MAP: <tool> ... (fresh)` line in every sub-task brief [prompts/codemap.md:13; prompts/check.md:22; prompts/fix.md:19]
- Plan goal 1: "Workflow uses a code map ... when present during exploration, after verifying it is up to date." [docs/plans/2026-11-16-codemap-report-guardrails.md:4]
- Plan's own map check, 2026-11-16: "MAP: none (no graphify-out/, code-graph index dirs, or graph MCP tools in repo; checked 2026-11-16)" [docs/plans/2026-11-16-codemap-report-guardrails.md:9]

### Feature 2: HTML compliance report
- Every `merge` and `report --write` also writes `<report>.html` beside the `.md` report [LOG-main-to-dev.txt:4; docs/engine-commands.md:65]
- "a single self-contained page (no JavaScript) with level and tier progress, what needs attention, and all Rules by tier." [CHANGELOG.md:17]
- "Inline CSS only, no JavaScript or external URLs, light/dark and print styles, all values escaped." [LOG-main-to-dev.txt:5-6]
- Default path example: `docs/eqc/COMPLIANCE.html` [README.md:61]
- Writer: `buildHtmlReport` (`<!doctype html>`, no `<script>`, selftest asserts this) [DIFF-main-to-dev.patch:1120-1176, 1320-1321]
- CI guidance: "The same result as a page to open in a browser. Review the Markdown diff instead." [docs/ci.md:16]
- Report also gains: `Baseline:` line, `## Regressions`, `## To reach <Tier>`, `## Not audited` [docs/engine-commands.md:122-128]
- Problem statement for the HTML page is not written in any plan or ADR (see Gaps).
- Plan goal 2 (the readable check report, related): "`/eqc-check` report names every missing compliance by ID + title, not just IDs/chart." [docs/plans/2026-11-16-codemap-report-guardrails.md:5]

### Feature 3: compliance baseline and `eqc guard`
- Problem: "once a compliance is achieved, later work (features, fixes, config, refactor, reorg) must not regress it." [docs/plans/2026-11-16-codemap-report-guardrails.md:6]
- Baseline definition: "It only ever rises; a later fail never lowers it." [CONTEXT.md:51-52]
- Protected rule: "A Rule recorded as pass in the Baseline. Any later Verdict other than pass or na for it is a Regression." [CONTEXT.md:55-56]
- Regression definition: "A Protected rule whose current Verdict is fail or partial, or a Compliance level below the Baseline level." [CONTEXT.md:59-60]
- Naming: `guard` replaces the planned `gate`; glossary: "_Avoid_: gate (a Gate is an approval pause)" [CONTEXT.md:65; LOG-main-to-dev.txt:16]
- Command: `eqc guard [--min TIER]`, exit 1 on failure [docs/engine-commands.md:41; docs/engine-commands.md:22]
- Guard fails when a protected rule is `fail`, `partial` or unaudited; when level is below baseline; or with `--min` below that tier [docs/engine-commands.md:171-177]
- `pass` to `na` is not a regression [docs/engine-commands.md:174 (bullet text "A change from `pass` to `na` is not a regression.")]
- Before first merge: "guard: no baseline yet", exit 0 [docs/engine-commands.md:181]
- Example run: `guard: ok · baseline BRONZE · 13 protected rules` [docs/engine-commands.md:184-185]
- Example run: `guard: REGRESSION` then `- BRONZE-1 — CI runs on every pull request — now fail` and `- level HARD_FAIL below baseline BRONZE`, exit 1 [docs/engine-commands.md:186-191] (example text; see Gaps on capture)
- Baseline file: "Written only by `merge`, never by hand." Level "is kept when a later merge would lower it." [docs/engine-commands.md:451]
- "The only way to lower the baseline is to delete the file by hand, which is a deliberate decision." [docs/concepts.md:138]
- Why commit it: "Commit it: CI's `guard` reads it." [docs/engine-commands.md:451]
- `reset` now also deletes `baseline.json`; "Deleting the baseline forgets the protected Rules" [docs/engine-commands.md:293]
- Guard result is printed by `merge`: `guard: 2 regressions — run eqc guard` [docs/engine-commands.md:273-274]
- Guard "reads recorded Verdicts only and audits nothing" [docs/engine-commands.md:179]
- Guard vs verify: "`verify` checks the code itself; Guard checks recorded Verdicts. Git hooks and CI run both." [CONTEXT.md:66]
- Why guard alone is not enough: "on its own it is only as fresh as the last Audit and never looks at new code." [docs/adr/0004-engine-runs-verify-commands.md:11]
- Tests: "60/60 tests, selftest ok" at the 1.1 step; "npm test 60/60" at final verify [docs/plans/2026-11-16-codemap-report-guardrails.md:37, 42]

### Feature 4: per-rule `verify` commands run by the Engine
- Problem and mechanism: "To stop new code from breaking Rules between Audits, a Rule in `rules.json` may carry a `verify` shell command, and `eqc.mjs verify` runs it for passing Rules from git hooks and CI." [docs/adr/0004-engine-runs-verify-commands.md:3]
- "Only passing Rules are run, so a known fail never blocks a commit; only a regression does." [docs/adr/0004-engine-runs-verify-commands.md:3]
- "The command decides, and the agent wrote it at index time." [docs/adr/0004-engine-runs-verify-commands.md:3]
- Trust: "`rules.json` is committed and reviewed like `package.json` scripts, which carry the same trust: anyone who can change it can make hooks and CI run a command." [docs/adr/0004-engine-runs-verify-commands.md:5]
- Bends the old rule: "This bends ADR 0002's 'the Engine never reads code': the Engine now executes commands, but it still never interprets a Rule." [docs/adr/0004-engine-runs-verify-commands.md:3]
- Command: `eqc.mjs verify [ID,...]`; runs `verify` of passing Rules only; exits 1 on any failure [docs/engine-commands.md:50, 346-348]
- Example output: "verify: 1 of 2 failed — fix the code, or re-audit if the Rule no longer passes" [docs/engine-commands.md:356]
- No passing Rule has a command: prints `verify: no passing rules with a verify command`, exit 0 [docs/engine-commands.md:361]
- Command is run from repo root with `shell: true` [DIFF-main-to-dev.patch:1293]
- Indexer adds `verify` only for mechanically checkable rules: "Add it ONLY for rules a command can check mechanically on the code (lint clean, no debug prints, no hardcoded URLs, formatter clean)." [prompts/index.md:19]
- Indexer rule: "When unsure, omit it: git hooks and CI run these commands, so a noisy one blocks every commit." [prompts/index.md:19]
- Repo-level rules (CI exists, README, release process) get no `verify` [prompts/index.md:19]
- Example entry: `"verify": "npm run lint"` [docs/engine-commands.md:404; prompts/index.md:25]
- Audit prompt: a non-zero `verify` exit means not `pass` [prompts/audit.md:8]
- Fixer: after a fix, a `verify` command must exit 0 [prompts/fixer.md:24]
- Rejected alternatives (ADR 0004): LLM audit in pre-commit; generating ESLint/ruff configs from Rules [docs/adr/0004-engine-runs-verify-commands.md:9-10]
- Rationale for linter option: "A `verify` command can call the project's own linter instead." [docs/adr/0004-engine-runs-verify-commands.md:10]

### Feature 5: git hooks and `npx eqc-kit hooks`
- New installer command `hooks` with flags `--force` (enable anyway) and `--off` [docs/commands.md:19, 21, 159]
- `pre-commit` runs `node .eqc/bin/eqc.mjs verify`; exit 2 (not indexed) allows the commit [adapters/git-hooks/pre-commit:3-7]
- `pre-push` runs `verify`, then `guard`; exit 2 allows [adapters/git-hooks/pre-push:3-12]
- Hooks table: pre-commit blocks when a passing Rule's verify fails; pre-push also blocks on a protected Rule regression [docs/commands.md:163-166]
- Opt-in, per clone: "Git config is not committed, so each teammate runs it once per clone" [docs/commands.md:161]
- Command sets `git config core.hooksPath .eqc/hooks` [docs/commands.md:161]
- "It never bypasses an existing setup." [docs/commands.md:176]
- With an existing hook setup, exits 1 and prints lines to add: `sh .eqc/hooks/pre-commit` / `sh .eqc/hooks/pre-push` [docs/commands.md:178-184]
- `--force` "enables them anyway, which turns your `.git/hooks/` off" [docs/commands.md:186]
- `git commit --no-verify` skips hooks, so "also run them in CI" [docs/commands.md:168]
- Rationale, opt-in: "Hooks are opt-in per clone (`npx eqc-kit hooks`), in line with ADR 0001." [docs/adr/0004-engine-runs-verify-commands.md:5]
- ADR 0001 rationale: "npm 7+ hides lifecycle output and gives scripts no TTY, so prompts hang or are skipped" [docs/adr/0001-no-postinstall.md:3]
- `uninstall` removes `.eqc/hooks/` and unsets `core.hooksPath` if it points there [docs/commands.md:137, 140; DIFF-main-to-dev.patch:327-328]
- Why CI too: "They are the build-time guard that `--no-verify` cannot skip" [docs/ci.md:54]
- Pipeline example: `verify` then `guard --min BRONZE` in GitHub Actions [docs/ci.md:63-75]
- Engine commands in hooks and CI are described as "cheap and deterministic": "Two Engine commands are cheap and deterministic, and do belong in CI." [docs/ci.md:54]

### Feature 6: CLAUDE.md guard block and AGENTS.md guard text
- Why a CLAUDE.md block: "since Claude Code then ignores `AGENTS.md`" [CHANGELOG.md:8]
- Why not always create CLAUDE.md: "It never creates a `CLAUDE.md` that would hide your `AGENTS.md`" [docs/agents/claude-code.md:26]
- Written only if CLAUDE.md exists, or the `agents-md` adapter is off [docs/agents/claude-code.md:19, 26; DIFF-main-to-dev.patch:246-249]
- Shared guard text, one source: `adapters/guard.md`, injected into AGENTS.md and CLAUDE.md blocks [adapters/guard.md:1-11; adapters/agents-md/block.md:11; adapters/claude-code/claude-md.md:1-5]
- Guard text: "Never edit or delete `.eqc/baseline.json`. Never weaken lint, test, CI or type-check settings, skip or delete tests, or relax thresholds to make a rule, `verify` or the guard pass." [adapters/guard.md:10]
- Guard text: "If a change cannot comply with a Rule, or a protected rule truly must change, stop and ask the user." [adapters/guard.md:11]
- Digest file `.eqc/RULES.md`: "Rule digest ... that agents read before writing code. Regenerated by `merge`." [CONTEXT.md:37-38]

### Changed behaviour of /eqc-check and /eqc-fix
- /eqc-check Path A prints the report verbatim: "Print it exactly as the engine outputs it: never shortened, summarized or turned into a chart." [prompts/check.md:25]
- Path C before/after format: `ID — title: <before> → <after>` [prompts/check.md:38]
- After every merge, run `guard`; exit 1 shows lines under a `Regressions` heading [prompts/check.md:55]
- Always name rules as `ID — title`, never bare IDs [prompts/check.md:58]
- Closing line names up to ~5 blockers, then "+N more — see report" [prompts/check.md:59]
- Closing line gives the HTML path: "Open <path> in a browser for the visual report." [prompts/check.md:60]
- /eqc-check output order in dev docs: level, Baseline line, Regressions, To reach, Not audited [docs/agents/claude-code.md:42]
- /eqc-fix: code map checked once per run before audit/plan/fix [prompts/fix.md:19]
- /eqc-fix: "A fix is not done while guard exits 1: repair the regression first." [prompts/fix.md:22]
- /eqc-fix: after merge runs guard and shows regressions as `ID — title — now fail|partial|not audited` [DIFF-main-to-dev.patch:452]
- /eqc-fix: "Never edit or delete `.eqc/baseline.json`." [prompts/fix.md:23]
- fixer: "`guard: REGRESSION` = not DONE." [prompts/fixer.md:28]
- Changelog "Changed" entry: "after each merge it runs the guard and shows regressions." [CHANGELOG.md:20]

### Contradictions with the current deck (everyday-ai-workflow)
- Deck says guardrails are "coming soon (unreleased)" [index.html:503; transcript.md:142; work/outline.md:343]. Sources: built on dev with tests, docs and prompts; not in 0.1.0 [CHANGELOG.md:7, 22]. "Coming soon" is stale; "built, unreleased" fits the sources.
- Deck says "a gate fails on regressions below a tier" and context says "`gate --min TIER`" [index.html:503; context.md:52]. Dev command is `guard [--min TIER]`, and `gate` is replaced [LOG-main-to-dev.txt:16]. Also guard fails on a single protected Rule regression even when the level stays the same [docs/engine-commands.md:174].
- Deck says "each rule gets a plain shell verify command" [index.html:503; transcript.md:142]. Sources: `verify` is optional, only for mechanically checkable Rules [prompts/index.md:19; docs/adr/0004-engine-runs-verify-commands.md:3; CONTEXT.md:43-44]. Contradiction.
- Deck says "No LLM in pre-commit" [index.html:497, 502; transcript.md:140]. Sources agree: ADR 0004 rejects LLM audit in pre-commit [docs/adr/0004-engine-runs-verify-commands.md:9]. Reason in source: "slow, costly and nondeterministic, and it needs agent credentials on every machine and in CI." [docs/adr/0004-engine-runs-verify-commands.md:9]
- Deck says the commit "takes 40 seconds" / "forty seconds" [index.html:502; transcript.md:140]. No timing figure exists in any source. Unsupported number.
- Deck says pre-commit / pre-push are opt-in via `npx eqc-kit hooks` [index.html:503]. Consistent with sources [docs/commands.md:161; README.md:69].
- Code and docs still say pre-push runs "verify + gate" in `hooks` output [DIFF-main-to-dev.patch:357; docs/commands.md:172]. The pre-push script actually runs `guard` [adapters/git-hooks/pre-push:9]. Stale wording; will show if the demo runs `hooks`.
- Engine: deck wording "never judges code" is consistent [README.md:9]. Engine now executes `verify` commands, so do not say the Engine never runs anything [docs/adr/0004-engine-runs-verify-commands.md:3].

### Demo candidates
- DEMO: `node .eqc/bin/eqc.mjs report --write`, then open the generated `docs/eqc/COMPLIANCE.html` in a browser (no JavaScript; print styles) [docs/engine-commands.md:65, 97; CHANGELOG.md:17]. Needs a real index and merged verdicts; no HTML file or screenshot is in the export.
- DEMO: regression. Re-audit one passing Rule as `fail`, `merge`, then `node .eqc/bin/eqc.mjs guard` prints `guard: REGRESSION` and exits 1 [docs/engine-commands.md:268-274, 184-191]. Documented example output only (see Gaps).
- DEMO: `node .eqc/bin/eqc.mjs verify` with a passing Rule whose command breaks (example: `console.log` grep) prints `FAIL ...` and exits 1, the same check the pre-commit hook runs [docs/engine-commands.md:351-357; adapters/git-hooks/pre-commit:4]. Example output in docs, not captured in export.
- DEMO (optional): `npx eqc-kit hooks` in a repo with Husky refuses and prints the `sh .eqc/hooks/pre-commit` lines [docs/commands.md:178-184].

### Gaps
- Engine source (`engine/eqc.mjs`), `bin/cli.mjs` and tests are not in the export. Engine and CLI facts rely on the patch only.
- The Baseline/`Regressions` report example and the `guard` REGRESSION example are not captured runs. The Baseline example is "written from the Engine's report code, not captured from a run" [docs/engine-commands.md:130]. The plan says the e2e run matches all doc formats except the Baseline case [docs/plans/2026-11-16-codemap-report-guardrails.md:42].
- No timing, speed or cost numbers for `verify`, hooks or guard anywhere in sources.
- No stated problem for the HTML report in any plan, ADR or CHANGELOG line beyond the feature description.
- No real code map (graphify run) example; the map feature is prompt text only.
- No dev release date or version number for these changes (CHANGELOG `[Unreleased]` has none).
- Not mined for dev changes: docs/troubleshooting.md, docs/writing-a-standard.md, docs/agents/{cursor,codex,copilot,gemini-cli,other}.md. The diff shows no dev changes in them.
- Deck's 40-second figure has no source.

## /orchestrate: current skill (AI-Skills repo, 2026-11-17)

Base dir for skill paths: `/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/` (abbreviated below as `orchestrate/`, full path in each citation). Git log and git show were not available (no Bash); commit dates and hashes come from the local reflog, with epoch timestamps converted by hand to +0600 dates.

### Characteristics
- Never implements: "**It never implements.** Every task goes to a `haiku`, `sonnet` or `opus` sub-agent." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:11]
- Never implements (skill wording): "**You never implement.** Every task row is `haiku`, `sonnet` or `opus`, except the one VERIFY fix in `references/execution.md`." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:14]
- VERIFY fix exception: "You may make one fix of ≤5 lines per task, only for a defect found in VERIFY." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/execution.md:34]
- Read cap: "You read at most 2 files per phase yourself, each ≤100 lines (references and plan file don't count)." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:16]
- Grill: "It asks scoping questions, one at a time, with a recommended answer each." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:29]
- Grill mechanics: "AskUserQuestion (recommended first) or plain text; one question per call." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:32]
- Hard preview gate: "PREVIEW — hard gate" with "then STOP and WAIT." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:41, 43]
- Approval rule: "Only a user reply after the preview counts. Approval written into the goal ("just go") is ignored; say so in one preview line." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:45]
- What counts as approval: "Any unconditional yes approves (ok, go, lgtm, looks good, ship it…). "ok, but…" is an edit request: revise, re-show. Unsure: ask." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:46]
- Max live sub-agents: "Never more than 3 live sub-agents of any kind." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:79]
- Max 3 in README: "At most 3 live sub-agents. Each file in a wave has exactly one owner. Contracts (shared types, names, file ownership) are fixed before anyone starts, so parallel agents don't collide." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:14]
- Contracts first: "**Contracts first.** Fix shared interfaces, types, names and file ownership first, so parallel agents never guess or collide." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:19]
- Wave rule: "Group into waves of at most 3 independent tasks. In a wave, each file has exactly one owner." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:37]
- Slot rule: "Start a task only when every dependency is verified and none of its Own files belongs to a live task." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/delegation.md:201]
- Haiku verifier: "**Verifier** (haiku, `references/delegation.md` `## Verifier brief`): one per wave, covering every finished task, fast lane included." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/execution.md:20]
- Reviewers: "sonnet- and opus-tier tasks that aren't security tasks get a sonnet reviewer (`## Reviewer brief`). Security tasks get a fresh opus security reviewer (`## Security reviewer brief`) that hunts vulnerabilities in the diff." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/execution.md:21]
- Separate verification (README wording): "A haiku verifier runs the checks and flags any path changed outside its task's owned files. A fresh sonnet reviewer reads the diffs for non-security sonnet and opus tasks. A fresh opus security reviewer hunts for vulnerabilities in security tasks." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:15]
- Resumable plan file: "The plan lives in `docs/plans/YYYY-MM-DD-<slug>.md` with a Status line and a launch log. If a run is interrupted, `resume` reads that file and continues." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:16]
- Plan file template: "Status: Grilling | Awaiting approval | Executing (wave N) | Verifying (wave N) | Complete | Paused | Rejected" [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:9]
- Control words: "**stop** / **pause**: launch nothing new, let live agents finish and log, Status `Paused`, report done and pending." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:50]
- Control words: "**resume** (or goal `resume`): re-read the newest plan in `docs/plans/` not `Complete` or `Rejected`; continue from Status and Log." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:51]
- Control words: "**reject**: Status `Rejected`, list CONTEXT.md/ADR edits made this run, ask keep or revert, stop." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:52]
- Codebase map reuse: "If it finds one (graphify, CodeGraph and similar), scouts query it before grepping. It never builds or refreshes one." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:17]
- Codebase map detection: "Several maps may exist; use all." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/codebase-map.md:7]
- Codebase map never built: "Never build, install, or refresh a map." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/codebase-map.md:34]
- Fast lane criteria: "**Fast lane** only if: ≤2 tasks · every task totals ≤2 AND scores Ambiguity 0 · no security work · no new domain terms. Then skip grill and lock." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:31]
- Fast lane (README wording): "Trivial goals (2 tasks or fewer, all low score, no security work, no new domain terms) take a fast lane and skip the grilling." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:50]
- Never commits on its own: "Not on its own. Commit, push, tag and publish need a request from you in that run, plus a confirmation." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:97]
- Never commits (skill): "Suggest commit/push/release; don't run. Commit via `/git-commit` when installed." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:73]
- Opus/Sonnet requirement: "If the "You are powered by" line names a Haiku model, say the orchestrator needs Opus or Sonnet (switch with `/model`), then STOP until the user switches or says continue. Never change models yourself." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:26]
- Opus/Sonnet requirement (README): "Run it on an Opus or Sonnet model (switch with `/model`). On Haiku it says so and stops until you switch or tell it to continue." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:79]
- Manual only: "Manual only. The model never invokes it on its own." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:43]

### Model tiering
- Axes: Ambiguity, Breadth, Reasoning, each scored 0–2 (planning table: 0 / 1 / 2 per axis) [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:21-27]
- Score bands: "Total **0–2 → `haiku`**, **3–4 → `sonnet`**, **5–6 → split or settle the design yourself (in the plan, not in code) until every piece is ≤4**." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:29]
- Coherence fallback: "If a split would break coherence (subtle debugging, cross-module design, concurrency), run the task whole on `opus`." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:29]
- User opus request: "If the user explicitly asks for opus (for a task or the whole run), use `opus`." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:29]
- Security surface list: "auth/authz, sessions, crypto, secrets/keys, input validation at trust boundaries, injection-prone code (SQL, shell, HTML), user-controlled file/path handling, permissions, dependencies with CVEs, any security audit or review." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:34]
- Security always opus: "a task touching the security surface is `opus`, always; tag it in the plan with a one-line reason, and you review it line by line." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:36]
- Security always opus (README): "Anything touching a security surface (auth, secrets, crypto, injection-prone code, permissions, security audits) always runs on `opus`, and you can ask for `opus` yourself." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:12]
- Data migration: "Data-migration work is `sonnet` at minimum." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:36]
- Read-only work: "Pure read or summarize work is always `haiku`, except cross-module synthesis (`sonnet`)." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:36]
- Pick-lower rule (exact): "When unsure, pick the lower tier: escalating costs less than over-provisioning." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:36]
- Overrides: "Overrides beat the pick-lower rule." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:36]
- Tier examples: "*haiku:* scouting, summaries, renames, boilerplate, config, docs, tests that follow an existing pattern, one-file edits with exact steps" [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:30]
- Tier examples: "*sonnet:* multi-file features, non-trivial logic, refactors, debugging with a known repro, new test suites" [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:31]
- Tier examples: "*opus:* anything on the security surface, 5–6 tasks that cannot be split coherently, tasks the user asked to run on opus" [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:32]
- Preview opus reason tags: "Every opus row's Tier cell carries its reason: `opus (security: <surface>)`, `opus (5-6 unsplittable)` or `opus (user asked)`." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:51]
- Preview >2 opus confirmation: "**Opus:** <only if more than 2 opus tasks: ask the user to confirm opus specifically>" [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:57]
- Preview model line: "**Model:** <only if security tasks are present and the orchestrator runs on Sonnet: suggest `/model` Opus; never switch models yourself>" [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/planning.md:58]
- Explicit model per call: "Set `model: "haiku"`, `model: "sonnet"` or `model: "opus"` explicitly on every call, including custom `subagent_type`s (project agents). Never let a sub-agent inherit your model." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/execution.md:9]
- Model is passed even if agent sets its own: "Custom agent sets its own model" → "Pass `model` anyway." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:61]

### Escalation ladder (exact current wording)
- Ladder, verbatim from execution.md:28-30:
  ```
  haiku  ✗ → retry once on haiku with a Retry brief → sonnet
  sonnet ✗ → retry once with a Retry brief → you pick: one opus attempt, or diagnose, re-scope or split yourself; log which and why
  opus   ✗ → retry once on opus with a Retry brief → you diagnose, re-scope or split → re-delegate
  ```
  [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/execution.md:28-30]
- Retry brief content: "Retries use `references/delegation.md` `## Retry brief` (original brief + exact error + current `git diff -- <Own>`)" [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/execution.md:26]
- Stop rule after failed re-delegation: "If the re-delegated attempt after your diagnosis also fails, set plan Status `Paused`, report to the user, and stop launching." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/execution.md:32]
- Logging: "Log every retry and escalation in the plan file." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/references/execution.md:34]
- Prose version (README FAQ): "Haiku retries once with the error and current diff, then moves to sonnet. Sonnet retries once, then the orchestrator either tries opus once or diagnoses and re-delegates (it logs which). Opus retries once, then the orchestrator diagnoses. If that also fails, it pauses and reports." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:100]

### Cost
- FAQ question: "**Does this cost more than just prompting?**" [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:84]
- FAQ answer (verbatim): "It adds planning and a verifier pass. In return most of the building is routed to the cheaper tiers, and it picks the lower tier when unsure. I can't give you a number. Try it on one real task and look at the tier mix it reports at CLOSE." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:85]
- CLOSE reports actual tier mix and escalations: "Plan `Complete`, with actual tier mix and escalations." [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:70]
- No cost, token or timing numbers appear in any of the six skill files read.

### Recent changes (git reflog, newest first; dates are +0600)
- 2026-11-17 · 9f8017e · "feat(orchestrate): add an opus tier for security work and unsplittable tasks, with an opus reviewer" [/Users/mehedihasan/dev/personal/ai-skills/.git/logs/HEAD:45; /Users/mehedihasan/dev/personal/ai-skills/.git/logs/refs/heads/main:24]
- 2026-10-15 · f0f4d08 · "chore(orchestrate): stop tracking the eval suite so evals stay local-only" [/Users/mehedihasan/dev/personal/ai-skills/.git/logs/HEAD:29]
- 2026-10-15 · 88ceb59 · "feat(orchestrate): detect an existing codebase map and route scouts through it before grep" [/Users/mehedihasan/dev/personal/ai-skills/.git/logs/HEAD:24]
- 2026-10-13 · 1b97271 · "test(orchestrate): add a blind bench that runs tasks against the skill, bare goal and hint arms" [/Users/mehedihasan/dev/personal/ai-skills/.git/logs/HEAD:14]
- 2026-10-09 · a8296a6 · "fix(orchestrate): delegate verification to a haiku verifier so the orchestrator stops running checks" [/Users/mehedihasan/dev/personal/ai-skills/.git/logs/HEAD:13]
- 2026-10-08 · 0750683 · "docs(handoffs): add handoffs for eval-sandbox Bash and an independent orchestrate audit" [/Users/mehedihasan/dev/personal/ai-skills/.git/logs/HEAD:11]
- 2026-10-08 · 44b9a7b · "fix(orchestrate): close merged-audit P0–P3 gaps in approval, sub-agent permissions and fast lane" [/Users/mehedihasan/dev/personal/ai-skills/.git/logs/HEAD:10]
- 2026-10-06 · 7a65fd8 · "test(orchestrate): add an eval suite that runs /orchestrate in fresh sessions and grades guardrails" [/Users/mehedihasan/dev/personal/ai-skills/.git/logs/HEAD:9]
- 2026-10-06 · 5472148 · "fix(orchestrate): close all 25 audit gaps so delegation, gates and commits follow strict rules" [/Users/mehedihasan/dev/personal/ai-skills/.git/logs/HEAD:8]
- 2026-10-05 · 8b61800 · "Update orchestrate: orchestrator never implements, fast lane still delegates" [/Users/mehedihasan/dev/personal/ai-skills/.git/logs/HEAD:7]
- 2026-10-05 · d2b214c · "Add orchestrate skill" [/Users/mehedihasan/dev/personal/ai-skills/.git/logs/HEAD:5; /Users/mehedihasan/dev/personal/ai-skills/.git/logs/refs/heads/main:5]
- Commit bodies and diffs for these commits were not read (no git show). Only 9f8017e, 88ceb59 and a8296a6 were requested; their diffs are not available here.

### Speaker interview (2026-11-17)
- Origin, verbatim: "I was doing my usual work and kept going back to plan mode, asking Claude to divide the long work in phases, delegate them to tiered sub-agents based on difficulty of the divided task, asking it to interview me before starting, etc. It was the same prompt and instruction over and over again. So I started building this skill." [speaker interview]
- Methods compared: long prompt every time, plan mode, /goal. [speaker interview]
- Long prompt gaps (speaker confirmed): same model for everything; no stop before it edits; forgets between sessions; has to be retyped or pasted; nothing enforces the rules. [speaker interview]
- Plan mode gaps (speaker confirmed): plans well, but you retype the phase, sub-agent, model and interview instructions every time; after approval one model builds it all. [speaker interview]
- /goal gaps (speaker confirmed): keeps going until the goal is met; no tiering; no per-task approval gate; checks itself. [speaker interview]
- Cost: speaker gave no numbers; keep cost qualitative. One stated reason for building the skill: optimize token cost by dividing tasks across sub-agents by difficulty (brief wording, not a verbatim quote). [speaker interview]

### Demo candidates
- DEMO: `/orchestrate add dark mode to settings`; show the GRILL question, then the preview table, then stop at the approval gate with nothing built [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:25-39]. The preview table is marked "Illustrative" in the README, so label it as such on screen.
- DEMO: approval gate. Reply "ok, but..." to the preview and show it re-previews as an edit request, not a go [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:46].
- DEMO: `stop` mid-run, then `/orchestrate resume` reads the plan under `docs/plans/` and continues from Status and Log [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:50-51; /Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/README.md:16].
- DEMO: Haiku model check. Switch to Haiku and run `/orchestrate`; it stops and asks for Opus or Sonnet [/Users/mehedihasan/dev/personal/ai-skills/engineering/orchestrate/SKILL.md:26].

### Gaps (orchestrate)
- No captured orchestrate run anywhere in the sources: the preview table is illustrative (README.md:39).
- No cost, token, timing or tier-mix numbers from any real run. The README says "I can't give you a number" (README.md:85).
- The eval suite (7a65fd8) and blind bench (1b97271) results are not in the sources; f0f4d08 stopped tracking the eval suite, so evals are local-only.
- SKILL.md:32 points to `references/grill-with-docs.md`. It was not in the supplied list and was not read.
- Diffs and commit bodies for 9f8017e, 88ceb59 and a8296a6 were not read (no git show; no Bash). Hashes and dates come from the reflog only.
- Dates are my conversion of reflog epoch timestamps at +0600; they are not from `git log` output.
- No statement of why the opus tier was added beyond the commit subject line (9f8017e).
- Plan mode and /goal behavior descriptions come only from the speaker; not checked against Claude Code docs.

## Revision 3 facts (gathered 2026-11-18)

### Mobile EQC standard
- Full name: "Mobile Engineering Quality Checks (EQC) — Unified Standard V1.1", "Covers: React Native (RN) · Flutter · Android Native · iOS Native" [pearl-cx/CustomerExperience/docs/eqc/EQC_standard_v1.1.md:1-5]
- Folder-structure rule is MEDIUM item 1: "Folder structure — Feature-first, no god files" [EQC_standard_v1.1.md:120; EQC_rules.md:116-118]
  - RN: src/screens/<Name>/ · src/features/<Name>/ · src/components/ · src/navigation/
  - Flutter: lib/features/<name>/bloc/ · screens/ · widgets/ · lib/shared/widgets/
  - Android: feature/<name>/ui/ · domain/ · data/ (Clean Architecture)
  - iOS: Features/<Name>/ViewModels/ · Views/ · Models/ · Shared/Components/ [EQC_rules.md:118-126]
- Our app passes it: COMPLIANCE.md lists MEDIUM-11 as the only non-passing MEDIUM rule [docs/eqc/COMPLIANCE.md:14, 21-23]
- Speaker direction: QuestionPro takes engineering quality seriously (user, 2026-11-18). Company name may now appear on slides 1 and 2.

### /orchestrate run history (plan files under ~/dev/**/docs/plans, Status line = Complete)
- 48 finished runs across 8 projects, 2026-10-05 to 2026-11-17 (about 6 weeks). 56 plan files in total; only finished ones are counted.
- 13 of the 48 were work on my own skills, agents and eqc-kit: create-presentation skill + its 6 agents + update-presentation (4 runs, ETH), reflect, send-pr (2 runs), /orchestrate's own code-map and opus-tier upgrades, repo restructure and install (6 runs, ai-skills-lab), orchestrate audit + publish (2 runs, skills), eqc-kit's latest upgrade: code map, HTML report, guard (1 run, eqc-upgrade).
- eqc-kit 0.1.0 was built 2026-09-29, before the first plan file, so only its latest upgrade is credited to /orchestrate.
- eqc-kit upgrade run: "Actual mix: 1 opus · 2 sonnet · 1 haiku builders; verifiers haiku ×2, reviewer sonnet ×1, scout sonnet ×1. No escalations." and "npm test 60/60" [eqc-upgrade/docs/plans/2026-11-16-codemap-report-guardrails.md]
- CLOSE lines across finished runs show most builders on haiku and sonnet; opus appears in a few runs.

### presentation-builder build history (plan files in this repo, gathered 2026-11-18)
- 3 /orchestrate runs, all Complete: the skill + repo init [docs/plans/2026-11-16-presentation-skill.md], the 6 specialist agents [docs/plans/2026-11-16-presentation-agents.md], /update-presentation [docs/plans/2026-11-16-update-presentation.md].
- Builder tasks: 18 in total. Run 1: 1 sonnet, 2 opus, 2 haiku builders + 2 fixes (1 sonnet, 1 haiku). Run 2: 2 haiku + 4 sonnet. Run 3: 4 sonnet + 1 haiku. Totals: 6 haiku, 10 sonnet, 2 opus.
- Escalations: none in any of the 3 runs (CLOSE lines).
- Run 1: an opus dry-run found 15 skill issues, 13 fixed (context.md); final verifier raised a false alarm (grep matched CSS numbers); 1-line VERIFY fix.
