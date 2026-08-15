# DFR1154 vogelhuisje-camera — firmware releases

Publieke releases-repo voor de gecompileerde firmware van het vogelhuisje-camera-project
(DFRobot ESP32-S3 AI Camera / DFR1154). Bevat alleen het gecompileerde `.bin`-bestand en
een versienummer, geen broncode — de firmware-bronrepo blijft privé.

Bedoeld om door het board zelf te worden uitgelezen voor automatische OTA-updates:
- `version.txt` — huidige versienummer (vergelijkt het board met zijn eigen `APP_VER`)
- `firmware.bin` — bijbehorend, klaar-om-te-flashen app-binary (compatibel met de bestaande
  `Update.write()`-OTA-route in de firmware, dezelfde soort bestand als handmatig via de
  "OTA Upload"-tab wordt geüpload)

Bij elke nieuwe release worden beide bestanden hier overschreven.
