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
