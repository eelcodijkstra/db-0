# Data in meerdere tabellen

* noodzaak van meerdere tabellen
    * voorkomen van redundante vormen (duplicatie van gegevens)
* gebruik van verwijzingen naar gemeenschappelijke data
* combineren van tabellen: join ("selectie uit cartesisch product")
* verband met DB-ontwerp: tabel komt overeen met *Entiteit* (of met relatie).

In een relationele database gebruik je gewoonlijk meerdere tabellen.
De belangrijkste reden voor hetb gebruik van meerdere tabellen is dat je

Beschouw de onderstaande tabel, van inschrijvingen van leden van een club, voor events van die club.
Wat opvalt is dat sommige gegevens, zoals voornaam, achternaam en emailadres, bij elke event-inschrijving herhaald worden.
Dit heeft twee problemen:

1. je hebt door deze duplicatie meer ruimte nodig voor de tabel;
2. als het emailadres van een lid verandert, moet je dat op meerdere plekken aanpassen om de database consistent te houden.

Het eerste probleem is met de huidige mogelijkheden voor massa-data-opslag steeds minder een probleem.
Het tweede probleem is serieuzer; en dit probleem wordt nog groter als we meer gegevens van de leden willen opslaan.

De tabel hierboven is een voorbeeld van een *redundante vorm* (letterlijk: overtollige vorm): gegevens die je meervoudig opslaat zijn erg lastig te veranderen op een consistente manier.

> redundantie is niet altijd slecht: we gebruiken redundantie bijvoorbeeld om de efficiëntie te vergroten, zoals we later zullen zien. We maken soms een afweging tussen snelheid en "mogelijk vertraagde" consistentie. (*eventual consistency*).

In een relationele database kunnen we op de volgende manier tot een niet-redundante vorm komen:

* gebruik in plaats van duplicatie van gemeenschappelijke gegevens, *verwijzingen* naar deze gegevens.

Voor een verwijzing gebruiken we de key van de gegevens in een andere tabel: dit heet een *foreign key*.

Voor het bovenstaande voorbeeld krijgen we dan:

* een tabel met de gegevens van een lid, bijvoorbeeld voornaam, achternaam, en emailadres;
    * de *key* van deze tabel is het *lidnr*.
* een tabel met inschrijfgegevens voor een event: de deelnemer (lidnr), de event-datum, en de maaltijdkeuze.
    * het *lidnr* is hier de foreign key die naar de gegevens van de deelnemer verwijst.
    * als identificatie (key) van een inschrijving kunnen we een apart inschrijfnr gebruiken; of de combinatie van lidnr en event-datum.

Opmerking: de consistentie-eis, dat een deelnemer één naam en één emailadres heeft, volgt uit het (logische) datamodel, niet uit de data in de tabellen zelf.
In een ander model wil je het misschien toestaan dat een lid zich voor elke event met een andere naam en een ander emailadres inschrijft. Dan heb je andere tabellen nodig!
