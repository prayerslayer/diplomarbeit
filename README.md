# Diplomarbeit

My diploma thesis at Dresden University of Technology.

## Implementierung

**Zeit**: 14 Wochen ab 22.7.

Zuerst:

1. Szenario mit Komponenten überlegen
2. Komponentenbeschreibung der Komponenten erstellen (wie in Konzept)
3. SVN Branch von allem erstellen, programmieren anfangen

Implementierungsablauf:

1. CoRe: Uploadprozess erweitern, dass er neue SMCDL lesen kann
2. CoRe: Neue SMCDL Daten in MCDO übertragen
3. Hilfeservice: Integration von MRE, DaRe und CoRe
4. Hilfeservice: Schnittstelle um Hilfegenerierung für Komponente anzustoßen
5. Hilfeservice: Hilfegenerierung
6. Hilfeservice: Schnittstelle um Hilfepanels auszugeben
7. Hilfesystem: Grundlegendes Frontend (Backbone + jQuery wär nice)
8. Komponente: Titelleiste um Buttons erweitern. Aufruf HS?
9. Hilfesystem: Frontend für Bedienung schreiben

=== bedienungshilfe fertig ===

10. Hilfesystem: Irgendwie an Kommunikationsmodell (Event Broker?) kommen, analysieren, Frontend für Kommunikation schreiben

=== kommunikationshilfe fertig ===

11. DaRe: Kommentare Backend schreiben
12. DaRe: REST API für Kommentare
13. Hilfesystem: Kommentar schreiben Frontend
14. Hilfesystem: Kommentar anzeigen Frontend

=== kommentare fertig ===


## TODO
* Problem für "eindeutige ID ist super" benennen?
* History: Properties beschreiben Komp.zustand, wenn sich Zustand ändert, ändern sich auch Props und ich krieg ein propChanged Event.
* History: Link zw. Op und Ev bringt in Komp.beschr. nicht viel, lieber Eventnachricht ordentlich ausstatten. Nochmal genau erklären, was Hilfesystem macht wenn Nutzerinteraktion (ev.operation löschen, evtl neue Box).
## Ergebnisse Paper Mockup

* Überlegen: Auswahlhilfen für Bereiche --> Lieber in Ausblick.
* Machen: No-Click-Area ist weg, wenn Arrow/Text ausgewählt
* Überlegen: Bedienungshilfe animieren mit Maus --> Ausblick

## Ausblick

* Bedienungshilfe mit Maus animieren
* Auswahlhilfen für Annotationsbereiche
* CSS von Komponente im CoRe auf relative Einheiten trimmen (schwierig weil man nicht weiß, was skaliert werden muss und was nicht)
* Aktionen abhängig von Aktionen (Suche -> Anzeige) wär auch gut, würde mehr High-Level erklärung ermöglichen

## Kleinscheiss

* Bessere Listen
* Datenhochlader -> Data Provider

## Capability Markup

Jetzt:

    <capability id="search" activity="ua:search" entity="trvl:location"/>
    <event dependsOn="search"/>

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