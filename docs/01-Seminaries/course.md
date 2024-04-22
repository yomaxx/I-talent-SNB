# Quality Engineering
<img src="https://raw.githubusercontent.com/yomaxx/I-talent-SNB/main/docs/01-Seminaries/src/Capgemini_Logo.png" alt="logo capgemini" width="500"/><br>


**Gegeven door**: Capgemini<br>
**Datum**: 7/03/2023<br>
**Locatie**: Hogeschool PXL
## Inhoud
Het seminarie van Capgemini ging over quality engineering binnen de SDLC (Software Development Lifecycle). De inhoud van de seminarie was gefocust op waarom quality engineering noodzakelijk is, hoe het mogelijk moet zijn om slechte quality deliverance te vermijden.


# Forensics
<img src="https://raw.githubusercontent.com/yomaxx/I-talent-SNB/main/docs/01-Seminaries/src/Logo-pwc.png" alt="logo PWC" width="500"/>

**Gegeven door**: PWC<br>
**Datum**: 21/03/2023<br>
**Locatie**: Hogeschool PXL

## Inhoud
Door middel van een VM die kwam met een aantal tools voor forensics toe doen. Hier zagen we bijvoorbeeld een programma "jiggly mouse" wat verdacht was.


# Multi-cloud
<img src="https://raw.githubusercontent.com/yomaxx/I-talent-SNB/main/docs/01-Seminaries/src/gluo_logo.png" alt="logo gluo" width="500"/>

**Gegeven door**: Gluo<br>
**Datum**: 18/04/2023<br>
**Locatie**: Hogeschool PXL

## inhoud
Dit seminarie stond in teken van het de verschillende manieren om een applicatie op te zetten en de infrastructuur te beheren. Van het manueel opzetten van een docker image tot het automatisch deployen van een multi-cloud setup. Zo konden we de lessen automatisatie eens in de praktijk zien.

# Meraki (Cloud) + converged (Cloud + on prem)
<img src="https://raw.githubusercontent.com/yomaxx/I-talent-SNB/main/docs/01-Seminaries/src/logo_cisco.png" alt="logo cisco" width="500"/>

**Gegeven door**: Cisco<br>
**Datum**: 08/11/2023<br>
**Locatie**: Hogeschool PXL

## inhoud
Hier kregen we eerst wat uitleg over het Meraki platform van cisco waar we daarna mee aan de slag mochten. We kregen een aantal oefeningen met de API en met de website om zo verschillende aspecten in te stellen en op te vragen.


# Cyber security operations in the real world
<img src="https://raw.githubusercontent.com/yomaxx/I-talent-SNB/main/docs/01-Seminaries/src/logo_secwise.png" alt="logo secwise" width="500"/>

**Gegeven door**: Secwise<br>
**Datum**: 06/12/2023<br>
**Locatie**: Hogeschool PXL

## inhoud
Hier hebben we wat `blue team` uitleg en een blik in de wereld van incident response gekregen. We kregen te zien hoe een security incident onderzocht werd en hoe dit in de toekomst vermeden kon worden.


# SAP: AI en process automation
<img src="https://raw.githubusercontent.com/yomaxx/I-talent-SNB/main/docs/01-Seminaries/src/logo_thevaluechain.png" alt="logo the Value Chain" width="500"/>

**Gegeven door**: TheValueChain<br>
**Datum**: 13/12/2023<br>
**Locatie**: Hogeschool PXL 

## inhoud
Seminarie over SAP en process automation. SAP is een resource planning softwarepakket wat bedrijven helpt op efficiënter te werken. Hier kregen we uitleg over en enkele voorbeelden van oplossingen die ze gevonden hebben voor klanten.


# Digital forensics
<img src="https://raw.githubusercontent.com/yomaxx/I-talent-SNB/main/docs/01-Seminaries/src/logo_politie.jpg" alt="logo the Value Chain" width="500"/>

**Gegeven door**: Politie<br>
**Datum**: 10/01/2024<br>
**Locatie**: Hogeschool PXL

## inhoud
In deze seminarie hebben we geleerd hoe de politie te werk gaat bij een digitale analyse van een systeem.<br>
Dit process gebeurt in 3 stappen:
- acquisition: Halen van de digitale media.
- analyse: Heeft 3 categorieen
    - identificatie: Waar zijn er artifacts
    - analyse: File systeem bekijken
    - Interpretatie
- Presentatie: De resultaten delen.

Voor we beginnen met de analyse moet de inhoud van de harde schijf gecloned worden. Je mag nooit op de drive zelf werken. Dan kun je achteraf de vraag krijgen, heb je dat zelf niet op de drive gezet? Er wordt gebruik gemaakt van hashes om te controleren dat er niks is veranderd op de originele schijf.
Om dit te voorkomen wordt de drive ook best met een `writeblocker` op zowel hard als software niveau uitgevoerd. Zo kun je nooit per ongeluk iets naar de drive toeschrijven en het onderzoek beinvloeden. Verder is het ook niet handig dat als de schijf nog 400GB vrije opslag heeft om dit mee te kopiëren. Tools zoals dd geven de optie om alleen de data te kopiëren en niet de lege plekken.

Eerst hebben we wat commando's geleerd om informatie over een drive te verkrijgen.
```bash
lsusb -v | grep -i -a3 kingston
hdparm /dev/sda
lsblk
lssci # Geeft meer info over de gebruikte drive, niet de partities.

# ls in een disk
fls -o 1026048 /dev/sdb
```

Hierna wat oefeningen met een usb stick (of vhd in virtualbox).
Via fdisk hier partities opgemaakt. Hierna een bestandje op de drive aangemaakt en deze weer verwijderd. Bestanden die je verwijdert worden niet echt verwijderd. Je schijf zet deze ruimte gewoon als 'beschikbaar' en als je nog een bestandje aanmaakt kan deze over de vorige worden heen geschreven. Het is dus mogelijk om recent verwijderdere bestanden vaak helemaal intact terug te vinden of nog een groot deel hiervan.<br>
Het beste om dit tegen te gaan is de schijf `schredden`. Dit wil zeggen een patroon (meestal allemaal 0en) meerdere keren over heel de schijf te schrijven. 

Met tools zoals `fls`, `icat` en `tsk_recover` is het mogelijk om recent verwijderde bestanden terug te halen.

loop devices worden gebruikt als je geen open partities meer hebt maar toch partities wilt gebruiken. Je kunt zo een `file` aanmaken en dan een loop device met deze file.

Hierna hebben we geleerd hoe je foto's kunt onderzoeken met `file` en `display`. Hierna hebben we verborgen texten uit de foto's gehaald. Fijn om weer even de security lessen op te frissen.
