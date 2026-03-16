
![header](img/header.png)
</br>
</br>

# Brugervejledning til QGIS DMP Manager – ET QGIS baseret plugin til håndtering og redigering af data fra Miljøportalen

## Indledning

QGIS DMP Manager er et plugin, som giver brugeren mulighed for at downloade valgfri datalag fra DAI, Miljøportalen. Data placeres i en lokal database baseret datakilde i form en tabel. Modtager databasen kan være af typen PostgreSQL eller GeoPackage.  Download funktionen medfører, at der oprettes to tabeller for hvert data-lag, som hentes fra DAI: Et ”redigeringslag”, som brugeren kan rette i, dvs. oprette nye samt modificere eller slette eksisterende poster. Samtidigt oprettes en ”referencelag” i samme database hvor referencelaget struktur- og datamæssigt er fuldkommen ens med redigeringslaget (før brugeren begynder at rette data) - blot under et andet tabelnavn.
Redigeringslaget er et helt almindeligt data-lag i QGIS og du kan derfor benytte alle QGIS’s avancerede redigeringsfunktioner på dette lag. (Du må ikke rette i referencelaget, da man fjerner muligheden for plugin-et senere kan sammenligne dataindhold i redigeringslag og referencelag.)
Man kan downloade flere typer af data-lag fra DAI, således at disse lag findes samtidigt som redigerings/referencelag i QGIS. Dette giver mulighed for at tilrette data på tværs af forskellige data-lag fra DAI. 
Når tilretning er færdiggjort i redigeringslaget kan brugeren sammenligne data mellem redigeringslag og referencelag vha. en funktion i plugin-et. Funktionen finder alle forskelle redigerings- og referencelag (oprettelser, rettelser og sletninger) og viser disse som lag, hhv. ”Oprettet”, ”Rettet” eller ”Slettet” i QGIS kortvinduet. Brugeren kan herefter kontrollere de enkelte modificerede elementer og ”skubbe” (uploade) modifikationerne tilbage til DAI.
Plugin-et har mulighed for at gemme en tematisering (symbolisering) for hver DAI lagtype, således at samme tematisering vil blive benytte ved senere downloads af data-lag fra DAI. 
Plugin-et har slutteligt en række administrative funktioner, f.eks. kunne opstarte QGIS geometri-tjekker på det valgte lag.
Plugin-et kan benyttes til både demo-miljøet og produktionsmiljøet hos DAI, Miljøportalen.    
NB! Denne vejledning er skrevet til den engelske udgave af DMP Manager. 
Men brugervejledningen indeholder de danske oversættelser i parenteser () umiddelbart efter de engelske betegnelser.

## Installation

**Dette plugin fungerer kun på QGIS ver. 3.22 eller senere.**

Installation af plugin plus hjælpeprogram er beskrevet i en separat vejledning, som findes i samme GitHub repository: https://github.com/septima/DMP-MANAGER-DISTRIBUTION

## Opstart af Plugin

DMP Manager kan startes ved at klikke på menupunkt ”Web” -> ”DMP Manager” -> ”Dmp Manager”. Eller at ved at klikke på følgende ikon:

![header](img/icon.png)

Herefter vises Brugerdialogen for DMP Manager – normalt placeret i højre side af QGIS’s hoved skærmbillede:

![header](img/dialog.png)

## Initiel opsætning af DMP Manager.

Før du kan bruge DMP Manager skal du foretage nogle få opsætninger i faneblad ”Administration”:

![header](img/administration.png)

* I afsnit ”Administration” kan du sætte en række informationer.

    * I valgfeltet CVR number (CVR nummer) vælges CVR nummeret for en bestemt virksomhed / institution ved at vælge firmaets / institutionens navn . Dette CVR nummer kan benyttes som en filterværdi, således man kun downloader objekter fra DMP med det valgte CVR Nummer.
    NB! Nummeret vil også automatisk tilføjes alle nyoprettede objekter lokalt i QGIS. Men ved upload af data vil Miljøportalens datasystemer automatisk indsætte et (evt. andet) CVR nummer værdi fastlagt ud fra brugerens brugernavn og tilhørsforhold ved login til Miljøportalen. Dette gælder for størstedelen af  de forskellige datalag. 
    * Ved tryk på knap: Set layer choice in tab ”fetch” as preferred (Sæt datatype valg som foretrukkent) vil plugin finde hvilke lagtype, som er valgt til download i faneblad Fetch (Hent data) og sørge for, at dette lag er valgt på forhånd ved senere opstarter af plugin.
