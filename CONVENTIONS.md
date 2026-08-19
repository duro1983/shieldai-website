# ShieldAI site conventions — READ BEFORE EDITING ANY PAGE

Every page shares one stylesheet: `assets/shield.css`. `index.html` is the
reference implementation. Read both before you touch anything.

## Non-negotiable rules

1. **Never redefine a token.** No raw hex values, px font sizes, or ad-hoc
   spacing in page CSS. Use `var(--b-600)`, `var(--s-6)`, `var(--t-lg)` etc.
   The only exception is a genuinely page-unique value that has no token.

2. **Never edit the contents of a `<script>` block.** Preserve every `id`,
   `name`, `data-*` attribute, and any class name JavaScript queries
   (`getElementById`, `querySelector`, `classList.toggle`, etc.). You may add
   classes alongside them. If a JS-referenced class must also carry styling,
   keep the original class and add the shield class next to it:
   `class="filter-btn active"` stays exactly as-is.

3. **No emoji anywhere.** Replace every emoji with an inline SVG using
   `viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"
   stroke-linecap="round" stroke-linejoin="round"` and `aria-hidden="true"`.
   Icons inherit colour from `currentColor` — never hardcode a stroke colour.

4. **WCAG AA minimum.** 4.5:1 for body text, 3:1 for text ≥24px or ≥18.66px
   bold. Never put `--n-500` on white or on `--n-950`; both land at ~4.4:1.
   Use `--text-muted` on light grounds and `--n-400` on dark ones.

5. **No horizontal overflow at 390px.** Do not put a flex or grid container
   around mixed inline content (text with inline `<code>`, `<strong>`, `<a>`
   in the middle of a sentence) — each element becomes its own item and the
   sentence cannot wrap. Use normal flow with a hanging absolutely-positioned
   icon instead. See `.spec` in shield.css.

## Required page skeleton

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>PAGE TITLE — ShieldAI</title>
<meta name="description" content="...">
<link rel="icon" href="logo.svg" type="image/svg+xml">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<link rel="stylesheet" href="assets/shield.css">
<style>
  /* ONLY page-unique components. Built from tokens. Keep it short. */
</style>
</head>
<body>
<a class="skip-link" href="#main">Skip to content</a>
<!-- header: copy verbatim from index.html, including the nav-toggle button
     and the mobile-menu <script> immediately after </header> -->
<main id="main"> ... </main>
<!-- footer: copy verbatim from index.html -->
</body>
</html>
```

Copy the `<header>` block, the mobile-menu `<script>`, and the `<footer>`
block **verbatim from index.html**. Do not re-author them. The only permitted
change is marking the current page's nav link with `aria-current="page"`, and
on tool pages adding a context label after the brand:

```html
<span class="app-header__context">Eligibility checker</span>
```

## Component vocabulary (already in shield.css — do not reinvent)

Layout `.wrap` `.section` `.section--sunken` `.section--dark` `.grid grid--2|3|4`
`.split` `.sec-head` `.eyebrow` `.measure` `.stack`
Marketing `.hero` `.pill` `.trust` `.card` `.card--hover` `.icon-chip`
`.product` `.tags` `.tag` `.steps` `.step` `.spec` `.stats` `.stat`
`.frameworks` `.framework` `.cta-band` `.link-arrow`
Buttons `.btn` + `.btn--primary` `.btn--secondary` `.btn--ghost` `.btn--lg`, `.btn-row`
App `.app-main` `.page-head` `.panel` (`__header` `__body` `__footer`)
`.field` `.label` `.input` `.select` `.textarea` `.hint` `.error-text`
`.field-row` `.choice-group` `.choice` `.stepper` `.status--*` `.table`
`.table-wrap` `.toolbar` `.filter-btn` `.alert--info|success|warn|danger`
`.timeline` `.chat` `.msg` `.modal` `.dl` `.empty`

On dark sections add `on-dark` to the element so button and focus variants flip.

## Content rules

- Company voice: precise, unhedged, no marketing inflation. Short sentences.
- **Do not invent facts** — no customer names, testimonials, case studies,
  logos, staff counts, funding, or performance numbers that are not already
  in the file you are editing.
- Keep existing factual claims as they are, with one exception: if a page
  asserts a compliance *certification* (ISO 27001, SOC 2), soften to
  "aligned with" / "built against" rather than "certified".
- Use Canadian/British spelling consistent with index.html (organisation,
  centralised, licence as a noun).
- `© 2026 ShieldAI` in the footer.

## Definition of done

- Renders with no horizontal scrollbar at 1440px, 820px and 390px.
- Every interactive control reachable by keyboard with a visible focus ring.
- All original JS still works; no console errors.
- No emoji, no inline `style="..."` except for a genuinely one-off value.
- Page CSS block is dramatically smaller than what it replaced.
