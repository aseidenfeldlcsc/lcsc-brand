# lcsc-brand

The one copy of how LCSC apps look, feel and speak.

- `brand.css`: colors, fonts, shapes and the shared component classes. Apps import it after Tailwind.
- `BRAND.md`: the rules that cannot be code. Each app's `CLAUDE.md` imports it so Claude follows it automatically.

## Connect an app

```bash
npm install github:aseidenfeldlcsc/lcsc-brand
```

In the app's main stylesheet:

```css
@import "tailwindcss";
@import "@lcsc/brand/brand.css";
```

In the app's `CLAUDE.md`:

```md
@node_modules/@lcsc/brand/BRAND.md
```

The fonts come with the package; the app loads none of its own.

## Change the brand

Edit here, commit, then run `npm update @lcsc/brand` in each app. If that app has a dev
server running, stop it, delete its `.next/dev` folder and start it again.

## Prompts to paste into an app's Claude session

To connect an app for the first time:

> Connect this app to the shared LCSC brand. It lives at github.com/aseidenfeldlcsc/lcsc-brand (npm package `@lcsc/brand`). Read its README and BRAND.md first. Then install it, import `@lcsc/brand/brand.css` right after the Tailwind import in the main stylesheet, and remove this app's own copies of the same colours, fonts and component classes. Remove any `next/font/google` imports and the `--font-body` / `--font-display` variables from the root layout; the brand ships its own fonts. Add the line `@node_modules/@lcsc/brand/BRAND.md` to CLAUDE.md, creating the file if needed, with an empty "## Brand exceptions" section under it. Then go through every screen and apply the rules in BRAND.md: Anthropic palette, icons instead of words for simple actions, instructions only in tooltips, one clay primary action per screen. Run the app and check the main pages, then commit and push. If this app does not use Tailwind v4, stop and tell me before changing anything.

To pick up a brand change later:

> Refresh the brand in this app: update `@lcsc/brand`, restart the dev server after deleting `.next/dev`, check the main pages still look right, then commit and push.
