# 🍒 Mapa rozvozu ovoce

Jednoduchá webová mapa (Leaflet + OpenStreetMap), která načte excelový seznam
rozvozů (Obst.xlsx) a ukáže zastávky na mapě Rakouska — s množstvím, cenami,
filtrem „ještě rozvézt / doručeno" a součty.

**Data zůstávají u vás:** stránka čte Excel přímo z vašeho počítače
(File System Access API) a nikam ho neodesílá. Adresy se vyhledávají přes
[Nominatim](https://nominatim.openstreetmap.org/) (OpenStreetMap).

Použití: otevřít stránku → „Vybrat excelový soubor" → vybrat Obst.xlsx.
Mapa se pak aktualizuje automaticky při každém uložení v Excelu.
