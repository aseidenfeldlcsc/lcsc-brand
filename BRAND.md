# LCSC brand

The shared look, feel and voice for every LCSC app. `brand.css` holds the styles;
this file holds the rules that cannot be code. Both are read by Claude when it works
on an app that is connected to this package.

An app's own `CLAUDE.md` may override any rule here under a heading **Brand exceptions**.
Those exceptions win, for that app only. Everything not mentioned there follows this file.

## Feel

Warm, quiet, uncluttered. A paper background, ivory neutrals and a single clay accent.
A screen should read like a well-set page, not a dashboard. When in doubt, remove something.

## Color

- The palette is Anthropic's, all the way: the lightest ivory for the page (`#faf9f5`), the next ivory for side panels and hover (`#f5f4ee`), white for cards, slate `#141413` for the darkest text, and clay `#d97757` as the accent. When a new colour is needed, take it from Anthropic's brand palette before inventing one.
- Neutrals are the ivory scale, exposed as `zinc-50` to `zinc-950`. The page background is `paper`; surfaces such as cards, inputs and menus are white.
- Clay is the one accent. It is used for exactly two things: the single primary action on a screen and the active navigation item. Never for decoration, headings, links or status.
- Status colors: amber means needs attention, red means a problem or a destructive action, green means done or good, blue is informational and rare. They appear on badges, notices, stat values and small controls, never on large areas.
- Text is `zinc-900`. Secondary text is `zinc-500` or `zinc-600`. Field labels are `zinc-600`.

## Type

- Body text is Inter. Display text is Source Serif 4. Both ship with the brand package; see **Fonts** below.
- Serif is for `h1` and `h2` only, weight 500, slightly tightened. Everything else is sans.
- Sizes: page title `text-3xl`, section title `text-lg`, body `text-sm`, helper text `text-xs`, table headers 11px uppercase with wide tracking.

## Shape

- Buttons and badges are pills (`rounded-full`). Cards, menus and notices are `rounded-xl`; inputs are `rounded-lg`.
- Borders are one pixel: `zinc-200` on cards and tables, `zinc-300` on controls.
- Shadows only on floating menus, and faint.

## Icons, not words

- Simple, universally understood actions are shown as an icon, never as a word: edit (pencil), close or cancel (cross), delete or remove (bin), add (plus), open or go to (arrow right), download (arrow into tray), open in a new tab, back (arrow left).
- Test: if the word on a button is one of those verbs, it is an icon. A row's "Open" button is an arrow; a dialog's "Close" is a cross in its corner.
- Every icon control carries an `aria-label` and a tooltip saying what it does. The icon is all that shows on screen; the words appear on hover, on focus and to screen readers.
- Icons are 16px line icons with a 2px stroke, drawn in the current text color, inside a round `.iconbtn` in the quiet, danger or primary tone.
- Words remain for actions that are not universal, such as "Approve request" or "Export table". Even then they are short: a verb and a noun at most.

## Instructions live in tooltips

- A screen shows data and controls, not explanations. No instructional paragraphs. No helper sentences under fields or sections by default.
- When something needs explaining, it goes in a tooltip: `data-tip` on the control itself, or a small info icon carrying `data-tip`. It appears only on hover, focus or tap.
- Tooltip text is one short sentence, about twelve words or fewer, with no full stop. "Downloads the table as a spreadsheet", not "Click this button in order to download the table".
- A tooltip floats above the page: it stays inside the window, flips sides when there is no room and wraps when long. Never reword a tooltip or loosen a container's overflow to make one fit.
- The only on-screen prose beyond labels: a one-line subtitle under a page title when the page's purpose is not obvious, and a notice when something has gone wrong.

## Voice

- Plain words, short sentences, present tense. Say what happens, not what the user should do.
- When something is refused or blocked, say why in one line: "Fix the errors first".
- Labels are nouns, buttons are verbs. Sentence case everywhere. No Title Case, no exclamation marks.
- Use the words staff use, not the system's. Never "entity", "record", "payload", "instance".

## Interaction

- Everything clickable shows a hand cursor. `brand.css` does this.
- Destructive actions confirm first, with one short line saying what will happen.
- Every button, link and icon control has a visible hover state, always. Outlined buttons darken their border and fill one step (white to `zinc-100`); primary and danger buttons go one shade darker; quiet controls gain a `zinc-100` background. If a control does nothing on hover, it is a bug.
- Hover feedback is a color change of about 120ms. No other motion, apart from a disclosure chevron rotating.
- Detail hides behind a disclosure. A screen shows the one-line status, not the whole panel.
- One way to do a thing. If a row's name is already the link to its page, the row gets no second "open" control, not even an arrow. Icons in a row are for actions the name cannot carry: edit, delete, download.

## Components in brand.css

| Class | Use |
|---|---|
| `.btn`, `.btn-primary`, `.btn-danger`, `.btn-quiet`, `.btn-sm` | Pill buttons. One `.btn-primary` per screen. |
| `.iconbtn`, `.iconbtn-danger`, `.iconbtn-primary` | Round icon-only buttons. |
| `.input`, `.label` | Form controls and their small labels. |
| `.card` | A white, bordered, rounded surface. |
| `.table` | Quiet data table with uppercase headers. |
| `.badge` | Pill status marker; add a status color. |
| `.menu`, `.menu-item` | Floating dropdown. |
| `[data-tip]`, `data-tip-pos="top|bottom|left|right"` | Tooltip from an attribute, no library. |

Layout patterns each app builds for itself, in the same spirit: a page header with the
title, an optional one-line subtitle, a back link and the actions on the right; sections
with a serif heading; notices in the four tones; stat cards; and disclosures, a quiet
one-line status that expands.

## Fonts

The brand ships its own fonts. `brand.css` imports Inter and Source Serif 4 as
variable fonts from the `@fontsource-variable` packages, so they are installed with
this package and served by the app's own build. No build ever downloads them from
Google, and nothing is fetched from a font service at runtime.

Apps load nothing: no `next/font/google`, no `--font-body` or `--font-display`
variables, no `<link>` tags. The root layout keeps only its own classes:

```tsx
<html lang="en" className="h-full antialiased">
  <body className="min-h-full flex flex-col bg-paper text-zinc-900">
```

If an app still has the `next/font/google` imports from before brand 1.2.0, remove
them and the two `variable` class names; the brand's `--font-sans` and
`--font-serif` tokens already name the self-hosted faces.

## Overrides, per app

Rules: in the app's `CLAUDE.md`, under `## Brand exceptions`, write the exception and the reason.

```md
## Brand exceptions
- Tables use a second accent, blue-800, for the "selected" row because clay already marks the active tab.
```

Styles: redefine the token in the app's stylesheet after the brand import. The later value wins.

```css
@import "tailwindcss";
@import "@lcsc/brand/brand.css";

@theme {
  --color-clay-500: #b85a3a; /* this app's accent is a shade darker */
}
```

Keep exceptions rare. If the same exception appears in two apps, it is not an exception; move it into this file.

## Updating the brand

1. Edit `brand.css` or this file in the `lcsc-brand` repository and commit.
2. Add a line to `CHANGELOG.md`.
3. In each app, refresh the package (`npm update @lcsc/brand`). Claude does this when asked to "refresh the brand".
4. If a dev server is running, stop it, delete the `.next/dev` folder, and start it again. Turbopack caches package files and will keep showing the old styles otherwise.
