---
layout: page
title: Tutorials
nav: false
---

---
[Einleitung](/tutorials.html) &nbsp;&nbsp; Erste Schritte &nbsp;&nbsp; [Sprachsynthese](sprachsynthese.html) &nbsp;&nbsp; [Spracherkennung](spracherkennung.html) &nbsp;&nbsp; [Grammatiken](grammatiken.html) &nbsp;&nbsp; [Externe Programme](extprogramme.html)

---
&nbsp;
## Erste Schritte mit DialogOS

###  DialogOS starten

Um DialogOS starten zu können wird eine [Java Runtime](https://java.com/de/download/) benötigt. 
(Evtl. bald nicht mehr, ist TODO)


- Windows:  

über das DialogOS Icon [TODO Icon] auf dem Desktop

Es ist auch möglich DialogOS über die Kommandozeile zu starten. 
(Durch Windows-Suche mit Suchbegriff *Cmd* aufzufinden)
<br>
Dazu muss erst der Pfad in dem sich DialogOS befinden aufgerufen werden. 
(Kommando cd "Pfad zu DialogOS")
<br>
Durch das Kommando gradlew.bat run wird zuerst Gradle installiert, falls es benötigt wird
und anschließend DialogOS gestartet.
(Das kommt wahrscheinlich doch weg. Gradle soll nur zum builden gebraucht werden. TODO)




- Mac:  
TODO
- Linux:  
TODO

### Das Arbeitsfenster
Mit Klick auf *neuen Dialog erstellen* öffnet sich das Arbeitsfenster mit einem neuen, bis auf den Startknoten, noch leeren Dialog. Das Fenster besteht aus den folgenden vier Bereichen:
- **Arbeitsfläche**: befindet sich in der Mitte des Fensters. Diese dient der Beschreibung des Dialogs und ermöglicht das Verschieben, Verbinden und (durch ein Doppelklick auf einen Knoten) Konfigurieren von Dialogzuständen. 
- **Knotenleiste**: Menü am rechten Rand des Bildschirms mit allen verfügbaren Knotentypen. Diese lassen sich per Drag&Drop in die Arbeitsfläche ziehen.
- **Symbolleiste**: befindlich am oberen Rand des Fensters. Bietet Zugriff auf häufig benötigte Funktionen in DialogOS (ermöglicht z.B. den Abbruch eines laufenden Dialogs).
- **Prozedurliste**: Menü am linken Rand mit einer Liste aller Untergraphen (Teildialoge) -- es können mehrere Knoten zu einem eigenen (Teil-)Dialog zusammengefasst werden. 

### Speichern
Auch wenn es selbstverständlich sein sollte, möchten wir hier noch einmal auf die Wichtigkeit des häufigen Speicherns hinweisen. Wie immer beim programmieren solltet ihr möglichst häufig speichern, um euren Fortschritt nicht zu verlieren, falls das Programm abstürzen sollte. Das sollte nicht passieren, aber man weiß ja nie...

### Einen Dialog erstellen
Ein einfacher Dialog besteht erst einmal aus Spracheingabe und Sprachausgabe. Der Sprachausgabe-Knoten lässt den Computer etwas sagen, der Spracherkennungs-Knoten lässt ihn zuhören.

#### Sprachausgabe-Knoten
Um eine Sprachausgabe einzurichten, muss erst einmal per Drag&Drop einen Sprachausgabe-Knoten in den Dialog eingefügt werden. (Du findest diesen im Menü unten rechts.) Mit Doppelklick auf den soeben erstellten Sprachausgabe-Knoten öffnet sich ein neues Fenster. Wähle dort *Sprachausgabe* und füge in dem Feld *Ausgabe* den Text ein, den der Computer ausgeben soll. Mit *Anhören* kannst du die erstellte Sprachausgabe testen. Zum Schluss mit *OK* bestätigen.

#### Spracherkennungs-Knoten
Um eine Spracherkennung einzurichten, muss auch erst einmal per Drag&Drop einen Spracherkennungs-Knoten in den Dialog eingefügt werden. (Auch diesen findest du in der Knotenleiste.) Mit Doppelklick auf den soeben erstellten Spracherkennungs-Knoten öffnet sich ein neues Fenster. Wähle dort *Spracherkennung* und füge mit *Neu* in die Liste *Eingabemuster* neue Wörter / Sätze ein, die dein Programm erkennen können soll.  Wie auch schon bei der Sprachausgabe kannst du deine Einstellungen austesten (mit *Ausprobieren*) und mit *OK* bestätigen. DialogOS hat nun an den bearbeiteten Spracherkennungs-Knoten genau so viele Pfeile angefügt, wie du Möglichkeiten für die Erkennung vorgegeben habt. Verbleibt man eine kleine Weile mit dem Mauszeiger über einem dieser Ausgänge erscheint ein Tooltipp, welcher anzeigt, welchem Kommando dieser zugeordnet ist. 

Tipp: Keine ganzen Sätze vorgeben, denn diese müssen dann auch **exakt** wie vorgegeben gesagt werden, um erkannt zu werden. Besser sind ein oder zwei Wörter.

### Dialog Ausführen
Um aus den erstellten Spracherkennungs- und Sprachausgabe-Knoten einen Dialog zu formen, müssen diese in der richtigen Reihenfolge verbunden werden. Dies funktioniert durch Anklicken eines Ausgangspfeils eines Knotens und ziehen der entstehenden Kante auf einen beliebigen anderen Knoten. Füge nun noch ein *Ende* Symbol ein (wieder zu finden in der Knotenleiste). Achte darauf, alle Knoten, nach denen kein weiterer Dialog mehr folgt, mit dem *Ende* Symbol zu verbinden. Nun kannst du deinen Dialog mit einem Klick auf *Ausführen* ausprobieren (denk ans speichern!). 

Tipp: mit Headset klappt die Erkennung besser.

#### Dialog prüfen
Durch Auswählen des Menüpunktes *Graph* (oberhalb der Symbolleiste) und im folgenden Dropdown-Menü *Überprüfen*, kann der erstellte Dialog überprüft werden. Dadurch werden Fehler, welche zum Abbruch des Dialogs führen würden, gefunden und angezeigt (z.B. nicht verbundene Knoten oder ein fehlendes *Ende* Symbol).





