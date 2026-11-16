# ETH: Presentation Builder

This repo creates presentations. Each deck is one self-contained HTML file.

## Layout

```
ETH/
├── .claude-plugin/marketplace.json        (marketplace "eth")
├── plugins/presentation-builder/
│   ├── .claude-plugin/plugin.json
│   ├── skills/create-presentation/
│   │   ├── SKILL.md
│   │   ├── references/
│   │   │   └── best-practices.md
│   │   └── templates/
│   │       └── default/
│   │           ├── template.html
│   │           └── DESIGN.md
│   └── agents/                            (six review/build agents)
├── presentations/<slug>/
│   ├── index.html
│   ├── transcript.md        (optional)
│   └── work/                (sources.md, outline.md, reviews/)
└── docs/plans/              (orchestration plans)
```

## Setup

One-time per machine, from the repo root:

```
claude plugin marketplace add .
claude plugin install presentation-builder@eth
```

After changing plugin files, run `/reload-plugins`. Validate with `claude plugin validate plugins/presentation-builder`.

## Making a deck

Run `/create-presentation` or ask for a presentation. The skill:

1. Interviews you: topic, audience/context, duration, slide count, template, details/sources, demos, transcript.
2. Shows an outline, flow preview, and engagement suggestions, then waits for approval.
3. Builds the deck.
4. Runs the content-reviewer and design-reviewer agents and applies fixes only after you confirm.

## Agents

- knowledge-explorer (haiku): reads your sources → `work/sources.md`
- content-writer (opus): outline, narrative, timing, demo plan, slide copy + notes → `work/outline.md`
- transcript-writer (sonnet): spoken transcript → `transcript.md`
- design-creator (sonnet): builds `index.html` from the template + self-check
- content-reviewer (opus): read-only content audit → `work/reviews/content.md`
- design-reviewer (sonnet): read-only HTML/CSS/JS/a11y check → `work/reviews/design.md`

Only `/create-presentation` or an explicit @-mention (e.g. `@agent-presentation-builder:content-writer`) invokes them.

## Conventions

- One file per deck. No build step, no JS libraries. The only external dependency is Google Fonts.
- Follow the chosen template's DESIGN.md (default: `plugins/presentation-builder/skills/create-presentation/templates/default/DESIGN.md`).
- Don't edit a template's chrome (CSS/nav JS) inside a deck. Change the template instead.
- New template = new folder under `plugins/presentation-builder/skills/create-presentation/templates/` with `template.html` + `DESIGN.md`.
- Keep the plugin self-contained: no references outside `plugins/presentation-builder/`. It will move to the team "ai-skills" marketplace.

## Viewing

- Open `presentations/<slug>/index.html` in a browser.
- Keys: ←/→ or Space to move, Home/End to jump, N toggles speaker notes.
- Cmd+P exports to PDF.

## Commits

- Author: Mehedi Hasan. Use the `/git-commit` skill.
- No AI attribution trailers.
