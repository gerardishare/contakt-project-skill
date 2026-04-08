# Standaard SharePoint projectstructuur

## Boomstructuur

```text
/[client] - [project]
  /00_Projectcontext
  /01_Bronbestanden
  /02_Werkbestanden
  /03_Definitief
  /04_Admin
```

## Doel per map

### 00_Projectcontext
Gebruik voor vaste projectinstructies die alle chats en outputs sturen.
Voorbeelden:
- projectbrief
- klantprofiel
- scope en uitsluitingen
- definities en terminologie
- kwaliteitscriteria
- schrijfrichtlijnen

### 01_Bronbestanden
Beschouw dit als de primaire kennisbasis (bron van waarheid voor inhoud).
Voorbeelden:
- klantdocumenten
- interviewnotities
- beleidstukken
- bronrapporten
- onderzoeksinput

### 02_Werkbestanden
Gebruik voor werk-in-uitvoering.
Voorbeelden:
- concepten
- analyses
- werkaantekeningen
- tussenversies
- vergelijkingsdocumenten

### 03_Definitief
Gebruik voor goedgekeurde eindresultaten.
Voorbeelden:
- eindrapporten
- goedgekeurde presentaties
- afgestemde/afgetekende aanbevelingen

### 04_Admin
Gebruik voor projectvoering; standaard niet leidend voor inhoudelijke analyse.
Voorbeelden:
- planningen
- budgetten
- administratie
- interne logistiek

## Interpretatieregel (bronprioriteit)

Beantwoord projectvragen bij voorkeur op basis van bronnen in deze volgorde (tenzij de gebruiker anders aangeeft):
1. 00_Projectcontext
2. 01_Bronbestanden
3. 03_Definitief
4. 02_Werkbestanden
5. 04_Admin
