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
