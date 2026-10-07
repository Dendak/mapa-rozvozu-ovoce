# Pracovní poznámky

Deník práce na mapě rozvozu, aby šlo navázat z jakéhokoli zařízení. Nejnovější nahoře.
Na konci každé session: co je hotové, co je rozdělané, co dál.

## Rozdělané / další kroky
- [ ] Mapa na Wedos za přihlášením (PR v obou repech): založit schránku `denis@ovoce-holub.cz` ve Wedosu,
  nastavit FTP secrets v tomhle repu, sloučit PR, otestovat přihlášení Pavla i Denise.
- [ ] Potom repo přepnout na soukromé a vypnout GitHub Pages (data zákazníků jsou zatím veřejná).
- [ ] `README.md` je zastaralé: popisuje výběr lokálního souboru (File System Access API), který byl odstraněn. Data se teď načítají jen z webu.
- [ ] Na notebooku leží stará kopie v OneDrive (`…\Radtour 2026\mapa-rozvozu-ovoce`), 13 commitů pozadu, bez lokálních změn. Až nebude potřeba, smazat ručně.

## Historie
### 2026-10-07 (2)
- Přidán workflow `deploy-wedos.yml` (FTP do `api/data/mapa/`). Přihlášení e-mailem a heslem
  pro pavel@ a denis@ovoce-holub.cz je v `ovocnarstvi-holub` (`api/mapa/index.php`).

### 2026-10-07
- Repo naklonováno do `C:\Users\holub\code\mapa-rozvozu-ovoce` (mimo OneDrive).
- Přidán tento soubor a odkaz na něj v `CLAUDE.md` (sekce „Práce napříč zařízeními“).
- Stav při převzetí: poslední commit db9f3c8 (Doručeno 6. 10.: Moser 800 kg Alexander Lucas, #15).
