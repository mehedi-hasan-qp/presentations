# DESIGN.md: default presentation template

Derived from `template.html` as built. Every class, value and key here exists in that file. Read this before writing slides.

## 1. Overview

A clean, white, single-file slide deck set in Fira Sans. One blue accent carries emphasis; orange marks live demos and small secondary labels (`.code-lang`, `.card-sub`, via `--demo-text`), never headings or emphasis. It originated as a CI/CD pipeline talk deck, so it favours short statements, plain tables, code panels and flow diagrams over decoration.

## 2. Tokens

### Colour tokens (`:root`)

| Variable | Value | Use |
|---|---|---|
| `--bg` | `#ffffff` | Page and slide background |
| `--fg` | `#0f0f0f` | Headings, strong text |
| `--fg-sub` | `#2e2e2e` | Body paragraphs, table cells, `.vs-attr strong` |
| `--fg-muted` | `#666666` | Labels, descriptions, counter, nav button text |
| `--border` | `#e0e0e0` | Card, table and step dividers, `code` border |
| `--surface` | `#f4f4f6` | Card, step-row and code-head background, `code` background |
| `--accent` | `oklch(61.6% 0.1696 251.2)` | Large `.accent` headings, progress bar, title-slide rule, highlighted borders and other non-text uses |
| `--accent-soft` | `oklch(61.6% 0.1696 251.2 / 8%)` | Highlighted card and step-row fill |
| `--accent-mid` | `oklch(61.6% 0.1696 251.2 / 18%)` | `.flow-badge` fill |
| `--accent-text` | `oklch(50% 0.17 251)` | Small accent text (WCAG AA, 5.9:1 on white, 5.4:1 on `--surface`): `.kicker`, `.code-head`, `.step-num`, `.vs-card.hi .vs-card-label`, `.card-slash`, `.flow-badge`, `.flow-step.on .flow-step-name`, `th.acc`; also the button focus ring |
| `--demo-text` | `oklch(52% 0.15 50)` | Small demo-orange text (5.8:1 on white, 5.3:1 on `--surface`): `.code-lang`, `.card-sub`, `.kicker.demo`, `.step-num.demo` |

Literal colours used outside `:root` (not tokens):
- Demo orange `oklch(72.3% 0.1755 56.7)`: fills and borders only (`.demo-badge` background and border). Orange text uses `--demo-text`.
- Badge colours: `.badge-same` (green oklch) and `.badge-diff` (amber oklch).
- Code panel: `.code-body` `#0e0e0e` background, `#ccc` text; `.tok-warn` `#e5c07b`, `.tok-ok` `#98c379`, `.tok-dim` `#9a9a9a` (6.9:1 on the code background).
- Divider slide: background `oklch(50% 0.17 251)` (white text 5.9:1), `h2` `#fff`, `.sub` `#fff` at `opacity: 0.94`.
- `body.on-dark` chrome: white text, `oklch(100% 0 0 / 70%)` button border, `oklch(100% 0 0 / 18%)` button fill (`/ 32%` on hover), white progress bar and focus ring.
- Notes panel: background `var(--fg)`, text `#eee`, `.none` `#999`.
- Nav hover background `#ebebeb`.

### Typography

Font import (line 8):
`@import url('https://fonts.googleapis.com/css2?family=Fira+Sans:ital,wght@0,300;0,400;0,500;0,600;0,700;1,300;1,400;1,500&display=swap');`

Stack: `'Fira Sans', system-ui, sans-serif`. Code uses `monospace`. Body is 16px, line-height 1.5.

| Element | Size | Weight | Line-height | Other |
|---|---|---|---|---|
| `h1` | `clamp(2.25rem, 6vw, 5.25rem)` | 700 | 1.06 | letter-spacing -0.025em |
| `h2` | `clamp(1.9rem, 4.5vw, 3.75rem)` | 600 | 1.1 | letter-spacing -0.015em |
| `h3` | `clamp(1.4rem, 2.5vw, 2rem)` | 600 | 1.2 | |
| `p` | `clamp(1.05rem, 1.8vw, 1.45rem)` | 400 | 1.65 | colour `--fg-sub` |
| `.kicker` | 0.85rem | 700 | | uppercase, letter-spacing 0.15em, `--accent`, margin-bottom 1.5rem |
| `code` | 0.88em | 400 | | monospace, `--surface` background |

