# Mapa rozvozu ovoce

Jednostránková webová aplikace (čistý HTML/JS, žádný build) pro plánování rozvozu
ovoce po Rakousku. Majitel vozí ovoce (letos višně/Weichsel) z Krtel (CZ) zákazníkům
v Rakousku a data vede v Excelu.

**Živý web:** https://dendak.github.io/mapa-rozvozu-ovoce/ (GitHub Pages, větev `main`, kořen)

## Soubory

- `index.html` — celá aplikace (Leaflet + OpenStreetMap, SheetJS z CDN, UI česky)
- `Obst.xlsx` — data rozvozu; **kopie**, originál je v OneDrive na PC majitele.
  Na web se nahrává vědomě a záměrně (majitel byl na veřejnost dat upozorněn).
- `README.md` — popis pro návštěvníky

## Jak aplikace funguje

1. Po otevření zkusí `fetch("Obst.xlsx")` — načte data přímo z webu
   (status „🌐 Data načtena z webu"), novou verzi kontroluje každých 5 minut.
2. Tlačítkem „Vybrat excelový soubor" lze připojit lokální soubor přes
   File System Access API — pak má přednost, sleduje se `lastModified` každé 3 s
   (auto-aktualizace po uložení v Excelu). Handle se ukládá do IndexedDB.
3. Adresy se geokódují přes Nominatim (max. 1 dotaz/1,1 s, cache v localStorage,
   několik fallback variant: `+", Österreich"` → raw s `countrycodes=at,cz,de,…` →
   jen segmenty s číslicemi → jen PSČ). Slovo „Selbstabholung" se z dotazu odstraňuje.

## Formát Obst.xlsx (formát A)

Bez hlavičky sloupců; list `Tabelle1`:
| A | B | C | D | E | F | G |
|---|---|---|---|---|---|---|
| Geliefert (TRUE/FALSE) | jméno zákazníka | množství kg | €/kg | součet € | adresa (volný text) | poznámka |

- Řádek, kde je v B název ovoce a chybí množství i adresa = nadpis bloku (druh ovoce).
- Součtové a prázdné řádky se přeskakují (bez jména a adresy).
- GPS souřadnice v adrese nebo poznámce (formát Google, např. `(47.7264661, 13.4350206)`)
  mají přednost před geokódováním a přepíší i starou cache — řeší špatně nalezené adresy.
- Parser podporuje i formát B (pojmenované sloupce Datum/Kunde/Adresse/PLZ/Ort/Obst/Menge/Notiz).

## Zásady

- Vše v jednom `index.html`, žádné závislosti kromě CDN (Leaflet, SheetJS). Žádný build.
- UI texty česky; názvy ovoce se poznávají česky i německy (regexy `farbeFuer`, `OBST_MUSTER`).
- `fitBounds` volat s `animate: false` (animace se ruší při překreslování markerů).
- Do repa nikdy nepřidávat zálohy ani jiné soubory s daty zákazníků nad rámec `Obst.xlsx`.
- Na PC majitele existuje mimo git `aktualizovat-web.cmd` (kopie Obst.xlsx z OneDrive + commit + push)
  a lokální kopie stránky `…\Desktop\Zeiterfassung\Obstlieferungen\Lieferkarte.html` —
  při změnách `index.html` připomenout, že lokální kopii je potřeba synchronizovat.
