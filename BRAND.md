# LCSC brand

The shared look, feel and voice for every LCSC app. `brand.css` holds the styles;
this file holds the rules that cannot be code. Both are read by Claude when it works
on an app that is connected to this package.

An app's own `CLAUDE.md` may override any rule here under a heading **Brand exceptions**.
Those exceptions win, for that app only. Everything not mentioned there follows this file.

## Feel

Warm, quiet, uncluttered, and modelled on anthropic.com: a paper background, ivory
neutrals, bold plain headings, slate for what matters most and a little clay. A screen
should read like a well-set page, not a dashboard. When in doubt, remove something.

The values in `brand.css` were read off the live anthropic.com (its news and home
pages), not judged by eye. When a new pattern is needed, look at how that site does it,
measure it in the browser, and follow it. Its typeface is its own and is not copied.

## Color

- The palette is Anthropic's, all the way: the lightest ivory for the page (`#faf9f5`), the next ivory for side panels (`#f5f4ee`), ivory dark for hover and selected fills (`#e8e6dc`), white for cards, slate `#141413` for the darkest text, and clay `#d97757` as the accent. When a new colour is needed, take it from Anthropic's brand palette before inventing one.
- Neutrals are the ivory scale, exposed as `zinc-50` to `zinc-950`. The page background is `paper`; surfaces such as cards, inputs and menus are white.
- Fills laid over a surface (a hovered control, a selected row, a neutral badge) are `zinc-100`, Anthropic's ivory dark (`#e8e6dc`), the hover colour of the nav buttons on anthropic.com. One colour for all of them; anything paler cannot be seen on a hovered button.
- Slate is the colour of emphasis: the single primary action on a screen (`zinc-800`, darker on hover), whatever is switched on (`zinc-950`), and a dark band.
- Clay is the one accent and is rare: the active navigation item and an app's own mark. Never for buttons, decoration, headings, links or status.
- A dark band (`.band`: `zinc-950` with ivory words) sets off the one featured thing on a page and makes the footer. One featured band per screen at most. Buttons inside it are ivory.
- Status colors: amber means needs attention, red means a problem or a destructive action, green means done or good, blue is informational and rare. They appear on badges, notices, stat values and small controls, never on large areas.
- Text is `zinc-900`. Secondary text is `zinc-500` or `zinc-600`. Field labels are `zinc-600`.

## Contrast

Measured as WCAG contrast ratios, not judged by eye.

- Text is at least 4.5:1 against whatever it sits on, including a hover or selected fill. `zinc-500` is the lightest text colour: it passes on white, paper, `zinc-50` and `zinc-100` (4.59 on the fill). `zinc-400` is for placeholders and disabled text only.
- The fill is about 1.25:1 against white, so it never carries a state alone. Hover may be a fill only. Selected, active or on must add a cue of at least 3:1: a solid slate fill (`.chip-on`, `.seg-on`), a dark bar (`.row-selected`), a dark underline on a tab, a tick, or the clay icon of the active nav item.
- Solid slate means "on", "main action" or "featured", and nothing else: a chip or segment that is on, the primary button, the viewer's own item on a calendar, a count badge, a tooltip, a band. On a dark band, text is ivory (`paper`, `zinc-100`) and secondary text is `zinc-300`.

## Type

- Everything is Inter, headings included. It ships with the brand package; see **Fonts** below.
- Headings (`h1`, `h2`, and the title of a post or card) are bold, weight 700, tightened (-0.02em), with a line height near 1.2, as on anthropic.com. Buttons, chips and body text are regular weight; medium is for a label or a name inside a row.
- Source Serif 4 is kept for an app's wordmark beside its mark, and nothing else.
- 13px text (`text-xs`) is tracked +0.01em; `brand.css` does this.
- Sizes: page title `text-3xl`, section title `text-lg`, body `text-sm` (15px), helper text `text-xs` (13px), table headers 11px uppercase with wide tracking. `brand.css` sets `text-sm` and `text-xs` one step above Tailwind's defaults.
- 13px is the floor. Nothing a person has to read is smaller, apart from table headers and the labels inside a dense chart or calendar block.

## Space