### Spacing

- Slide padding: `clamp(1.5rem, 5vw, 4.5rem) clamp(1.25rem, 7vw, 7rem)`, bottom `clamp(4rem, 8vw, 5.5rem)` (leaves room for nav).
- Content is vertically centred by `::before`/`::after` auto-margin spacers and scrolls if taller than the screen.
- Component margins: `margin-top: 2rem` on `.vs-grid`, `.dtable`, `.flow`, `.card-grid`, `.steps-list`; `1.75rem` on `.code-block`.
- Inline style used in samples: `margin-top: 2rem; max-width: 640px` on the lead paragraph.

### Radii and borders

- 4px `.flow-badge`; 5px `code`, `.badge`; 6px `.demo-badge`, `.slide-nav button`; 8px `.flow-step`; 12px `.card`; 14px `.vs-card`, `.code-block`, first/last `.step-row`.
- Borders are 1px (`--border`), or 1.5px on cards and flow steps, 2px under `.dtable th`, 6px left on `.title-slide`, 3px top on `.notes-panel`. The `.progress-bar` is 4px tall, not a border.

### Motion

- Slide fade: `.slide` `transition: opacity 0.35s ease, visibility 0s 0.35s`; `.slide.active` `transition: opacity 0.35s ease` (visibility flips instantly on show, after the fade on hide).
- Progress: `width 0.35s cubic-bezier(.2,.8,.2,1)`.
- Nav buttons: background 0.15s, `:active` scale(0.92).
- Keyframes (inside `@media (prefers-reduced-motion: no-preference)`): `riseIn`, `popIn`, `slideInL`. Applied only to `.slide.active` descendants, with staggered `animation-delay` on `.step-row`, `.card`, `.vs-card`, `.flow-step`.
- Print disables all animation and transition.

## 3. Slide anatomy

```html
<!-- SLIDES:START -->
  <!-- SAMPLE: center -->
  <div class="slide center">
    <div class="kicker">The problem</div>
    <h1>Key point.<br><span class="accent">Bold claim.</span></h1>
    <p style="margin-top: 2rem; max-width: 680px;">Supporting sentence.</p>
    <aside class="notes">Pause here and let the statement land.</aside>
  </div>
<!-- SLIDES:END -->
```

- Every slide is a direct child of `.slides` and matches `.slides > .slide`. The script selects slides with that selector.
- `.slide` is absolutely positioned and `visibility: hidden` (out of the accessibility tree and tab order). `.slide.active` is shown; exactly one slide is active. The script sets `active` on load (`show(0)`).
- Place new slides between `<!-- SLIDES:START -->` and `<!-- SLIDES:END -->`. Keep the markers.
- `{{TITLE}}` is the only placeholder, in `<title>`. Replace it when building.
- `<aside class="notes">` is the last child of each slide. Its text feeds the notes panel. It is hidden on the slide itself.
- Slide modifiers: `.center` (centres content, `text-align: center`), `.title-slide`, `.divider`.

## 4. Components

Each entry: when to use, then a trimmed snippet from the sample slide.

**title-slide** (`.slide.title-slide`): opening slide only. Adds a blue left rule.
```html
<div class="slide title-slide active">
  <div class="kicker">Event or context · Date</div>
  <h1>Main title.<br><span class="accent">Subtitle hook.</span></h1>
  <p style="margin-top: 2rem; max-width: 640px;">One sentence.</p>
```

**center** (`.slide.center`): single statements and closing slides.
```html
<div class="slide center">
  <div class="kicker">Thank you · Questions?</div>
  <h1>Call to action.<br><span class="accent">Next step.</span></h1>
```

**divider** (`.slide.divider`, with `.sub`): section break. Full blue background, white text. Use `center`.
```html
<div class="slide divider center">
  <h2>01 · Section title</h2>
  <div class="sub">One-line section description</div>
```

**kicker** (`.kicker`): small uppercase label above every heading. Use one per slide.
```html
<div class="kicker">Agenda</div>
```

