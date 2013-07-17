# Diplomarbeit

My diploma thesis at Dresden University of Technology.

## TODO

* Bei jeder Entscheidung für oder gegen was die entsprechende Anforderung angeben
* Was für einen Effekt hat Kommentar löschen, wenn die Referenzen drauf erhalten bleiben?

## Ergebnisse Paper Mockup

* Besser erklären: Icon Kommentare angucken
* Überlegen: Auswahlhilfen für Bereiche --> Lieber in Ausblick.
* Machen: No-Click-Area ist weg, wenn Arrow/Text ausgewählt
* Überlegen: Bedienungshilfe animieren mit Maus --> Ausblick

## Anmerkungen Martin 5.7.

* Allgemein: Mehr Referenzen ins RW in der Arbeit, bessere Listen.

## Anmerkungen Martin 28.6.

* Datenhochlader -> Data Provider

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