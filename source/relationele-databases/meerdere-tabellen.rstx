Meerdere tabellen
=================

Bekijk de onderstaande tabel, met de aanmeldingen van de leden voor een event.

.. figure:: redundante-tabel.png
  :width: 600px
  :align: center

  Een (redundante) tabel met event-aanmeldingen van leden

**Redundantie.**
Je ziet dat in deze tabel de elementaire gegevens van de leden, zoals hun naam en geslacht,
voor elke aanmelding herhaald worden.
Deze vorm is daardoor *redundant* ("overtollig"):
je kunt deze overtollige gegevens wegwerken zonder verlies aan informatie.
Bovenstaande redundante vorm heeft twee nadelen:

1. je hebt meer opslagruimte nodig dan strikt noodzakelijk;
2. en, belangrijker: het is lastiger om de *consistentie* van de de gegevens te garanderen,

Met de huidige opslagmedia is (1) niet het grootste probleem meer,
maar (2) blijft belangrijk.
Daarom proberen we dergelijke redundante vormen in databases te vermijden.

In de onderstaande vorm hebben we deze redundantie verwijderd,
door een extra tabel ``inschrijvingen`` in te voeren.
We identificeren een inschijving met behulp van het ``inschrijfnr``:
dat is de *key* van deze tabel.

.. figure:: genormaliseerde-tabellen.png
  :width: 500px
  :align: center

  Genormaliseerde tabellen voor leden en inschrijvingen

**Foreign key**
We gebruiken hier een verwijzing van de ene tabel naar de andere:
een aanmeldingen verwijst naar de overeenkomstige rij in ``leden`` met behulp van de key ``lidnr``.
Een verwijzing via een *key* van een andere tabel heet een *foreign key* in de verwijzende tabel.
``lidnr`` is in de tabel ``inschrijvingen`` dus een *foreign key*.

**Normalisatie.**
Een vorm zonder de redundantie zoals hierboven noemen we een *genormaliseerde vorm*.
Het wegwerken van deze redundantie heet dan *normaliseren*.
Dit is een onderdeel van het ontwerpen van een relationele database.

**Join: combineren van tabellen.**
Het gebruik van een verwijzing naar een andere tabel heeft niet alleen voordelen:
als je een overzicht wilt maken van alle leden, met hun naam, die zich aangemeld hebben voor een bepaalde event,
dan moeten we de informatie uit beide tabellen combineren.
In een relationele database kan dit met behulp van een *join*.
Dit werken we in het volgende onderdeel verder uit.
Zo'n join kost extra tijd: we hebben het voordeel van de genormaliseerde vorm uitgewisseld tegen
extra kosten voor het raadplegen van de database.

Opdrachten
----------

Toetsvragen
-----------
