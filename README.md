# Diplomarbeit

My diploma thesis at Dresden University of Technology.

## TODO

* Was für einen Effekt hat Kommentar löschen, wenn die Referenzen drauf erhalten bleiben?

## Notes wegen RW

Überblick: Welche Fragen, welche davon gewählt, Grundlage, warum.
Bedienung: Comic Generation, UA mit Screenshots, welche Fragen
Kommunikation: Welche Fragen
History: Beispiel Tableau (Heer2008) oder andre Mashups, unterschiede rausstreichen
Meta-Hilfe: Interaction Trace-based Reasoning (Champin, Cordier)


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
* Kommunikation: Überarbeiten nach Paper Mockup
* Kommentare: Umschaltbutton für Highest Ranked und Newest.
* Kommentare: API Referenz RW, erklären was neuartig.
* History: Timeline vereinfachen

## Anmerkungen Martin 28.6.

* Überlegen: Kommunikation nicht ad-hoc, wenn es passiert, sondern ähnlich wie Bedienung. Nachteil: Benutzer kapiert erst, wenn er aktiv auf den Knopp drückt. Kann man machen, dynamische Kommunikationshilfe könnte dann die Pfeile ad-hoc rendern. --> Paper Mockup.
* Martin: Abgrenzung komponentenspezifische Hilfe?
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