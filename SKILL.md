---
name: contakt-project-setup
description: Zet een klant- of intern project op waarbij SharePoint de documentbron is en een ChatGPT Project de vaste werkcontext. Gebruik wanneer ChatGPT SharePoint-beschikbaarheid moet verifiëren, de project-rootmap moet vaststellen, een standaard mappenstructuur moet voorstellen/aanmaken, en een interactieve intake moet doen die eindigt in herbruikbare projectcontext + starter prompts.
---

# Contakt Project Setup (ChatGPT)

Voer deze workflow in volgorde uit. Wees expliciet over wat je **hebt geverifieerd**, wat je **hebt afgeleid**, en wat de gebruiker **handmatig** nog moet doen.

## Setup workflow

1. **Verifieer SharePoint-beschikbaarheid (eerst).**
2. **Stel de SharePoint project-rootmap vast (canoniek).**
3. **Stel mappenstructuur voor of maak deze aan (als dat echt kan).**
4. **Doe een intake-interview (één hoofdvraag per beurt).**
5. **Lever de eindoutput: setup status + mappenstructuur + projectcontext + starter prompts.**

Sla stap 1 niet over. **Claim nooit** dat SharePoint, een connector, of schrijf-rechten bestaan tenzij je dit **daadwerkelijk hebt geverifieerd** met beschikbare mogelijkheden.

## Wanneer (niet) impliciet starten

Deze vaardigheid mag impliciet starten **alleen** bij vragen zoals:
- “Zet een SharePoint projectmap/structuur op”
- “Maak een projectcontext voor dit klantproject op basis van SharePoint”
- “We willen SharePoint als bron van waarheid + ChatGPT Project context”

Start **niet** impliciet bij:
- algemene SharePoint-vragen (bijv. “wat is SharePoint”)
- enkel document-samenvattingen zonder project-setup intent
- situaties waar de gebruiker expliciet geen SharePoint wil gebruiken

## 1) Verifieer SharePoint-beschikbaarheid

Begin met vaststellen of SharePoint beschikbaar is in de huidige ChatGPT-omgeving.

### Definitie “geverifieerd”

Beschouw SharePoint pas als **geverifieerd** als je minimaal dit kunt bevestigen:
- Connector/app is zichtbaar in de omgeving
- Authenticatie is voltooid (ingelogd)
- Toegang tot de beoogde site/bibliotheek/rootmap is mogelijk (**lezen/read**)
- (Optioneel) Je kunt ook schrijven (**write**) of mappen aanmaken

Rapporteer het toegangsniveau expliciet als één van:
- `none` (geen connector / niet beschikbaar)
- `unauthenticated` (wel beschikbaar, niet ingelogd)
- `read` (wel ingelogd, alleen lezen)
- `write` (wel ingelogd, lezen + schrijven)

### Beslisregels

- Als de omgeving connected apps/connectors/sources toont, inspecteer die eerst.
- Als SharePoint beschikbaar en geauthenticeerd is, zeg dat en noteer het access level.
- Als SharePoint bestaat maar niet geauthenticeerd is, zeg dat de gebruiker moet inloggen.
- Als SharePoint niet beschikbaar is, stop de automatisering en leg de handmatige stap uit: SharePoint verbinden via **Settings > Apps** of via de workspace admin.

### Edge-cases die je expliciet afhandelt

- **Geen toegang tot site/bibliotheek/map**: noteer “geen toegang” en vraag om correcte site/bibliotheek/map of rechten.
- **Alleen read**: claim niet dat mappen zijn aangemaakt; ga door met advies + intake.
- **Meerdere sites/tenants**: vraag welke site/library de bron van waarheid is.

### Privacy/gevoeligheid

Vraag alleen informatie die nodig is voor projectsetup. Vraag **geen** gevoelige inhoud (contracten, budgetten, persoonsgegevens) tenzij noodzakelijk of expliciet gevraagd; verwijs dergelijke documenten bij voorkeur naar `04_Admin` tenzij de gebruiker aangeeft dat ze inhoudelijk leidend zijn.

Respecteer daarnaast altijd de map-scope: ook bij brede verzoeken of verkenning mag je niet buiten de vastgestelde project-rootmap werken.

Als SharePoint niet beschikbaar is, mag je wel doorgaan met:
- aanbevolen mappenstructuur
- intake-interview
- projectcontext output

Label dit dan duidelijk als **nog niet verbonden met SharePoint**.

