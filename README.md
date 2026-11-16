# Presentations

Single-file HTML slide decks, built with the `create-presentation` Claude Code skill.

## Decks

| Deck | Topic |
|---|---|
| [`presentations/everyday-ai-workflow`](presentations/everyday-ai-workflow/index.html) | Ask first, build cheap, ship clean: my everyday AI workflow (eqc-kit, `/orchestrate`, the ship chain) |

Each deck folder has `index.html` (the deck), and optionally `transcript.md` (spoken script) and `context.md` (research and prep checklist).

## Presenting

Open a deck's `index.html` in a browser. No build step, no install.

- ←/→ or Space: next/previous slide · Home/End: first/last
- N: speaker notes · swipe on touch screens
- Print (Cmd+P): PDF, one slide per page

## Making a new deck

In Claude Code, run `/create-presentation` from this repo. It interviews you, shows an outline with suggestions, waits for approval, builds the deck into `presentations/<slug>/`, then runs a content review and a technical check before applying any fixes you confirm.

The skill and its agents ship as the `presentation-builder` plugin in `plugins/presentation-builder/` (install once: `claude plugin marketplace add .` then `claude plugin install presentation-builder@eth`); the default look is documented in `skills/create-presentation/templates/default/DESIGN.md` inside it.
