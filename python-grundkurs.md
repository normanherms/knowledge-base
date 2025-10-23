# Python Grundkurs

---

## Anmerkung

Dieses Cheatbook basiert auf dem von ChatGPT (GPT-5) erstellten Python-Grundkurs.
Es dokumentiert die Lerninhalte und Übungen der Module 1.0 bis 1.5 in fortlaufender, praxisnaher Form.
Die Aufzeichnungen, Beispiele und Erklärungen wurden während des Lernprozesses automatisch erstellt und anschließend geglättet.
Ziel ist eine klare, nachvollziehbare Darstellung der Python-Grundlagen – nicht nur als Befehlsliste, sondern als erklärendes Nachschlagewerk mit Kontext und Struktur.

---

## Einführung

* Universelle, interpretierte Programmiersprache
* Plattformunabhängig (Linux, macOS, Windows)
* Dynamisch typisiert (keine explizite Typdeklaration nötig)
* Große Standardbibliothek, aktive Community
* Ideal für Einsteiger und produktive Nutzung

**Anwendungsbereiche:**

* Automatisierung und Scripting (z. B. Systemaufgaben)
* Webentwicklung (Django, Flask)
* Datenanalyse & Machine Learning (pandas, NumPy, scikit-learn)
* DevOps & Infrastruktur (Ansible, Terraform-Integration)
* KI & neuronale Netze (PyTorch, TensorFlow)

**Ziel des Cheatbooks:**

* Grundlagen verstehen und anwenden
* Python strukturiert und praxisnah lernen
* Codebeispiele auf jedem System direkt lauffähig

---

## Modulübersicht

| Modul | Thema                              |
| ----- | ---------------------------------- |
| 1.0   | Setup & Syntaxbasis                |
| 1.1   | Variablen & Datentypen             |
| 1.2   | Operatoren & Ausdrücke             |
| 1.3   | Benutzerinteraktion (`input`)      |
| 1.4   | Bedingungen (`if`, `elif`, `else`) |
| 1.5   | Schleifen (`for`, `while`)         |
| 1.6   | Funktionen & Modularisierung       |
| 1.7   | Dateien lesen/schreiben            |
| 1.8   | Mini-Projekt: Konsolen-Tool        |

---

## Modul 1.0 – Setup & Syntaxbasis

Ziel: Python-Umgebung erstellen, erstes Programm ausführen und grundlegende Syntax verstehen.

**Begriffe:**

* Interpreter: führt Code Zeile für Zeile aus
* venv: virtuelle Umgebung, um Abhängigkeiten getrennt zu halten
* print(): gibt Text oder Werte auf der Konsole aus

**Beispiel:**

```bash
mkdir ~/projects/python-grundkurs
cd ~/projects/python-grundkurs
python3 -m venv venv
source venv/bin/activate
code .
```

Datei `main.py`:

```python
print("Python läuft! Willkommen im Grundkurs.")
```

---

## Modul 1.1 – Variablen & Datentypen

**Kernkonzept:** Variablen speichern Werte. Python erkennt den Typ automatisch. Variablen sind Namen, die auf Werte im Speicher zeigen. Sie können jederzeit überschrieben oder neu zugewiesen werden.

```python
name = "Norman"
alter = 40
größe = 1.76
geschlecht = "männlich"

print(f"Ich heiße {name} und bin {alter} Jahre alt.")
print(f"Ich bin {größe} m groß und {geschlecht}.")
```

**Grundtypen:**

* str: Zeichenkette
* int: Ganzzahl
* float: Gleitkommazahl
* bool: Wahrheitswert (True, False)

**Typabfrage:**

```python
print(type(name))
```

**Typkonvertierung:**

```python
alter_text = str(alter)
zahl = int("10")
```

**Formatierung:**

`f"Text {variable}"` ermöglicht lesbare, direkte Ausgabe.

---

## Modul 1.2 – Operatoren & Ausdrücke

