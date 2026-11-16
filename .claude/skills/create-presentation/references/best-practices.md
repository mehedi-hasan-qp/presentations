# Presentation best practices

Rules to audit an outline against (step 3) and to build by (step 5). Each rule names the template component that serves it; check `DESIGN.md` of the chosen template for exact markup.

## Structure and story

- **Open with a hook, not an agenda.** A story, a surprising number, a question, or the problem's cost in the first 60 seconds. Component: `title-slide`, then a `center` slide with one line.
- **Story arc.** Problem → stakes → insight → solution → proof → call to action. Every slide should move one beat forward; a slide that serves no beat gets cut or folded into notes.
- **Signpost sections.** One `divider` (+ `.sub` for the one-line promise) per major section, 3–5 sections for a 20–45 min talk; dividers are optional under 15 min. Dividers are breathing room, roughly 15–30 s each.
- **Climax before the close.** Put the strongest proof (demo, result, before/after) at about 70–80% of the runtime, not at the end, where it collides with Q&A and overruns.
- **Recap + one clear CTA.** The `closing` slide carries 3 takeaways at most and one action ("try X", "approve Y", "ping Z"). Leave it up during Q&A.

## Slide design

- **One idea per slide.** If the title needs "and", split it.
- **Density limit:** ≤6 lines or ~30 words of on-slide text. Everything else lives in the speaker notes.
- **Titles state the takeaway**, not the topic: "Caching cut p95 latency 4x", not "Caching".
- **Visuals over bullets.** Map content to the component that shows its shape:
  - comparison / before–after → `vs-grid` (mark the winner with `vs-card.hi`)
  - sequence / process → `steps-list` or `flow` (`flow-step.on` for the current stage)
  - data with several dimensions → `dtable` with `badge-same` / `badge-diff`
  - a set of options or features → `card-grid`
  - code → `code-block`, ≤10 lines, highlight the one line that matters with `tok-warn` / `tok-ok`, dim the rest with `tok-dim`
  - one statement or number → `center`
- **Progressive emphasis.** Use `.hi` on the single row/card the speaker is talking about rather than bolding everything.

## Demos

- **Place demos after the concept they prove**, and no later than ~80% of runtime.
- **Announce it** with a `demo` slide (`demo-badge`, `kicker.demo`) stating what the audience should watch for.
- **Keep each live segment ≤5 min** for talks under 30 min; script the clicks in the notes.
- **Always have a fallback**: screenshot or recording referenced in the notes, plus the one sentence to say if it breaks.
- **Return slide**: after the demo, the next content slide plus one line in the notes restating what was just shown; it needn't cost a slide.

## Timing and delivery

- **Pacing:** ~1 content slide per minute; dense tables/code 2 min; dividers and `center` slides 15–30 s. Sum per-slide minutes and keep within ±10% of the slot, leaving ~10% for Q&A if the format has it.
- **Speaker notes on every slide:** what to say (not what is on screen), the transition sentence to the next slide, and a time cue.
- **Rehearsal notes:** mark in notes where to slow down, pause for a question, or cut if running late (tag the cuttable slides).
- **Interaction:** for talks over 15 min, plan one audience moment roughly every 8–10 min (show of hands, a question, a prediction before a reveal).

## Audience tuning

- **Executives:** lead with the decision or result; numbers and cost/risk up front; few slides, no code; CTA is a decision. Prefer `center`, `vs-grid`, `dtable`.
- **Engineers:** show the mechanism; real code and data; trade-offs and failure modes; honest limits. Prefer `code-block`, `flow`, `steps-list`, `dtable`; demos land well.
- **Mixed:** layer it. Plain-language takeaway in each slide title, the technical detail in the body or notes, and say out loud who each section is for. Keep code to the one or two slides that earn it.
- **External / customer:** their problem first, product second; proof via customer outcomes; no internal jargon.
