# DFR1154 vogelhuisje-camera — firmware releases

Publieke releases-repo voor de gecompileerde firmware van het vogelhuisje-camera-project
(DFRobot ESP32-S3 AI Camera / DFR1154). Bevat alleen het gecompileerde `.bin`-bestand en
een versienummer, geen broncode — de firmware-bronrepo blijft privé.

Bedoeld om door het board zelf te worden uitgelezen (via `GITHUB_PATH` in `appGlobals.h`),
zowel voor automatische OTA-updates als voor het verse-SD-kaart-downloadmechanisme:
- `version.txt` — huidige versienummer (vergelijkt het board met zijn eigen `APP_VER`)
- `firmware.bin` — bijbehorend, klaar-om-te-flashen app-binary (compatibel met de bestaande
  `Update.write()`-OTA-route in de firmware, dezelfde soort bestand als handmatig via de
  "OTA Upload"-tab wordt geüpload)
- `data/MJPEG2SD.htm`, `data/common.js` — de webinterface-bestanden; worden door het board
  gedownload als ze nog niet op de SD-kaart staan (verse kaart), en na een OTA-update
  automatisch opnieuw gedownload zodat de webinterface in sync blijft met de firmware

Bij elke nieuwe release worden al deze bestanden hier overschreven, met hetzelfde versienummer.

## `rollback/` — één stap terug

Het board zelf heeft geen dual-partition A/B-rollback (na een OTA-write is er geen
gegarandeerde, bekende vorige image meer in flash staan om automatisch op terug te vallen).
In plaats daarvan onthoudt deze repo het net-vorige release hier expliciet, inclusief de
bijbehorende webinterface-bestanden (anders zou een rollback wel de oude firmware terugzetten,
maar met de nieuwste — mogelijk niet-passende — webinterface):
- `rollback/firmware.bin`, `rollback/version.txt` — exacte kopie van wat vóór de huidige
  release in `firmware.bin`/`version.txt` stond.
- `rollback/data/MJPEG2SD.htm`, `rollback/data/common.js` — idem voor de webinterface-bestanden.

**Bij elke nieuwe release, vóórdat de root-bestanden overschreven worden**: kopieer eerst de
huidige (nog-niet-overschreven) `firmware.bin`/`version.txt`/`data/*` naar `rollback/` (zelfde
structuur). Dat geeft precies één stap terug (niet de volledige historie) — voldoende om een
kapotte release ongedaan te maken vanaf de webinterface ("Roll Back"-knop), zonder het board
fysiek te hoeven benaderen. Board-kant: na een rollback-herstart wordt precies één keer van
`rollback/` i.p.v. de root gedownload (`otaDataSubPath()` in `otaUpdate.cpp`, via een
`RTC_NOINIT_ATTR`-marker die de ESP.restart() overleeft), zodat firmware en webinterface na een
rollback altijd bij elkaar passen.