**Ziel:**
Verstehen, wie Python Werte miteinander verrechnet, vergleicht und kombiniert.
Ein Ausdruck ist dabei **jede Anweisung, die zu einem Wert führt** – z. B. `3 + 4` oder `a > b`.

---

### 1. Arithmetische Operatoren

Verwenden wir zum Rechnen mit Zahlen (int oder float).

| Operator | Bedeutung                       | Beispiel | Ergebnis |
| -------- | ------------------------------- | -------- | -------- |
| `+`      | Addition                        | `3 + 2`  | `5`      |
| `-`      | Subtraktion                     | `5 - 2`  | `3`      |
| `*`      | Multiplikation                  | `4 * 3`  | `12`     |
| `/`      | Division (mit Nachkommastellen) | `5 / 2`  | `2.5`    |
| `//`     | Ganzzahl-Division               | `5 // 2` | `2`      |
| `%`      | Modulo (Restwert)               | `5 % 2`  | `1`      |
| `**`     | Potenzierung                    | `2 ** 3` | `8`      |

**Merke:**

* `/` gibt immer ein **float** zurück.
* `//` teilt und rundet **nach unten** auf eine ganze Zahl.
* `%` ist nützlich, um gerade/ungerade Werte zu prüfen (`x % 2 == 0`).
* `**` wird in mathematischen Berechnungen häufig für Quadrate oder Exponenten verwendet.

---

### 2. Vergleichsoperatoren

Diese liefern **boolesche Werte** (`True` oder `False`).

| Operator | Bedeutung           | Beispiel | Ergebnis |
| -------- | ------------------- | -------- | -------- |
| `==`     | Gleich              | `3 == 3` | `True`   |
| `!=`     | Ungleich            | `4 != 5` | `True`   |
| `<`      | Kleiner als         | `2 < 5`  | `True`   |
| `>`      | Größer als          | `7 > 9`  | `False`  |
| `<=`     | Kleiner oder gleich | `5 <= 5` | `True`   |
| `>=`     | Größer oder gleich  | `6 >= 3` | `True`   |

**Beispiel:**

```python
alter = 20
print(alter >= 18)  # True
```

**Merke:**
Vergleiche werden in der Regel für Entscheidungsstrukturen (`if`) oder Logikabfragen verwendet.

---

### 3. Logische Operatoren

Kombinieren mehrere Bedingungen.

| Operator | Bedeutung                      | Beispiel                      | Ergebnis |
| -------- | ------------------------------ | ----------------------------- | -------- |
| `and`    | beide müssen wahr sein         | `(alter > 18 and alter < 30)` | True     |
| `or`     | mindestens eine Bedingung wahr | `(alter < 18 or alter > 65)`  | False    |
| `not`    | kehrt Wahrheitswert um         | `not True`                    | False    |

**Beispiel:**

```python
temperatur = 22
regnet = False

if temperatur > 20 and not regnet:
    print("Perfektes Wetter!")
```

---

### 4. Funktion round()

Rundet numerische Ergebnisse.

```python
ergebnis = 10 / 3
print(round(ergebnis, 2))  # 3.33
```

**Syntax:** `round(wert, stellen)`

* `stellen` = Anzahl der Nachkommastellen
* Wenn kein zweiter Parameter angegeben wird, rundet Python auf die nächste ganze Zahl.

---

### 5. Kurzüberblick

* Operatoren verknüpfen Werte oder Variablen.
* Ausdrücke erzeugen neue Werte.
* Das Ergebnis eines Ausdrucks kann sofort weiterverwendet oder gespeichert werden.

**Beispiel:**

```python
a = 5
b = 2
summe = a + b
print(summe > 5 and summe < 10)
```

→ Ausgabe: `True`

---

## Modul 1.3 – Benutzerinteraktion mit input()

**Ziel:**
Programme sollen auf Eingaben des Benutzers reagieren und diese weiterverarbeiten.

---

### 1. Funktionsweise

`input()` pausiert das Programm und wartet, bis der Benutzer etwas eingibt und mit Enter bestätigt.
Der eingegebene Text wird **immer als Zeichenkette (str)** zurückgegeben.