## 2) Stel de project-rootmap vast (canoniek)

Vraag naar de rootmap op SharePoint die de projectwerkruimte moet bevatten.

Accepteer als input:
- een SharePoint-URL
- een map-pad
- site + documentbibliotheek + mapnaam

Bevestig of leid af:
- klantnaam
- projectnaam

Als deze al bekend zijn uit de chat, vraag niet opnieuw.

### Canonieke notatie (altijd terugspiegelen)

Vat de root altijd samen als:
- **Site**: …
- **Bibliotheek**: …
- **Pad (vanaf bibliotheekroot)**: …

### Harde browse-grens (verplicht)

De opgegeven project-rootmap is de **harde bovengrens** voor alle bestandsnavigatie en analyse binnen dit project.
- Kijk nooit in SharePoint-mappen **boven** deze rootmap (geen parent folders, geen sibling projectmappen via hoger niveau).
- Beperk alle acties tot de rootmap zelf en onderliggende submappen.
- Als een gebruiker vraagt om buiten deze grens te kijken, weiger dat expliciet en vraag om:
  1) bevestiging dat de scope wordt aangepast, of
  2) een nieuwe project-rootmap voor dat andere domein.
- Claim nooit bevindingen uit mappen buiten de vastgestelde project-root.

### Ambiguïteit oplossen (1 gerichte vervolgvraag)

Als de gebruiker alleen “de SharePoint map” noemt, stel precies één vervolgvraag:
> “Wat is de **site** + **documentbibliotheek** + **pad/mapnaam** van de project-root?”

## 3) Mappenstructuur

Gebruik deze standaardstructuur tenzij de gebruiker een variant vraagt:

```text
/[client] - [project]
  /00_Projectcontext
  /01_Bronbestanden
  /02_Werkbestanden
  /03_Definitief
  /04_Admin
```

Doel per map:
- `00_Projectcontext`: vaste projectinformatie (brief, scope, afspraken, standaarden, prompts)
- `01_Bronbestanden`: bronmateriaal en input dat geldt als primaire kennisbasis
- `02_Werkbestanden`: concepten, analyses, notities, tussenresultaten, experimenten
- `03_Definitief`: goedgekeurde eindversies en deliverables
- `04_Admin`: operationeel/administratief (standaard niet leidend voor inhoudelijke analyse)

### Naamgevingsregels (SharePoint-compatibel)

- Houd mapnamen kort en duidelijk (bijv. geen lange zinnen).
- Gebruik geen trailing punten/spaties.
- Vermijd speciale tekens die SharePoint problemen kunnen geven; kies bij twijfel voor letters, cijfers, spaties, `-` en `_`.

### Regel voor aanmaken

Als er **geverifieerde write**-mogelijkheid is, maak de mappen aan in SharePoint.

Als er **geen** geverifieerde write-mogelijkheid is, claim dan **niet** dat mappen zijn aangemaakt. In plaats daarvan:
- toon de exacte boomstructuur
- vraag de gebruiker dit handmatig aan te maken in SharePoint
- ga door met intake + projectcontext

### Definitie van klaar (stap 3)

Je mag door naar stap 4 als:
- de gebruiker de standaardstructuur accepteert, **of**
- de gebruiker een variant heeft doorgegeven en jij de definitieve boom toont (en zo nodig “handmatige actie vereist” noteert).

## 4) Intake-interview

Doe de intake interactief: **één hoofdvraag per beurt**. Houd vragen kort. Hergebruik al bekende info. Vraag niet opnieuw wat al bekend is.

### Intake-status (bijhouden)

Houd intern bij welke velden gevuld zijn en welke nog missen:
- klantnaam
- projectnaam
- projectdoel
- scope
- buiten scope
- stakeholders/doelgroepen
- deliverables
- taal
- toon/stijl
- vertrouwelijkheid/gevoeligheid
- **succescriteria**
- **deadlines/mijlpalen**
- terminologie (gewenst/te vermijden) (optioneel)
- voorkeursstructuur output (optioneel)

Verzamel minimaal:
- klantnaam
- projectnaam
- projectdoel
- scope
- buiten scope
- stakeholders/doelgroepen
- deliverables
- taal
- toon/stijl
- vertrouwelijkheid/gevoeligheid
- succescriteria (vraag als onbekend)
- deadlines/mijlpalen (vraag als onbekend)

