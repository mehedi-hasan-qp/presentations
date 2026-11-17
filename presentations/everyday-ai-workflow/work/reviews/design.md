Verdict: ready after fixes

1. [major] slide 6 — overflows one screen at 1280x720 by ~47px (scrolls on screen, clipped in print) — trim copy or drop the inline margin on the closing `<p>` (e.g. `margin-top:.75rem`), or cut one item.
2. [major] slide 10 — overflows by ~29px at 1280x720 — same fix: shorten the lead `<p>` (index.html:400-401, inline margin 1.5rem/1rem -> `.75rem`) or cut a row.
3. [major] slide 15 — overflows by ~65px at 1280x720 (32px at 900px) — reduce the table or copy (index.html:~474-475, `.dtable` + intro `<p>`); split if needed.
4. [major] slide 24 — overflows by ~66px at 1280x720 (32px at 900, 14px at 375) — trim table (index.html:~586-587, intro `<p>` margin 1.25rem -> `.75rem`) or move rows to notes.
5. [minor] slide 8 — overflows 126px at 900px and 105px at 375px (fits at 1280x720). Fine on screen because `.slide` has `overflow-y:auto`, but it is clipped in print at those widths. Fix: shorten the slide.
6. [minor] slide 19 — overflows 100px at 900px and 103px at 375px (fits at 1280). Same as 5.
7. [minor] 36 inline `style=` attributes, mostly margin/max-width/font-size/color on `<p>` and `.dtable` (e.g. index.html:285, 299, 475, 587, 369, 419). They use theme tokens and break nothing. Prefer a template utility class if the template adds one. Do not patch chrome in the deck.

No other problems found. Slides 22 is out of focus, though the whole-file checks cover it (see below).

Checks (areas 1-8)
1. HTML validity: PASS. 31 slides, 31 notes asides, 0 `{{`, 0 SAMPLE, no duplicate ids, div/table/aside/p/span/code tags balanced.
2. CSS: PASS. Every class used is defined in the template stylesheet. The inline styles are the minor item above.
3. JS: PASS. The nav JS is identical to the template.
4. Behaviour: PASS. The chrome diff is clean, so keys, swipe, buttons, N notes, progress bar and print rules come from the template.
5. Responsive: PASS. No horizontal overflow at 375, 900 or 1280. `.dtable` scrolls in x at <=900px. Vertical overflow is covered in 8.
6. Accessibility: PASS. `<html lang="en">`, no `<img>` elements. Contrast follows the template tokens (I did not recompute it).
7. Template conformance: PASS. The diff with the SLIDES block stripped is identical, `<title>` excepted.
8. Print: FAIL. Slides 6, 10, 15 and 24 exceed one screen at 1280x720 and slides 8 and 19 exceed it at narrower widths. The print CSS clips with `overflow:hidden`.
