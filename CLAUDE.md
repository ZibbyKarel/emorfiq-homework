# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A frontend demo/homework task: a responsive product-card grid (e-shop). The deliverable (`tasks.md`, in Czech) is to (1) read the readme, (2) restyle the product card to match the design in `theme.fig`, and (3) propose HTML/CSS improvements (accessibility, performance, structure). `theme.fig` is the Figma source of truth for the visual target — open it in Figma to compare against the rendered output.

## Commands

- `npm i` — install deps (sass, vite).
- `npm run development` — Vite dev server on port 5173 with HMR. Does **not** serve HTML; it only provides the JS/CSS module + hot reload.
- `npm run production` — Vite build. Bundles `assets/js/index.js` → `dist/app.js` and `dist/app.css` (entry/asset names are fixed in `vite.config.js`).
- Serve the page by running `index.php` under a PHP HTTP server (e.g. `php -S localhost:8000`). The Vite server alone will not render the page.

There is no test suite, linter, or formatter configured.

## How the page renders

`index.php` is the only HTML entry. Line 2 sets `$mode` (`development` | `production`):
- **development** — pulls `@vite/client` and `assets/js/index.js` from `http://localhost:5173`. Requires `npm run development` running alongside the PHP server. HMR works; the printed localhost:5173 URL is not browsable on its own (no page served there).
- **production** — links the built `/dist/app.css` and `/dist/app.js`. Requires `npm run production` to have been run first.

`index.php` loops 20× including `templates/productCard.php`. That template uses `rand(0,1)` throughout to randomly show/hide badges, stock states, and swap title/image — so the grid looks different on every refresh. This is intentional demo scaffolding, not a bug.

The JS pipeline is CSS-only: `assets/js/index.js` does nothing but `import '../scss/index.scss'`. Vite compiles the SCSS and emits it as `app.css`.

## SCSS architecture

`assets/scss/index.scss` imports, in order: `functions`, `variables`, `theme`, `mixins`, `root`, `reboot`, `typography`, `components`. Each directory has an `_index.scss` barrel.

This is a **token-driven, themeable component library**. The core conventions:

- **Override via variables, never edit component CSS.** Components (`components/product-card/`, `button/`, `badge/`, etc.) declare every styleable value as a SCSS variable with `!default` in their local `_variables.scss`. To change a component's appearance, set that variable in the theme layer (`assets/scss/theme/`) so it wins over the `!default`. See `theme/product-card/_index.scss` — it's a commented-out catalog of every override knob available for the product card. Uncomment and set values there rather than touching `components/product-card/*.scss`. Custom CSS that can't be expressed as a variable is allowed in the theme layer too, but the component partials should stay untouched. HTML in `templates/` should also be left as-is where possible.

- **Mobile/desktop variable pairs.** Most properties come as `$..._mobile-*` and `$..._desktop-*`. Mobile values apply at base; desktop values are re-applied inside `@include media-breakpoint-up($product-card-breakpoint)` (breakpoint defaults to `lg`). Desktop defaults usually inherit from their mobile counterpart.

- **`change-value` mixin** (`mixins/change-value.scss`) is used pervasively: `@include change-value($prop, $value, $default)` emits the property *only if* `$value != $default`, keeping generated CSS minimal. It special-cases `font-size`/`line-height` to route through the font mixins. The sentinel for "unset" is the literal `none` (note: a few defaults have typos like `nones` / `display: nones` — preserve or fix deliberately, don't assume).

- **Breakpoints** (`variables/global.scss` → `$grid-breakpoints`, Bootstrap-style map `0/xs/sm/md/lg/xl/xxl/hd`). Use the `media-breakpoint-up/down/between/only` mixins from `mixins/breakpoints.scss`; don't hand-write media queries.

- **CSS cascade layers** order the cascade: `settings.ui` (`:root` custom props in `root/`), `components.eshop` (component rules). Font sizes are emitted as `--fs-300`…`--fs-2600` custom properties generated in `root/_index.scss` from the `$ui-fs` map, then referenced as `var(--fs-500)` etc.

- **Design tokens** live in `variables/global.scss` (spacers `$spacer-0..7`, font weights, font-size scale, breakpoints) and `variables/color.scss`. Reference tokens; avoid magic numbers.

## Notes

- `desktop.ini` files are Windows artifacts — ignore them.
- Not a git repo. There is no remote, CI, or deploy step.
