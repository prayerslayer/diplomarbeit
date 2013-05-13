# Diplomarbeit

My diploma thesis at Dresden University of Technology.

# Stuff to think about

* Beispiel generisches Barchart: Wie zur Laufzeit herausfinden, was auf den Achsen dargestellt wird?
* Beispiel generisches Barchart: Wie interaktionsversprechende Elemente kennzeichnen im MCDL? --> Über Capabilities und API, sodass dann .getInteractionElementsForCapability( capId ) ausgeführt werden kann
* Kommentare: Überlegen wie Darstellung von Kommentaren bei Relationen 1:n und n:1 sowie n:n zwischen DOM Element : Datenelement.
* Kommentare: Wie können Daten per Multiselections und Bereichsselektionen in Charts wie Karten, Scatterplots oder Linecharts markiert werden mit quasi null Aufwand für Entwickler? In Scatterplots mit eigenem Overlay und API, weil Relation DOM:Daten 1:n oder 1:1. In Linecharts ist die Relation n:1 (mehrere Datenpunkte in einer SVG Kurve), in Karten auch (mehere Datenpunkte in einer Kachel).
* Kommentare: Wie können Freihandmarkierungen abgespeichert werden, sodass sie einfach wiederherstellbar sind? Größtes Problem ist wohl die Skalierung.

# Anforderungen

Anforderungen an das Hilfesystem für komposite Informationsvisualisierungen. Das Hilfesystem besteht aus:
* Überblickshilfe
* Hilfe zur Bedienung einer Komponente
* Kommentare
* Hilfe zur Kommunikation zwischen Komponenten

## NF

* Korrektheit: Die Hilfestellung darf keine Fehlinformationen enthalten, ansonsten ist sie praktisch nutzlos weil sie verwirrt anstatt hilft.
* Vollständigkeit: Die Hilfestellung muss alle Informationen enthalten, die der Nutzer benötigt um danach seine gewünschte Aufgabe ausführen zu können.
* Verständlichkeit: Die Hilfestellung muss in einer Form präsentiert werden, die der Benutzer schnell und mit geringem mentalen Aufwand verarbeiten kann.
* Einheitlichkeit: Das Look & Feel von Teilen des Hilfesystems (z.B. Kommentare) muss komponentenübergreifend einheitlich sein.
* Minimalität: Das Hilfesystem soll dem Komponentenentwickler möglichst wenig Aufwand zumuten. Hier ist zu beachten, dass Aufwand in Form von zusätzlichem MCDL Markup geringer gewichtet wird als Aufwand in Form von zu implementierenden APIs.
* Universalität: Das Hilfesystem soll für alle Komponenten in gleicher Qualität funktionieren.

## F

* Überblick: Das Hilfesystem soll einen kurzen Überblick über das InfoVis-System geben und Darstellungsform sowie Inhalt jeder Komponente kurz erläutern.
* Bedienung: Das Hilfesystem soll erklären können, wie eine Komponente bedient wird. Diese Informationen umfassen welche Operationen (1) auf welchen DOM Elementen (2) welche Aktionen (3) (eventuell auf welchen Daten (3a)) ausführen. Zum Beispiel bei einer Tabelle den Spalten "Land" und "BIP": Mit einem **Linksklick** (1) auf den **Kopf der Spalte "BIP"** (2) wird die Tabelle **nach BIP** (3a) **sortiert** (3).
* Reporting: Fehler in Komponenten sollen über ein Reporting-System gemeldet werden können.
* Kommunikation: Das Hilfesystem soll erklären können, wie zwei gegebene Komponenten miteinander kommunizieren. Die notwendigen Informationen sind dieselben wie in *Bedienung*, aber komponentenübergreifend.
* Kommentare: Der Benutzer soll die Möglichkeit haben Daten zu kommentieren und Bereiche der Visualisierung zu markieren und mit ebenfalls mit einem Kommentar zu versehen, sodass auch auf fehlende Daten hingewiesen werden kann.
* Wiederverwendbarkeit: Die Kommentare sollen möglichst in allen Visualisierungen wiederverwendet werden, sodass alle etwas davon haben.

# Kommentare

Folgende Voraussetzungen sind gegeben:

1. Es ist notwendig, einen Bereich oder Elemente markieren zu können (damit klar ist, worauf sich der Kommentar bezieht).
2. Zusätzlich wäre es sehr schick, wenn die Kommentare an die Daten selbst drangehangen werden könnten, weil sie dann in anderen Visualisierungen auch hilfreich sein können.

Wie kriegt man das jetzt gebacken? Grundsätzlich gibt es zwei Möglichkeiten:
* **A**: Entweder man lässt die Komponente die Kommentare managen (Bereiche auswählen, pullen und anzeigen). Vorteil: Dev weiß am besten, wie Kommentare gehandelt werden sollten. Stichworte Hierarchie und dynamisches Erstellen von DOM Elementen. Nachteil: Viel Entwicklungs- und konzeptioneller Aufwand für Dev, einheitliches Styling und Interaktion wahrscheinlich nicht gegeben.
* **B**: Oder das Hilfesystem bildet ein Overlay über die Komponente, wo die Kommentare und Markierungen angezeigt werden. Vorteil: Kein Aufwand für Dev, einheitliches Styling und Interaktion gewährleistet. Nachteil: Wir kommen nicht an die Daten und das Overlay muss sich verschiedenen Zooms, Pans, Scrolls, Tabwechseln und what not anpassen.

1. Lösung: A wird bevorzugt, B als Fallback für den Fall, dass Dev keinen Bock hat die Kommentar-API zu implementieren. Nachteil: Devs sind faul und Hilfe uninteressant, deswegen stehen wir dann in 99 % der Fälle mit B da.
2. Lösung: Wir bringen die Vorteile von A und B zusammen. Das bedeutet wir haben grundsätzlich folgende Varianten zur Verfügung:
**Amin**: Eine kleinstmögliche API, die uns sagt welche Daten ausgewählt sind (sodass wir dort unsere Kommentare anhängen können) und welches DOM Element welches Datenelement repräsentiert (sodass wir dort unser Overlay anbringen können). Dev muss jetzt nicht mehr so viel implementieren, aber immer noch: Auswahl von Elementen muss klappen, Relation zwischen DOM Element und Daten muss bekannt sein. Nachteil: Die Lösung klappt sicher toll bei Listen und Tabellen, vielleicht auch Treemaps, wo recht einfach eine Selektion eingebaut werden kann. Aber was ist mit Karten? Oder Linecharts? Wie werden Multiselections und Bereichsselektionen umgesetzt? Sicher nicht immer mit denselben Interaktionen. Das kann man zwar umgehen indem man sich die daten-repräsentierenden DOM Elemente per API ausgeben lässt und Selektionen selbst managed. Bleiben die Karten. Und Line Charts. Oder Scatterplots.
**Bmax**: Wir finden irgendwie eine Möglichkeit, wie wir von einem Shape auf dem SVG/Canvas Overlay über der Komponente auf die Daten kommen. Ohne API. Klingt für mich nach zu viel Aufwand für zu wenig Erfolgsversprechen.