## Vážné

1. `alt=""` na produktovém obrázku (řádek 5) — prázdný alt = dekorativní; pro screen reader hlavní obrázek zmizí. Alt = název produktu.
2. `<h2>` bez `<h1>` (řádek 30) — rozbitá hierarchie nadpisů.
3. "Do košíku" je `<a href="#basket">` (řádek 52) — akce, ne navigace; má být `<button>`. Pokud zůstane odkaz: `aria-label="Do košíku: <název produktu>"`.

## Středně vážné

4. Cena (řádek 49) — holý `<div>`, není sémanticky svázaná s produktem.
5. Badges (řádky 10, 15, 22) — holé `<div>`, screen reader nemá kontext; `-10%` nezná referenční produkt.
6. Stav skladu (řádky 40, 42) — rozlišen barvou (`u-textColorGreen` / `u-textColorOrange`); text to zachraňuje, ale barva nesmí být jediný nositel informace (WCAG 1.4.1).

## Drobnosti

7. Zakomentovaný overlay odkaz (řádek 2) — při odkomentování prázdný odkaz bez textu = accessibility chyba.
8. Karta nemá `<article>` — zvážit pro lepší orientaci screen readeru. 
9. Unitř karty může být `<header>` i `<footer>` a pro body bude nejlepší `<section>`
