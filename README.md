# Diplomarbeit

My diploma thesis at Dresden University of Technology.

# TODO
* Howto Hilfe, manchmal erste zwei Panels falsch -> schwer reproduzierbar, passiert nur manchmal.
* umgang mit nominalen properties! -> array möglicher werte
* Pfade starten mit /assistanceImgs/, damit Frontend keine unnötigen Annahmen drüber machen muss
* Den Scale of Measurement Req wieder rausnehmen. Bei nominalen Attributen kommt einfach ein Array von möglichen Werten.
* Studie: Versteckte Funktion, transitive Verbindungen..? --> Nutzer verstehen (und besser) die Bedienung. Für Entwickler aufzeigen, wie unterschiedlich der Aufwand im Vergleich zu vorher bzw. ohne Assistance ist.
* Studie: SUS Fragebogen
* Testdaten
* Events pausieren während Hilfe! --> Martin sagte, das wär schon drin, is aber nicht? -> Gregor
* Assistance --> Timmah
	* Dataset ID
	* Label von DV
	* Originale Mappings
	* Visualized Properties müssen eine Kombination aus Datensatz ID, Klasse und Property sein. Und nicht vom generischen Datenschema, sondern von den Original URIs. Die bekomme ich über Tims Schnittstelle*, die Komponente lädt das Mapping dann bei der Initialisierung selbst.


## Arbeit
* Bessere Listen
* 3 Sachen: Bessere Bedienung für Nutzer, besseres Datenverständnis für Nutzer, weniger Entwicklungsaufwand für Dev
* Homogenität des Konzepts betonen (Aussehen, Bedienung, Metaphern…)
* Konzept: Wie gehe ich damit um, dass die Hilfe für Komponenten potenziell unterschiedliche Labels hat als was der Benutzer gerade sieht? Variante 1: Labels haben eigene CSS Klasse, die ich in der Hilfe auf "visibility:none" setze. Variante 2: Hilfe wird erst generiert, wenn der Benutzer Komponenten und Datensatz ausgewählt hat. --> verstecken
* Was wenn Komponenten selbst komposit? Eigentlich reichen mehrere visualization roots, oder?
* CSS Klassen --> Datenattribute, weil ich will ja keine CSS Styles drauf tun
* Überarbeiten wie Howto Hilfe aussieht, generiert wird etc.
* Überarbeiten wie Comment Backend arbeitet (Memento=JSON)
* Rechtfertigen warum ich nicht überall RDFa nehm

## Implementierung

**Zeit**: 14 Wochen ab 22.7.

Zuerst:

1. Szenario mit Komponenten überlegen
2. --Komponentenbeschreibung der Komponenten erstellen (wie in Konzept)--
3. --SVN Branch von allem erstellen, programmieren anfangen--

Implementierungsablauf:

1. --CoRe: Uploadprozess erweitern, dass er neue SMCDL lesen kann--
2. --CoRe: Neue SMCDL Daten in MCDO übertragen--
3. -Hilfeservice: Integration von MRE, DaRe und CoRe-
4. --Hilfeservice: Schnittstelle um Hilfegenerierung für Komponente anzustoßen--
5. --Hilfeservice: Hilfegenerierung--
6. --Hilfeservice: Schnittstelle um Hilfepanels auszugeben--
7. --Hilfesystem: Grundlegendes Frontend (Backbone + jQuery wär nice)--
8. --Komponente: Titelleiste um Buttons erweitern (GenericUIC.js) Aufruf HS?--
9. --Hilfesystem: Frontend für Bedienung schreiben--

=== bedienungshilfe fertig ===

10. Hilfesystem: Irgendwie an Kommunikationsmodell (Event Broker?) kommen, analysieren, Frontend für Kommunikation schreiben

=== kommunikationshilfe fertig ===

11. --DaRe: Kommentare Backend schreiben--
12. --DaRe: REST API für Kommentare--
13. --Hilfesystem: Kommentar schreiben Frontend--
14. --Hilfesystem: Kommentar anzeigen Frontend--

=== kommentare fertig ===

## Einschränkungen

### Howto
* Hintergrund setzen funktioniert nur, wenns wirklich am "obersten" Div klappt. Wenn drunter was den background überschreibt, krieg ich das nicht mit.
* Hintergrund kann nicht abgedunkelt werden, wenn ein relevantes Element viewportfüllend ist - ist halt so.
* Problem wenn das Seitenverhältnis des Elements nicht annähernd quadratisch, aber riesengroß ist. Siehe timeline-band

## Ausblick

* Legende gleich bei Integration angeben
* Bedienungshilfe mit Maus animieren
* Auswahlhilfen für Annotationsbereiche
* CSS von Komponente im CoRe auf relative Einheiten trimmen (schwierig weil man nicht weiß, was skaliert werden muss und was nicht)
* Aktionen abhängig von Aktionen (Suche -> Anzeige) wär auch gut, würde mehr High-Level erklärung ermöglichen

# Checkliste
* Schreibweise von zusammgesetzten Wörtern: Javabibliothek, Java Bibliothek oder Java-Bibliothek? Was mit Akronymen (VISO, HTTP…)? VISO Operation oder VISO-Operation? HTTP Request oder HTTP-Request?
* Möglichst Aktiv statt Passiv verwenden.
* Immer brav zurück referenzieren wenn möglich.
* Referenzen schön und einheitlich. Vornamen abkürzen, DOIs raus.
