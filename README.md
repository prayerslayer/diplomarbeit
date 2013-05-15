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
**Amin**: Eine kleinstmögliche API, die uns sagt welche Daten ausgewählt sind (sodass wir dort unsere Kommentare anhängen können) und welches DOM Element welches Datenelement repräsentiert (sodass wir dort unser Overlay anbringen können).  Klappt relativ super, wenn wir an existierenden Datenpunkten kommentieren wollen. Wie aber Markierungen so umsetzen, dass sie visualisierungsunabhängig funktionieren und einfach + zuverlässig wiederhergestellt werden können?
**Bmax**: Wir finden irgendwie eine Möglichkeit, wie wir von einem Shape auf dem SVG/Canvas Overlay über der Komponente auf die Daten kommen. Ohne API. Klingt für mich nach zu viel Aufwand für zu wenig Erfolgsversprechen.

Die Frage ist nun, wie wir zu einer zufriedenstellenden, universalen **Amin** kommen. Dazu nehmen wir die Visualisierungen in Heer2010 her, klassifizieren sie anhand Keim2002 und überlegen uns was.

Faktoren:
* Ob Daten durch Komponente aggregiert werden oder nicht, weil wenn ja kann mans sich sparen an Originaldaten kommentieren zu wollen.
* Anzahl der Dimensionen der Daten. D = { 1, 2, 3 ..} **Warum noch mal wichtig?**
* Achsen der Visualisierung? zB Abweichung von Gaussverteilung. Ist relevant wenn man an die Daten selbst annotieren will.
* Visualisierungstyp: Standard, Karte (Projektion!?), Mixed… **Warum noch mal wichtig?**
* Visualisierungsverhalten: statisch, dynamisch. Bei dynamischen Visualisierungen, wo ständig neue Daten reingeladen werden zB neueste Tweets von @XY, brauch ich keine Bereiche markieren. Ändert sich ja eh in den nächsten 2 Sekunden.
* Ob Visualisierung idempotent ist, d.h. liefern bei zwei unterschiedlichen Anzeigen derselben Daten das exakt gleiche Ergebnis? Eine Treemap ist es, nehme ich an, aber Force Layout gar nicht. Hängt vom **Layoutalgorithmus** ab.
* Sich ändernde Daten - wird das berücksichtigt? Wenn ja, dann muss ich irgendwie noch einen Hash als Checksumme einbauen. Selber Hash = selbe Daten = okay einen Kommentar anzuzeigen.

**API**
Im Prinzip ein Memento nach Gamma2001. Die Komponente definiert selbst, wie es aussieht. Ob das jetzt nur ein Tupel (X, Y) oder (X, Y, S, R) oder ein String oder whatever ist, ist mir egal. Wichtig ist, dass ich mit getMemento() ein Memento m bekomme und mit setMemento(m) den Zustand wiederherstellen kann. 

**Problem**: Unterschiedliche Viewportgröße bei der Wiederherstellung. Die sollte wohl auch abgespeichert werden, sodass später entsprechend skaliert werden kann.

* Memento, Grenzen markierten Bereichs, Viewportgröße zusammen mit Kommentardaten ablegen
* Zusätzlich optional Transformationsfunktionen Koordinaten -> Daten und Daten -> Koordinaten, optional weil evtl viel Aufwand. Nötig um Bereich direkt in Daten kommentieren zu können. "Direkt in Daten" geht halt nicht bei uns weil alles Tripel sind. Deswegen eigenes Kommentar-Tripel, was sagt auf welchen Achsen welcher Bereich kommentiert wurde. **Kriegen wir das in 100 % der Fälle raus?**
* Was selektiert ist mit data-vizboard-selected=true markuppen
* URI von Daten mit data-vizboard-uri markuppen
* Die Visualisierung selbst mit data-vizboard-vizroot markuppen, hier kommt das Overlay drüber
* Was muss jetzt definitiv in die MCDL? -> Ob Komponente aggregiert (performsAggregation), ob Komponente dynamisch Daten lädt (loadsDynamicData), ob Komponente idempotentes Layout hat (isLayoutIdempotent), wie das Memento aussieht.
* Wie funktioniert die Wiederherstellung eines Kommentars? -> Kommentaranzeige wird getoggelt. Wenn ja, wird über jedem DOM Element mit data-vizboard-uri die entsprechende Anzahl an Kommentaren angezeigt. Mit Klick drauf werden die Kommentare geladen. Bei Bereichen wird ein Overlay über data-vizboard-vizroot erstellt und dort entsprechend den gespeicherten Koordinaten - auf neue Komponentengröße skaliert - draufgemalt.