**Beispiel:**

```python
name = input("Wie heißt du? ")
print(f"Hallo {name}, willkommen im Kurs!")
```

**Ablauf:**

1. Das Programm zeigt die Frage an.
2. Der Benutzer gibt Text ein (z. B. „Lisa“).
3. Die Eingabe wird als String gespeichert.

---

### 2. Typumwandlung

Da `input()` immer Text liefert, musst du bei Zahlen **explizit umwandeln**, wenn du mit ihnen rechnen möchtest.

```python
alter = int(input("Wie alt bist du? "))
print(f"In 10 Jahren bist du {alter + 10} Jahre alt.")
```

**Typische Umwandlungen:**

* `int()` für ganze Zahlen (z. B. Alter, Stückzahl)
* `float()` für Kommazahlen (z. B. Temperatur, Preis)
* `str()` nur selten nötig, weil `input()` ohnehin String liefert

---

### 3. Beispielprogramm

```python
Name = input("Wie heißt du? ")
Alter = input("Wie alt bist du? ")
Wohnort = input("Wo wohnst du? ")

print(f"Mein Name ist {Name}, ich bin {Alter} Jahre alt und wohne in {Wohnort}.")
```

> **Hinweis:**
> Dieses Beispiel nutzt nur Textverarbeitung – keine Berechnungen.
> Darum bleibt alles vom Typ `str`.

---

### 4. Merksätze

* `input()` → wartet auf Eingabe, Rückgabe immer `str`
* Typwandlung nur, wenn du mit Zahlen arbeitest
* `print()` → Ausgabe, `input()` → Eingabe
* Fehlende Umwandlung führt bei Rechenoperationen zu Fehlern oder falscher Verkettung

---

## Modul 1.4 – Bedingungen (if, elif, else)

**Ziel:**
Programmabläufe steuern und Entscheidungen treffen.
Bedingungen sind das Herzstück der Logik in Python – sie bestimmen, **welcher Code ausgeführt wird** und welcher nicht.

---

### 1. Grundprinzip

```python
alter = 20

if alter < 18:
    print("Du bist minderjährig.")
elif alter < 65:
    print("Du bist erwachsen.")
else:
    print("Du bist im Ruhestand.")
```

**Ablauf:**

1. Die erste `if`-Bedingung wird geprüft.
2. Wenn sie **True** ist, wird der Block ausgeführt und alle weiteren übersprungen.
3. Wenn sie **False** ist, prüft Python die nächste (`elif`).
4. Wenn keine Bedingung zutrifft, läuft der `else`-Block.

---

### 2. Syntaxregeln

* Einrückung (vier Leerzeichen oder ein Tab) ist Pflicht.
* Nur der eingerückte Code gehört zur Bedingung.
* Die Blöcke müssen **in der richtigen Reihenfolge** stehen (`if` → `elif` → `else`).
* Ein `else` ist optional, aber empfehlenswert, um alle Fälle abzudecken.

---

### 3. Logische Kombinationen

Mehrere Bedingungen können miteinander verknüpft werden.

```python
temperatur = 22
regnet = False

if temperatur > 20 and not regnet:
    print("Perfektes Wetter!")
else:
    print("Bleib lieber drin.")
```

**Erklärung:**

* `and` → beide Bedingungen müssen wahr sein
* `or` → mindestens eine muss wahr sein
* `not` → kehrt den Wahrheitswert um

---

### 4. Bereichsprüfungen

Mit Vergleichsoperatoren kannst du auch Bereiche abfragen.

```python
temp = float(input("Temperatur: "))

if temp < 18:
    print("Heizung an")
elif temp >= 18 and temp <= 24:
    print("Alles in Ordnung")
else:
    print("Fenster auf")
```

---

### 5. Kurzform (Ternäre Bedingung)

Eine kompakte Schreibweise für einfache Entscheidungen.

```python
alter = 17
status = "volljährig" if alter >= 18 else "minderjährig"
print(status)
```

**Struktur:**
`variable = wert_wenn_true if bedingung else wert_wenn_false`

