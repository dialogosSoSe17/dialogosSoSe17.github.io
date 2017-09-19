---
layout: page
title: Tutorials
nav: false
---

---
[Einleitung](/tutorials.html) &nbsp;&nbsp; [Erste Schritte](ersteschritte.html) &nbsp;&nbsp; [Sprachsynthese](sprachsynthese.html) &nbsp;&nbsp; [Spracherkennung](spracherkennung.html) &nbsp;&nbsp; Grammatiken &nbsp;&nbsp; [Externe Programme](extprogramme.html)

---
&nbsp;
## Grammatiken

TODO Einleitung

### Variablen
Mit steigender Komplexität von Dialogabläufen kann es nützlich sein -- oder sogar notwendig werden -- sich im Dialog etwas zu merken, um später darauf zugreifen zu können. Dies ermöglicht DialogOS durch Nutzung von Variablen.

Der Datentyp einer Variable beschreibt, welche Informationen in ihr gespeichert werden können. Unterstützt werden durch DialogOS folgende Datentypen:
* `bool` : Wahrheitswert (true, false)
* `int` : ganzzahliger Wert (z.B. 4, -21) 
* `real` : realer Zahlenwert (z.B. 6.0, -5.27) 
* `string` : Zeichenkette / Text, mit doppelten Anführungszeichen (z.B. "Hallo")
* `list` : Liste von Daten, mit eckigen Klammern und durch Kommas getrennt (z.B. [0, 1, 2])
* `struct` : Liste von Daten, bei der jedes Element eine eigene Bezeichnug hat (name = wert), mit geschweiften Klammern und durch Kommas getrennt (z.B.  {eins = 1, zwei = 2})  
Weiterführende Informationen zu den Datentypen in der [User-Documentation](/userdocumentation.html).

#### Variablen definieren
Bevor eine Variable genutzt werden kann, muss sie definiert werden. Dazu im Menü *Graph* den Befehl *Variable* klicken. (Alternativ durch Rechtsklick auf die Arbeitsfläche und anschließenden Linksklick auf *Variable*.) Anschließend im sich öffnenden Fenster durch Klick auf *Neu* eine neue Variable erstellen und mit Name, Typ und Wert versehen. 

#### Beispiel
Um DialogOS z.B. eine ganze Zahl aus einer Variable aussprechen zu lassen, muss wie folgt vorgegangen werden: 
* Eine Variable mit Namen (z.B. meineZahl), Typ `int` und einem ganzzahligen Wert (z.B. 5) anlegen. 
* Einen Sprachausgabe-Knoten in die Arbeitsfläche einfügen, bei diesem im Reiter *Sprachausgabe* den Ausgabe-Typ auf *Ausdruck* setzen. Im Ausdruckfeld darunter folgenden Ausdruck eingeben: &nbsp;`"Das Ergebnis ist" + meineZahl`

Dieser Ausdruck führt nun dazu, dass DialogOS bei Ausführung des Dialogs "Das Ergebnis ist" und im Anschluß den Wert der Variable meineZahl sagt. 

### Grammatiken
Wollen wir DialogOS z.B. eine gesprochene Ziffer erkennen lassen, welche es dann in einer vorher definierten Variable speichern soll, benötigen wir Grammatiken.

Eine Grammatik ist eine Menge formaler Regeln, die beschreibt, welche Äußerungen an einem Spracheingabe-Knoten möglich sind. Vorteil von Grammatiken gegenüber einfachen Spracherkennungsmustern ist, dass sie komplexere Beschreibungen der Äußerungen ermöglichen und universell verfügbar sind, also an mehreren Spracherkennungs-Knoten genutzt werden können.

#### Grammatik erstellen / bearbeiten
Um eine neue Grammatik zu erstellen oder vorhandene zu verändern oder zu löschen, klickt man im Menü *Graph* auf den Menüpunkt *Grammatiken*. (Alternativ durch Rechtsklick auf die Arbeitsfläche und anschließenden Linksklick auf *Grammatiken*.) Daraufhin öffnet sich ein Fenster, welches die vorhandenen Grammatiken anzeigt. In diesem Fenster kann durch Klick auf *Neu* eine neue Grammatik erstellt werden. Dadurch öffnet sich wiederrum ein weiteres Fester, in welchem im sog. Kopf der Grammatik der Name eingegeben wird und im sog. Rumpf (das große weiße Feld darunter) die Regeln der Grammatik.

