# Diplomarbeit

My diploma thesis at Dresden University of Technology.

# TODO
* CoRe, DaRe, TSR, Models Ordner auf CD
* Quellen umbenennen für CD
* CD am Ende nicht vergessen!
* Gregor fragen wegen Event Broker
* URLs der Dependencies auf localhost:8080 umstellen - nach demo, weil ich hab keinen bock die auf meinem rechner zu hostne
* Alles in SVN trunk, Dokumentation schreiben

## Arbeit
* Schreibweise von zusammgesetzten Wörtern:Java Bibliothek oder Java-Bibliothek? Was mit Akronymen (VISO, HTTP…)? VISO Operation oder VISO-Operation? HTTP Request oder HTTP-Request?
* Möglichst Aktiv statt Passiv verwenden.
* Immer brav zurück referenzieren wenn möglich.
* Bessere Listen
* 3 Sachen: Bessere Bedienung für Nutzer, besseres Datenverständnis für Nutzer, weniger Entwicklungsaufwand für Dev
* Homogenität des Konzepts betonen (Aussehen, Bedienung, Metaphern…)
* Konzept: Wie gehe ich damit um, dass die Hilfe für Komponenten potenziell unterschiedliche Labels hat als was der Benutzer gerade sieht? Variante 1: Labels haben eigene CSS Klasse, die ich in der Hilfe auf "visibility:none" setze. Variante 2: Hilfe wird erst generiert, wenn der Benutzer Komponenten und Datensatz ausgewählt hat. --> verstecken
* Was wenn Komponenten selbst komposit? Eigentlich reichen mehrere visualization roots, oder?

## Einschränkungen

### Howto
* Hintergrund setzen funktioniert nur, wenns wirklich am "obersten" Div klappt. Wenn drunter was den background überschreibt, krieg ich das nicht mit.
* Hintergrund kann nicht abgedunkelt werden, wenn ein relevantes Element viewportfüllend ist - ist halt so.
* Problem wenn das Seitenverhältnis des Elements nicht annähernd quadratisch, aber riesengroß ist. Siehe timeline-band
* Problem, wenn vor eigentlicher Operation eine andere durchgeführt werden muss, die aber nicht Teil der Aktion ist. Konkret war das bei der Tabelle der Fall, wo man auf einen Spaltenheader klicken sollte, der gerade nicht sichtbar war. Da muss man zuerst nach rechts scrollen, das ist aber nicht immer so.
* Drag ist irgendwie implementierungsabhängig.

## Ausblick

* Legende gleich bei Integration angeben
* Bedienungshilfe mit Maus animieren
* Auswahlhilfen für Annotationsbereiche
* CSS von Komponente im CoRe auf relative Einheiten trimmen (schwierig weil man nicht weiß, was skaliert werden muss und was nicht)
* Aktionen abhängig von Aktionen (Suche -> Anzeige) wär auch gut, würde mehr High-Level erklärung ermöglichen