Diese Form eignet sich gut für einfache Zuweisungen, aber nicht für lange Logik.

---

### 6. Bedeutung der Schlüsselwörter

| Schlüsselwort | Bedeutung  | Beschreibung                                               |
| ------------- | ---------- | ---------------------------------------------------------- |
| `if`          | wenn       | prüft eine Bedingung einmal                                |
| `elif`        | sonst wenn | prüft eine weitere Bedingung, falls die erste nicht zutraf |
| `else`        | ansonsten  | wird ausgeführt, wenn keine Bedingung wahr ist             |

`if` steht also für **Entscheidung**, nicht für Wiederholung.
Schleifen wie `while` oder `for` folgen in Modul 1.5.

---

### 7. Merksätze

* Bedingungen steuern den Ablauf deines Programms.
* Nur der **erste zutreffende Block** wird ausgeführt.
* Einrückung ist syntaktisch zwingend.
* Logische Operatoren (`and`, `or`, `not`) können kombiniert werden.
* `elif` ist die Kurzform von *else if*.

---

## Modul 1.5 – Schleifen (for, while)

**Ziel:**
Wiederkehrende Abläufe automatisieren und kontrolliert wiederholen.

---

### 1. for-Schleife (vorwärts zählen)

> Wird verwendet, wenn die Anzahl der Durchläufe bekannt ist.

```python
for x in range(1, 11):
    print(x)
```

* `range(1, 11)` erzeugt die Werte 1 bis 10.
* `x` nimmt nacheinander jeden Wert an.
* Der eingerückte Code läuft bei jedem Durchlauf einmal.

---

### 2. while-Schleife (rückwärts zählen)

> Wird verwendet, wenn die Wiederholungen dynamisch sind oder von einer Bedingung abhängen.

```python
x = 10

while x > 0:
    print(x)
    x -= 1

print("Fertig.")
```

* Die Schleife läuft, solange die Bedingung `x > 0` wahr ist.
* `x -= 1` reduziert den Zähler bei jedem Durchlauf.
* Wenn `x` 0 erreicht, endet die Schleife.

---

### 3. break und continue

**break:** Beendet eine Schleife sofort, auch wenn die Bedingung noch wahr ist.

```python
for i in range(10):
    if i == 5:
        break
    print(i)
```

**continue:** Überspringt den aktuellen Durchlauf und springt zum nächsten.

```python
for i in range(6):
    if i == 3:
        continue
    print(i)
```

---

### 4. Vergleich for vs while

| Schleifenart | Verwendung                             | Bedingung                      | Beispiel            |
| ------------ | -------------------------------------- | ------------------------------ | ------------------- |
| `for`        | feste Anzahl an Wiederholungen         | vordefiniert (z. B. `range()`) | `for i in range(5)` |
| `while`      | unklare oder dynamische Wiederholungen | prüft fortlaufend              | `while x < 10`      |

---

### 5. Merksätze

* `for` → feste Wiederholungen
* `while` → prüft fortlaufend bis Bedingung False wird
* `break` → Schleife sofort beenden
* `continue` → nächsten Durchlauf starten
* Schleifen können ineinander geschachtelt werden
* Einrückung ist auch hier zwingend

---

## Zwischenquests um Wissen zu festigen

### Projekt: Bot

**Ziel:**
Schrittweiser Aufbau eines eigenen Konsolen-Bots.
Der Bot wächst mit jedem Modul und verbindet alle Grundlagen zu einem funktionierenden Programm.
Jede Aufgabe nutzt ausschließlich das Wissen des jeweiligen Moduls.

---

### Modul 1.0 – Begrüßung

Der Bot soll den Benutzer begrüßen.
Er gibt erste Ausgaben auf der Konsole aus.

---

### Modul 1.1 – Identität

Der Bot stellt sich vor.
Er besitzt eigene Daten wie Name, Version und Herkunft.

---

### Modul 1.2 – Rechenfähigkeit

Der Bot kann einfache Berechnungen ausführen.
Er verwendet Operatoren und zeigt das Ergebnis an.

