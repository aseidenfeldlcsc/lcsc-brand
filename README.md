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

Then load the two fonts as described in `BRAND.md`, under "Fonts".

## Change the brand

Edit here, commit, then run `npm update @lcsc/brand` in each app.