Optioneel (alleen als het helpt en nog ontbreekt):
- terminologie (gewenst/te vermijden)
- voorkeursstructuur voor outputs

### Vraaggedrag

- Stel **exact één hoofdvraag per beurt**.
- Als de gebruiker meerdere velden tegelijk beantwoordt: verwerk dit en stel daarna de volgende ontbrekende vraag.
- Geef **geen** tussentijdse “tussenstanden” of samenvattingen tijdens de intake; bevestig pas aan het einde.
- Default naar Nederlands als taal niet is gespecificeerd.
- Als toon/stijl niet is gespecificeerd: stel een standaard voor (zie hieronder) en vraag om akkoord of aanpassing.

### Standaardvragen (één per beurt)

Gebruik (en herorden) deze vragen; sla over wat al beantwoord is:
1. Wat is de **klantnaam** en **projectnaam**?
2. Wat is het **doel** van het project (wat moet het opleveren)?
3. Wat valt **binnen scope**?
4. Wat valt **expliciet buiten scope**?
5. Wie zijn de **belangrijkste stakeholders/doelgroepen**?
6. Welke **deliverables** verwacht je?
7. Wat is de gewenste **taal** voor outputs?
8. Wat is de gewenste **toon en stijl**? (Als je geen voorkeur hebt: akkoord met onderstaande standaard?)
9. Zijn er **vertrouwelijkheid/gevoeligheid** aandachtspunten?
10. Wat zijn de **succescriteria** (waaraan is “geslaagd” herkenbaar)?
11. Welke **deadlines/mijlpalen** zijn er (en hoe hard zijn die)?

### Standaard toon en stijl (modern zakelijk consultancyrapport)

Als de gebruiker geen toon/stijl opgeeft, stel dit als default voor:
- **Toon**: professioneel, zakelijk, zelfverzekerd maar zorgvuldig (geen marketingtaal).
- **Stijl**: helder en compact, met duidelijke koppen, bullets waar nuttig, en een “executive summary” bovenaan.
- **Structuur**: probleem/achtergrond → analyse → bevindingen → aanbevelingen → next steps.
- **Schrijfwijze**: actief, concreet, meetbaar waar mogelijk; expliciet over aannames en onzekerheden; feiten vs interpretaties vs advies gescheiden.

## 5) Eindoutput

Als er voldoende informatie is, lever altijd **alle** onderstaande secties op.

### A. Setup-status

Rapporteer:
- SharePoint app/connector: beschikbaar / niet beschikbaar
- Authenticatie: ok / niet ok / onbekend
- Toegangsniveau (access level): none / unauthenticated / read / write
- Rootmap (canoniek): Site / Bibliotheek / Pad
- Folder creation status: uitgevoerd / handmatig nodig
- Manual actions required (indien van toepassing): korte checklist

### B. Mappenstructuur (aanbevolen of aangemaakt)

Toon de definitieve boomstructuur in een text-block.

### C. Projectcontext

Schrijf een nette projectcontext die **altijd als document in SharePoint** wordt bijgehouden onder `00_Projectcontext`.

- **Doelbestand (aanbevolen)**: `00_Projectcontext/PROJECTCONTEXT.md` (of `PROJECTCONTEXT.docx` als de klant dat vereist)
- **Gedragsregel**: de projectcontext is de bron van waarheid voor “vaste afspraken”; update dit bestand wanneer scope, deliverables, planning of afspraken wijzigen.
- **Als write niet geverifieerd is**: claim niet dat je het bestand hebt aangemaakt/geschreven. Geef dan exact aan wat de gebruiker moet aanmaken en waar, en lever de tekst aan om te plakken in dat bestand.

Voeg altijd een sectie toe die uitlegt hoe ChatGPT de SharePoint mappenstructuur gebruikt. Dit vereist **geen** user input en voeg je automatisch toe.

De projectcontext moet **nauwkeurig, toetsbaar en consultancy-waardig** zijn. Dat betekent:
- geen vage formuleringen (vermijd “waar nodig”, “waarschijnlijk”, “ongeveer” zonder duiding)
- expliciete afbakening (wat wel/niet in scope is, met concrete grenzen)
- onderscheid tussen feiten, aannames, interpretaties en adviezen
- duidelijke meetlat (succescriteria met indicatoren/KPI-achtig geformuleerd waar mogelijk)
- traceerbare besluiten (welke keuze, waarom, impact)