**accent** (`.accent`): wrap the second line of a heading. Use it as the only emphasis in a title.
```html
<h2>Short heading.<br><span class="accent">Accent phrase.</span></h2>
```

**steps-list** (`.steps-list`, `.step-row`, `.step-num`, `.step-title`, `.step-desc`): ordered points or an agenda. `.step-row.hi` highlights one row.
```html
<div class="steps-list">
  <div class="step-row">
    <div class="step-num">01</div>
    <div><div class="step-title">First step</div><div class="step-desc">Short description.</div></div>
  </div>
```

**vs-grid** (`.vs-grid`, `.vs-card`, `.vs-card.hi`, `.vs-card-label`, `.vs-card-title`, `.vs-attr`): two options side by side. Use `.hi` on the recommended one. Stacks to one column under 900px.
```html
<div class="vs-grid">
  <div class="vs-card">
    <div class="vs-card-label">Before</div>
    <div class="vs-card-title">Card title</div>
    <div class="vs-attr"><strong>Attribute:</strong> short value</div>
  </div>
  <div class="vs-card hi">…</div>
</div>
```

**dtable** (`.dtable`, `th.acc`, `.badge`, `.badge-same`, `.badge-diff`): reference tables, up to about four rows. Badges mark same or different. `th.acc` highlights one column.
```html
<table class="dtable">
  <tr><th>Column one</th><th class="acc">Column two</th><th>Column three</th></tr>
  <tr>
    <td><strong>Row A</strong></td>
    <td>Description with <code>inline code</code></td>
    <td><span class="badge badge-same">Same</span></td>
  </tr>
</table>
```

**code-block** (`.code-block`, `.code-head`, `.code-lang`, `.code-body`, `.tok-warn`, `.tok-ok`, `.tok-dim`): a code, config or log excerpt. Use `tok-ok` for passing lines, `tok-warn` for lines to point at, `tok-dim` for comments. Keep to 10 lines or fewer.
```html
<div class="code-block">
  <div class="code-head"><span>filename.ext</span><span class="code-lang">language</span></div>
  <div class="code-body"><span class="tok-dim"># comment</span>
key: value
<span class="tok-warn">warn_line: check this</span></div>
</div>
```

**inline code** (`code`): filenames, commands and identifiers inside a sentence or table cell.
```html
<td>Description with <code>inline code</code></td>
```

**flow** (`.flow`, `.flow-step`, `.flow-step.on`, `.flow-step-name`, `.flow-badge`, `.flow-arr`, `.flow-arr.on`): a left-to-right pipeline of up to five steps. `.on` marks the current step. Arrows hide under 900px and steps wrap.
```html
<div class="flow">
  <div class="flow-step"><span class="flow-step-name">Step one</span></div>
  <div class="flow-arr">→</div>
  <div class="flow-step on"><span class="flow-step-name">Step two</span><span class="flow-badge">Focus</span></div>
  <div class="flow-arr on">→</div>
  <div class="flow-step"><span class="flow-step-name">Step three</span></div>
</div>
```

**card-grid** (`.card-grid`, `.card`, `.card.hi`, `.card-slash`, `.card-name`, `.card-sub`): a recap or set of 3 to 6 items. Use `.hi` on one. Columns are `repeat(auto-fit, minmax(150px, 1fr))`.
```html
<div class="card-grid">
  <div class="card"><div class="card-slash">/one</div><div class="card-name">Card name</div><div class="card-sub">small note</div></div>
  <div class="card hi"><div class="card-slash">/three</div><div class="card-name">Highlighted card</div><div class="card-sub">small note</div></div>
</div>
```

**demo-badge** (`.demo-badge`, `.kicker.demo`, `.step-num.demo`): marks a live-demo slide. Orange is the demo colour (see section 2).
```html
<div class="demo-badge">Live demo</div>
<div class="kicker demo">Demo title</div>
<div class="step-num demo">01</div>
```

**notes** (`aside.notes`, `.notes-panel`): speaker notes. Press N to toggle the panel at the bottom. Hidden on screen and in print. Every slide needs one.

## 5. Slide types to components

