# Diplomarbeit

My diploma thesis at Dresden University of Technology.

# TODO

* Layout überlegen für Panels, wenn Anleitungen unterschiedlich lang sind: Mal 3 Panels, mal fünf? --> In Instructions nur kürzeste, in Kommunikation mehrere Zeilen (weil da ja tatsächlich verschiedene Aktionen erklärt werden).
* Überlegen, was alles so für die Positionierung nötig ist: HTML margins, paddings, positions, SVG x's, y's, widths, transforms --> das alles muss nämlich beim highlight berücksichtigt werden, zumindest konzeptionell

## Implementierung

**Zeit**: 14 Wochen ab 22.7.

Zuerst:

1. Szenario mit Komponenten überlegen
2. Komponentenbeschreibung der Komponenten erstellen (wie in Konzept)
3. --SVN Branch von allem erstellen, programmieren anfangen--

Implementierungsablauf:

1. --CoRe: Uploadprozess erweitern, dass er neue SMCDL lesen kann--
2. --CoRe: Neue SMCDL Daten in MCDO übertragen--
3. -Hilfeservice: Integration von MRE, DaRe und CoRe-
4. --Hilfeservice: Schnittstelle um Hilfegenerierung für Komponente anzustoßen--
5. Hilfeservice: Hilfegenerierung
6. --Hilfeservice: Schnittstelle um Hilfepanels auszugeben--
7. --Hilfesystem: Grundlegendes Frontend (Backbone + jQuery wär nice)--
8. Komponente: Titelleiste um Buttons erweitern (GenericUIC.js) Aufruf HS?
9. Hilfesystem: Frontend für Bedienung schreiben

=== bedienungshilfe fertig ===

10. Hilfesystem: Irgendwie an Kommunikationsmodell (Event Broker?) kommen, analysieren, Frontend für Kommunikation schreiben

=== kommunikationshilfe fertig ===

11. --DaRe: Kommentare Backend schreiben--
12. --DaRe: REST API für Kommentare--
13. Hilfesystem: Kommentar schreiben Frontend
14. Hilfesystem: Kommentar anzeigen Frontend

=== kommentare fertig ===


## TODO
### Integration
* GenericUIC.js erweitern für Standardtoolbar?
* Wie Aufruf, wenn Hilfesystem in Backbone geschrieben?

### Kommentare
* CommentBackend: Votes!
* CommentBackend: Was ist mit Arrays und Objekten beim Memento? Hab ich in meinem Key-Value Schema ursprünglich nicht vorgesehen. Variante 1: Values können wieder Key-Values sein (wie JSON). Variante 2: Arrays und Objekte werden als JSON String serialisiert und beim laden ge-eval()-t. Problem bei beiden ist, dass Infos verloren gehen, weil Regexes, functions und what not nicht serialisiert werden.
* CommentBackend: hasCommentId einfügen um Comments einzeln rauszuholen. Solange ich das nicht brauch: Nicht machen.
* CommentBackend: double statt float -.-
### Konzept
* Homogenität des Konzepts betonen (Aussehen, Bedienung, Metaphern…)
* Konzept: Wie gehe ich damit um, dass die Hilfe für Komponenten potenziell unterschiedliche Labels hat als was der Benutzer gerade sieht? Variante 1: Labels haben eigene CSS Klasse, die ich in der Hilfe auf "visibility:none" setze. Variante 2: Hilfe wird erst generiert, wenn der Benutzer Komponenten und Datensatz ausgewählt hat. --> verstecken
* Was wenn Komponenten selbst komposit? Eigentlich reichen mehrere visualization roots, oder?
* Wie ActivityActions Ontologie ansprechen? In der MCDL.owl ist die nicht importiert.
### Arbeit
* Bessere Listen

## Ausblick

* Bedienungshilfe mit Maus animieren
* Auswahlhilfen für Annotationsbereiche
* CSS von Komponente im CoRe auf relative Einheiten trimmen (schwierig weil man nicht weiß, was skaliert werden muss und was nicht)
* Aktionen abhängig von Aktionen (Suche -> Anzeige) wär auch gut, würde mehr High-Level erklärung ermöglichen