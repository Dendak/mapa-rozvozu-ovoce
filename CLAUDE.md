# Mapa rozvozu ovoce

Jednostránková webová aplikace (čistý HTML/JS, žádný build) pro plánování rozvozu
ovoce po Rakousku. Majitel vozí ovoce (letos višně/Weichsel) z Krtel (CZ) zákazníkům
v Rakousku a data vede v Excelu.

**Živý web:** https://dendak.github.io/mapa-rozvozu-ovoce/ (GitHub Pages, větev `main`, kořen)

## Soubory

- `index.html` — celá aplikace (Leaflet + OpenStreetMap, SheetJS z CDN). UI dvojjazyčné
  cs/de: slovník `TEXTE`, `t(klíč, …)`, statické prvky `data-t`/`data-t-ph`, přepínač
  `#sprachen` (localStorage `sprache`, výchozí podle jazyka prohlížeče). Názvy ovoce
  z Excelu jsou německé, česká verze je překládá přes `OBST_CS`; poznámky (sloupec G,
  německy) překládá po frázích `NOTIZ_CS` (`notizText`) — při nové poznámce s novým
  obratem přidat frázi do slovníku; locale `LOC()`.
- `Obst.xlsx` — data rozvozu; **kopie**, originál je v OneDrive na PC majitele.
  Na web se nahrává vědomě a záměrně (majitel byl na veřejnost dat upozorněn).
- `README.md` — popis pro návštěvníky

## Jak aplikace funguje

1. Po otevření `fetch("Obst.xlsx")` — data jen z webu (status „🌐 Data načtena z webu"),
   novou verzi kontroluje každých 5 minut. (Připojení lokálního souboru přes File System
   Access API bylo odstraněno — nepoužívalo se.)
2. Adresy se geokódují přes Nominatim (max. 1 dotaz/1,1 s, cache v localStorage,
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

## Plánovač (režim „plan")

Čtvrté tlačítko ve Stavu rozvozu. Zaškrtnuté nedoručené zastávky (klíč = geoKey,
pořadí v poli `planAuswahl`, localStorage) tvoří plán: mapa/součty ukazují jen je.
Pořadí se mění přetažením karty za úchyt ⠿ (pointer events na `document` —
capture na úchytu nejde, přesun v DOM by ho zrušil). Trasa přes veřejný OSRM
(`router.project-osrm.org`): route s `annotations=duration` pro značky povinné
pauzy po 4:30 jízdy, trip pro „nejkratší pořadí". Start je Krtely 70 (Nominatim,
cache `startPos`); volby: návrat do Krtel (výchozí ano) a průjezd přes Wullowitz
(„přes Freistadt", výchozí ano — jinak OSRM vede z Linze přes Bad Leonfelden).
Průjezdní body nejsou cíle (`ziel: false`) — úseky se pro dojezdy slučují.
Výběr je po druzích ovoce (klíč `geoKey§druh`), karta zastávky ukazuje rozpis druhů
se zaškrtávátky. Odjezd z Krtel (`planAbfahrt`, localStorage) → odhad příjezdů na
zastávky: jízda + 45 min za každou pauzu (po 4:30) + `ENTLADE_MIN` (15) za zastávku.

## Seznam zastávek

Karta = jedna adresa (geoKey), sloučené řádky. Ukazuje poznámky (📝, `notizHtml`
dělá z telefonů odkazy `tel:`, slova Urlaub/dovolená/! zvýrazní červeně) a odkaz
🧭 Waze (waze.com/ul deep link na souřadnice). Klik na kartu = zoom + otevření
bubliny (marker uložen v `orte.get(key).marker`). Hledání `#suche` filtruje jen
seznam, mapa/součty/trasa zůstávají. Mobil (≤700 px): tlačítko `#kartenToggle`
přepíná `body.nur-karte` (skryje panel, mapa přes celou obrazovku).

## Zásady

- Vše v jednom `index.html`, žádné závislosti kromě CDN (Leaflet, SheetJS). Žádný build.
- UI texty česky; názvy ovoce se poznávají česky i německy (regexy `farbeFuer`, `OBST_MUSTER`).
- `fitBounds` volat s `animate: false` (animace se ruší při překreslování markerů).
- Do repa nikdy nepřidávat zálohy ani jiné soubory s daty zákazníků nad rámec `Obst.xlsx`.
- Na PC majitele existuje mimo git `aktualizovat-web.cmd` (kopie Obst.xlsx z OneDrive + commit + push)
  a lokální kopie stránky `…\Desktop\Zeiterfassung\Obstlieferungen\Lieferkarte.html` —
  při změnách `index.html` připomenout, že lokální kopii je potřeba synchronizovat.
