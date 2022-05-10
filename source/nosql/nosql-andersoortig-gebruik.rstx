Andersoortig gebruik
====================

Een tweede reden om NoSQL te gebruiken is dat het gebruik eisen stelt die lastig en/of duur zijn voor een relationele database.
Voor veel "klassieke" database-toepassingen hebben relationele databases duidelijke voordelen:

* door te werken met een genormaliseerde relationele database is het eenvoudig om bij updates de consistentie te bewaren;
* het database-systeem bewaakt zelf veel van de constraints, onafhankelijk van de verschillende toepassingen waarin de database gebruikt wordt. Dit zorgt ervoor dat fouten in toepassingen geen groot risico vormen inconsistenties in de database.
* de database (en de consistentie daarvan) is grotendeels onafhankelijk van de toepassingen.

De relationele aanpak is relatief duur als het om erg grote hoeveelheden data gaat (schaling),
waarbij het belangrijk is om snel over de gegevens te kunnen beschikken (lezen, in plaats van update).
In dit soort gevallen kan een NoSQL-oplossing een grote snelheid bieden tegen relatief lage kosten.
Een nadeel van de NoSQL-oplossing is dat de verantwoordelijkheid voor de consistentie verschuift van het DBMS naar de toepassing(en).

.. rubric:: Niet-genormaliseerde data: kopie

Eén van de manieren waarop in een document-database het lezen van data voor een toepassing kan versnellen,
is het werken met niet-genormaliseerde data.
Je kunt in een document, in plaats van verwijzingen naar andere documenten, data uit andere documenten overnemen,
om te voorkomen dat je steeds die andere documenten moet opzoeken.

  Het werken met niet-genormaliseerde data maakt updates lastiger: je moet de data op meerdere plekken bijwerken. Als de data niet snel verandert, is dat niet altijd een groot probleem.

.. rubric:: Verwijzing (referencing)

Als voorbeeld behandelen we de relatie "neemt deel in" tussen Contact en Event.

  In het geval van een relationele database gebruiken we voor deze N-M relatie ("many-many relatie") een aparte tabel, met daarin de foreign keys van Contact en Event.

Deze relatie heeft de volgende eigenschap:

* het aantal deelnemers aan een Event ("afspraak" in agenda) is beperkt, vaak minder dan 10. Je werkt in een agenda niet met lange lijsten deelnemers; dan geef je deze meestal als groep een naam.
* de verzameling deelnemers van een Event verandert niet erg vaak.
* een Contact kan deelnemen aan een groot aantal Events (mogelijk honderden).
* de verzameling Events waar een Contact in deelneemt verandert vaak.

Dit betekent dat we deze relatie kunnen vormgeven als een meerwaardig veld van Event, met verwijzingen (foreign keys) naar Contact-documenten: dit is efficiënt als het aantal niet te groot is (100? 1000?),
en als deze verzameling niet vaak verandert.
Omgekeerd is niet handig: dat aantal is mogelijk erg groot, en verandert bovendien vaak.

  Met andere woorden: in een relationele database beschouwen we "M-N" als "many-many", als M of N groter dan 1 kunnen zijn. In een MongoDB document is M of N kleiner dan (ongeveer) 100 nog niet "many", en kunnen we deze in het document zelf opnemen.

We krijgen op deze manier een genormalisereerde, "referencing" oplossing: als we de gegevens van een deelnemer aan een Event nodig hebben,
dan vinden we deze door via de foreign key ("_id") in het Event-document het bijbehorende Contact-document te zoeken (in de andere collection <code>contacts</code>).

Een voorbeeld met Event:

.. code-block:: none

  {'Beschrijving': 'Jaarvergadering',
   'Locatie': 'Domstad Utrecht',
   'Datum': '2020-2-21',
   'Deelnemers': [ObjectId("5d6280bc6f385c47986b6c52"), ObjectId("5d6280bc6f385c47986b4e31") ]
  }

en de bijbehorende Contacten:

