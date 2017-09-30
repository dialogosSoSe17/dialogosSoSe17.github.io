---
layout: page
title: Tutorials
nav: false
---

---
[Einleitung](/tutorials.html) &nbsp;&nbsp; Erste Schritte &nbsp;&nbsp; [Sprachsynthese](sprachsynthese.html) &nbsp;&nbsp; [Spracherkennung](spracherkennung.html) &nbsp;&nbsp; [Grammatiken](grammatiken.html) &nbsp;&nbsp;

---
&nbsp;
## Erste Schritte mit DialogOS

###  DialogOS starten

Um den Installer und DialogOS starten zu können wird eine [Java Runtime](https://java.com/de/download/) benötigt. 

Nach erfolgreicher Installation von Java, dem Download des [DialogOS Installers](/download.html) 
und der Installation von DialogOS, kann das Programm durch Doppelklick auf die Datei *dialogos-all.jar*
im Installationspfad gestartet werden.
Wurde während der Installation ein DialogOS-Icon auf dem Desktop und/oder ein Eintrag im Startmenü erstellt, kann DialogOS auch 
mithilfe dieser gestartet werden.


### Das Arbeitsfenster
Mit Klick auf *neuen Dialog erstellen* öffnet sich das Arbeitsfenster mit einem neuen, bis auf den Startknoten, noch leeren Dialog. Das Fenster besteht aus den folgenden vier Bereichen:
- **Arbeitsfläche**: befindet sich in der Mitte des Fensters. Diese dient der Beschreibung des Dialogs und ermöglicht das Verschieben, Verbinden und (durch ein Doppelklick auf einen Knoten) Konfigurieren von Dialogzuständen. 
- **Knotenleiste**: Menü am rechten Rand des Bildschirms mit allen verfügbaren Knotentypen. Diese lassen sich per Drag&Drop in die Arbeitsfläche ziehen.
- **Symbolleiste**: befindlich am oberen Rand des Fensters. Bietet Zugriff auf häufig benötigte Funktionen in DialogOS (ermöglicht z.B. den Abbruch eines laufenden Dialogs).
- **Prozedurliste**: Menü am linken Rand mit einer Liste aller Untergraphen (Teildialoge) -- es können mehrere Knoten zu einem eigenen (Teil-)Dialog zusammengefasst werden. 

### Speichern
Auch wenn es selbstverständlich sein sollte, möchten wir hier noch einmal auf die Wichtigkeit des häufigen Speicherns hinweisen. Wie immer beim Programmieren solltet ihr möglichst häufig speichern, um euren Fortschritt nicht zu verlieren, falls das Programm abstürzen sollte. Das sollte nicht passieren, aber man weiß ja nie...

### Einen Dialog erstellen
Ein einfacher Dialog besteht erst einmal aus Spracheingabe und Sprachausgabe. Der Sprachausgabe-Knoten lässt den Computer etwas sagen, der Spracherkennungs-Knoten lässt ihn zuhören.

#### Sprachausgabe-Knoten
Um eine Sprachausgabe einzurichten, muss erst einmal per Drag&Drop ein Sprachausgabe-Knoten in den Dialog eingefügt werden. (Ihr findet diesen im Menü unten rechts.) 
Mit Doppelklick auf den soeben erstellten Sprachausgabe-Knoten öffnet sich ein neues Fenster. 
Dort muss *Sprachausgabe* ausgewählt und dann in dem Feld *Ausgabe* der Text eingegeben werden, den der Computer ausgeben soll. Mit *Anhören* könnt ihr die erstellte Sprachausgabe testen. Zum Schluss mit *OK* bestätigen.

#### Spracherkennungs-Knoten
Um eine Spracherkennung einzurichten, muss auch erst einmal per Drag&Drop ein Spracherkennungs-Knoten in den Dialog eingefügt werden. 
(Auch diesen findet ihr in der Knotenleiste.) Mit Doppelklick auf den soeben erstellten Spracherkennungs-Knoten öffnet sich ein neues Fenster. 
Wählt dort *Spracherkennung* und fügt mit *Neu* in die Liste *Eingabemuster* neue Wörter / Sätze ein, die das Programm erkennen können soll.  
Wie auch schon bei der Sprachausgabe können die Einstellungen getestet werden (mit *Ausprobieren*). Anschließend mit *OK* bestätigen. 
DialogOS hat nun an dem bearbeiteten Spracherkennungs-Knoten genau so viele Pfeile angefügt, wie Möglichkeiten für die Erkennung vorgegeben 
wurden. Verbleibt man eine kleine Weile mit dem Mauszeiger über einem dieser Ausgänge erscheint ein Tooltipp, welcher anzeigt welchem Kommando 
dieser zugeordnet ist. 

Tipp: Keine ganzen Sätze vorgeben, denn diese müssen dann auch **exakt** wie vorgegeben gesagt werden, um erkannt zu werden. Besser sind ein oder zwei Wörter.

### Dialog ausführen
Um aus den erstellten Spracherkennungs- und Sprachausgabe-Knoten einen Dialog zu formen, müssen diese in der richtigen Reihenfolge verbunden werden.
 Dies funktioniert durch Anklicken eines Ausgangspfeils eines Knotens und ziehen der entstehenden Kante auf einen beliebigen anderen Knoten. 
 Fügt nun noch ein *Ende* Symbol ein (wieder zu finden in der Knotenleiste). Wieder gelöscht werden können Kanten außerdem durch einfaches Anklicken der unerwünschten
 Kante und das Drücken der Entfernen-Taste.
 Achtet darauf, alle Knoten, nach denen kein weiterer Dialog mehr folgt, mit dem *Ende* Symbol zu verbinden. 
 Nun kann der Dialog mit einem Klick auf *Ausführen* ausprobiert werden. (Denkt ans Speichern!). 

Tipp: mit Headset klappt die Erkennung besser.

#### Dialog prüfen
Durch Auswählen des Menüpunktes *Graph* (oberhalb der Symbolleiste) und im folgenden Dropdown-Menü *Überprüfen*, kann der erstellte Dialog überprüft werden. 
Dadurch werden Fehler, welche zum Abbruch des Dialogs führen würden, gefunden und angezeigt (z.B. nicht verbundene Knoten oder ein fehlendes *Ende* Symbol).





