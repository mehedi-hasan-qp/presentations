# ETH: Presentation Builder

This repo creates presentations. Each deck is one self-contained HTML file.

## Layout

```
ETH/
├── .claude/skills/create-presentation/
│   ├── SKILL.md
│   ├── references/
│   │   ├── best-practices.md
│   │   └── review-agents.md
│   └── templates/
│       └── default/
│           ├── template.html
│           └── DESIGN.md
├── presentations/<slug>/
│   ├── index.html
│   └── transcript.md        (optional)
└── docs/plans/              (orchestration plans)
```

## Making a deck

Run `/create-presentation` or ask for a presentation. The skill:

1. Interviews you: topic, audience/context, duration, slide count, template, details/sources, demos, transcript.
2. Shows an outline, flow preview, and engagement suggestions, then waits for approval.
3. Builds the deck.
4. Runs two review agents (content audit; HTML/CSS/JS check) and applies fixes only after you confirm.

## Conventions

- One file per deck. No build step, no JS libraries. The only external dependency is Google Fonts.
- Follow the chosen template's DESIGN.md (default: `.claude/skills/create-presentation/templates/default/DESIGN.md`).
- Don't edit a template's chrome (CSS/nav JS) inside a deck. Change the template instead.
- New template = new folder under `templates/` with `template.html` + `DESIGN.md`.
- Keep the skill self-contained: no references outside its folder. It will move to global `~/.claude/skills` and the team "ai-skills" collection.

## Viewing

- Open `presentations/<slug>/index.html` in a browser.
- Keys: ←/→ or Space to move, Home/End to jump, N toggles speaker notes.
- Cmd+P exports to PDF.

## Commits

- Author: Mehedi Hasan. Use the `/git-commit` skill.
- No AI attribution trailers.