---

### Modul 1.3 – Kommunikation

Der Bot fragt den Benutzer nach Informationen.
Eingaben werden gelesen und in Antworten integriert.

---

### Modul 1.4 – Entscheidungen

Der Bot bewertet Eingaben logisch.
Er reagiert situationsabhängig und gibt passende Rückmeldungen.

---

### Modul 1.5 – Kontrolle

Der Bot kann Gespräche wiederholen oder beenden.
Er entscheidet selbst, wann das Programm endet.

---

### Endziel

Am Ende des Grundkurses entsteht ein vollständiger, eigenständiger Konsolen-Bot mit
Eingabe, Verarbeitung, Entscheidung und Wiederholung.

---

### Ergebnis der Quest

```python
version = "v0.3"
print()
print("Hallo ich bin dein persönlicher Bot.")
print(f"Ich bin ein Prototyp in Version: {version} ")
name= input("Wie heißt du? ")
print()
print(f"Hallo {name} wie kann ich dir helfen?")
print()
print("Ich kann zum Beispiel Berechnungen durchführen.")
print("Möchtest du es versuchen?")
versuch = input("Ja oder Nein?").lower()
while versuch == "ja":
    print("Super, gib mir 2 Zahlen und einen Operator, sowas wie +,-,* oder /: ")
    x = float(input("Die erste Zahl lautet?: "))
    Operator = input("Was möchtest du rechnen? Zulässig ist +, -, * und /: ")
    y = float(input("Die zweite Zahl lautet?: "))
    if Operator == "+":
        Ergebnis = x+y
        print(f"Dein Ergebnis der Addition ist: {Ergebnis}")
    elif Operator == "-":
        Ergebnis = x-y
        print(f"Dein Ergebnis der Subtraktion ist: {Ergebnis} ")
    elif Operator == "*":
        Ergebnis = x*y
        print(f"Dein Ergebnis der Multiplikation ist: {Ergebnis} ")
    elif Operator == "/":
        Ergebnis = x/y
        print(f"Dein Ergebnis der Division ist: {Ergebnis} ")
    else:
        print("Das ist kein gültiger Operator")
    versuch = input("Möchtest du noch mal rechnen? ").lower()
else:
    print("Was wollen wir stattdessen machen?")
    print("Zur Auswahl steht aktuell......leider nichts. Tschüß.")
```

---

## Modul 1.6 – Funktionen & Modularisierung

**Ziel:**
Strukturierung von Programmen durch wiederverwendbare Codebausteine.
Funktionen ermöglichen es, Aufgaben zu kapseln, mehrfach zu verwenden und Programme übersichtlicher zu gestalten.

---

### 1. Grundprinzipien

Eine Funktion ist ein benannter Codeblock, der nur ausgeführt wird, wenn er aufgerufen wird.

```python
def funktionsname(parameter):
    # auszuführender Code
    return ergebnis
```

* **def**: leitet die Funktionsdefinition ein
* **parameter**: Eingabewerte, die in der Funktion genutzt werden können
* **return**: gibt ein Ergebnis zurück (optional)

**Beispiel:**

```python
def addiere(a, b):
    return a + b

summe = addiere(3, 4)
print(summe)
```

Ergebnis: `7`

---

### 2. Parameter und Argumente

Parameter sind Platzhalter für Werte, die beim Aufruf übergeben werden.
Die übergebenen Werte heißen Argumente.

```python
def begruessung(name):
    print(f"Hallo {name}")

begruessung("Norman")
```

---

### 3. Lokale und globale Variablen

* **Lokal:** innerhalb der Funktion definiert, nur dort gültig
* **Global:** außerhalb definiert, überall im Programm sichtbar

**Beispiel:**

```python
x = 10  # global

def verdopple(y):  # lokal
    return y * 2

print(verdopple(x))
```

---

### 4. Funktionen in mehreren Dateien nutzen

Funktionen können in eigene Dateien ausgelagert werden.
So entsteht eine modulare Struktur mit klar getrennten Aufgabenbereichen.

