# Salena AU – TODO

**Tavoite:** Edetä vaiheittain siten, että jokainen askel tuottaa testattavan “valmiin palan” eikä lisää kriittisiä riippuvuuksia.  
**Periaate:** Ensin mitat ja testipenkki, sitten yksi toimiva ohjausketju (painike → rele → kuorma), vasta sen jälkeen laajennukset.

---

## 1. Mittaukset ja mekaaninen layout (seuraava työvaihe)

- [ ] Ota sähkökeskuksen mitat layouttia varten:
  - [ ] kaapin sisämitat (leveys/korkeus/syvyys)
  - [ ] DIN-kiskojen pituudet ja sijainnit (x/y/z)
  - [ ] läpivientien sijainnit ja halkaisijat
  - [ ] kiinnityspisteet / ruuvijaot / “ei saa porata” -alueet
  - [ ] johtokourujen reitit ja maksimikoot
- [ ] Kirjaa “komponenttien sijoitteluperiaate”:
  - [ ] korkea virta / pääsyötöt erilleen signaalijohdoista
  - [ ] service loop ja huoltovara liittimille
  - [ ] selkeä moduulijako (RPi / ESP / sulakkeet / kytkimet)
- [ ] Tee karkea 2D-layout (paperi/ruutupaperi/CAD) mittojen pohjalta

**Valmistumistulos:** yksi mitoitettu layout-luonnos + mitat dokumentoituina repoan.

---

## 2. Autopilotti testipenkkiin (purku ja sähköinen varmistus)

- [ ] Pura Raymarine ST5000 testipenkkiin:
  - [ ] dokumentoi johdot ja liittimet (kuvat + nimilaput)
  - [ ] kirjaa virtasyöttövaatimukset ja sulakekoko (nykyinen)
- [ ] Rakenna testipenkki:
  - [ ] 12 V virtalähde (nykyiset rajat: 11–14.5 V)
  - [ ] asianmukainen sulake testipenkkiin
  - [ ] kuormitustesti (ilman että rikot laitteita)
- [ ] USB–RS422-adapteri kiinni RPi:hin:
  - [ ] varmista että adapteri näkyy käyttöjärjestelmässä
  - [ ] lokita portti ja asetukset (tty, nopeus, parity, jne.)
- [ ] “Read-only” vaihe:
  - [ ] ota talteen raakadata (raw capture) 5–10 min
  - [ ] tallenna loki `docs/autopilot/` alle (päiväys + olosuhde)
  - [ ] kirjaa havainto: tuleeko dataa jatkuvasti vai vain tapahtumista

**Valmistumistulos:** autopilotti toimii penkissä + RPi näkee RS422-linkin + ensimmäinen raakadata talteen.

---

## 3. Rele-ESP: ensimmäinen toimiva ohjausketju (minimi)

- [ ] Valitse yksi rele-ESP moduuli “pilotiksi”
- [ ] Kytke 1 painike inputtiin ja 1 rele ulostuloon (testikuorma)
- [ ] Määrittele “minimum viable firmware”:
  - [ ] painike togglaa relettä paikallisesti
  - [ ] boottaa turvalliseen tilaan
  - [ ] Ethernet ylös, mutta ei pakollinen toimintaan
  - [ ] tilatieto sarjaporttiin
- [ ] Tee yksinkertainen tilaraportti (yksi valitaan):
  - [ ] HTTP `/status` JSON
  - [ ] UDP broadcast status
  - [ ] MQTT (vain jos broker jo valmiina)
- [ ] Dokumentoi pinnit, johdot ja testaus `docs/relay-esp/` alle

**Valmistumistulos:** yksi luotettava ohjausketju, joka toimii ilman RPi:tä ja ilman HA:ta.

---

## 4. Sähkökeskuksen “kanavakartta” (ennen kuin johtoja vedetään)

- [ ] Päätä mitä kuormia menee rele-ESP:ien taakse (ensimmäinen versio)
- [ ] Tee listaus:
  - [ ] kanava → kuorma
  - [ ] arvioitu virta
  - [ ] sulakekoko
  - [ ] johdinpoikkipinta (arvio)
  - [ ] manuaaliohitus kyllä/ei
- [ ] Linkitä listaus layoutiin (mihin fyysisesti mikäkin päätyy)

**Valmistumistulos:** yksi “relekartta v1” jonka mukaan voi oikeasti rakentaa.

---

## 5. Anturi-ESP (vain kun releohjaus on tosi)

- [ ] Päätä mittauspaketin minimisetti:
  - [ ] 1 tankki
  - [ ] 1 akkujännite
  - [ ] 1 päävirta tai kuormavirta
- [ ] Tee firmware niin, että data tulee ulos USB:n yli
- [ ] Lisää datan tallennus (RPi) ja dokumentoi mittauskalibrointi

**Valmistumistulos:** ensimmäinen mitattu arvo näkyy luotettavasti ja toistettavasti.

---

## 6. Home Assistant (käyttöliittymä vasta kun on sisältöä)

- [ ] Käynnistä HA konttina
- [ ] Lisää 3–5 ensimmäistä entiteettiä (releet + 1 mittaus)
- [ ] Tee yksi selkeä dashboard-näkymä (veneessä käytettävä)

**Valmistumistulos:** käyttöliittymä, joka näyttää oikeaa dataa ja ohjaa ei-kriittisesti.

---

## 7. Valaistus (PWM) viimeistelyvaiheessa

- [ ] päätä kanavamäärä ja ryhmät
- [ ] valitse 1 valo-ESP pilottiin
- [ ] testaa PWM häiriöt ja taajuus
- [ ] lisää painikeohjaus ja vasta sitten HA-integraatio

---

## Repo-rakenne (minimisuositus)

- `docs/current_state.md`
- `docs/architecture.md`
- `docs/todo.md`
- `docs/layout/` (mitat, kuvat, luonnokset)
- `docs/autopilot/` (kytkennät, RS422, raw-logit)
- `docs/relay-esp/` (pinnit, firmware, testit)

---