◦	Ved tryk på knap: Reset administrative data from DMP (Genindlæs administrative oplysninger fra DMP) udfører plugin en genindlæsning af en række administrative oplysninger fra Miljøportalen. Plugin’et er fra start installeret med et sæt af disse oplysninger, så det er ikke umiddelbart nødvendigt at udføre funktionen.  Men Miljøportalen vil løbende ændre på dette datasæt, så hvis man begynder at opleve driftsfejl kan man muligvis udbedre disse fejl ved at trykke på knappen.

* Under afsnit Placement of edit and reference data (Placering af redigerings- og referencelag) skal du vha. drop-down boks “Database” vælge hvilken database du ønsker at DAI data til redigering skal placeres i. Drop-down listen viser alle database dataforbindelser der er opsat i QGIS under ”Open data source manager  (CTRL-L)”  (”Åbn Datakilde-håndtering  (CTRL-L)”). Hvis din database ikke findes i listen, skal du først oprette dataforbindelsen vha. førnavnte standard QGIS funktion.
Efter valg af database udfyldes drop-down boks Schema automatisk med alle tilgængelige schemaer i den valgte database. Hvis databasetypen ikke benytter sig af schema begrebet, forbliver drop-down listen tom og vil være inaktiv.
    * Hvis du ønsker at lave et nyt schema til dine data i databasen kan du trykke på den smalle knap umiddelbart til højre for drop-down boks Schema. Denne vil give dig mulighed for at lave et nyt, tomt schema til dine data (Hvis du har rettigheder til dette i den valgte database).
    * I tekst-felt Primary key name (Navn for primær nøgle) kan du endvidere indtaste navnet på det felt (kolonne) i redigerings og referencelag, som vil komme til at indeholde den for QGIS interne unikke nøgle (primary key). Navnet er forskelligt fra database system til databasesystem, men vil normalt sættes til id for Postgres database kilder og fid for GeoPackage datafiler. 
    * I tekst-felt Primary key quote (Tekst adskiller) kan du indtaste karakteren for en tekstafgrænser for den valgte databasetype hvis din primary key er af typen tekst. Tekstafgrænser er normalt en apostrof (’). Ellers skal du efterlade feltet tomt.
Det er yderst sjældent at feltet skal være andet end tomt.

* I afsnit Environment (Data miljø)  kan du vælge om du skal arbejde mod test Miljøportalens demo miljø eller produktions miljø.
Ved skift af data miljø – fra Demo til Produktion eller vice-versa – Vil du blive advaret om, at QGIS skal genstartes føres skiftet fungerer. Du risikerer endvidere at skulle vente op mod en time på at en evt. allerede gennemført logon timer ud, før du kan logge på det nye data miljø. 
    * Hvis du fortsætter med skiftet, bliver data-miljø skiftet permanent og QGIS bliver lukket ned. Vherefter vil QGIS benytte det valgte data-miljø
(Note: Grunden til forsinkelsen på en time er, at det ikke har været muligt at få ”logoff” til Miljøportalen til at fungere inde fra plugin’et. Så  man må vente på, at Milportalens automatiske logoff foretages efter en time) 

Når alle relevante parametre i fanebladet er værdisat, trykkes der på knap Save as default (Gem opsætninger). Dette vil gemme alle valg og indtastninger som den nye opsætning. 
Hvis man har lavet en række (evt. fejlagtige) valg eller indtastninger kan man genindlæse de oprindelige oplysninger for plugin’et ved at trykke på knap Reset to default (Genindlæs opsætninger). 
NB! Når man først har trykket på Save as default (Gem opsætninger) knappen kan man ikke genindlæse de oprindelige oplysninger.
 
## Dagligt arbejde med DMP Manager  

Det daglige arbejde med DMP Manager følger – i store træk – følgende cyklus.
1.	Bruger indlæser et eller flere lag fra Miljøportalen. Disse lag indsættes automatisk som tabeller i databasen og tabellerne vises automatisk i QGIS’s kortvindue.

![header](img/main.png)

2.	Bruger redigerer de indlæste data med QGIS’s indbyggede redigeringsværktøjer. Redigering- sessionen kan strække sig over flere dage og/eller nedlukninger af QGIS ved at gemme opsætningen som et QGIS-projekt og indlæse dette projekt ved genopstart af QGIS.

3.	Når bruger er klar til at skubbe rettelser tilbage til Miljøportalen benyttes DMP Managers værktøjer til at kontrollere / sammenligne redigerede og oprindelige data og derefter skrives data til Miljøportalen eller forkastes én efter én. 

