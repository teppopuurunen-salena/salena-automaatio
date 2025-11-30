Rele-ESP
Rele-ESP on osa Salena Automaatio -järjestelmää. Se vastaa Amigo 40 "Salena" -purjeveneen 12V toimilaitteiden ohjauksesta, virranmittauksesta ja vianmäärityksestä. Järjestelmä perustuu ESP32-mikrokontrolleriin ja kommunikoi muun järjestelmän kanssa MQTT:n välityksellä.
Päätoiminnot

Ohjaa 12V releitä (esim. valot, pumput, viihde, verkko, lämmitys)
Lukee virta- ja jänniteanturit (INA219/INA226, I2C)
Valvoo kriittisten laitteiden toimintaa (esim. pilssipumput)
Toteuttaa vianmäärityslogiikkaa (esim. hälytys, jos virta ei kulje)
Kommunikoi MQTT:n kautta älykeskukselle (RPi5/Home Assistant/SignalK)
Tukee fyysisiä painonappeja ja LED-indikaattoreita (MCP23017 I/O-laajennin)

Laitteisto

ESP32 Development Board (WROOM-32)
2 x 12-kanavainen 12V relemoduuli (optoerotettu)
INA219/INA226 virta-anturit (I2C)
MCP23017 I/O-laajennin (painonapit ja LEDit)
WiFi-yhteys veneen sisäverkkoon

Ohjelmisto

Kieli: C++ (Arduino/PlatformIO)
Kirjastot: Adafruit INA219, PubSubClient, Adafruit MCP23017, WiFi, Wire
MQTT-yhteys: esim. mqtt://192.168.10.2, aiheina esim. vene/pilssi1_virta
Koodi löytyy src/-kansiosta

Asennus ja käyttöönotto

Kytke laitteisto dokumentaation mukaisesti.
Syötä WiFi- ja MQTT-tiedot src/config.h-tiedostoon.
Käännä ja lataa ohjelma ESP32:lle PlatformIO:lla.
Tarkista sarjaportista, että virranmittaus ja MQTT-lähetys toimivat.
Testaa painonapit ja LEDit.

Dokumentaatio

Tekninen järjestelmäkuvaus
Kytkentäkaaviot ja relekartta
Testipenkin ohjeet

Lisenssi
Tämä lohko kuuluu Salena Automaatio -projektin MIT-lisenssin piiriin.
