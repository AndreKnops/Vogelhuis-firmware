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