![header](img/flow.png)

Workflow gentages med andre / nye områder / temaer  

Ovenstående workflow understøttes af 2 faneblade i DMP Manager:

### Faneblad Fetch (Hent data)

Faneblad Fetch (Hent data) benyttes til at downloade data fra Miljøportalen

For at downloade data fra Miljøportalen skal man først foretage et login til portalen. Det gøres ved at trykke på knap Login to DMP (Login til Miljøportalen). 
QGIS har i mellemtiden modtaget de nødvendige oplysninger til kommunikation med Miljøportalen for at hente og opdatere data.
Resultatet kan aflæses ved at tekstfelterne Acces token (Adgangs nøgle) og Token timeout (Nøgle udløber) udfyldes med information fra Miljøportalen.
NB! Disse felter kan redigeres, men dette gøres kun i forbindelse med test af nye opsætninger (Så lad være med det!)
NBB! Det er faktisk ikke strengt nødvendigt at trykke på knap Login to DMP (Login til Miljøportalen) - Hvis du begynder at hente data uden at have foretaget et login, vil DMP Manager detektere denne situation, og automatisk starte en login-proces før download fa data fra Miljøportalen gennemføres. 
Samme forhold gør sig også gældende, hvis login bliver ugyldigt pga. tidsudløb. 

#### Hente data fra Miljøportalen

For at hente data fra Miljøportalen bruges afsnit Fetch layer from DMP (Hent lag fra Miljøportalen) i faneblad Fetch (Hent data). Øverst i dette afsnit findes der en drop-down liste med kode-nr. og navn på alle de lag, som kan hentes. 
Vha. denne drop-down liste vælger hvilket lag, du ønsker at hente.
Dernæst kan du sætte ”flueben” i felt Use mapper extent af datafilter (Benyt kortvindue som datafilter) hvis du kun ønsker at hente data i den valgte lagtype, som ligger indenfor det kortudsnit der pt. vises i QGIS. Hvis du derimod ønsker data fra hele landet efterlades boksen uden flueben.
Dernæst sættes der flueben i boks Overwrite existing DMP layer (Overskriv eksisterende DMP lag), hvis du ønsker at overskrive evt. eksisterende data i databasen fra tidligere download sessioner. Hvis der ikke er sat flueben i boksen og databasen indeholder eksisterende data i den relevante tabel, vises en fejlmeddelelse og der hentes ikke nye data fra Miljøportalen.   
Slutteligt kan der sættes flueben i felt Use CVR number af filter (Brug CVR nummer som filter) hvis du kun vil hente data fra Miljøportalen med ét bestemt CVR nummer. Dette nummer skal først du indtaste i faneblad Administration  (Administration) , felt CVR Number (CVR nummer).
Selve hentning af data igangsættes ved tryk på knap Download (Hent data). 
NB! Det er ikke kun data fra selve laget, som hentes. Det er også opslagsdata, som indlæses som separate tabeller og vises i QGIS lagviser.
Hele processen med at hente data kan gentages med et vilkårligt antal forskellige data-lag fra Miljøportalen således mange forskellige lag kan redigeres i samme QGIS-projekt.

### Faneblad Checks (Data tjek)

Faneblad Checks (Data tjek) benyttes til kontrol af modificerede data samt upload af disse data til Miljøportalen. 

![header](img/check.png)

