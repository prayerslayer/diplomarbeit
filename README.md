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

## Anmerkungen Martin 28.6.

* Heer2008 in die verwandten Arbeiten
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