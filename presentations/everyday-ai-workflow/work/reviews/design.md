Verdict: ready after fixes (focus: slides 11-17)

1. [major] slide 13 (index.html:541-562) — 6-row x 5-column table at 0.76rem (~12px) plus 2-line h2, 3-line header and a 2-line "catch" paragraph is likely taller than one 720p screen. On screen it scrolls (.slide overflow-y:auto). In print it is clipped (overflow:hidden, height:100vh). 12px is also hard to read when projected. — Cut the "Picks up after a break?" row, or merge it into "Who checks the work?". Raise td font-size to 0.9rem. Move "The catch" to the notes or shorten it to one line. Or split into two slides.
2. [minor] slide 13 — 39 inline style attributes (padding, font-size, width per cell). They override the theme and are hard to maintain. Not a chrome violation. — Add the padding and font-size once on the table (`<table class="dtable" style="font-size:.9rem">`), or ask for a template `.dtable.dense` modifier. Chrome stays untouched in the deck.
3. [minor] slides 14, 15 — dense tables at 0.82-0.9rem with a long paragraph under the table. Slide 14 has 5 multi-line rows. Slide 15 has the table plus a 3-line muted paragraph, close to the 720p limit. — Check at 1280x720 and in print preview. If clipped, move the "retry ladder" line (cut-able in the notes already) out of the slide.
4. [minor] slides 13-15 at 375px — `.dtable` becomes display:block with overflow-x:auto, so the table scrolls sideways. Percent widths on th (15/17/20/18/30%) squeeze the 5 columns. Slide 13 is unreadable on a phone unless you scroll. — Acceptable for a talk deck. Optionally add `min-width:640px` on the table in the template CSS (not in the deck).
5. [minor] slide 12 — 5 inline styles on step-rows/list (padding, max-width). The theme is unchanged and no overflow. — No action needed.

Checks:
- Slide count: 26 slides, 26 notes asides, 0 leftover `{{` or SAMPLE markers.
- Tags balanced: div 191/191, table 8/8, tr 45/45, td 110/110, aside 26/26. No duplicate ids.
- Chrome outside the SLIDES block is identical to template.html, apart from the title. No undefined classes.
- Slides 11-17 all have notes. The demo slide 16 has PREP and FALLBACK.
- Contrast: --fg-muted #666 on #fff and on #f4f4f6 passes AA. Accent text uses --accent-text. The divider (slide 11) is white on oklch(50% .17 251), which passes.
- Heading order fine: kicker div, h2, no h1 skips.
- No images, so no alt text issues. The `<html lang>` and the focus-visible styles come from the template chrome.

1 HTML validity: pass
2 CSS: pass, with the inline-style overuse on slide 13
3 JS: pass (unchanged from template)
4 Behaviour: pass (template chrome identical)
5 Responsive: pass with caveat (table side-scroll, finding 4)
6 Accessibility: pass
7 Template conformance: pass
8 Print: fail on slide 13 (likely clipped), watch slides 14 and 15