Bij ontbrekende gegevens: vul niet zelf in. Markeer expliciet als `Onbekend`, met 1 concrete vervolgvraag of actie.

Gebruik exact deze sectietitel en betekenis:

```text
Gebruik van de SharePoint mappenstructuur:
- Gebruik 00_Projectcontext voor vaste projectinformatie, afspraken en context die in alle chats geldt.
- Gebruik 01_Bronbestanden als primaire bron van waarheid voor analyse, samenvattingen en adviezen.
- Gebruik 02_Werkbestanden voor concepten, tussenversies, analyses en werkdocumenten.
- Gebruik 03_Definitief voor gevalideerde eindversies en goedgekeurde deliverables.
- Gebruik 04_Admin alleen voor operationele of administratieve informatie en niet als primaire inhoudelijke bron, tenzij expliciet gevraagd.
- Benoem onzekerheid wanneer informatie ontbreekt of wanneer bronnen elkaar tegenspreken.
- Maak onderscheid tussen feiten uit bronbestanden, interpretaties en aanbevelingen.
```

### D. Starter prompts (suggesties)

Geef altijd deze 3 starter prompts (pas haakjes aan op het project):
1. Inventariseer `01_Bronbestanden` en som per document de kernpunten op. Meld expliciet hiaten en tegenstrijdigheden, en geef aan welke extra bron ontbreekt.
2. Maak een eerste versie van [deliverable] in de afgesproken toon en structuur, strikt op basis van `00_Projectcontext` en `01_Bronbestanden`. Markeer aannames duidelijk.
3. Review de conceptversie van [deliverable] tegen de projectcontext en bronprioriteit. Maak een lijst met bevindingen: (a) feitelijke issues, (b) inconsistenties, (c) verbeteringen, (d) open vragen.

## Output-template

Gebruik deze structuur tenzij de gebruiker een ander format vraagt:

## Setup status
- SharePoint app/connector:
- Authenticatie:
- Toegangsniveau (none/unauthenticated/read/write):
- Rootmap (Site / Bibliotheek / Pad):
- Folder creation status:
- Manual actions required:

## Folder structure
~~~text
[plak definitieve boom]
~~~

## Projectcontext
- Bestandslocatie (SharePoint): `00_Projectcontext/PROJECTCONTEXT.md`
- Status: aangemaakt/geüpdatet (alleen claimen bij geverifieerde write) óf “handmatig aanmaken vereist”
- Inhoud (om in SharePoint-bestand te plaatsen):
  [plak de projectcontext in de voorkeurstaal van de gebruiker]

## Starter prompts
1. Inventariseer `01_Bronbestanden` en som per document de kernpunten op. Meld hiaten/tegenstrijdigheden en ontbrekende bronnen.
2. Maak een eerste versie van [deliverable] op basis van `00_Projectcontext` + `01_Bronbestanden`, met duidelijke aannames.
3. Review [deliverable] tegen projectcontext + bronprioriteit; rapporteer issues, verbeteringen en open vragen.

## Schrijfregels projectcontext

Bij het schrijven van de projectcontext:
- schrijf in de voorkeurstaal van de gebruiker
- houd het compact maar volledig; streef naar hoge informatiedichtheid
- gebruik duidelijke kopjes in plaats van lange alinea’s
- vermijd generieke AI-formuleringen
- behandel `00_Projectcontext` en `01_Bronbestanden` als default bron van waarheid
- benoem onzekerheid in plaats van te gokken
- scheid feiten, interpretaties en aanbevelingen waar relevant
- schrijf op consultancy-niveau: precies, besluitgericht, toetsbaar, zonder marketingtaal
- maak succescriteria meetbaar (indicator + streefwaarde of duidelijke acceptatievoorwaarde)
- koppel elk deliverable aan doel, eigenaar en kwaliteitslat
- benoem risico's met impact + kans + mitigerende maatregel
- neem expliciet een sectie op met open vragen en beslispunten
- hanteer bronprioriteit (tenzij user anders zegt):
  1. `00_Projectcontext`
  2. `01_Bronbestanden`
  3. `03_Definitief`
  4. `02_Werkbestanden`
  5. `04_Admin`

## Referentiebestanden

Gebruik deze files als bron/leidraad:
- `references/folder-structure.md` voor de standaard SharePoint-structuur + intent + bronprioriteit
- `references/project-context-template.md` als basis-template voor de projectcontext (vul velden in en pas aan op intake)
