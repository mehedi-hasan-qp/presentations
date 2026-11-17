Verdict: ready after fixes

1. [major] slides with tables (index.html:378-386 slide 5, 404-409 slide 6, 466-472 slide 9) — taller than a 1280x633 screen (slides 5, 6 overflow, as known): on screen the slide scrolls (overflow-y:auto), in print `overflow:hidden` (line 267) clips the bottom (e.g. "The catch" paragraph) — trim copy to about 4 rows, or add inside the deck's slide block only: `<style>` is not allowed, so shorten text and remove the `margin-top` on the h2/lead; do not change the chrome. Template fix to consider: `@media print { .slide { height:auto; min-height:100vh; overflow:visible; } }`.
2. [major] slide 8 (index.html:430-444, steps-list with inline padding) — overflows slightly at 1280x633 (known); same print clipping. Fix: drop the "Watch for" line (444) into the notes, or reduce to 3 step-rows.
3. [minor] slides 5, 6, 9 — per-cell inline `style="padding..; font-size.."` on every th/td breaks theme consistency and is hard to maintain; it works. Fix: leave it (user wants density), or move to one template class `.dtable.dense td,th` in template.html and re-copy.
4. [minor] slides 5, 6, 9 at <=900px — template makes `.dtable` display:block with overflow-x:auto, so the tables scroll sideways; the inline `width: NN%` on th is ignored in that mode, and 3-4 columns of text stay readable only by scrolling. Acceptable; no fix needed.
5. [minor] slides 4-10 — inline `font-size: 0.82rem/0.85rem` in tables is at the low end for projection; raise to 0.9rem if the fit allows after fix 1.

No other issues found in the focus range. All 29 `<aside class="notes">` are present. Tag balance, undefined classes and `{{` leftovers are clean. The only difference from the template outside SLIDES is `<title>` (allowed). Chrome is identical.

Checks: 1 pass; 2 pass (inline styles only); 3 pass; 4 pass (print clips tall slides, see 1-2); 5 pass with scrolling tables (see 4); 6 not checked beyond the focus range, no problems seen; 7 pass; 8 fail for slides 5, 6, 8 (and possibly 9).
