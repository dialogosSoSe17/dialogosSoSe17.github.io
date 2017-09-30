---
layout: page
title: Tutorials
nav: false
---

---
[Einleitung](/tutorials.html) &nbsp;&nbsp; [Erste Schritte](ersteschritte.html) &nbsp;&nbsp; [Sprachsynthese](sprachsynthese.html) &nbsp;&nbsp; Spracherkennung &nbsp;&nbsp; [Grammatiken](grammatiken.html) &nbsp;&nbsp;

---
&nbsp;
## Spracherkennung

DialogOS ist im Stande, jeden beliebigen Sprecher zu erkennen. Es muss zur Erkennung einer Stimme nicht erst auf eben diese trainiert werden (Voraussetzung hierfür ist natürlich eine klare und deutliche Aussprache).  
Da natürliche Sprache sehr komplex ist, muss jedoch, bis ins kleinste Detail, ganz genau angegeben werden, welche Wörter und Sätze, in welcher Dialogsituation, verstanden werden sollen. **Zuverlässig funktionieren kann die Spracherkennung erst durch eben diese Einschränkung des möglichen Vokabulars, auf eine konkrete Liste von Wörtern und Sätzen.**

Wurde ein Spracheingabe-Knoten zum Arbeitsbereich hinzugefügt, kann dieser mit einen Doppelklick bearbeitet werden. Durch Klick auf den Reiter *Spracherkennung*, kommt man zur Eingabe der zu erkennenden Sprachkommandos. 

Tipp: Wie in Erste Schritte erwähnt: Bei neu hinzugefügten Spracheingabe-Knoten werden anfangs keine Ausgangspfeile angezeigt. Diese sind von der Anzahl der zu erkennenden Sprachkommandos abhängig.

### Spracherkennung konfigurieren
Spracheingabe-Knoten benötigen zwei Dinge: Eine Liste von Eingabemustern (die Wörter und Sätze die erkannt werden sollen) und eine Grammatik, auf welche die Muster passen. 
Für einfache Kommandos reicht es bei *Grammatik* die Option *Automatisch aus den Mustern generieren* auszuwählen. (Mehr zu Grammatiken im Tutorial [Grammatiken](grammatiken.html) und in der [User-Documentation](/userdocumentation.html).) Nicht zu vergessen ist einzustellen, in welcher **Sprache** die Kommandos gesprochen werden sollen.
 
Um ein neues zu erkennendes Kommando einzutragen, muss zuerst bei *Eingabemuster* auf die Schaltfläche *Neu* geklickt werden. Dies fügt eine leere Zeile ein, in die jeweils ein Kommando (ein Wort oder Satz) eingetragen werden kann. Einfache Beispiele: "Ja", "Nein". Die Schaltfläche *Löschen* ermöglicht es, ausgewählte Kommandos zu entfernen. 

Kommandos müssen exakt so gesagt werden wie angegeben. "Ja", "Ja, bitte", "Ja, gerne" und alle anderen ähnlichen Wortkombinationen sind dementsprechend alle als unterschiedliche Kommandos anzusehen und müssen, wenn sie erkannt werden sollen, auch alle separat als Kommando eingetragen sein.

Tipp: Es kann die **Standardsprache** für die Spracheingabe umgestellt werden. Die Einstellungsmöglichkeit ist zu finden under *Dialog* (oberhalb der Symbolleiste), *Spracherkennung*. 

### Zur Laufzeit
Die Spracherkennung wird im laufe eines Dialogs immer nur dann aktiv, wenn ein Spracheingabe-Knoten erreicht wird. (Hierauf macht ein Fenster mit der Anmerkung "Spracherkennung aktiviert" aufmerksam.) Beim verlassen des Knotens wird sie wieder deaktiviert. Nur innerhalb dieses Zeitraums nimmt DialogOS eine Spracheingabe an.

In Abhängigkeit davon, welches der voreingestellten Kommandos erkannt wurde, wird der Dialog über den dazugehörigen Ausgangspfeil fortgesetzt.

### weitere Optionen
Spracheingabe-Knoten verfügen noch über einen weiteren Reiter *Optionen*. Hier wird die Möglichkeit angeboten, eine Zeitbegrenzung für die Spracheingabe vorzugeben. Die Angabe geschieht in Form von Millisekunden (1000 entspricht einer Sekunde). Durch die Aktivierung dieser Option erhält der Knoten einen zusätzlichen Ausgang, über den der Dialog im Falle einer Zeitüberschreitung fortgeführt wird. (z.B. mit einer Kante zu einem Sprachausgabe-Knoten, der den Text "Ihre Zeit ist abgelaufen" ausgibt.) 