For at udføre en kontrol af redigerede data (som også er en forberedelse til at kunne uploade modificerede data til Miljøportalen vælges først hvilket lag, som skal kontrolleres ved hjælp af drop-down boks i afsnit Choose layer (Vælg lag)
NB! For at alle modifikationer bliver vist ved kontrollen skal man først have gemt sine rettelser i databasen ved at hoppe ud af redigerings modus i QGIS (”Blyanten” skal være ”grået ud” for redigeringslaget)
Dernæst trykkes der på knap Compare (Sammenlign) i afsnit Compare edit and reference layer (Sammenlign redigerings- og referencelag).
Dette starter en proces i plugin, som finder alle nyindsatte elementer, alle rettede elementer og alle slettede elementer i det valgte redigeringslag. Disse oplysninger viser 2 steder:

1.	I QGIS kortvinduet som 3 nye lag: ”Oprettede elementer”, ”Slettede elementer” og ”Rettede elementer” i laggruppe ”Miljøportalen” -> ”rettede data”. 

2.	I faneblad Checks (Hent data), afsnit Compare edit and reference layer (Sammenlign redigerings- og referencelag) udfyldes der en 3-grenet liste med de samme data.

![header](img/check2.png)

Ved udfoldning af listen kan man undersøge de enkelte modificerede data. 
Ved højreklik på de enkelte elementer vises en under-menu, som giver dig mulighed for at foretage en række handlinger på elementet.

![header](img/compare.png)

* Cancel modification (Tilbagefør rettelse):  Det valgte element føres tilbage til sin oprindelige tilstand: Slettede elementer genindsættes, Rettede elementer føres tilbage til sine oprindelige værdier/geometri og oprettede elementer fjernes.

* Upload modification (Skub rettelse til DMP): Modifikation
en af det enkelte element skubbes tilbage til Miljøportalen. Hvis modifikationen godkendes af Miljøportalen tilpasses både redigeringslag og reference-lag således at elementet får samme udseende/værdisætning, som elementet nu har i Miljøportalen. 
Hvis upload til Miljøportalen gennemføres uden fejl bliver det enkelte element i listen gjort inaktiv, så der ikke kan foretages flere handlinger på det.

* Show DMP error (Vis sidste DMP fejl): Viser sidste fejlmeddelelse fra Miljøportalen, hvis skrivning af elementet til Miljøportalen fejlede.

* Zoom/pan to feature (Zoom / panorér til element): Kortvindue zoomes / flyttes, således at det relevante element vises tydeligt i kortvinduet

Ved at bruge ovenstående funktioner på hvert enkelt modificeret element kan alle modificerede elementer  skrives til Miljøportalen.

Der er tre inaktive knapper placeret umiddelbart over sammenligningstræet. Disse bliver aktive, når der gennemføres en sammenligning. Knapperne benyttes til ved masse opdatering af ændrede data til Miljøportalen.  
Ud for hver objekt id i sammenligningstræet er der et afkrydsningsfelt, som bestemmer, om et objekt omfattes af en masse opdatering. Dette felt kan sættes manuelt. 

Alternativt kan man afkrydse samtlige poster i sammenlignings træet ved at trykke på knap  Check All (Sæt alle krydser). Alle satte krydser kan fjernes ved at trykke på knap  Uncheck All (Fjern alle krydser).
Slutteligt kan selve masse upload af rettelser til Miljøportalen gennemføres ved at trykke på knap  Upload Checked (Skub alle afkrydsede) .  Masseupload svarer til, at man for hver afkrydset objekt havde højreklikket på objektid og valgt funktion Upload modification (Skub rettelse til DMP)

Ved tryk på knap Clear (Nulstil) i afsnit Compare edit and reference layer  (Sammenlign redigerings- og referencelag) fjernes kontrol lag fra kortvinduet og listevinduet nulstilles. 

Afsnit Actions (Aktioner) indeholder 2 trykknapper, som igangsætter forskellige funktioner
* Geometry check (Geometri tjekt)
Opstarter QGIS’s indbyggede geometritjekker på det valgte lag under Choose layer (Vælg lag)
* Multipart to singlepart (Multipart til singlepart)
Opstarter en funktion, som gennemløber selekterede objekter i det valgte lag under Choose layer (Vælg lag). Hvert undersøgt objekt, som består af flere delobjekter vil blive konverteret til 2 eller flere objekter med samme attributværdi som originalen. Det første nye objekt har samme objekt-id og version-id, som det originale objekt.

Der er to krav for at bruge denne funktion
1.	Laget må ikke være i redigerings modus, dvs. med ”blyanten” aktiveret.
2.	Der skal være etableret en selektion af objekter, der skal behandles. Selektionen kan laves via alle selektions metoder i QGIS.  

## Automatisk tematisering af hentede lag fra Miljøportalen

Plugin-et har mulighed for at automatisk tematisere hentede lag. Dette gøres på følgende måde:
1.	Hent et lag fra Miljøportalen. Første gang du henter det, vil det optræde med en simpel farvelægning valgt vilkårligt ag QGIS

2.	Du tematiserer så kort-laget vha. den indbyggede symbologi-funktion i QGIS. Du kan bruge alle faciliteter i denne, inkl. opsætning af felter med lookup funktioner osv.

![header](img/style.png)

3.	Herefter går du ind i faneblad Administration (Administration), afsnit Save layer as default (Gem lag symbologi som standard), hvor du i Layer Name (Lag navn) vælger laget, du vil gemme symbologi for og slutteligt trykker på Save (Gem).

Herefter vil det valgte lag automatisk blive tematiseret, hver gang du downnloader dette lag fra Miljøportalen.
