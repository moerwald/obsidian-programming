
## Was ist Refactoring

  

Refactoring ist die Verbesserung der Struktur eines Codes ohne dessen Verhalten zu ändern. Es ist ein Prozess, der die Qualität des Codes verbessert, indem er ihn verständlicher, wartbarer und flexibler macht. Refactoring ist ein kontinuierlicher Prozess, der sich auf die Verbesserung der Codequalität konzentriert, ohne neue Funktionen hinzuzufügen.

  

- Strukturverbesserung von Quellcode unter Beibehaltung des Programmverhaltens

- Vebessert: Lesbarkeit, Wartbarkeit, Flexibilität, Testbarkeit und Erweiterbarkeit.

- Ziel den Aufwand für die Fehleranalyse und funktionale Erweiterungen deutlich zu senken (Reduzierung von technischen Schulden)

  

## Die wichtigste Basis vom Refactoring

- Versionsverwaltung

- Unit-Tests / E2E-Tests

  

## Wichtig vor dem Refactoring

- Plan haben

- Unit-Tests (Hilft auch beim verstehen vom Code - ala Smoke Tests, Blackbox Tests)

  

## Refactoring Plan

- Problem ermitteln

    - Eigene Probleme analysieren (Brauche zu Lange für ein neues Feature, Bug-Fixing..)

    - Code Komplexität messen mit Tools (Zyklomatische Komplexität, Code Analysis, Code Metrics)

    - Code wiederholungen ermitteln

- Ziel definieren

    - Wie soll die neue Architektur aussehen

    - Was soll verbessert werden

    - Clean-Code

    - Code Smells beseitigen

    - Prinzipien einbringen (z.B. SOLID, KISS, DRY, YAGNI, GRASP, ...)

- Risiko analyse

    - Was kann schief gehen

- Plannung

    - Wann und wie kann es umgesetzt werden

    - Wo sind "Baby steps" möglich

   (Lieber mit dem kleinen beginnen, das erleichtert of das ganz Große)

  

## Wichtig beim Refactoring

- Micro commits

- Permanent Unit-Tests ausführen

- Baby steps

  

## Tools Unterstützen beim Refactoring

- ReSharper / Plugins

- Visual Studio 2022 selbst

- Architecture Tools (VS2022 Enterprise)

- Code Metrics

- Code Analysis

- NDepend (Kostet Geld)

  

## Dauerhaft die Qualität einhalten

- Automatisiert Probleme ermitteln (IDE Tools, CI)

- Mit TDD/BDD arbeiten

- Muss e2e / integrationstest

- Pfadfinderregel berücksichtigen