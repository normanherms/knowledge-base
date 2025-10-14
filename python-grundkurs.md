# Python Grundkurs

---

## Anmerkung

Dies ist ein persönliches Cheatbook.
Es dient als Nachschlagewerk für meine eigenen Lerninhalte im Rahmen des Python-Grundkurses.
Die Inhalte wurden teilweise mit Unterstützung von ChatGPT geglättet und erweitert.
Auch wenn ich auf Richtigkeit achte, können Fehler enthalten sein.
Es dient nicht nur als Befehlsübersicht, sondern als erklärendes Nachschlagewerk mit Beispielen, Kontext und Praxisbezug.

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

**Kernkonzept:** Variablen speichern Werte. Python erkennt den Typ automatisch.

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

**Ziel:** Mit Variablen rechnen und logische Vergleiche durchführen.

```python
a = 3
b = 4

print(f"Addition: {a + b}")
print(f"Subtraktion: {a - b}")
print(f"Multiplikation: {a * b}")
print(f"Division: {round(a / b, 1)}")
```

**Arithmetische Operatoren:** +  -  *  /  //  %  **

**Vergleiche:** ==  !=  <  >  <=  >=

**Logik:** and  or  not

**Beispiel:**

```python
alter = 20
print(alter > 18 and alter < 30)  # True
```

**Funktion round():** rundet numerische Ergebnisse auf definierte Nachkommastellen.

---

## Modul 1.3 – Benutzerinteraktion mit input()

**Ziel:** Programme reagieren auf Nutzereingaben.

**Grundlage:**

```python
name = input("Wie heißt du? ")
print(f"Hallo {name}, willkommen im Kurs!")
```

**Datentypen beachten:**

* Alle Eingaben von input() sind vom Typ str
* Wenn du rechnen willst, musst du umwandeln

```python
alter = int(input("Wie alt bist du? "))
print(f"In 10 Jahren bist du {alter + 10} Jahre alt.")
```

**Beispiel:**

```python
Name = input("Wie heißt du? ")
Alter = input(str("Wie alt bist du? "))
Wohnort = input("Wo wohnst du? ")

print(f"Mein Name ist {Name}, ich bin {Alter} Jahre alt und wohne in {Wohnort}.")
```

**Hinweis:**

* Eingaben mit input() sind immer vom Typ str
* Typwandlung (int, float) ist nur nötig, wenn mit Werten gerechnet wird
* Für reine Ausgaben oder Textverarbeitung reicht str

---

## Modul 1.4 – Bedingungen (if, elif, else)

**Ziel:** Programmabläufe steuern und Entscheidungen treffen.

**Grundprinzip:**

```python
alter = 20

if alter < 18:
    print("Du bist minderjährig.")
elif alter < 65:
    print("Du bist erwachsen.")
else:
    print("Du bist im Ruhestand.")
```

**Wichtige Punkte:**

* Einrückung (vier Leerzeichen oder ein Tab) ist Pflicht
* Nur der eingerückte Block gehört zur Bedingung
* Bedingungen werden nacheinander geprüft; nur die erste zutreffende wird ausgeführt

**Logische Kombination:**

```python
temperatur = 22
regnet = False

if temperatur > 20 and not regnet:
    print("Perfektes Wetter!")
else:
    print("Bleib lieber drin.")
```

**Kurzform (Ternäre Bedingung):**

```python
alter = 17
status = "volljährig" if alter >= 18 else "minderjährig"
print(status)
```

**Beispiel aus Aufgabe:**

```python
alter = int(input("Wie alt bist du? "))

if alter < 18:
    print("Du bist minderjährig")
elif alter < 65:
    print("Du bist volljährig")
else:
    print("Du bist hoffentlich im Ruhestand")
```

**Hinweis:**

* Bedingungen steuern den Programmablauf
* Einrückung ist syntaktisch zwingend
* Nur der erste zutreffende Block wird ausgeführt
* Logische Operatoren (and, or, not) können kombiniert werden

---

## Modul 1.5 – Schleifen (for, while)

**Ziel:** Wiederkehrende Abläufe automatisieren.

**for-Schleife (vorwärts zählen):**

```python
for x in range(1, 11):
    print(x)
```

* `range(1, 11)` erzeugt die Werte 1 bis 10
* `x` nimmt nacheinander jeden Wert an
* Der eingerückte Code läuft bei jedem Durchlauf einmal

**while-Schleife (rückwärts zählen):**

```python
while x > 0:
    print(x)
    x -= 1

print("Fertig.")
```

* Die Schleife läuft, solange die Bedingung `x > 0` wahr ist
* `x -= 1` reduziert den Zähler bei jedem Durchlauf
* Wenn `x` 0 erreicht, endet die Schleife

**Gesamtes Beispiel:**

```python
x = 0

for x in range(1, 11):
    print(x)

while x > 0:
    print(x)
    x -= 1

print("Zählung abgeschlossen.")
```

**Hinweis:**

* Python führt Schleifen **sequentiell** aus – zuerst `for`, danach `while`
* Eine `while`-Bedingung wird erst geprüft, wenn die vorherige Schleife beendet ist
* Beide Schleifen laufen niemals gleichzeitig
* `for` wird verwendet, wenn die Anzahl der Durchläufe bekannt ist
* `while` eignet sich für unklare oder dynamische Wiederholungen

---

## Zwischenquest – Konsolenprojekt „Little-Helper“

Ziel dieser Quest ist die praktische Anwendung der Module 1.0 bis 1.5 in einem durchgängigen, lauffähigen Programm. Der Little-Helper wird Schritt für Schritt aufgebaut und verbindet alle bisher gelernten Konzepte.

**Zielsetzung:**

* Eingaben entgegennehmen und auswerten
* Entscheidungen basierend auf Eingaben treffen
* Wiederholungen mit Schleifen umsetzen
* Den Programmablauf verständlich strukturieren

**Aufgabenstellung:**

1. Begrüßung ausgeben und den Nutzer einführen.
2. Name und Alter abfragen.
3. Eine individuelle Rückmeldung je nach Alter ausgeben (Bedingungen).
4. Eine Schleife implementieren, um den Ablauf mehrfach zu wiederholen.
5. Am Ende das Programm ordentlich beenden.

**Regeln:**

* Nur Techniken aus den Modulen 1.0 bis 1.5 verwenden.
* Keine Funktionen, Listen oder Dateien nutzen.
* Saubere Einrückung und nachvollziehbare Struktur sind Pflicht. Kommentare zur Orientierung erwünscht.

**Ziel der Quest:**
Am Ende entsteht ein vollständiges, interaktives Konsolenprogramm, das den gesamten Lernfortschritt bis hierher abbildet und eigenständig lauffähig ist.
