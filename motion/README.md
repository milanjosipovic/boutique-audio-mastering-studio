# Tideline Mastering — Website

A production-quality, mobile-first marketing site for a boutique audio
mastering studio, built with pure HTML5 and CSS3. There is no JavaScript
anywhere in the project — every interactive behavior (the mobile navigation,
hover and focus states, and scroll-linked motion) is implemented with native
HTML and CSS.

## Live structure

```
tideline/
├── index.html          # Single-page site: all markup and content
├── css/
│   └── styles.css       # All styling — tokens, layout, components, motion
└── README.md
```

Open `index.html` directly in any modern browser, or serve the folder with
any static file server. There is no build step and no dependencies to
install.

## Design approach

The studio subject — a one-engineer analog/digital mastering chain — shapes
the design directly rather than sitting inside a generic template:

- **Typography.** [Fraunces](https://fonts.google.com/specimen/Fraunces) (a
  warm display serif) is paired with
  [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono) for specs,
  labels, and data — the same contrast a mastering engineer lives in, between
  the feel of a record and the numbers on a meter. Inter carries body copy.
- **Color.** A warm, near-black studio palette (`#14130f`) with a tape-amber
  accent (`#c9793d`) and a muted phosphor-green meter glow (`#8fbf9f`),
  rather than a stock dark-mode neon or a generic light theme.
- **Signature element.** A CSS-only animated level meter, built from plain
  `<span>` elements and `@keyframes`, doubles as both hero backdrop and the
  divider between every section — a real reference to the subject rather
  than a decorative rule.
- **Content.** All copy — the signal-chain steps, work samples, studio
  spec sheet, and testimonials — is original placeholder content written
  for this fictional studio, not lorem ipsum.

## Front-end techniques used

This project is a working reference for building fully-featured interfaces
in HTML and CSS alone:

| Technique | Where |
|---|---|
| Mobile-first responsive layout | Entire stylesheet, breakpoints layered upward from a single column |
| Checkbox-hack navigation | `.nav-toggle` in `index.html` / `css/styles.css` — an accessible, keyboard-operable mobile menu with no JavaScript |
| CSS custom properties (design tokens) | `:root` in `css/styles.css` — colors, type scale, spacing |
| Fluid type scale | `clamp()`-based `--step-*` variables |
| CSS Grid + Flexbox | Page layout, the work grid, the signal-chain list, the booking form |
| Container queries | `.work-card` — card padding adapts to the card's own width, not the viewport |
| Scroll-linked animation | `animation-timeline: scroll()` on the meter bars, with a static fallback |
| `prefers-color-scheme` | Automatic light variant of the palette |
| `prefers-reduced-motion` | Disables all animation and smooth scrolling |
| `prefers-contrast` | Strengthens borders and text contrast |
| `:focus-visible` | Visible keyboard focus throughout, including the custom nav toggle |
| `accent-color` | Native form control theming (checkboxes, selects) |
| `color-mix()` | Header backdrop tint |
| Semantic HTML5 | `header`, `nav`, `main`, `section`, `article`, `blockquote`, `table` used for their actual meaning, not generic `div`s |

## Accessibility notes

- The mobile menu toggle is a real, keyboard-focusable `<input type="checkbox">`
  paired with a `<label>` — it can be opened and closed without a mouse and
  without JavaScript.
- Landmarks (`header`, `nav`, `main`, `footer`) and heading order are used
  correctly for screen reader navigation.
- All interactive elements have a visible `:focus-visible` state distinct
  from `:hover`.
- Color contrast targets WCAG AA in both the dark (default) and light
  (`prefers-color-scheme: light`) palettes.
- All motion — the level meter animation and smooth-scroll navigation — is
  disabled under `prefers-reduced-motion: reduce`.

## The contact form

The booking form submits with a plain `mailto:` action
(`action="mailto:hello@tidelinemastering.example"`), since the site has no
backend and includes no JavaScript. This is a deliberate trade-off worth
knowing about before you rely on it:

- It opens the visitor's configured email client with the form fields
  pre-filled in the message body. It does **not** send the email directly
  from the browser.
- Behavior varies by browser and OS, and it does nothing at all if the
  visitor has no email client configured (common on many phones and in
  webmail-only setups).
- The email address on the page (`hello@tidelinemastering.example`) is a
  placeholder — replace it with a real address before deploying.

If you need reliable form delivery, the form can be pointed at a form
backend service (for example Formspree or Getform) by changing the `action`
and `method` attributes — no JavaScript required for that either. A fully
custom submission flow with client-side validation feedback would require
introducing JavaScript, which is intentionally out of scope for this build.

## Customizing

- **Colors and type scale** live entirely in the `:root` block at the top of
  `css/styles.css`. Changing a token there updates it everywhere.
- **Copy and content** live entirely in `index.html`; there is no templating
  layer.
- **Work samples** are plain `<article class="work-card">` blocks with an
  inline gradient (`--art-a` / `--art-b`) standing in for artwork — swap in
  real `<img>` elements when artwork is available.
- **Fonts** are loaded from Google Fonts via `<link>` tags in the `<head>`.
  To self-host instead, download the font files and replace the `<link>`
  tags with local `@font-face` declarations.

## Browser support

Built against current evergreen browsers (recent Chrome, Firefox, Safari,
Edge). Two techniques are used as progressive enhancement and degrade
gracefully on older engines:

- `animation-timeline: scroll()` — where unsupported, the meter bars simply
  run their ordinary looping animation instead of a scroll-linked one.
- `container-type: inline-size` — where unsupported, the work cards keep
  their default padding at every size.

Nothing in the layout depends on either feature; both are additive polish.

## License

This is a demonstration project. Replace the placeholder studio name,
contact details, and sample work with real content before using it for an
actual business.