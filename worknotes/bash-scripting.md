# Bash Scripting - In Progress

---

## Anmerkung

Dies ist ein persönliches Cheatbook.
Es dient als Nachschlagewerk für meine eigenen Lerninhalte und erhebt keinen Anspruch auf Vollständigkeit.
Die Inhalte wurden teilweise mit Unterstützung von ChatGPT geglättet und ergänzt.
Auch wenn ich auf Richtigkeit achte, können Fehler enthalten sein.

---

## Einführung

- Bash = Bourne Again Shell – eine Kommandozeilen-Shell, die Befehle ausführt
- Dient primär zur Automatisierung von Systemaufgaben, nicht zur Softwareentwicklung
- Syntax basiert auf Textverarbeitung und Prozesssteuerung (Pipes, Redirects, Variablen, Exit-Codes)
- Unterstützt programmatische Strukturen (if, loops, functions) – ist damit Turing-vollständig, jedoch nicht für komplexe Programme gedacht
- „Turing“ bezeichnet die theoretische Grenze dessen, was Computer grundsätzlich berechnen können
- Typische Anwendungsbereiche: Startskripte, Cronjobs, Server-Automation, Installationsroutinen

## Hello World

- wir brauchen einen Shebang dieser gibt an welcher Interpreter verwendet wird

```bash

#!/bin/bash

echo "hello world"

echo "my working dir is"
pwd

```
