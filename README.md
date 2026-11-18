# machine-readable_entscheidungsbaumdiagramme

Dieses Repository enthält Entscheidungsbaumdiagramme (EBD) in einem maschinenlesbaren Format, das deutlich einfacher zu verarbeiten ist als `.docx` oder `.pdf`.

## Unter der Haube

Zur Erstellung der hier veröffentlichten Daten nutzen wir [`ebd_amame`](https://github.com/Hochfrequenz/ebdamame/) und [`r_ebd_huhn`](https://github.com/Hochfrequenz/rebdhuhn/), zwei Hochfrequenz Libraries zur Verarbeitung von EBDs.
Konkret verwenden wir unsere [EBD Toolchain](https://github.com/Hochfrequenz/ebd_toolchain) mit der Datengrundlage aus dem [edi-energy-mirror](https://github.com/Hochfrequenz/edi_energy_mirror) in [einer Github Action](https://github.com/Hochfrequenz/edi_energy_mirror/blob/master/.github/workflows/ebdamame_rebdhuhn.yml).

## Struktur & Datenformate

Zur Strukturierung nutzen wir nicht die Format- oder AHB-Versionen (z.B. UTILMD `5.2e` oder GPKE AHB `6.1e`), sondern lediglich den Zeitraum zu dem die Daten gültig sind.
Beispielsweise bezeichnet `FV2210` die Datenformate, die seit 2022-10-01 gültig sind oder `FV2304` die Datenformate, die seit 2023-04-01 gültig sind.

Jeder EBD ist in je bis zu 4 verschiedenen Dateiformaten verfügbar:

- JSON (die rohen Daten, die aus der Word-Datei gescraped wurden)
- [PlantUML](https://plantuml.com/de/), falls der Entscheidungsbaumgraph in PlantUML plotbar ist
- [DOT](https://graphviz.org/docs/layouts/dot/) (das Format hinter GraphViz, falls das Diagramm nicht zu komplex ist)
- SVG

## Maschinelle & KI-Zugänglichkeit

Damit KI-Assistenten (z. B. Claude, GitHub Copilot, opencode) und Programme die EBDs finden und lesen können, ohne das Repository zu durchsuchen, stellen wir Discovery-Dateien bereit (die drei formatversionsspezifischen davon werden automatisch erzeugt, siehe unten):

- [`llms.txt`](llms.txt) — Kurzanleitung für KI-Assistenten (Roh-URL-Vertrag, Discovery-Dateien, Beispiele).
- `format_versions.json` (Repo-Wurzel) — alle Formatversionen inkl. `valid_from` und `latest`.
- `<FV>/index.json` — Katalog je Formatversion (`ebd_code`, `ebd_name`, `chapter`, `section`, `role`, `pruefidentifikatoren`).
- `<FV>/pruefi_to_key.json` — Prüfidentifikator → EBD-Kennung (der wichtigste Lookup, da Prüfidentifikatoren direkt aus AHBs/EDIFACT zitiert werden).
- `<FV>/ebd.schema.json` — JSON-Schema der `<EBD>.json`-Dateien.
- `<FV>/<EBD>.outcomes.json` — je EBD mit Tabelle: welche Prüfschritte ein Ergebniscode impliziert und welche Codes nach einer Antwort noch erreichbar sind (ab `FV2510`; berechnet mit [`rebdhuhn.explain_outcomes`](https://github.com/Hochfrequenz/rebdhuhn#explain-the-outcomes-which-checks-lead-to-a-result-code)).
- `<FV>/ebd_outcomes.schema.json` — JSON-Schema der `<EBD>.outcomes.json`-Dateien.

Für Menschen gibt es dieselben Diagramme in der Web-Ansicht, per Deep-Link direkt auf einen EBD: `https://ebd.hochfrequenz.de/ebd/?formatversion=<FV>&ebd=<EBD>` (z. B. [E_0003 in FV2610](https://ebd.hochfrequenz.de/ebd/?formatversion=FV2610&ebd=E_0003)). KI-Assistenten sollten ihren Nutzer:innen neben den Rohdaten diesen Link mitgeben.

Einzelne Dateien sind stabil über Roh-URLs abrufbar: `https://raw.githubusercontent.com/Hochfrequenz/machine-readable_entscheidungsbaumdiagramme/main/<FV>/<EBD>.<ext>`.

Die formatversionsspezifischen Dateien (`<FV>/index.json`, `<FV>/pruefi_to_key.json`, `<FV>/ebd.schema.json`, `<FV>/ebd_outcomes.schema.json`, `<FV>/<EBD>.outcomes.json`) sind Nebenprodukte der [EBD Toolchain](https://github.com/Hochfrequenz/ebd_toolchain) und werden bei jedem Lauf neu erzeugt — bitte nicht von Hand pflegen. `format_versions.json` (Repo-Wurzel) wird nicht von der Toolchain erzeugt (die Formatversionen inkl. `valid_from` stammen aus `efoli`); `llms.txt` wird von Hand gepflegt.

## Motivation

Wir freuen uns über jede durch dieses Repository ersparte Stunde Arbeit, in der wichtige Probleme gelöst werden können anstatt EBDs zu analysieren.

## Urheberrecht

Das Urheberrecht der hier versionierten Daten liegt bei EDI@energy bzw. den Autor\*innen der Anwendungshandbücher selbst.
Dieses Repository macht die Daten aus den den EBDs zugrunde liegenden Tabellen lediglich leichter zugänglich.
Hochfrequenz garantiert weder für die Korrektheit noch die Vollständigkeit der hier bereitgestellten Daten.

## Rückmeldungen & Mitwirken

Die hier bereitgestellten Daten sind wahrscheinlich nicht fehlerfrei und mit Sicherheit unvollständig.
Probleme oder Fehler können gerne als [Issue](https://github.com/Hochfrequenz/machine-readable_entscheidungsbaumdiagramme/issues/new) gemeldet werden.
Es ist jedoch nicht sinnvoll, Änderungen direkt hier an den Ergebnis-Daten vorzunehmen; Stattdessen sollten die den Problemen zu Grunde liegeneden Scrapingfehler im Paket [`ebd_amame`](https://github.com/Hochfrequenz/ebdamame/) und Probleme beim Plotten bzw. Erstellen eines Graphen im Paket [`r_ebd_huhn`](https://github.com/Hochfrequenz/rebdhuhn/) adressiert werden.

## Weiterführendes Tooling

Dieses Repository ist Teil der [Hochfrequenz Libraries und Tool für eine echte Digitalisierung der Marktkommunikation](https://github.com/Hochfrequenz/digital_market_communication/).
Insbesondere die [maschinenlesbaren Anwendungshandbücher](https://github.com/Hochfrequenz/machine-readable_anwendungshandbuecher) könnten ebenfalls relevant sein.
