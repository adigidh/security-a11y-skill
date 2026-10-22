# Accessibility checklist (WCAG 2.1 AA)

Read this only when the routed or changed files include rendered UI (HTML, JSX/TSX, Vue, Svelte, templates, CSS). Report each finding with the **control** (element or component at `path:line`) and the **impact** — what a keyboard, screen-reader or low-vision user can no longer do. Check shared components for a role, label or focus style before you report a missing one. You read code; do not report computed contrast ratios unless both colors are literal values in the diff.


**Text alternatives (1.1.1)** — an `img`, `svg` or icon that carries meaning
with no `alt`, `aria-label` or `title`; an empty `alt=""` on an image that
carries meaning; an icon-only button or link with no accessible name.

**Semantic controls (4.1.2, 2.1.1)** — a clickable `div` or `span` (an
`onClick` on a non-interactive element) with no `role`, no `tabIndex` and no
key handler; a link used as a button with no `href`; a custom widget (tabs,
menu, dialog, combobox) with no ARIA role or state (`aria-expanded`,
`aria-selected`).

**Labels (1.3.1, 3.3.2)** — a form input, select or textarea with no
`<label>`, `aria-label` or `aria-labelledby`; a placeholder used as the only
label; an error message that is not tied to its field (`aria-describedby`)
or not announced.

**Color and contrast (1.4.1, 1.4.3)** — a status, error or required marker
shown by color alone, with no text or icon; a literal text and background
color pair in the diff below 4.5:1 (3:1 for large text).

**Focus and keyboard (2.1.1, 2.4.3, 2.4.7)** — `outline: none` or
`outline: 0` with no replacement focus style; a positive `tabIndex` that
breaks the tab order; a control that a keyboard cannot reach or operate; a
modal with no focus move on open or no return on close; a keyboard trap.

## Severity

- **Critical** — a primary task (submit, sign in, navigate, pay) that a keyboard or screen-reader user cannot complete.
- **Warning** — a control such a user cannot reach, name or operate outside a primary task, or a state they cannot perceive.
- **Suggestion** — an improvement with no lost function behind it.
