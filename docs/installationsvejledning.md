
![header](img/header.png)
</br>
</br>

# Installationsvejledning til QGIS DMP Manager – Et QGIS baseret plugin til håndtering og redigering af data fra Miljøportalen

QGIS DMP Manager er et plugin, som giver brugeren mulighed for at downloade valgfri datalag fra DAI, Miljøportalen. Data placeres i en lokal database baseret datakilde i form en tabel. Modtager databasen kan være af typen PostgreSQL eller GeoPackage.  Download funktionen medfører, at der oprettes to tabeller for hvert data-lag, som hentes fra DAI: Et ”redigeringslag”, som brugeren kan rette i, dvs. oprette nye samt modificere eller slette eksisterende poster. Samtidigt oprettes en ”referencelag” i samme database hvor referencelaget struktur- og datamæssigt er fuldkommen ens med redigeringslaget (før brugeren begynder at rette data) - blot under et andet tabelnavn.

Redigeringslaget er et helt almindeligt data-lag i QGIS og du kan derfor benytte alle QGIS’s avancerede redigeringsfunktioner på dette lag. (Du må ikke rette i referencelaget, da man fjerner muligheden for plugin-et senere kan sammenligne dataindhold i redigeringslag og referencelag.)
Man kan downloade flere typer af data-lag fra DAI, således at disse lag findes samtidigt som redigerings/referencelag i QGIS. Dette giver mulighed for at tilrette data på tværs af forskellige data-lag fra DAI. 
Når tilretning er færdiggjort i redigeringslaget kan brugeren sammenligne data mellem redigeringslag og referencelag vha. en funktion i plugin-et. Funktionen finder alle forskelle redigerings- og referencelag (oprettelser, rettelser og sletninger) og viser disse som lag, hhv. ”Oprettet”, ”Rettet” eller ”Slettet” i QGIS kortvinduet. Brugeren kan herefter kontrollere de enkelte modificerede elementer og ”skubbe” (uploade) modifikationerne tilbage til DAI.

Plugin-et har mulighed for at gemme en tematisering (symbolisering) for hver DAI lagtype, således at samme tematisering vil blive benytte ved senere downloads af data-lag fra DAI. 
Plugin-et har slutteligt en række administrative funktioner, f.eks. kunne opstarte QGIS geometri-tjekker på det valgte lag.

Plugin-et kan benyttes til både demo-miljøet og produktionsmiljøet hos DAI, Miljøportalen.    
NB! Denne vejledning er skrevet til den engelske udgave af DMP Manager. Hvis du arbejder med den danske udgave af DMP Manager og bliver forvirret over sprog forskelle kan du indtil videre skifte din QGIS til at fungere med engelsk som sprog. Vejledningerne vil blive opdateret med danske oversættelser hurtigst muligt.

##  Installation af DMP Manager plugin.

**Dette plugin fungerer kun på QGIS ver. 3.22 eller senere.**

Plugin zip fil kan downloades fra hjemmesiden: 
https://github.com/septima/DMP-MANAGER-DISTRIBUTION/blob/main/dmp_manager.zip
og trykke på knap ”Download”

Eller downloades som en del af hele repositoriet:
https://github.com/septima/DMP-MANAGER-DISTRIBUTION

og tryk på grøn knap ”Code” og derefter på under-menupunkt: ”Download ZIP”. Du skal herefter udfolde den hentede zip-fil for at finde selve installationsfilen ”dmp-manager.zip”.
Herefter foretages installationen i QGIS med følgende:
Tryk på menupunkt ”Plugins” -> ”Manage and Install Plugins….” -> Faneblad ”Install from ZIP”
(”Plugins” -> ”Administrér og Installér Plugins…” -> Faneblad ”Installér fra ZIP”)

Følgende brugerdialog vises:

![header](img/install_qgis.png)

Tryk på knappen fremhævet med gult og vælg filen ”dmp_manager.zip” fra mappe ”Overførelser” (eller hvor zip-filen blev downloadet til)

Installationen gennemføres herefter ved at trykke på knap ”Install Plugin”.

