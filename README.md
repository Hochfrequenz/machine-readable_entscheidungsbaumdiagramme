# machine-readable_entscheidungsbaumdiagramme

Dieses Repository enthält Entscheidungsbaumdiagramme (EBD) in einem maschinenlesbaren Format, das deutlich einfacher zu verarbeiten ist als `.docx` oder `.pdf`.
Wir pflegen analog zu den hier abgelegten Daten auch:
* [`machine-readable_message-implementation-guide`](https://github.com/Hochfrequenz/machine-readable_message-implementation-guide) für MIGs
* [`machine-readable_anwendungshandbuecher`](https://github.com/Hochfrequenz/machine-readable_anwendungshandbuecher/) für AHBs
* [`edi_energy_ahb_conditions_and_packages`](https://github.com/Hochfrequenz/edi_energy_ahb_conditions_and_packages) für Bedingungen und Paket-Definitionen aus den AHBs

## Unter der Haube

Zur Erstellung der hier veröffentlichten Daten nutzen wir [`ebddocx2table`](https://github.com/Hochfrequenz/ebddocx2table/) und [`ebdtable2graph`](https://github.com/Hochfrequenz/ebdtable2graph/), zwei Hochfrequenz Libraries zur Verarbeitung von EBDs.

## Struktur & Datenformate

Zur Strukturierung nutzen wir nicht die Format- oder AHB-Versionen (z.B. UTILMD `5.2e` oder GPKE AHB `6.1e`), sondern lediglich den Zeitraum zu dem die Daten gültig sind.
Beispielsweise bezeichnet `FV2210` die Datenformate, die seit 2022-10-01 gültig sind oder `FV2304` die Datenformate, die seit 2023-04-01 gültig sind.

Jeder EBD ist in je bis zu 4 verschiedenen Dateiformaten verfügbar:

- JSON (die rohen Daten, die aus der Word-Datei gescraped wurden)
- [PlantUML](https://plantuml.com/de/), falls der Entscheidungsbaumgraph in PlantUML plotbar ist
- [DOT](https://graphviz.org/docs/layouts/dot/) (das Format hinter GraphViz, falls das Diagramm nicht zu komplex ist)
- SVG

## Motivation

Wir freuen uns über jede durch dieses Repository ersparte Stunde Arbeit, in der wichtige Probleme gelöst werden können anstatt EBDs zu analysieren.

## Urheberrecht

Das Urheberrecht der hier versionierten Daten liegt bei EDI@energy bzw. den Autor\*innen der Anwendungshandbücher selbst.
Dieses Repository macht die Daten aus den den EBDs zugrunde liegenden Tabellen lediglich leichter zugänglich.
Hochfrequenz garantiert weder für die Korrektheit noch die Vollständigkeit der hier bereitgestellten Daten.

## Rückmeldungen & Mitwirken

Die hier bereitgestellten Daten sind wahrscheinlich nicht fehlerfrei und mit Sicherheit unvollständig.
Probleme oder Fehler können gerne als [Issue](https://github.com/Hochfrequenz/machine-readable_entscheidungsbaumdiagramme/issues/new) gemeldet werden.
Es ist jedoch nicht sinnvoll, Änderungen direkt hier an den Ergebnis-Daten vorzunehmen; Stattdessen sollten die den Problemen zu Grunde liegeneden Scrapingfehler im Paket [`ebddocx2table`](https://github.com/Hochfrequenz/ebddocx2table/) und Probleme beim Plotten bzw. Erstellen eines Graphen im Paket [`ebdtable2graph`](https://github.com/Hochfrequenz/ebdtable2graph/) adressiert werden.

## Weiterführendes Tooling

Dieses Repository ist Teil der [Hochfrequenz Libraries und Tool für eine echte Digitalisierung der Marktkommunikation](https://github.com/Hochfrequenz/digital_market_communication/).
Insbesondere die [maschinenlesbaren Anwendungshandbücher](https://github.com/Hochfrequenz/machine-readable_anwendungshandbuecher) könnten ebenfalls relevant sein.
