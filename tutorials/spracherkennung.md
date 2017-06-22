---
layout: page
---
# Tutorials
---
[Einleitung](/tutorials.html) &nbsp;&nbsp; [Erste Schritte](ersteschritte.html) &nbsp;&nbsp; [Sprachsynthese](sprachsynthese.html) &nbsp;&nbsp; Spracherkennung &nbsp;&nbsp; [Grammatiken](grammatiken.html) &nbsp;&nbsp; [Externe Programme](extprogramme.html)

---
&nbsp;
## Spracherkennung

DialogOS ist im Stande, jeden beliebigen Sprecher zu erkennen. Es muss zur Erkennung einer Stimme nicht erst auf eben diese trainiert werden (Voraussetzung hierfür ist natürlich eine klare und deutliche Aussprache).  
Da natürliche Sprache sehr komplex ist, muss jedoch, bis ins kleinste Detail, ganz genau angegeben werden, welche Wörter und Sätze, in welcher Dialogsituation, verstanden werden sollen. **Zuverlässig funktionieren kann die Spracherkennung erst durch eben diese Einschränkung des möglichen Vokabulars, auf eine konkrete Liste von Wörtern und Sätzen.**

<!--
(wie schon zuvor erwähnt: Bei neu hinzugefügten Spracheingabe-Knoten werden anfangs keine Ausgangspfeile angezeigt, da diese von der Anzahl der zu erkennenden Sprachkommandos abhängen.) 
-->

Wurde ein Sprachausgabe-Knoten zum Arbeitsbereich hinzugefügt, kann dieser mit einen Doppelklick bearbeitet werden. Durch Klick auf den Reiter *Spracherkennung*, kommt man zur Eingabe der zu erkennenden Aussagen. [TODO *Kommandos durch Aussagen ersetzt - so lassen?*]

### Spracherkennung konfigurieren
Spracheingabe-Knoten benötigen zwei Dinge: Eine Liste von Eingabemustern (die Wörter und Sätze die erkannt werden sollen) und eine Grammatik, auf welche die Muster passen. 
Für einfache Kommandos reicht es bei *Grammatik* die Option *Automatisch aus den Mustern generieren* auszuwählen. (Mehr zu Grammatiken im Tutorial [Grammatiken](grammatiken.html) und im Handbuch [TODO *Link*].) Nicht zu vergessen ist einzustellen, in welcher **Sprache** die Kommandos gesprochen werden sollen.
 
Um ein neues zu erkennendes Kommando einzutragen, muss zuerst unter *Eingabemuster* auf die Schaltfläche *Neu* geklickt werden [TODO *Reiter oder Überschschrift? Diese Info fehlt unter erste schritte - nach dort verschieben?*]. Dies fügt eine leere Zeile ein, in die jeweils ein Kommando (ein Wort oder Satz) eingetragen werden kann. Einfache Beispiele: "Ja", "Nein". Die Schaltfläche *Löschen* ermöglicht es, ausgewählte Kommandos zu entfernen. 

Kommandos müssen exakt so gesagt werden wie angegeben. "Ja", "Ja, bitte", "Ja, gerne" und alle anderen ähnlichen Wortkombinationen sind dementsprechend alle als unterschiedliche Kommandos anzusehen und müssen, wenn sie erkannt werden sollen, auch alle separat als Kommando eingetragen sein.

Tipp: Es kann eine **Standardsprache** für die Spracheingabe eingestellt werden. Die Einstellungsmöglichkeit ist zu finden under *Dialog* (oberhalb der Symbolleiste), *Spracherkennung*. [TODO *muss eine eingestellt werden? was wenn nicht?*]

### Zur Laufzeit
Die Spracherkennung wird im laufe eines Dialogs immer nur dann aktiv, wenn ein Spracheingabe-Knoten erreicht wird. (Hierauf macht ein Fenster mit der Anmerkung "Spracherkennung aktiviert" aufmerksam.) Beim verlassen des Knotens wird sie wieder deaktiviert. Nur innerhalb dieses Zeitraums nimmt DialogOS eine Spracheingabe an.

In Abhängigkeit davon, welches der voreingestellten Kommando erkannt wurde, wird der Dialog am dazugehörigen Knoten fortgesetzt (von dem zum erkannten Kommando gehörenden "Ausgangspfeil" über die gezogenen Kante zum verbundenen Knoten). [TODO *Text in klammern nötig?*]

### weitere Optionen
Spracheingabe-Knoten verfügen noch über einen weiteren Reiter *Optionen*. Hier wird die Möglichkeit angeboten, eine Zeitbegrenzung für die Spracheingabe vorzugeben. Die Angabe geschieht in Form von Millisekunden (1000 entspricht einer Sekunde). Durch die Aktivierung dieser Option erhält der Knoten einen zusätzlichen Ausgang, über den der Dialog im Falle einer Zeitüberschreitung fortgeführt wird. (z.B. mit einer Kante zu einem Sprachausgabe-Knoten, der den Text "Ihre Zeit ist abgelaufen" ausgibt.) 

