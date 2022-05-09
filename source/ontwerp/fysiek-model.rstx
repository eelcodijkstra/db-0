Een fysiek model
================

Een volgende stap is het vertalen van het logische model in een fysiek model, passend bij het DBMS dat voor de database gebruikt wordt.
We geven hier het fysieke model voor de *relationele database* Leden-Inschrijvingen-Events.
(Het fysiele model voor een NoSQL database zal er anders uitzien.)

.. figure:: MySQL-inschrijvingen-3.png
  :width: 650px
  :align: center

  Fysiek model van het voorbeeld, voor een relationele database

Het logische ERD-model is omgezet naar het fysieke relationele model:

* *entiteiten* worden *tabellen*: leden en events
* de relatie *inschrijving'* wordt een *tabel*: inschrijvingen
* *attributen* worden *kolommen* van deze tabellen.
* voor elk attribuut is het datatype bepaald (bijvoorbeeld: ``INT``, of ``VARCHAR(30)``).

Een instantie van een Lid, bijvoorbeeld met als waarden :code:`{"email": "jklaassen@kpnmail.nl", "voornaam": "Jan", "achternaam": "Klaassen"}`, wordt een rij in de tabel ``leden``.

Voor de identificatie van een lid gebruiken we een uniek nummer: :code:`lidnr`.
Hiermee identificeren we een rij in de tabel :code:`leden`.
De kolomnaam :code:`lidnr` heet de **primary key** van deze tabel.
Als primary key van de tabel :code:`events` gebruiken we de kolom :code:`eventnr`.
Een inschrijving identificeren we met de combinatie :code:`(lidnr, eventnr)`.
Zoals je ziet kan een primary key uit meerdere kolomnamen bestaan.

Met de primary key van de tabel
Vanuit de tabel :code:`inschrijvingen` verwijzen we naar de tabellen :code:`leden`,
en :code:`events`, via de genoemde keys.
Een verwijzing van een tabel naar een andere tabel, via de primary key van de doel-tabel,
heet een **foreign key**.

Enkele opmerkingen hierbij:

* in het E-R Diagram gebruiken we meestal een enkelvoud, voor een tabelnaam een meervoud;
* een relatie wordt niet altijd een tabel; dit kan ook een verwijzing tussen tabellen zijn.

Enkele voorbeelden van deze tabellen:

.. csv-table:: leden
   :file: leden.csv
   :widths: 5, 10, 15, 20
   :header-rows: 1

.

.. csv-table:: inschrijvingen
   :file: inschrijvingen.csv
   :widths: 5, 5, 10
   :header-rows: 1

.

.. csv-table:: events
   :file: Events.csv
   :widths: 5, 8, 20
   :header-rows: 1

Voorbeeld: de eerste inschrijving verwijst naar eventnr 1 en naar lidnr 1:
met andere woorden, Hans de Boer heeft zich ingeschreven voor het Schaaktoernooi Breda,
op 21-8-2019, met als maaltijd-keuze: maaltijd A.

Schema
------

Uiteindelijk moeten we dit model in SQL beschrijven.
Zo'n beschrijving van een database of van een tabel noemen we ook wel een schema van de database of van de tabel.

In een relationeel DBMS wordt het schema van elke database in een database van het DBMS opgeslagen.
Je kunt dit dan ook opvragen via SQL.
Je krijgt dan bijvoorbeeld als resultaat de SQL-opdracht om de tabellen aan te maken:

.. code-block:: sql

  CREATE TABLE leden(
                      lidnr INTEGER PRIMARY KEY,
                      voornaam VARCHAR(255) NOT NULL,
                      achternaam VARCHAR(255) NOT NULL,
                      email VARCHAR(255) NOT NULL UNIQUE
                    );
  CREATE TABLE events(
                    eventnr INTEGER,
                    datum VARCHAR(255) NOT NULL,
                    beschrijving VARCHAR(255),
                    PRIMARY KEY (eventnr),
                    CONSTRAINT name UNIQUE (datum, beschrijving)
                    );
  CREATE TABLE inschrijvingen(
                    eventnr INTEGER,
                    lidnr INTEGER,
                    maaltijd VARCHAR(255),
                    PRIMARY KEY (lidnr, eventnr),
                    FOREIGN KEY (lidnr) REFERENCES leden (lidnr),
                    FOREIGN KEY (eventnr) REFERENCES events (eventnr)
                    );

Constraints
-----------

Zoals je ziet bevat het schema ook enkele constraints:

* als (externe) identificatie (UID) van een Lid gebruiken we het email-adres; dat moet daarom uniek zijn.
* als (externe) identificatie van een Event gebruiken we de combinatie (datum, beschrijving); deze moet uniek zijn.

Het relationele DBMS zorgt ervoor dat bij operaties op de database deze constraints gehandhaafd blijven,
ook als een gebruiker of een toepassing opdrachten geeft die hiermee in strijd zijn.

Index
-----

Een relationele DBMS maakt voor elke key een index, om daarmee efficiënt te kunnen zoeken.
Als je ook op een andere kolomwaarden efficiënt wilt kunnen zoeken, dan kun je daarvoor in het fysieke model een index opnemen.
Zo'n index vraagt wel extra ruimte.

Oefeningen
----------

* oefening/opdracht: opvragen van schema
* oefening: effect van constraints
* oefening: index????
