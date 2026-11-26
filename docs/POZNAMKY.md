# Pracovní poznámky

Deník práce na mapě rozvozu, aby šlo navázat z jakéhokoli zařízení. Nejnovější nahoře.
Na konci každé session: co je hotové, co je rozdělané, co dál.

## Rozdělané / další kroky
- [ ] Mapa na Wedos běží (https://ovoce-holub.cz/api/mapa/), FTP secrets nastavené (hlavní účet `w395099`),
  první nahrání proběhlo. Zbývá: založit schránku `denis@ovoce-holub.cz`, otestovat přihlášení Pavla i Denise.
- [ ] Potom repo přepnout na soukromé a vypnout GitHub Pages (data zákazníků jsou zatím veřejná).
- [ ] `README.md` je zastaralé: popisuje výběr lokálního souboru (File System Access API), který byl odstraněn. Data se teď načítají jen z webu.
- [ ] Originál `Obst.xlsx` v OneDrive je z 29. 9. a chybí v něm změny z října (Moser, Neuwirth, Burgstaller, Steinbichler). `aktualizovat-web.cmd` by je přepsal – nejdřív originál srovnat s repem.
- [ ] Na notebooku leží stará kopie v OneDrive (`…\Radtour 2026\mapa-rozvozu-ovoce`), 13 commitů pozadu, bez lokálních změn. Až nebude potřeba, smazat ručně.

## Historie
### 2026-11-26
- Frutteria GmbH (Sonystraße 8, 5081 Anif), faktura 202, doručeno 10. 11.: 130 kg Novembra à 2,00 € a 312 kg jablek Idared à 0,50 €
  (celkem 416 €). Součtový řádek v Obst.xlsx rozšířen na C2:C74 / E2:E74.
- Doručeno Jakob Lukasser Weitlaner (Schrottendorf 7, 9911 Assling): 1850 kg hrušek Novembra paušálem 1300 €
  (≈ 0,70 €/kg), odvezeno 21. 11.
- Gasteiger Packham doručen: 600 kg paušálem 500 € (≈ 0,83 €/kg; objednáno za 1 €/kg). Datum zapsáno 26. 11. – upřesnit.
- Nová odrůda „Birnen Novembra“: barva `#3a9d8f`, překlad v `OBST_CS`, doma počítána jako ostatní hrušky (7 Kč/kg).

### 2026-11-05
- Burgstaller doručen: 1000 kg Packham za 1 100 € (datum doručení zapsáno 5. 11. – upřesnit, pokud jel jindy).
- L K (landwirt.com, Ramingstein) zrušeno – neodpověděl(a); STORNIERT, množství 0.
- Nová objednávka Gasteiger 600 kg Packham za 1 €/kg (nedoručeno).

### 2026-10-31
- Martin Neuwirth (400 kg Packham, odběr ve Spittalu) zrušil. Řádek zůstal jako STORNIERT (množství 0), kontakt na příští rok.

### 2026-10-16 (2)
- Steinbichler (300 kg Konference, Biberbach) zrušen – neozval se. Řádek zůstal jako STORNIERT (množství 0), kontakt na příští rok.

### 2026-10-16
- Burgstaller (1000 kg Packham, Döbriach): 26.–30. 10. pryč, dovézt až od 31. 10. (poznámka v Obst.xlsx).

### 2026-10-13
- Nová objednávka Martin Neuwirth: 400 kg Packham za 1 €/kg, odběr ve Spittalu an der Drau (bydlí v 9634 Gundersheim),
  zatím nepotvrzeno (poznámka „Zusage offen“). Do `NOTIZ_CS` přidány překlady.

### 2026-10-07 (2)
- Přidán workflow `deploy-wedos.yml` (FTP do `api/data/mapa/`). Přihlášení e-mailem a heslem
  pro pavel@ a denis@ovoce-holub.cz je v `ovocnarstvi-holub` (`api/mapa/index.php`).

### 2026-10-07
- Repo naklonováno do `C:\Users\holub\code\mapa-rozvozu-ovoce` (mimo OneDrive).
- Přidán tento soubor a odkaz na něj v `CLAUDE.md` (sekce „Práce napříč zařízeními“).
- Stav při převzetí: poslední commit db9f3c8 (Doručeno 6. 10.: Moser 800 kg Alexander Lucas, #15).
