# Review agent briefs

Two briefs for step 8. Replace every `<PLACEHOLDER>` (absolute paths), then send both in **one message** as two Agent calls with `subagent_type: general-purpose`. Pass each brief verbatim and add nothing about the other review or your own opinion of the deck, so each reviewer reads it fresh.

Placeholders: `<DECK>` (index.html), `<TRANSCRIPT>` (transcript.md, or "none"), `<DESIGN>` (template DESIGN.md), `<BEST_PRACTICES>` (this skill's references/best-practices.md), `<TITLE>`, `<AUDIENCE>` (who + setting), `<OUTCOME>` (what they should do or feel afterwards), `<DURATION>` (minutes), `<SLIDE_COUNT>`, `<DEMOS>` (agreed demo segments, or "none").

## (a) Content audit — model: opus

```
You are reviewing a presentation's content. Read-only: do not edit, create, or delete any file.

Deck: <DECK> (single HTML file; each slide is <div class="slide ...">, speaker notes are <aside class="notes"> inside each slide)
Transcript: <TRANSCRIPT>
Rules to judge against: <BEST_PRACTICES>
Talk: "<TITLE>" for <AUDIENCE>; desired outcome: <OUTCOME>; slot <DURATION> min; agreed <SLIDE_COUNT> slides; demos: <DEMOS>.

Read the deck (slides and notes) and the transcript in full, then assess:
1. Story & flow: is there a hook in the first minute, a clear arc, signposted sections, a climax before the close, a recap and one clear call to action?
2. Clarity: one idea per slide; titles state the takeaway; jargon fit for this audience.
3. Density: flag every slide over ~6 lines or ~30 words of on-slide text.
4. Audience fit: tone, depth, and examples right for <AUDIENCE> and the desired <OUTCOME>.
5. Timing: sum the per-slide time cues; compare to <DURATION> min; name slides that are over- or under-weighted and which could be cut if running late.
6. Engagement: audience moments, demo placement, demo fallback present.
7. Speaker notes: present on every slide; say more than the slide; include transitions.
8. Transcript consistency (if present): same points, order, and timing as the notes; reads as natural speech; ~130 words/min totals ≈ <DURATION> min.

Return:
- Verdict: one paragraph.
- Findings: numbered list, each "Slide N — severity (blocker / should fix / nice to have) — problem — concrete fix (rewritten title/text where relevant)".
- Timing table: slide, cue, assessment.
Cover every slide; say "no issues" for slides that have none.
```

## (b) Technical check — model: sonnet

```
You are checking a single-file HTML/CSS/JS slide deck for technical problems. Read-only: do not edit, create, or delete any file. You may run read-only commands (cat, grep, wc, python3 parsers that only read).

Deck: <DECK>
Component reference: <DESIGN>
Expected: <SLIDE_COUNT> slides, each <div class="slide ..."> inside <div class="slides">, between <!-- SLIDES:START --> and <!-- SLIDES:END -->; each slide ends with <aside class="notes">.

Check:
1. HTML validity: balanced tags, correct nesting, no duplicate ids, no leftover {{ placeholders or <!-- SAMPLE: --> slides, slide count equals <SLIDE_COUNT>.
2. CSS: classes used in slides exist in the stylesheet (or DESIGN.md); no inline styles that break the theme; no broken selectors.
3. JS: syntax errors, references to missing elements, counter derived from the DOM slide count.
4. Behaviour (by reading the code): ←/→/Space, Home/End, N toggles notes for the active slide, touch swipe, prev/next buttons, progress bar, @media print shows one slide per page with chrome and notes hidden.
5. Responsive: content that could overflow at ~375px and ~900px widths (long code lines, wide tables, fixed widths, unbroken strings).
6. Accessibility basics: <html lang>, alt text on images, heading order within slides, colour contrast of text against backgrounds (WCAG AA), keyboard focus visible on buttons.

Return a numbered list, each "file:line — severity (blocker / should fix / nice to have) — problem — exact fix (replacement snippet)". End with a one-line pass/fail summary per check area 1-6.
```
