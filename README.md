# salena-automaatio

Salena Automaatio modernisoi Amigo 40 "Salena" -purjeveneen sähkö- ja tietojärjestelmät hybridimallilla:

Analoginen vikasietoinen sähkö
ESP32-pohjainen automaatio
Raspberry Pi 5 -älykeskus

Tavoitteena on turvallinen, älykäs ja etäohjattava Smart Boat, jossa perinteinen mekaaninen varmistus yhdistyy nykyaikaiseen IoT-automaatioon.

Projektin tarkoitus
Tämä projekti toteuttaa kokonaisvaltaisen sähkö- ja automaatiojärjestelmän, jossa:

Kriittiset toiminnot (navigointi, pilssipumput, kulkuvalot) voidaan aina ohittaa fyysisillä kytkimillä (1-0-Auto).
ESP32-mikrokontrollerit hoitavat laitteiden normaalin ohjauksen, valvonnan ja mukavuustoiminnot.
Raspberry Pi 5 toimii järjestelmän aivoina (Home Assistant, SignalK, kameravalvonta), mutta sen vikaantuminen ei estä veneen peruskäyttöä.


Arkkitehtuuri

Fyysinen kerros: Tähtimäinen 12V DC -virranjakelu, manuaaliset ohituskytkimet.
Ohjauskerros: Hajautetut ESP32/Arduino-mikrokontrollerit ohjaavat releitä ja lukevat antureita.
Äly- ja datakerros: Raspberry Pi 5, Home Assistant, SignalK, MQTT, VPN-etäyhteys.


Päätoiminnot

Rele-ESP: Toimilaitteiden ohjaus, virranmittaus, vianmääritys, MQTT.
Valo-ESP: Valaistuksen ohjaus, himmennys, tilannevalaistus.
Ruori-ESP/Arduino: Autopilotti, PID-säätö, SignalK-integraatio.
Älykeskus (RPi5): Home Assistant, SignalK, videovalvonta, etäyhteydet.


Dokumentaatio

Tekninen järjestelmäkuvaus (PDF)
Kytkentäkaaviot
BOM / hankintalista
Testipenkki ja kehitysohjeet


Lisenssi
Tämä projekti on lisensoitu MIT-lisenssillä.