**Datei:** `funktionen.py`

```python
def addiere(a, b):
    return a + b
```

**Datei:** `main.py`

```python
import funktionen

ergebnis = funktionen.addiere(5, 7)
print(ergebnis)
```

Mit `import` können eigene Module oder externe Bibliotheken eingebunden werden.

---

### 5. Vorteile der Modularisierung

| Vorteil                  | Beschreibung                                                    |
| ------------------------ | --------------------------------------------------------------- |
| **Wiederverwendbarkeit** | Einmal definierte Funktionen können beliebig oft genutzt werden |
| **Struktur & Übersicht** | Programme bleiben lesbar und klar gegliedert                    |
| **Fehlerreduktion**      | Änderungen betreffen nur einzelne Module                        |
| **Testbarkeit**          | Funktionen können isoliert getestet werden                      |

---

### 6. Best Practices

* Eine Funktion sollte **genau eine Aufgabe** erfüllen.
* Namen sollten beschreiben, **was** die Funktion tut (z. B. `berechne_summe`, nicht `doStuff`).
* Funktionen möglichst **kurz und eigenständig** halten.
* Keine unkontrollierte Nutzung globaler Variablen.
* Rückgabewerte (`return`) nutzen, statt direkt in der Funktion zu drucken.

---

### 7. Zusammenfassung

Funktionen sind das Herz modularer Programme.
Sie teilen komplexe Aufgaben in kleine, verständliche Blöcke auf und ermöglichen:

* strukturierte Programmierung
* Wiederverwendung von Code
* bessere Wartbarkeit und Testbarkeit
* Grundlage für größere Projekte mit mehreren Modulen

---

##

## Endquest um Wissen weiter zu festigen

### Phase 2 – Von Skript zu Tool

| Modul   | Thema                        | Ziel                                          |
| ------- | ---------------------------- | --------------------------------------------- |
| **1.6** | Funktionen & Modularisierung | Logik in wiederverwendbare Bausteine zerlegen |
| **1.7** | Dateien lesen/schreiben      | Daten extern speichern und abrufen            |
| **1.8** | Mini-Projekt: Konsolen-Tool  | Eigenständiges, nützliches CLI-Programm bauen |

---

### Modul 1.6 Funktionen & Modularisierung

**Ziel:**
Den bestehenden Bot in klar getrennte Funktionsblöcke zerlegen.
Jeder Abschnitt des Codes bekommt eine eigene Aufgabe, z. B.:

* `begrüßung()`
* `rechnen()`
* `wiederholen()`
* `verabschiedung()`

**Lerninhalte:**

* Parameter und Rückgabewerte verstehen
* Lokale vs. globale Variablen unterscheiden
* Code wiederverwenden und testen können
* Einstieg in strukturierte Programmierung

---

### Modul 1.7 – Dateien lesen und schreiben

**Ziel:**
Der Bot kann Informationen speichern und wieder abrufen.
Beispielsweise:

* Protokoll der letzten Berechnungen
* Namen der Benutzer
* Einfache Konfigurationen (z. B. Standardname oder Version)

**Lerninhalte:**

* Dateioperationen mit `open()`, `read()`, `write()`
* Dateimodi (`'r'`, `'w'`, `'a'`) und ihre Unterschiede
* Fehlerbehandlung mit `try/except`
* Arbeit mit Textdateien (`.txt`, `.log`)

---

### Modul 1.8 – Mini-Projekt: Konsolen-Tool

**Ziel:**
Ein vollständiges, eigenständiges Programm mit klarer Struktur erstellen.

**Beispielideen:**

* Ein Rechner mit Protokollfunktion
* Ein Aufgaben-Tracker
* Ein kleiner CLI-Assistent für Alltag oder System

**Lerninhalte:**

* Aufteilung in mehrere `.py`-Dateien (Module)
* Einstiegspunkt mit `if __name__ == "__main__":`
* Fehler- und Eingabeprüfung
* Nutzbarkeit über Terminal
* Optionale Erweiterung: einfache Menüführung

---