## Index Charts
*Daten*: 2-dimensional (Zeit + Wert)
*Visualisierung*: Standard 2D
*Interaktion*: Panning

Ausgewählte Daten kriegt man mit entsprechendem Markup (data-vizboard-selected, data-vizboard-uri) an den DOM Elementen raus.

Jetzt mal davon ausgehend, dass das Linien SVG Elemente sind. Man würde sich den aktuellen Zustand (Monat) abspeichern wollen und dann einen Bereich mit Koordinaten auswählen und markieren. Dieser Bereich zusammen mit dem Monat würde mit Kommentardaten abgelegt.

Um Kommentare wiederverwendbar zu machen, würde die Komponente idealerweise noch XY Koordinaten in Punkte auf den tatsächlich dargestellten Dimensionen konvertieren können. Also beispielsweise (100, 75) entspricht (März 2004, 125 %).

## Stacked Graphs
*Daten*: 2-dimensional (Zeit + Aggregat)
*Visualisierung*: Stacked display
*Interaktion*: Browsing (Umschalten)

Same wie bei Index Charts. Außer dass wegen dem Aggregat nicht an die Daten selbst kommentiert werden kann (weil sie aggregiert wurden und nicht mehr auseinandergenommen werden können, duh).

## Small Multiples
*Daten*: 2-dimensional (Zeit + Aggregat)
*Visualisierung*: Multiple Standard 2D
*Interaktion*: keine visualisierungsverändernde

Stacked Graphs auseinandergenommen und parallel dargestellt. Wegen Aggregat kann wiederum nicht an Originaldaten kommentiert werden - außer Aggregate SIND Originaldaten.

## Horizon Graph
*Daten*: 2-dimensional (Zeit + Wert)
*Visualisierung*: Standard 2D - sort of
*Interaktion*: Browsing

Siehe Index Chart.

## Stem & Leaf Plots
*Daten*: 1-dimensional (Werte)
*Visualisierung*: Standard 2D - sort of
*Interaktion*: Keine

Siehe Index Chart, aber es gibt keine Transformation (x,y) in Werte der Dimensionen. X/Y bleibt X/Y.

## Q-Q Plots
*Daten*: 2-dimensional (Werte + Abweichung von Verteilung)
*Visualisierung*: Standard 2D
*Interaktion*: Browsing

Siehe Index Chart. Problem aber: Die Dimensionen des Charts entsprechen keinen Dimensionen in den Daten. Verteilung + Abweichung davon ist nicht im Datensatz. Deswegen kann man hier auch keinen Bereich in den Daten kommentieren. Außer man definiert sich halt Verteilungen.

## Scatter Plot Matrix
*Daten*: Multidimensional
*Visualisierung*: Geometrically transformed
*Interaktion*: Linking & Brushing

Ausgewählte Daten würde man leicht mit ein bisschen Markup (data-vizboard-selected, data-vizboard-uri) rauskriegen. Ansonsten siehe Index Chart.

## Parallel Coordinates
*Daten*: Multidimensional
*Visualisierung*: Geometrically transformed
*Interaktion*: Linking & Brushing

Same wie Scatter Plot Matrix.

## Flow Map
*Daten*: Multidimensional (Richtung, Anzahl, von, nach, …)
*Visualisierung*: Special 2D
*Interaktion*: Pan & Zoom

Siehe Index Chart, aber wie man an einzelne Datenpunkte kommen soll, ist mir nicht ganz klar. Weil ich nicht weiß, wie die Daten überhaupt aussehen.

