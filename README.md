# DMP MANAGER PLUGIN TIL QGIS

### Plugin er oprindeligt udviklet af Bo Victor Thomsen, AestasGIS Danmark - og er pr. Q2 2026 overgået til Septima, som fremadrettet vedligeholder dette plugin. 


**Dette plugin er beregnet til QGIS ver. 3.22 eller senere.**

QGIS DMP Manager er et plugin, som giver brugeren mulighed for at downloade valgfri datalag fra DAI, Miljøportalen. Man kan herefter bearbejde data ligesom alle andre redigérbare lag i QGIS. Slutteligt kan de redigerede data kopieres tilbage til Miljøportalen.

Data placeres i en lokal datakilde i form en tabel i en database. Modtager-databasen kan være af typen PostgreSQL eller GeoPackage.

Download funktionen medfører, at der oprettes to tabeller for hvert data-lag der hentes fra DAI: Et ”redigeringslag”, som brugeren kan rette i; dvs. oprette nye, modificere eller slette poster. Samtidigt oprettes en ”referencelag” i samme database hvor referencelaget struktur- og indholdsmæssigt er fuldkommen ens med redigeringslaget (før brugeren begynder at rette data) - blot under et andet tabel-navn.

Redigeringslaget er et helt almindeligt data-lag i QGIS og du kan derfor benytte alle QGIS’s avancerede redigeringsfunktioner på dette lag. (Du må ikke rette i referencelaget, da man fjerner muligheden for plugin’et senere kan sammenligne dataindhold i redigeringslag og referencelag.)

Man kan downloade flere typer af data-lag fra DAI, således at disse lag findes samtidigt som redigerings/referencelag i QGIS. Dette giver mulighed for at tilrette data på tværs af forskellige data-lag fra DAI.

Når data tilretning er færdiggjort i redigeringslaget kan brugeren sammenligne data mellem redigeringslag og referencelag vha. en funktion i plugin-et. Funktionen finder alle forskelle mellem redigerings- og referencelag (oprettelser, rettelser og sletninger) og viser disse som lag - hhv. ”Oprettet”, ”Rettet” eller ”Slettet” i QGIS kortvinduet. Brugeren kan herefter kontrollere de enkelte modificerede elementer og efter kontrol ”skubbe” (uploade) modifikationerne tilbage til DAI.

Plugin-et har mulighed for at gemme en tematisering (symbolisering) for hver DAI lagtype, således at samme tematisering vil blive benytte ved senere downloads af data-lag fra DAI.

Plugin-et har slutteligt en række administrative funktioner, f.eks. at kunne opstarte QGIS geometri-tjekker på det valgte lag.

Plugin-et kan benyttes til både demo-miljøet og produktionsmiljøet hos DAI, Miljøportalen.

Vejledninger
Download af alle filer i repository som én zip-fil udføres ved at trykke på den grønne knap med teksten "Code" i hovedskærmbilledet for repository (https://github.com/septima/DMP-MANAGER-DISTRIBUTION) og vælge "Download ZIP" i undermenuen.

Der findes to vejledninger til plugin: "Installationvejledning.pdf", som beskriver hvorledes systemet skal installeres. Og "Brugervejledning.pdf", som beskriver den daglige brug af systemet.


### Rettigheder, licens o.a.:
Dette system et QGIS plugin dvs. en integreret udvidelse af QGIS. Dette betyder, at koden til det udførte arbejde er underlagt samme licens som selve QGIS: GPL- licensen.

Kort fortalt medfører denne licens, at du som modtager af systemet:

Har fået den fulde programtekst (kildekoden) udleveret sammen med plugin-systemet.

Kan selv tilrette eller videreudvikle kildekoden uden tilladelse fra - eller kompensation til leverandøren.

Kan videreformidle plugin-systemet og kildekode til tredjepart uden tilladelse fra - eller kompensation til leverandøren.

Eventuelle ændringer og tilføjelser til kildekoden bliver automatisk tvangsunderlagt samme GPL–licens som originalen. Og ved videreformidling af programsystem og kildekode til tredjepart forbliver disse under GPL–licensen. Dvs. der gælder samme licensforhold mellem dig og tredjepart, som der gælder mellem den oprindelige udvikler og dig.

Man kan kort sige, at du har fuld råderet til plugin-programmet og kildekode. Men det er ikke muligt at ændre på licensen og konsekvenserne af samme; ej heller på de programdele, som du evt. selv har videreudviklet.

## Seneste rettelser
For overblik over seneste rettelser til plugin'et - se https://github.com/septima/DMP-MANAGER-DISTRIBUTION/changelog.txt


## Rapportering af fejl:
Alle fejlrapporter, forslag til forbedringer osv. bør først og fremmest oprettes som "issues" i dette repository (https://github.com/septima/DMP-MANAGER-DISTRIBUTION/issues). Hertil bruges tag'et 'Bug*

## Forslag til ny funktionalitet 
Ønsker og forslag til ny funktionalitet bedes ligeledes oprettes som issue - i dette tilfælde med tag 'improvement'.


Vær opmærksom på at MiljøPortalen begrænser download antal til maksimalt 10.000 poster. Det påvirker bl.a. "Beskyttede Sten og Jorddiger 2022", da der landsdækkende er flere diger end 10.000. DMP Manager har en facilitet til kun at downloade data indenfor kortvinduet. Denne kan bruges til at garantere, at alle data indenfor et geografisk afgrænset område kommer med.

Plugin er blevet installeret og testet mod "demo" udgave af Miljøportalen i QGIS versionerne 3.40, 3.42 og 3.44. og 4.00 Plugin fungerer muligvis på tidligere udgaver af QGIS, men er dette er ikke afprøvet.

Når DMP Manager geninstalleres, bliver opsætningen til database nulstillet, så husk at indstille DMP Manager til at bruge jeres Postgres database / GeoPackage igen.

