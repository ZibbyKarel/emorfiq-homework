## Critical

1. `alt=""` on the product image (line 5) — an empty alt means decorative; the main image disappears for screen readers. Set alt = product name.
2. `<h2>` without an `<h1>` (line 30) — broken heading hierarchy.
3. "Add to cart" is an `<a href="#basket">` (line 52) — this is an action, not navigation; it should be a `<button>`. If it stays a link: `aria-label="Add to cart: <product name>"`.

## Moderate

4. Price (line 49) — a bare `<div>`, not semantically tied to the product.
5. Badges (lines 10, 15, 22) — bare `<div>`s; screen readers get no context, and `-10%` has no reference product.
6. Stock status (lines 40, 42) — distinguished by color (`u-textColorGreen` / `u-textColorOrange`); the text saves it, but color must not be the only carrier of information (WCAG 1.4.1).

## Minor

7. Link (line 2) — an empty link with no text is an accessibility error.
8. The card has no `<article>` — consider it for better screen-reader orientation.
9. Inside the card, a `<header>` and `<footer>` would help, and a `<section>` would be best for the body.