.. code-block:: none

  {'_id': ObjectId("5d6280bc6f385c47986b6c52"),
   'Voornaam': 'Hans',
   'Achternaam': 'de Vries',
   'Adres': {'Straat': 'Achterweg 12', 'Plaats': 'Arnhem'},
   'Telefoon': ['06-1234 5678', '026-123 5678'],
   'Email': ['hdv@ziggo.nl', 'hansdevries@kpnmail.nl']
  }

  {'_id': ObjectId("5d6280bc6f385c47986b4e31"),
   'Voornaam': 'Anna',
   'Achternaam': 'Groen',
   'Email': ['anna67@ziggomail.nl']
  }

.. rubric:: Gedeeltelijke inbedding

Stel dat we in de agenda-toepassing de naam en het primaire email-adres van de Event-deelnemers vrijwel altijd nodig hebben.
We kunnen ervoor kiezen om een kopie van deze gegevens in het Event-document over te nemen.
We hoeven dan niet steeds bij het raadplegen van de agenda de bijbehorende Contact-documenten op te zoeken.

Het bovenstaande voorbeeld wordt dan:

.. code-block:: none

  {'Beschrijving': 'Jaarvergadering',
   'Locatie': 'Domstad Utrecht',
   'Datum': '2020-2-21',
   'Deelnemers': [ {'id': ObjectId("5d6280bc6f385c47986b6c52"),
                     'Voornaam': 'Hans',
                     'Achternaam': 'de Vries',
                     'Email': 'hdv@ziggo.nl'}
                 , {'id': ObjectId("5d6280bc6f385c47986b4e31")
                     'Voornaam': 'Anna',
                     'Achternaam': 'Groen',
                     'Email': 'anna67@ziggomail.nl'}
                 ]
  }

We kunnen de andere gegevens van de Contacten via de key (id) opzoeken in de oorspronkelijke Contact-documenten.

Deze vorm is niet-genormaliseerd (redundant): we hebben voornaam, achternaam en email-adres van deze Contacten dubbel opgeslagen.
Dit betekent dat we in principe bij het veranderen van deze gegevens in het Contact-document, ook de bijbehorende Event-documenten moeten bijwerken.
In dit geval kunnen we ervoor kiezen om dat niet te doen: in de eerste plaats zullen de voornaam en achternaam niet snel veranderen. En van het email-adres kunnen we als argument gebruiken dan dit het email-adres is waarmee de afspraak gemaakt is.

Dit voorbeeld is een vorm van ''gedeeltelijke inbedding'' (partial embedding), van delen van de Contact-documenten in het Event-document.

.. rubric:: Volledige inbedding

Soms is het zinvol om een document volledig in te bedden in een ander document.
In zekere zin hebben we dat ook gedaan met het samengestelde adres-attribuut: dit is een sub-document van Contact.

'Zwakke' entiteiten (weak entities) die niet zelfstandig gebruikt worden, en waar dus niet vanuit meerdere Entiteiten verwezen wordt, zijn geschikte kandidaten voor inbedding.

SQL versus NoSQL: samenvatting
------------------------------

+---------------------------+---------------------------------------+
| relationele DB (SQL)      | NoSQL DB                              |
+---------------------------+---------------------------------------+
| data in tabellen          | data in documenten, enz.              |
+---------------------------+---------------------------------------+
| "rechthoekige data"       | "niet-rechthoekige data"              |
+---------------------------+---------------------------------------+
| nadruk op consistentie    | nadruk op snelheid                    |
+---------------------------+---------------------------------------+
| nadruk op stabiliteit     | nadruk op flexibiliteit               |
+---------------------------+---------------------------------------+
| DB los van toepassing(en) | DB sterk gekoppeld aan toepassing(en) |
+---------------------------+---------------------------------------+


De bovenstaande tabel geeft het verschil in grote lijnen.
Een relationele (SQL) database-systeem is in principe universeel: je kunt daar alle soorten data in opslaan;
en er zijn ook manieren om snelheid of flexibiliteit te bereiken.
Maar die oplossingen zijn vaak duurder of complexer dan vergelijkbare oplossingen in een passende NoSQL database.
Anderzijds is het bereiken van consistentie in een NoSQL database vaak lastiger dan in een SQL database.

Bovendien kunnen er altijd andere overwegingen zijn om binnen een organisatie voor een bepaalde oplossing te kiezen.
