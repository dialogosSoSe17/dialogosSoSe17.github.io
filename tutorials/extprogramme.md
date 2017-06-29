---
layout: page
title:
---
# Tutorials
---
[Einleitung](/tutorials.html) &nbsp;&nbsp; [Erste Schritte](ersteschritte.html) &nbsp;&nbsp; [Sprachsynthese](sprachsynthese.html) &nbsp;&nbsp; [Spracherkennung](spracherkennung.html) &nbsp;&nbsp; [Grammatiken](grammatiken.html) &nbsp;&nbsp; Externe Programme

---
&nbsp;
## Externe Programme

[TODO *stimmt das alles (noch)?*]

DialogOS kann mit beliebig vielen -- in Java geschriebenen -- Programmen kommunizieren. Z.B. mit Geräten für Texteingabe und -ausgabe, mit Datenbanken, mit Treibersoftware für zu steuernde Maschinen... Diese können sowohl Eingabemedium für den Dialog sein als auch ausgegebene Kommandos empfangen. [TODO *Nur Java?*]

Informationen, die mit den externen Geräten ausgetauscht werden können, sind Werte der Skriptsprache von DialogOS (`bool`, `int`, `real`, `string`, `list`, `struct`). Wie die gesendeten Werte interpretiert werden und welche Antwort ggf. zurückgesendet wird, hängt dabei von der Art des externen Gerätes ab. In jedem Fall muss der Dialog in DialogOS die Kommunikation initiieren. 

Die benötigten externen Programme müssen immer vor Start des Dialogs gestartet werden, da DialogOS direkt zu Beginn eines Dialogs versucht, die Verbindung zum externen Programm herzustellen, um im Dialogverlauf Nachrichten austauschen zu können. Die Verbindung wird mit Ende des Dialogs wieder getrennt.

### Externe Programme anbinden
Im Menü *Dialog* unter dem Punkt *Geräte* können externe Geräte/Module hinzugefügt und bearbeitet werden.
Durch Klick auf *Neu* kann ein neues externes Gerät hinzugefügt werden. In dem sich anschließend öffnenden Fenster muss ein Name für das Gerät festgelegt werden und ein Connector, der festlegt wie die Verbindung zwischen DialogOS und dem externen Gerät aufgebaut wird. 
Man hat die Wahl zwischen "CLT Connector (Fixed Server)" , "CLT Connector (Rendezvous)" und "CLT Connector (Internal)". Empfehlenswert ist der "CLT Connector (Rendezvous)". Dieser kann vollautomatisch im Netzwerk nach verfügbaren Modulen suchen, vorausgesetzt das im Feld *Service Name* der eingegebene Name mit dem Namen des externen Modul übereinstimmt.

Angesteuert werden die externen Module innerhalb eines Dialogs in DialogOS über eigene Knotentypen. Diese können in beliebiger Reihenfolge beliebig oft eingebunden werden.

#### Ausgabe-Knoten
Ein Ausgabe-Knoten ermöglicht das Senden von Kommandos an externe Geräte/Module (auch gleichzeitig an mehrere Geräte).

Im Reiter *Ausgabe* werden links die verfügbaren externen Geräte/Module, zwischen denen gewählt werden kann, und rechts die für jedes hinzugefügte Gerät/Modul auszutauschenden Ausdrücke angezeigt. Durch Klick auf *Neu* können weitere Ausdrücke hinzugefügt werden. Diese werden sequentiell abgearbeitet. Um die Reihenfolge der Ausdrücke zu ändern, reicht ein einfaches Drag&Drop.

Im Reiter *Optionen* können außerdem noch, falls gewünscht, folgende  Optionen aktiviert werden:
* *Geräte erst zurücksetzen*: noch laufende Ausgaben werden abgebrochen, bevor Ausgaben des aktuellen Knotens gesendet werden  
und / oder  
* *Warten bis die Ausgabe abgeschlossen ist*: synchronisiert Dialogfluss mit tatsächlicher Ausgabedauer

Wird im Dialogablauf ein Ausgabe-Knoten erreicht, schickt DialogOS die entsprechende Mitteilung als Skript-Ausdruck an das gewählte Programm

#### Eingabe-Knoten
Eingabe-Knoten dienen der Verarbeitung von eingehenden Nachrichten externer Geräte. Sie fungieren jedoch gleichzeitig auch als Ausgabe-Knoten. Wird ein Eingabe-Knoten erreicht, so kann zunächst eine Ausgabe von DialogOS an das gewählte Programm geschickt werden. Dieses errechnet dann das benötigte Ergebnis und schickt es zurück, damit es in DialogOS als Eingabe weiterverarbeitet werden kann.

Im Reiter *Eingabe* können durch Klick auf *Neu* Erkennungsmuster hinzugefügt werden. Diese nutzt der Knoten bei Ausführung, um Werte von externen Geräten/Modulen mit diesen zu vergleichen. Pro Muster hat der Knoten ein eigenen Ausgang. Wie schon beim Ausgabeknoten werden auch hier die Muster sequentiell abgearbeitet. Das erste Muster welches zur Laufzeit auf eine Eingabe passt, wird ausgewählt. Passt keines, wird die Eingabe ignoriert, und es wird auf die nächse Eingabe gewartet. Es empfiehlt sich deshalb als letztes Muster `_` anzugeben, da dieses auf jede Eingabe passt. Oder alternativ die Option *Eine Kante für alle anderen Werte einfügen* zu aktivieren.
 
Im Reiter *Optionen* finden sich die selben Optionen wie in den Ausgabe-Knoten, sowie zusätzlich noch die folgenden: 
* Eine Auswahl zwischen allen, oder spezifischen Geräten: falls nicht die Eingaben aller Geräte berücksichtigt werden sollen
* *Bisherige Eingabe verwerfen*: falls Einträge in der Eingabeschlange gelöscht werden sollen
* *Globale Eingabebehandlung deaktivieren* (siehe Handbuch)[TODO *Link*] [TODO *Kurzform?*]
* *Zeitbegrenzung in ms*: zusätzliche Kante für Zeitüberschreitung
* *Barge-In*: erlaubt eine Eingabe zu tätigen, während
die Ausgabe noch bearbeitet wird, falls Spracheingabe und Sprachausgabe durch externe Geräte realisiert werden

Weiterführendes zur Anbindung externer Programme, den Knoten und zu globaler Eingabebehandlung im DialogOS Handbuch. [TODO *Link*]




