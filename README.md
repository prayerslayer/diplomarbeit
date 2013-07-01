# Diplomarbeit

My diploma thesis at Dresden University of Technology.

## TODO

* Was für einen Effekt hat Kommentar löschen, wenn die Referenzen drauf erhalten bleiben?

## Anmerkungen Martin 28.6.

* Generell wo möglich trennen in Hilfe, die allgemein für Mashups cool ist und Hilfe, die speziell für InfoVis ausgelegt ist
* Auswahl von verwandten Arbeiten an Anforderungen festmachen: Welche müssen mindestens erfüllt sein?
* Verwandte Arbeiten mehr auf Anforderungen ausrichten: Wie werden die von der Arbeit erfüllt, wie nicht, was lernen wir draus?
* Eventuell von komponentenspezifischer Hilfe explizit abgrenzen, implizit ist das schon drin durch die Anforderungen.
* Tableau: Polaris Paper

* Überlegen: Kommunikation nicht ad-hoc, wenn es passiert, sondern ähnlich wie Bedienung. Nachteil: Benutzer kapiert erst, wenn er aktiv auf den Knopp drückt. Kann man machen, dynamische Kommunikationshilfe könnte dann die Pfeile ad-hoc rendern.
* Memento von Komponente doch mit Propertys lösen, scheint Feature zu sein
* Verlinkung: 3 Varianten diskutieren (DaRe speichern, DaRe ad-hoc, selbst), konzeptionell aber sagen, dass das CoRe es auch können sollte (weil gut für alle Mashups).
* Verlinkung: URI hinzufügen wegen Bedienung (wo dann auch eine URI zur Capability muss --> Fragestellung wozu man überhaupt eine Log Skala braucht)
* Martin: Hilfebutton lieber in Navigationsleiste oder Komponentenspezifisch?
* CoRe kennt viso-graphic:position, muss also nicht in Komponentenbeschreibung
* Überlegen, wie man mit Paper Mockups arbeiten kann
* Domäne des Benutzers in Context Service (gut für Credibility von Kommentaren + UA)

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