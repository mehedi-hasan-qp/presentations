# Plan: Specialist sub-agents for /create-presentation
Status: Complete

## Goal / Done when / Non-goals
Goal: Split the /create-presentation skill's work into dedicated sub-agents (content-writer, content-reviewer, design-creator, design-reviewer, knowledge-explorer, + others found), each with its own model, invoked only by the user or the skill.
Done when: TBD (grill)
Non-goals: TBD (grill)

## Open questions
- [x] Which tasks does the skill do today? → 9 steps: interview, outline, engagement suggestions, approval, build HTML, transcript, self-check, 2 reviewers (content=opus, tech=sonnet, general-purpose, no tool allowlist), report+fix. Implicit jobs: source research, narrative/outline, speaker notes, demo planning, timing, transcript, a11y/contrast (review only), fix application. Bug: SKILL.md:83 refers to "step 8a" (doesn't exist).
- [x] Where do agent files live? → (re-confirmed after "why not a skill?" — alternatives: skill+.claude/agents, briefs-in-skill) Plugin bundle: plugins/presentation-builder/{.claude-plugin/plugin.json, skills/create-presentation/, agents/*.md} (user, 2026-11-16)
- [x] Call guard → soft: narrow description ("only via /create-presentation or @-mention"), no "proactively", no Agent tool, skill calls by full plugin name (user, 2026-11-16)
- [x] Roster + models → knowledge-explorer haiku, content-writer opus, transcript-writer sonnet, design-creator sonnet, content-reviewer opus, design-reviewer sonnet (user, 2026-11-16)

## Research (code.claude.com/docs/en/sub-agents, /skills, /plugins; anthropic.com/engineering/multi-agent-research-system)
- Skill folders can't hold agents; plugins bundle skills/ + agents/ (namespaced plugin:agent, ${CLAUDE_PLUGIN_ROOT}).
- No frontmatter flag blocks auto-delegation. Levers: narrow non-proactive description; @agent-name for user; permissions.deny Agent(name) (blocks entirely — untested vs skill-spawn).
- Subagents can nest (depth 3); omit Agent from tools to stop it.
- model: haiku/sonnet/opus/fable/inherit; per-call model overrides frontmatter.
- Plugin agents ignore permissionMode/hooks → least privilege via tools/disallowedTools.
- Hand off via files; orchestrator-worker ~15x tokens → don't over-split.

- [x] Handoff files → presentations/<slug>/work/{sources.md, outline.md, reviews/content.md, reviews/design.md}, committed (user, 2026-11-16)
- [x] Symlink into ai-skills? → not needed: local-path marketplace loads in place (/reload-plugins); symlinked plugin dirs undocumented.
- [x] Build where → in ETH at plugins/presentation-builder/, move to ai-skills later (user, 2026-11-16)
- [x] Repo wiring (default) → git mv skill into plugin; repo-root .claude-plugin/marketplace.json (name "eth"); CLAUDE.md documents `claude plugin marketplace add .` + install. Skip settings.json extraKnownMarketplaces (shape unverified).

## Contracts
MAP: none
Baseline `git status --porcelain`: `?? docs/plans/2026-11-16-presentation-agents.md`

P = plugins/presentation-builder
- P/.claude-plugin/plugin.json: {"name":"presentation-builder","version":"0.1.0","description":"...","author":{"name":"Mehedi Hasan"}}
- .claude-plugin/marketplace.json (repo root): {"name":"eth","owner":{"name":"Mehedi Hasan"},"plugins":[{"name":"presentation-builder","source":"./plugins/presentation-builder","description":"..."}]}
- Skill: P/skills/create-presentation/ (git mv of .claude/skills/create-presentation). Paths to agents' inputs passed as `${CLAUDE_PLUGIN_ROOT}/skills/create-presentation/...`.
- Agent file shape (P/agents/<name>.md):
  ---
  name: <name>
  description: <one job>. Invoked only by /create-presentation or an explicit @-mention; never delegate to it otherwise.
  model: <model>
  tools: <list; never Agent>
  ---
  Body: role, inputs (paths arrive in the task prompt), output file + exact format, rules restated (agents may not load CLAUDE.md), final reply ≤10 lines: STATUS, file written, top points.
- Roster (name · model · tools · writes):
  knowledge-explorer · haiku · Read, Grep, Glob, WebFetch, WebSearch, Write · work/sources.md
  content-writer · opus · Read, Write, Edit · work/outline.md (mode "outline": header, arc, outline table, timing, demo plan, engagement suggestions; mode "slides": adds per-slide copy + speaker notes; mode "fix": applies confirmed content findings to outline.md)
  transcript-writer · sonnet · Read, Write, Edit · transcript.md
  design-creator · sonnet · Read, Write, Edit, Bash · index.html (from template + outline.md) + self-check; mode "fix": applies confirmed findings to index.html
  content-reviewer · opus · Read, Grep, Glob, Write · work/reviews/content.md (read-only on deck)
  design-reviewer · sonnet · Read, Grep, Glob, Bash, Write · work/reviews/design.md (read-only on deck; read-only shell)
- Handoff dir: presentations/<slug>/work/ (committed). Review file format: verdict line, then numbered findings `[blocker|major|minor] slide N / file:line — problem — fix`.
- Skill flow: 1 interview (main) → 2 knowledge-explorer (if sources) → 3 content-writer outline mode → show outline+flow+timing+suggestions → 4 approval gate → 5 content-writer slides mode → design-creator build+self-check → 6 transcript-writer (if yes) → 7 content-reviewer ∥ design-reviewer → 8 merge, user confirms, route: deck text/HTML → design-creator fix; structure → content-writer fix then design-creator; transcript → transcript-writer; re-run self-check. Skill passes `model` on every Agent call, subagent_type `presentation-builder:<name>`.

## Waves
| # | Task | Tier | Own | Deps | Scores A/B/R |
|---|------|------|-----|------|------|
| 1.1 | git mv skill into P; add plugin.json + root marketplace.json | haiku | P/.claude-plugin/plugin.json, .claude-plugin/marketplace.json, moved skill dir | — | 0/1/0 |
| 2.1 | Write knowledge-explorer, content-writer, transcript-writer | sonnet | P/agents/{knowledge-explorer,content-writer,transcript-writer}.md | 1.1 | 1/1/1 |
| 2.2 | Write design-creator, content-reviewer, design-reviewer (port briefs from references/review-agents.md + SKILL step 5/7) | sonnet | P/agents/{design-creator,content-reviewer,design-reviewer}.md | 1.1 | 1/1/1 |
| 2.3 | Rewrite SKILL.md as orchestrator of the 6 agents (flow above); fix "step 8a" | sonnet | P/skills/create-presentation/SKILL.md | 1.1 | 2/1/1 |
| 3.1 | Delete references/review-agents.md; update CLAUDE.md (layout, install cmds, agent list) | haiku | CLAUDE.md, P/skills/create-presentation/references/review-agents.md | 2.1–2.3 | 0/1/0 |

## Log
- GRILL: scouts launched — skill task map (Explore/haiku), web best practices (general-purpose/sonnet)
- PREVIEW approved by user ("go"), 2026-11-16
- Baseline: `?? docs/plans/2026-11-16-presentation-agents.md`
- 1.1 launched (haiku, general-purpose)
- 1.1 done; wave-1 verifier (haiku): OUTSIDE-OWN none, 5 pure renames, json ok, validate pass (warnings: README/LICENSE/icon for directory profile, marketplace description) → VERIFIED
- Wave 2 launched: 2.1, 2.2, 2.3 (sonnet, general-purpose)
- 2.3 done (SKILL.md 96 lines, validate pass); 2.1 done (3 agents, validate pass); 2.2 done (3 agents, validate pass; note: color dupes purple/green across agents — minor)
- Wave-2 verifier (haiku) + reviewer (sonnet) launched
- Wave-2 verifier: OUTSIDE-OWN none, checks a/c-g pass; b partially truncated → orchestrator re-ran grep for 3 agents: models/tools/guard line OK → VERIFIED
- Wave-2 reviewer (sonnet): no blockers; 10 minors. Accepted 1-6,8,9 → new task 2.4 (sonnet; Own SKILL.md, content-writer.md, design-creator.md, transcript-writer.md). 7 (## Outline heading) and 10 (timing column) accepted as-is.
- Wave 3 launched: 2.4 (sonnet) ∥ 3.1 (haiku)
- 3.1 blocked (git rm on staged rename) → resumed same agent with permission for git rm -f on that one path
- VERIFY fix 2.4 (2 lines transcript-writer.md + 1 word SKILL.md): resync input for transcript-writer fix mode
- 3.1 done (git rm -f review-agents.md; CLAUDE.md rewritten). Final verifier: all checks a–h pass, OUTSIDE-OWN none. Final reviewer: no blockers; minor 1 fixed via VERIFY fix; minors 2–5 deferred to follow-ups.
- CLOSE: tier mix 2 haiku builders (1.1, 3.1) · 4 sonnet builders (2.1–2.4) · verifiers haiku · reviewers sonnet. Escalations: none. Retries: 3.1 resumed once (git rm on staged rename). Added task 2.4 from wave-2 review.
