# Salena AU – Architecture

**Versio:** v5.0.0  
**Projekti:** Integroitu veneautomaatio- ja navigointijärjestelmä (Amigo 40 “Salena”)  
**Periaate:** Vene toimii täysin ilman automaatiota. Automaatiokerros parantaa hallittavuutta ja näkyvyyttä, mutta ei ole kriittinen riippuvuus.

---

## 1. Kokonaiskuva

Salena AU on kerroksellinen järjestelmä, jossa navigointi, automaatio ja 12 V kuormat on erotettu toisistaan. Ohjauksen ensisijainen perusratkaisu on paikallinen ja deterministinen: kriittiset toiminnot eivät riipu Wi-Fi:stä, pilvestä tai Home Assistantista.

Järjestelmä jakautuu kolmeen tasoon:

- **Taso 1: Älytaso / Navigointi** – Raspberry Pi 5 (OpenPlotter, SignalK, OpenCPN)
- **Taso 2: Automaatiotaso** – ESP32-S3 Ethernet -moduulit (releet, I/O, mittaukset)
- **Taso 3: Kenttätaso** – 12 V kuormat, sulakkeet ja manuaalinen ohitus

---

## 2. Tavoitteet ja reunaehdot

### 2.1 Päätavoitteet
- Navigointi ja datakeruu yhdessä alustassa (RPi 5)
- Kuormien ohjaus modulaarisesti (ESP32-yksiköt)
- Vikasietoisuus ja huollettavuus
- Laajennettavuus ilman “uudelleenrakentamista”

### 2.2 Reunaehdot
- Veneen perustoiminnot eivät saa olla riippuvaisia:
  - Raspberry Pi:stä
  - Home Assistantista
  - Wi-Fi-yhteydestä
  - ulkoisesta verkosta / internetistä
- Kaikki kuormat suojataan sulakkeilla; ohjain ei suojaa kuormaa.

---

## 3. Looginen arkkitehtuuri

### 3.1 Taso 1 – Raspberry Pi 5 (Navigation & Integration Layer)

**Rooli**
- Navigointi (OpenCPN)
- Datan välitys ja aggregointi (SignalK)
- Dataloggaus ja integraatiot (myöhemmin HA-kontti)

**Laitteisto**
- Raspberry Pi 5
- WS-27709 PCIe → M.2 NVMe HAT+
- NVMe SSD
- WS-27966 UPS HAT (E)

**Rajapinnat**
- Ethernet ↔ ESP32-S3 (ohjaus/tilat)
- USB ↔ anturi-/mittaus-ESP (tankit, virrat)
- USB–RS422 ↔ Raymarine ST5000 (autopilotti)

**Kriittisyys**
- Ei kriittinen veneen perustoiminnalle

---

### 3.2 Taso 2 – ESP32-S3 (Automation Layer)

Automaatiotaso koostuu erillisistä, rajatuista ohjaimista. Jokaisella ohjaimella on selkeä vastuualue. Ohjainten logiikka ja fyysiset painikkeet toimivat paikallisesti, jolloin keskuskoneen tai verkon vika ei estä käyttöä.

#### 3.2.1 Rele-ESP (2 kpl)

**Rooli**
- 12 V kuormien on/off-ohjaus
- Paikallinen ohjaus fyysisillä painikkeilla
- Tilatietojen jakaminen Raspberry Pi:lle

**Liitännät**
- Ethernet ens