| Slide type | Sample comment | Classes to use |
|---|---|---|
| Title | `title` | `title-slide`, `kicker`, `h1` + `.accent`, `p` |
| Centre | `center` | `center`, `kicker`, `h1` + `.accent`, two `p` lines |
| Section divider | `divider` | `divider center`, `h2`, `.sub` |
| Agenda or steps | `steps-list` | `kicker`, `h2` + `.accent`, `steps-list` / `step-row` |
| Comparison | `vs-grid` | `vs-grid`, `vs-card`, `vs-card.hi` |
| Reference table | `dtable` | `dtable`, `badge-same` / `badge-diff` |
| Code or config | `code-block` | `code-block`, `tok-*` |
| Process | `flow` | `flow`, `flow-step.on`, `flow-badge` |
| Recap | `card-grid` | `card-grid`, `card.hi` |
| Live demo | `demo` | `demo-badge`, `kicker demo`, `step-row.hi`, `step-num demo` |
| Closing | `closing` | `center`, `kicker`, `h1` + `.accent`, two `p` lines |

## 6. Interaction

- Keys: `ArrowRight` and `Space` next; `ArrowLeft` previous; `Home` first; `End` last; `N` toggles notes. Navigation wraps at both ends.
- Buttons: `#prev` and `#next` in `.slide-nav`, bottom right. Both use `aria-label`.
- Swipe: horizontal movement over 50px and greater than vertical movement triggers next or previous. Ignored when the touch starts or ends inside `.code-body`, `.dtable` or `.notes-panel` (those scroll horizontally).
- Buttons keep native Space/Enter: the keydown handler returns early when the event target is inside a `button`, so Space on a focused nav button activates it once instead of also advancing. `.slide-nav button:focus-visible` shows a 3px `--accent-text` outline (white on dark).
- On dark slides: `show()` toggles `body.on-dark` when the current slide has `.divider`. CSS under `body.on-dark` recolours `.slide-counter`, `.kbd-hint`, `.slide-nav button` (text, border, fill, hover, focus ring) and `.progress-bar` to white so the chrome stays visible on the blue background.
- Progress: `#progress` (`.progress-bar`) is a 4px fixed top bar whose width is `(cur + 1) / total`.
- Counter: `#counter` (`.slide-counter`) shows `n / total`, bottom centre.
- Key hint: `.kbd-hint` bottom left.
- Each slide's scroll resets to the top on show.
- Modified keys (Cmd, Ctrl, Alt) are ignored so browser shortcuts work.
- Notes preserve line breaks (`white-space: pre-line`). Put demo steps and FALLBACK on separate lines.

Responsive (`max-width: 900px`): `vs-grid` becomes one column; `flow` wraps and hides `flow-arr`; `dtable` scrolls horizontally; `kbd-hint` is hidden.

Print and PDF: `@page { size: landscape; margin: 0; }`. Each `.slide` becomes a static page (`visibility: visible` forced) of `100vh` with a page break after it. Nav, counter, progress, hint and notes are hidden. Limit: a slide taller than one screen is clipped in print (`overflow: hidden`). Keep every slide within one screen.

## 7. Do and don't

Do:
- One idea per slide. Lead with a `kicker` and an `h1` or `h2`.
- Keep content slides to about 30 words of body text.
- Use a `divider` between sections. Talks under 15 minutes may skip dividers.
- Use one `.hi`, `.on` or `.accent` emphasis per slide.
- Use `tok-*` classes in code blocks, not new colours.
- Keep the `<aside class="notes">` on every slide, even if short.
- Keep a slide within one screen height so PDF output is complete.
- Reuse the sample snippets above as the starting point for each slide.

Don't:
- Don't edit the `<style>` chrome or the `<script>` nav logic inside a deck. Only add or change slides between the markers.
- Don't add libraries, fonts, or CDN scripts. The deck is one self-contained file apart from the Fira Sans import.
- Don't use orange for headings or emphasis. It marks live demos and small secondary labels only.
- Don't invent classes. Use only the ones in sections 4 and 5. If a new one is needed, add it to template.html first.
- Don't add `.hi` or `.accent` to every item in a list.
- Don't remove `{{TITLE}}` before the build step fills it.