#### Beispiel 1
Für die Spracherkennung mit anschließendem abspeichern von z.B. ganzen Zahlen (0-9) muss zu allererst eine zugehörige Grammatik erstellt werden (z.B. mit dem Namen "ziffern"). In den Rumpf muss exakt das Folgende:

```
language "Deutsch";
root $zahl;
$zahl = $ziffer { $ = parseInt($ziffer); };
$ziffer = "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" ;
```

Zunächst steht dort, dass der Spracherkenner Deutsch erkennen soll. Mit `root $zahl` wird `$zahl` als Standardregel bestimmt. `$ziffer` ist eine Grammatikregel, die die möglichen Ziffern (0-9) angibt. `$zahl` wandelt die Ziffer (mit `parseInt`) in eine Zahl um. Dies ist nötig, weil in `$ziffer` auch etwas anderes als eine Zahl drinstehen könnte (theoretisch).

In jeder Grammatik wird genau eine Grundregel `root` benötigt. `$` Zeichen deuten auf eine Regel hin und befinden sich immer vor dem Regelnamen. Darauf folgt immer ein `=` Zeichen mit der sog. Expansion der Regel. Das `|` Zeichen (oder) dient dem trennen alternativer Aussagen. Mehr zu komplexeren Grammatiken und weitere Beispiele finden sich in der [User-Documentation](/userdocumentation.html).

Um nun eine ganze Zahl durch den Computer erkennen zu lassen, muss folgendes getan werden: 
* Ein Spracherkennungs-Knoten zur Arbeitsfläche hinzufügen und im Reiter *Spracherkennung* unter *Grammatik* die neu erstellte Grammatik *ziffern* auswählen. 
* Unter *Eingabemuster* "meineZahl" eingeben (durch vorheriges Klicken auf *Neu*).
* Den gerade erstellten Spracherkennungs-Knoten im Dialog-Ablauf zwischen dem Start- und Sprachausgabe-Knoten einfügen (Kanten anpassen). 
* Jetzt kann die Spracherkennung eine Ziffer erkennen und diese in der vorher erstellten Variable "meineZahl" abspeichern.

Nun kann, wenn der Dialog gestartet wird, eine Zahl von 0-9 gesprochen werden, die DialogOS im Anschluss wiederholt.
(Damit größere Zahlen als 9 verstanden werden können muss die `$ziffer` Regel in der ziffern-Grammatik um weitere Alternativen erweitert werden: ..."10" | "11" | "12" | "13" usw.)

#### Beispiel 2
Soll DialogOS darüber hinaus auch rechnen können (z.B. Addition), wird eine etwas aufwendigere Grammatik benötigt. Neben Ziffern muss DialogOS auch Operatoren erkennen und wissen, was diese bedeuten (z.B. dass das Wort "plus" auf Deutsch Addition bedeutet).

Dazu erstellt man eine neue Grammatik (z.B. mit dem Namen "rechnen", die wie folgt aussieht:

```
language "Deutsch";
root $rechnen;
$rechnen = ($zahlA plus $ZahlB) { $ = $zahlA + $zahlB; };
$zahlA = $ziffer { $ = parseInt($ziffer); };
$zahlB = $ziffer { $ = parseInt($ziffer); };
$ziffer = "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" ;
```

Diese Grammatik ist gegenüber der vorherigen um die Regel `$rechnen` erweitert. Diese erlaubt zunächt Muster der Art `(zahl plus zahl)` zu verstehen, wobei die Zahlen aus den unter `$ziffer` festgelegten Ziffern bestehen müssen. Anschließend steht in der geschweiften Klammer in 
`$rechnen`, dass das Ergebnis von `$rechnen` die Addition der beiden Zahlen sein soll.

Um den Dialog lauffähig zu bekommen, muss wieder ein Spracherkennungs-Knoten zum Dialog hinzugefügt und zwischen Start-Knoten und Sprachausgabe eingefügt werden (anstatt des vorherigen). Bei diesem muss als Grammatik die neuerstellte Grammatik "rechnen" ausgewählt und als Ausgabe wieder "meineZahl" eingegeben werden.

### Weiteres
Anstelle des in diesem Tutorial vorgestellten DialogOS eigenen Skript-Codes, kann zum Schreiben von Grammatiken auch Groovy genutzt werden. Informationen zur Nutzung von Groovy findest du in der [User Documetation](/userdocumentation/groovy).  
Weitere Möglichkeiten, wie komplexe Datentypen oder Funktionen, in der [User-Documentation](/userdocumentation.html). 