## Choropleth Maps
*Daten*: 2-dimensional (Bundesstaat + Wert)
*Visualisierung*: Special 2D
*Interaktion*: Browsing

Eigentlich wie Index Charts.

## Graduated Symbol Maps
*Daten*: Multidimensional (Bundesstaat + Bevölkerung + % Normal + % Overweight + % Obese)
*Visualisierung*: Special 2D + Iconic display
*Interaktion*: Browsing

Siehe Index Chart.

## Cartogram
*Daten*: Multidimensional (Bundesstaat + Position + Bevölkerung + % Obese)
*Visualisierung*: Geometrically transformed
*Interaktion*: Browsing

Siehe Index Chart.

## Node-Link Diagram
Hier gibt es mehrere Möglichkeiten.

### Baum
*Daten*: Hierarchie
*Visualisierung*: Standard 2D (?)
*Interaktion*: Keine

Siehe Index Chart.

### Radial
*Daten*: Hierarchie
*Visualisierung*: Standard 2D (?)
*Interaktion*: Keine

Siehe Index Chart. Layoutalgorithmus? --> X/Y <-> Daten

### Indented Tree
*Daten*: Hierarchie
*Visualisierung*: Standard 2D
*Interaktion*: Keine

Siehe Index Chart.

### Adjacency Diagram
*Daten*: Hierarchie + 1-dimensional (Größe)
*Visualisierung*: Stacked
*Interaktion*: Keine

Siehe Index Chart, möglicherweise keine X/Y <-> Daten Transformation.

### Sunburst
*Daten*: Hierarchie + 1-dimensional (Größe)
*Visualisierung*: Stacked
*Interaktion*: Keine

Siehe Index Chart, aber keine X/Y <-> Daten Transformation.

### Enclosure Diagram
*Daten*: Hierarchie + 1-dimensional (Größe)
*Visualisierung*: Stacked
*Interaktion*: Keine

Siehe Index Chart, aber keine X/Y <-> Daten Transformation.

### Nested Circles
*Daten*: Hierarchie + 1-dimensional (Größe)
*Visualisierung*: Stacked
*Interaktion*: Keine

Keine X/Y <-> Daten Transformation

## Force-Directed Network
*Daten*: Netzwerk mit gewichteten Kanten
*Visualisierung*: Standard 2D
*Interaktion*: Pan, Zoom, Verschieben

Hier würde es gar nicht gehen, weil das Layout nicht vorhersehbar ist. Eine Möglichkeit: Checken, welche Elemente sich im ausgewählten Bereich befinden und ihn so definieren. In einer späteren Visualisierung würden es halt mehrere Bereiche sein. Nachteil: Was eigentlich interessant war, ist vermutlich _so_ nicht mehr sichtbar, weswegen man sich den Kommentar ohnehin schenken kann.

## Arc Diagram
*Daten*: Netzwerk
*Visualisierung*: Standard 2D
*Interaktion*: Keine

Wieder die Frage nach dem Layoutalgorithmus. Sonst wie Index Chart.

## Matrix View
*Daten*: Netzwerk
*Visualisierung*: Standard 2D
*Interaktion*: Keine

Wie Index Chart eigentlich.

## Was fehlt

Tja, gute Frage. Histogramme. Bar Charts. Stacked Bar Charts. Dendrogramme, sind aber wie Bäume. Listen. Tabellen.

## Timeline
                 A       B   C      D E 
         - - - - / - - - / - / - - -/ / - - -
*Daten*: 2-dimensional (Jahr + Beschreibung zB)
*Visualisierung*: Standard 1D
*Interaktion*: Zoom, Pan

Wie Index Chart.

### 3-dimensionale Visualisierungen

Standard 3D Plot, 3D Netzwerke… Lasse ich erstmal raus weil sie auch noch nicht so häufig sind im Web (obwohl sich das mit der Verbreitung von WebGL ändern wird). Das Prinzip wäre dasselbe. Voraussetzungen: Statische Visualisierung und Komponente macht Properties öffentlich, mit der ein Zustand wiederhergestellt werden kann.