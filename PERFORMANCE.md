## Runtime

1. **Images** — the dominant rendering cost (20× PNG 652×560, hover does `scale(1.25)` = bitmap repaint). `loading="lazy"` and `transform`-only transitions are fine. The real win: WebP/AVIF + `srcset`.

2. **`content-visibility: auto`** on `.ProductCard` — the biggest fundamental win; scales with the catalog. Required companion: `contain-intrinsic-size: auto 320px` (otherwise CLS).

3. **`contain: layout paint`** on `.ProductCard` — marginal with static content; relevant only with dynamic content.

## Build

4. **60× `@import`** instead of `@use`/`@forward` — `@import` is deprecated in Dart Sass 3.0 (global namespace, re-evaluation of partials). The win is correctness, not build speed.

## Loading

5. **Fonts** — `Montserrat`/`Ubuntu` are declared but not loaded; when adding them, `font-display: swap` + `<link rel="preload">` are required (otherwise FOIT/CLS).
