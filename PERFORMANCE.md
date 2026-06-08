## Runtime

1. **Obrázky** — dominantní cena vykreslení (20× PNG 652×560, hover dělá `scale(1.25)` = repaint bitmapy). `loading="lazy"` a `transform`-only tranzice jsou OK. Reálný zisk: WebP/AVIF + `srcset`.
2. **`content-visibility: auto`** na `.ProductCard` — největší principiální zisk; škáluje s katalogem. Nutný doplněk: `contain-intrinsic-size: auto 320px` (jinak CLS).
3. **`contain: layout paint`** na `.ProductCard` — marginální při statickém obsahu; relevantní až s dynamickým obsahem.

## Build

4. **60× `@import`** místo `@use/@forward` — `@import` je deprecated v Dart Sass 3.0 (globální namespace, re-evaluace partialů). Zisk je korektnost, ne rychlost buildu.

## Loading

5. **Fonty** — `Montserrat`/`Ubuntu` deklarovány, ale nenačteny; při přidání nutné `font-display: swap` + `<link rel="preload">` (jinak FOIT/CLS).
