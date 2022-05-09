
In het vorige hoofdstuk hebben we een relationele database gebruikt voor een eenvoudige webtoepassing.
In dit hoofdstuk gaan we in op het *ontwerpen* van databases: hoe kom je tot zo'n database?
Het resultaat van dit ontwerpproces is een databasemodel.
De  verdiepende hoofdstukken over database-ontwerp beschrijven de stappen om tot zo'n model te komen.
Hier gaan we vooral in op de grafische notatie van een databasemodel.
Zo'n grafisch model gebruik je om te communiceren met de opdrachtgever en gebruikers.
Als deze tevreden zijn over het model, gebruik je dit voor het maken van de eigenlijke database.

.. rubric:: Van analyse via databasemodel naar databasetabellen


.. figure:: ontwerp/DB-ontwerpproces.png
  :width: 500px
  :align: center

  Database-ontwerpproces

Het proces van het ontwerpen en maken van een database bestaat uit aantal stappen.

* In de 'Analyse'' ga je na waarvoor de database bedoeld is. Je probeert de *informatiebehoefte* van de organisatie (de "business") in kaart te brengen.
* Voor een groot ontwerp maak je eerst een **conceptueel model**, met alleen de belangrijkste business-elementen.
* Vervolgens maak je een **logisch model**. In het logische model neem je alle elementen op die relevant zijn voor de informatiebehoefte van de "business", zonder je daarbij druk te maken over de uiteindelijke (fysieke) database.
* Tenslotte vertaal je het logische model naar een **fysiek model**. Voor een relationele database vertaal je een entiteit naar een databasetabel, en de attributen naar de kolommen van die tabel.

Bij de analyse en het logisch ontwerp gaat het vooral om het begrijpen van de "business".
Via het logische model communiceer je met de opdrachtgever, gebruikers en andere experts uit de "business", om na te gaan of je inderdaad alle relevante elementen gemodelleerd hebt.
Je gebruikt daarbij vaak een grafische notatie, zoals Entity-Relation Diagrammen (ERDs).

Voor het vertalen van logisch model naar fysiek model heb je vooral kennis van databases nodig.
Het fysieke model gebruik je ook voor de toepassingsprogrammeurs en de gebruikers van de database.

In de hoofdstukken over Database-ontwerp werken we het bovenstaande ontwerpproces verder uit.
Hier gaan we vooral in op het *logische model*, als resultaat van het ontwerpproces.
Het kunnen lezen van zo'n model is ook voor potentiële opdrachtgevers en gebruikers van belang,
om te kunnen communiceren met de ontwerper van de database.

We geven ook een voorbeeld van een fysiek model als resultaat van de vertaling van het logische model naar een relationele database.

.. rubric:: Databasemodellen in soorten

Een databasemodel is een model van de wereld zoals die van belang is voor de informatievragen van een organisatie (de "business").
Een model is een *abstractie* met een *doel*: je laat alle elementen weg die niet relevant zijn voor het doel.

  Een voorbeeld van een model is een landkaart: bijvoorbeeld een autokaart bevat alleen de details die voor een automobilist van belang zijn, om van A naar B te reizen. Een wandelkaart bevat andere details dan een autokaart: een wandelaar reist veel langzamer en heeft andere informatie nodig.

Je neemt in een model alleen die elementen op die voor het doel van belang zijn.
In het *logische model* neem je alleen de elementen op die voor de informatiebehoefte van "business" van belang zijn.
Je laat de elementen weg die alleen voor de fysieke database van belang zijn.

.. rubric:: Voorbeeldtoepassing

Als voorbeeld gebruiken we een (web)toepassing waarmee gebruikers zich kunnen inschrijven voor verschillende events - zoals bijvoorbeeld schaakwedstrijden.

* Een deelnemer moet zich eerst als lid aanmelden, met voornaam, achternaam en email.
* De organisatie maakt een lijst van events;  een event wordt gegeven door een datum en een beschrijving.
* Een lid kan zich voor een (of meer) event inschrijven; bij inschrijving moet een keuze gemaakt worden uit de verschillende alternatieve maaltijden.
* Een lid kan zijn/haar inschrijvingen achteraf aanpassen.
* Een event-organisator kan een overzicht krijgen van de inschrijvingen voor een event.

Deze webtoepassing is uitgewerkt in Python en SQLite; deze is te vinden op glitch.com.
Daar kun je deze toepassing bekijken en er mee spelen. Je kunt er ook een eigen versie ("remix") van maken.
