# Changelog

## 1.0.0 (2026-11-05)

- First shared release.
- Rules added: icons instead of words for simple actions; instructions live in tooltips, never on screen; per-app exceptions in the app's CLAUDE.md.

## 1.0.1 (2026-11-05)

- Page background (`paper`) warmed from #faf9f5 to #f0eee6, Anthropic's ivory.
- Rule added: the palette follows Anthropic's brand colours.

## 1.0.2 (2026-11-05)

- Page background back to #faf9f5 after trying the darker ivory.

## 1.1.0 (2026-11-05)

- Every button now has a visible hover: outlined buttons darken their border and shift to zinc-100; menu items too.
- Rule added: every clickable control has a visible hover state.
- Icon list: open (arrow).

## 1.1.1 (2026-11-05)

- Rule added: one way to do a thing; a linked row name gets no extra open control.

## 1.2.0 (2026-11-05)

- Fonts are self-hosted: `brand.css` imports Inter and Source Serif 4 from `@fontsource-variable`, so no build downloads them from Google. Apps drop `next/font/google` and the `--font-body` / `--font-display` variables.

## 1.2.1 (2026-11-05)

- Tooltip bubbles are kept out of layout until shown (`display: none` instead of `opacity: 0`), so a tooltip inside a scrolling table no longer adds scrollable space and a stray scrollbar.

## 1.3.0 (2026-11-10)

- Tooltips float above the page instead of sitting inside their control's container (CSS anchor positioning). A tooltip near the edge of a dialog, card, table or menu no longer adds a sideways scrollbar or gets cut off: it stays inside the window, flips to the other side when there is no room, and wraps at 20rem. Browsers without anchor positioning keep the old behaviour.
- No change for apps: `data-tip` and `data-tip-pos` work as before.

## 1.3.1 (2026-11-10)

- `zinc-100`, the fill behind every hover, selected row and neutral badge, goes from #ebe9e0 to #ecebe7: the same weight with about half the yellow, so it reads as a soft warm grey on white instead of khaki. The page (`paper`), side panels (`zinc-50`) and borders are unchanged.
- Rule added: fills over a surface are the soft grey, not a deeper ivory.

## 1.3.2 (2026-11-10)

- `zinc-100` again: the grey of 1.3.1 lost the warmth, so the fill is now Anthropic's pale ivory, #f0eee6. Lighter than the original #ebe9e0, still ivory.
- New `.row-selected`: the pale fill plus a dark bar on the leading edge, because no pale fill reaches the 3:1 a selected state needs.
- `zinc-500` (secondary text) darkens from #76746b to #6b6961. The old value was under 4.5:1 on paper (4.45), on `zinc-50` (4.25) and on a fill (4.03); the new one passes on all of them.
- New section in BRAND.md: Contrast. Known gaps it does not fix yet: white text on the clay primary button is 3.67:1, and control borders (`zinc-300`) are 1.73:1 on white.

## 1.3.3 (2026-11-10)

- `zinc-100`, the fill for every hover, selected row and neutral badge, is now Anthropic's ivory dark, #e8e6dc: the hover colour of the nav buttons on anthropic.com. The pale #f0eee6 of 1.3.2 could not be seen on a hovered button.
- `zinc-500` (secondary text) goes to #68665f so it stays above 4.5:1 on the darker fill (4.59).
- Known gap: the clay icon of an active item is 2.93:1 on the fill, just under 3:1.

## 1.4.0 (2026-11-10)

Closer to anthropic.com, after measuring both: the colours already matched; the gap was size, space and weight.

- Type is one step larger: `text-sm` is 15px and `text-xs` is 13px (set as theme tokens, so every app picks it up with no class changes). 13px is now the floor.
- Headings: serif weight 400 with -0.015em tracking, was 500.
- Buttons: an ivory fill with an ivory border and a faint shadow on hover (was white with a grey border); 36px tall, small ones 32px. Inputs are 36px.
- New `.chip` / `.chip-on` and `.seg` / `.seg-item` / `.seg-on`. On is the ivory fill (or a white pill on an ivory track) with a slate outline. Solid dark pills are no longer how a filter, tab or toggle shows it is on.
- Dropdowns draw the brand chevron, checkboxes are slate, scrollbars are a thin ivory line.
- `.menu-item` is a rounded row with room for an icon; `.menu` pads 4px all round.
- BRAND.md: new **Space** section; Type, Shape, Contrast and Interaction updated to match.
- For apps: replace hand-rolled "selected" pills (`bg-zinc-900 text-white`) with `.chip-on` or `.seg-on`; a `select` with tight horizontal padding needs room on the right for the chevron; a top bar loses its border and takes the page colour.

## 1.5.0 (2026-11-11)

- The open list of a dropdown is drawn as a brand menu (white rounded panel, ivory hover, a tick on the current choice) instead of the system's blue list, in browsers that support `appearance: base-select`. Other browsers keep the system picker.
- Apps whose dialogs close on Escape must skip it while `select:open` matches, or Escape closes the list and the dialog together.
