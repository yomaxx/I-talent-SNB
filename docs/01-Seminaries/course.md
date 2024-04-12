# Capgemini: Quality Engineering

# Seminarie PWC

# Gluo: Multi-cloud
Dit seminarie stond in teken van het de verschillende manieren om een applicatie op te zetten en de infrastructuur te beheren. Van het manueel opzetten van een docker iamage tot het automatisch deployen van een multi-cloud setup. Zo konden we de lessen automatisatie eens in de praktijk zien.

# Inuits: Nomad
Deze seminarie, gegeven door Inuits, ging over de container orchestrator Nomad.  
Nomad is een alternatief of extensie voor kubernetes. Het kan ingezet worden om containerized of legacy applicaties te deployen en beheren.  
Nomad wil het beheren en opzetten van clusters makkelijk maken. Hierdoor is het minder uitgebreid dan de wel bekende kubernetes orchestrator.  

een kleine vergelijking tussen nomad en kubernetes:
| feature  | Kubernetes  | Nomad  |
|---|---|---|
| use case  | container orchestration op grote schaal  | general-purpose orchestrator voor diverse workloads  |
| community  | groot  | groeiend, kleiner als kubernetes  |
| complexiteit  | Heel complex om mee te beginnen  | Makkelijker te leren.  |

Eerst leerden we een paar commando's om logs op te vragen en het ip van een hostname te vinden.

```bash
# Geeft logs van laatste 5 min
journalctl --since "5m ago"

# geeft ip terug
dig +short pxl-nomad8.workshop.inuits.dev
> 167.90.226.122
```

Binnen nomad heb je servers en clients. Servers zijn verantwoordelijk voor het accepteren van jobs, managen van clients en de jobs plaatsen op een client.  
Clients daarintegen zijn verantwoordelijk voor het uitvoeren van de jobs.  
Een job binnen Nomad wordt gezien als een container die je opstart.

We hebben hierna een aantal opdrachten gekregen om op een Nomad instance uit te voeren.  
Dit begon met het aantal instances van een webserver te verhogen van 1 naar 3. Deze job wordt dan op meerdere clients, indien mogenlijk, uitgevoer en kan zo meer traffic aan en blijft ook werken als die client uitvalt.

<img src="./src/Nomad_instances.png" alt="image succesvol verhogen instances van een webserver" width="1000"/>

Hierna hebben we geleerd dat je bij de metadata van een job kunt specifieren op welke client deze moet runnen. Anders zal deze bij elke boot een andere toegewezen krijgen.
Dit kan soms handig zijn als een specifieke job op een client moet runnen die toegang heeft tot een bepaald netwerk of resources. Denk aan zwaardere calculaties die best op een GPU plaatsvinden. Of een host die is aangesloten op een antenne die je gebruikt om vluchten bij te houden.

Na een aantal opdrachten rond jobs hebben we de tool `grafana` bekeken. Deze wordt gebruikt voor dashboards met allerlei informatie over de Nomad installatie en jobs.

## reflectieverslag
Dit seminarie was zeer interesant om een andere container orchestration tool te zien dan we in de opleiding doen. Het kan zeker nooit kwaad om je bewust te zijn van andere tools of opties dan degene die je gebruikt en bekend mee bent. Het was heel fijn dat dit een hands on seminarie was omdat dit de beste manier is om de mogelijkheden van een tool te leren en zien.  

# Cisco: Meraki (Cloud) + converged (Cloud + on prem)
Hier kregen we eerst wat uitleg over het Meraki platform van cisco waar we daarna mee aan de slag mochten. We kregen een aantal oefeingen met de API en met de website om zo verschillende aspecten in te stellen en op te vragen.

# Secwise: Cyber security operations in the real world
Hier hebben we wat `blue team` uitleg en een blik in de wereld van incident response gekregen. We kregen te zien hoe een security incident onderzocht werd en hoe dit in de toekomst vermeden kon worden.

# TheValueChain: SAP: AI en process automation
Seminarie over SAP en process automation. SAP is een resource planning software pakket wat bedrijven helpt op efficienter te werken. Hier kregen we uitleg over en enkele voorbeelden van oplossingen die ze gevonden hebben voor klanten.

# Politie: Digital forensics'
In deze seminarie hebben we geleerd hoe de politie te werk gaat bij een digitale analyse van een systeem.  
Dit process gebeurt in 3 stappen:
- acquisition: Halen van de digitale media.
- analyse: Heeft 3 categorieen
    - identificatie: Waar zijn er artifacts
    - analyse: File systeem bekijken
    - Interpretatie
- Presentatie: De resultaten delen.

Voor we beginnen met de analyse moet de inhoud van de harde schijf gecloned worden. Je mag nooit op de drive zelf werken. Dan kun je achteraf de vraag krijgen, heb je dat zelf niet op de drive gezet? Er wordt gebruik gemaakt van hashes om te controleren dat er niks is veranderd op de originele schijf.
Om dit te voorkomen wordt de drive ook best met een `writeblocker` op zowel hard als software niveau uitgevoerd. Zo kun je nooit perongeluk iets naar de drive toeschrijven en het onderzoek beinvloeden. Verder is het ook niet handig dat als de schijf nog 400GB vrije opslag heeft om dit mee te kopieren. Tools zoals dd geven de optie om alleen de data te kopieren en niet de lege plekken.

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
Via fdisk hier partities opgemaakt. Hierna een bestandje op de drive aangemaakt en deze weer verwijderd. Bestanden die je verwijdert worden niet echt verwijderd. Je schijf zet deze ruimte gewoon als 'beschikbaar' en als je nog een bestandje aanmaakt kan deze over de vorige worden heen geschreven. Het is dus mogenlijk om recent verwijderdere bestanden vaak helemaal intact terug te vinden of nog een groot deel hiervan.  
Het beste om dit tegen te gaan is de schijf `schredden`. Dit wil zeggen een patroon (meestal allemaal 0en) meerdere keren over heel de schijf te schrijven. 

Met tools zoals `fls`, `icat` en `tsk_recover` is het mogenlijk om recent verwijderde bestanden terug te halen.

loop devices worden gebruikt als je geen open partities meer hebt maar toch partities wilt gebruiken. Je kunt zo een `file` aanmaken en dan een loop device met deze file.

Hierna hebben we geleerd hoe je foto's kunt onderzoeken met `file` en `display`. Hierna hebben we verborgen texten uit de foto's gehaald. Fijn om weer even de security lessen op te frissen.