- A screen breathes. When it feels cramped, the fix is more room or fewer things, never smaller type.
- Controls are at least 32px tall (`.btn-sm`, `.chip`, `.iconbtn`) and 36px by default (`.btn`, `.input`). On a phone, anything tapped often is 40px or more.
- Sections are 24px apart or more; a page title has 20px under it; cards pad 16px, dialogs 24px.
- One surface, not boxes in boxes: a card does not sit inside a card, and a filter row sits on the page, not in its own bordered box.
- No box around a list. A feed or list of rows sits on the page between rules (`.rows`), as on anthropic.com, with 20px or more above and below each row. A card is for a surface that has to be set apart: a form, a data table, a panel beside other panels, a dialog. When unsure, leave the box off.

## Shape

- Buttons have 10px corners; small buttons and icon buttons 8px. Chips and badges are pills (`rounded-full`). A segmented bar has 10px corners. Cards, menus and notices are `rounded-xl`; a band is `rounded-2xl`; inputs are `rounded-lg`.
- Borders are one pixel: `zinc-200` on cards, tables, buttons and chips; `zinc-300` on inputs.
- Fewer lines. The top bar is the page colour with no line under it; rows are divided, not boxed: by `zinc-100` inside a white card or table, by `zinc-200` on the page, where the paler line cannot be seen.
- Shadows only on floating menus, and faint.
- Controls are drawn by the brand, not the system: dropdowns show the brand chevron and open as a brand menu (ivory hover, a tick on the current choice, never the system's blue list, where the browser allows it), checkboxes are slate, scrollbars are a thin ivory line. `brand.css` does all of it.

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
- Every button, link and icon control has a visible hover state, always. Plain buttons darken their border and fill one step (`zinc-100` to `zinc-200`); primary and danger buttons go one shade darker; quiet controls gain a `zinc-100` background. If a control does nothing on hover, it is a bug.
- Hover feedback is a colour change over about 150ms. No other motion, apart from a disclosure chevron rotating.
- Detail hides behind a disclosure. A screen shows the one-line status, not the whole panel.
- A "Read more" under folded text stands apart from the text: its own line with room above, `zinc-900` and semibold, with the disclosure chevron. It never reads as the last line of the paragraph.
- One way to do a thing. If a row's name is already the link to its page, the row gets no second "open" control, not even an arrow. Icons in a row are for actions the name cannot carry: edit, delete, download.

## Components in brand.css

| Class | Use |
|---|---|
| `.btn`, `.btn-primary`, `.btn-danger`, `.btn-quiet`, `.btn-sm` | Buttons with 10px corners: ivory dark with a hairline border; the primary one slate with ivory words. One `.btn-primary` per screen. |
| `.iconbtn`, `.iconbtn-danger`, `.iconbtn-primary` | Icon-only buttons with 8px corners. |
| `.input`, `.label` | Form controls and their small labels. |
| `.card` | A white, bordered, rounded surface. |
| `.table` | Quiet data table with uppercase headers. |
| `.badge` | Pill status marker; add a status color. |
| `.chip`, `.chip-on` | A pill that can be on or off: a tag, or a filter where several can be picked. On is a solid slate pill. |
| `.seg`, `.seg-item`, `.seg-on` | Segmented control, for one choice of a few: a joined ivory bar, the choice that is on a slate block. |
| `.band` | A dark surface with ivory words: the featured thing on a page, the footer. |
| `.menu`, `.menu-item` | Floating dropdown. |
| `.row-selected` | The selected row of a list or table: pale fill plus a dark bar. |
| `.rows` | A list or feed with no box: a rule above, below and between its rows. |
| `[data-tip]`, `data-tip-pos="top|bottom|left|right"` | Tooltip from an attribute, no library. |

Layout patterns each app builds for itself, in the same spirit: a top bar in the page
colour with no line under it, its active item an ivory pill with a clay icon; a page header with the
title, an optional one-line subtitle, a back link and the actions on the right; sections
with a bold heading; the sections of one page as underlined tabs on a rule (the open
one `zinc-900`, semibold, with a 2px dark underline), kept apart from a `.seg` filter
under them; the next or featured item as a `.band` above plain rows; a dark footer
(`.band`) with the app's mark; on a phone, a bottom tab bar in ivory dark (`zinc-100`)
with near-black icons, the open one clay, and no line above it; notices in the four
tones; stat cards; and disclosures, a quiet one-line status that expands.

## Fonts

The brand ships its own fonts. `brand.css` imports Inter (everything) and Source Serif 4
(wordmarks only) as variable fonts from the `@fontsource-variable` packages, so they are installed with
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
