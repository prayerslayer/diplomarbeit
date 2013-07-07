# Diplomarbeit

My diploma thesis at Dresden University of Technology.

## TODO

* Was für einen Effekt hat Kommentar löschen, wenn die Referenzen drauf erhalten bleiben?

## Probleme globales Undo

* Vor Event Memento holen geht nicht gut, weil Eventlistener des Hilfesystems erst nach dem Handler der Komponente ausgeführt wird. Kann sein, dass wir was verpassen.
* Nach Event Memento holen geht nicht, weil Events kaskadieren und nicht klar ist, wann ein Event "fertig" ist.
* Analyse des Kommunikationsmodells bringt in der Hinsicht nix, weil zwar klar ist, durch welche Operation ein Event aufgerufen wurde, aber nicht anders herum (welche Events wirft eine Operation): Kann von vielen Bedinungen abhängen!
* Einfachste Lösung also sicherstellen, dass unser Event Handler vor dem des Entwicklers registriert wird. Dazu müsste man aber den Component Lifecycle erweitern (zwischen Loaded und Instantiated noch eine Stufe DOMReady oder so rein), weiß nicht obs das bringt. --> Auch nicht möglich weil dynamisch DOM Elemente erzeugt werden müssen, manchmal.
* Bleibt zur Laufzeit Rückwärtsanalyse machen und kucken, wodurch ein Event ursprünglich ausgelöst wurde. Problem: Muss 100 % sicher sein, sonst verwirrt Undo Funktion. Problem 2: Nachvollziehbarkeit überhaupt gegeben? Stichworte kaskadierende Events, asynchrone Operationen.

## Anmerkungen Martin 5.7.

* Allgemein: Mehr Referenzen in der Arbeit, bessere Listen.
* Anforderungen: nach Plattform/Domänenspezifischen unterscheidbar?
* Related Work: Mehr auch ansprechen, was Anforderungen nicht umsetzen und bessere Zusammenfassungen
* RW in Einführung Konzeption erwähnen
* Aufruf in Einführung anpassen, ist ja nicht nur Titelleiste jetzt
* Ort in Einführung: Grafik für Buttonleiste
* Optik => Implementierung?
* Bessere Überschriften
* Intro: Unterscheidung plattform/domänenspezifisch
* Intro: Nicht visuelle Mappings, sondern enthaltene Daten
* Intro: Domain Assignment genauer erklären
* Bedienung: Beschreibungssprache besser erklären?
* Bedienung: Auflistung der Änderungen für Komponentenbeschreibung
* Bedienung: Beispielhaft XML?
* Bedienung: Verweis auf Verlinkung
* Bedienung: Zusatzinfos vs Mappings erst zur Laufzeit
* Bedienung: Generierung überarbeiten -> Dev gibt Mappings als SPARQL Query an oder lädt halt Daten hoch
* Bedienung: Ablauf Generierung klären
* Bedienung: Raster der Panels erklären und was passiert, wenn Komponente zu schmal, Mindestgröße
* Reporting: Paper Verweis
* Reporting: Rating Repository statt DaRe
* Kommunikation: Überarbeiten nach Paper Mockup
* Kommunikation Backend: Lösung ist in der Komponentenbeschreibung
* Verlinkung: Generell und was sind Beschreibungen (Text, Bilder, was wenn nur japanisch?)
* Verlinkung: Klären wegen Aktualität der Informationen
* Verlinkung: Auch Bedienung über Fragezeichen? Maybe. Ist schwer im Paper Mockup zu klären. Martin findets gut, also vielleicht einfach machen.
* Kommentare: Was bringt löschen? Nachvollziehbarer Gesprächsverlauf, wenn Sortierung nicht zeitlich? Umschaltbutton?
* Kommentare: API Referenz RW, erklären was neuartig.
* Kommentare: Datenbezogen Bereich braucht nicht zwingend Positionskodierung, aber wenn leere Bereiche referenziert werden sollen, unbedingt (weil Position das einzige ist, was ich vom Auswahlrechteck habe).
* Kommentare: Aggregation nicht nur von Komponenten selbst blöd, sondern dürfen auch gar nicht erst aggregiert reingegeben werden. Daten sind im DaRe. Schluss.
* Kommentare: Icons kleiner als Text, vielleicht mit Referenz auf UX Movement erklären, dass das nicht schlecht ist.
* Kommentare: Avatar + Benutzername kommt aus UserService
* Kommentare: Backend klären
* History: Klären, dass ich nicht auf Granularitätsstufe Events zurücksetzen will, sondern auf Interaktion (weil das dem mentalen Modell des Benutzers entspricht, der die einzelnen Events/Operationen ja nicht mitbekommt)
* History: Daten kommen aus dem DaRe.
* History: PropertyLinks benutzen um weiterzuleiten, von wo ein Event ausgelöst wurde. --> Wie genau? Was steht in PL drin? Wann wird gesetzt? Wie viele sind nötig?
* History: Timeline vereinfachen

## Anmerkungen Martin 28.6.

* Überlegen: Kommunikation nicht ad-hoc, wenn es passiert, sondern ähnlich wie Bedienung. Nachteil: Benutzer kapiert erst, wenn er aktiv auf den Knopp drückt. Kann man machen, dynamische Kommunikationshilfe könnte dann die Pfeile ad-hoc rendern. --> Paper Mockup.
* Memento von Komponente doch mit Propertys lösen, scheint Feature zu sein --> Zuerst Paper Mockup abwarten
* Martin: Hilfebutton lieber in Navigationsleiste oder Komponentenspezifisch? nein.
* Domäne des Benutzers in Context Service (gut für Credibility von Kommentaren + UA)
* Datenhochlader -> Data Provider

## Paper Mockup

* Klären ob Pfeile nerven/verwirren und klären wann sie angezeigt werden sollen

## Capability Markup

Jetzt:

<capability id="search" activity="ua:search" entity="trvl:location"/>

Dann:

<!-- aktion -->
<capability id="search" activity="ua:search" entity="trvl:location" operations="searchOps" wait="5s" />

<!-- äquivalente operationen -->
<operations id="searchOps" testData="new york" relatedConcept="dbpedia:Search">
	<operation id="clickSearch" css="button.search" viso="a:click" />
	<operation id="typeSearch" css="button.search" viso="a:type" which="space" />
	<sequentialOperation id="menuSearch">
		<operation id="clickMenu" css="div.menu" viso="a:click" />
		<operation id="clickMenuSearch" css="div.menu > div.search" viso="a:click" />
	</sequentialOperation>
	<parallelOperation id="blublu" css=".vis">
		<operation id="pressStrg" viso="a:type" which="strg" />
		<operation id="pressA" viso="a:type" which="a"
	</parallelOperation>
</operations>