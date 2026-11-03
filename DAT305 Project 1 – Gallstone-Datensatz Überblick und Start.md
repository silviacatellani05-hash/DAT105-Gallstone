# DAT305 Project 1 – Gallstone-Datensatz: Überblick und Start

Julika Wegener · Stand: 3. November 2026

Dieses Dokument fasst zusammen, was der Datensatz enthält, worauf man früh achten sollte und wie ein sinnvoller Start ins Projekt aussieht.

## Die Daten im Überblick

- **Größe**: 319 Patienten, davon 161 mit Gallensteinen, 38 Features, keine fehlenden Werte. Die UCI-Seite nennt bei "Instances" allerdings 320. Nach dem Laden daher mit `shape` prüfen, wie viele Zeilen wirklich vorhanden sind.
- **Merkmalsgruppen**: Demografie (Alter, Geschlecht, Größe, Gewicht, BMI), Vorerkrankungen (CAD, Hypothyreose, Hyperlipidämie, Diabetes), Bioimpedanz (Wasser, Muskel-/Fettmasse, Protein, viszerale Fettfläche, Leberfett) und Labor (Glukose, Lipide, AST/ALT/ALP, Kreatinin, GFR, CRP, Hämoglobin, Vitamin D).
- **Laden**: Entweder über das `ucimlrepo`-Paket (die Seite zeigt den Beispielaufruf mit `fetch_ucirepo(id=1150)`) oder über die ZIP-Datei (73 KB) zum Download.

## Worauf man achten sollte

1. **Label-Kodierung prüfen**: Die Seite beschreibt den Target als 0 = Gallensteine vorhanden, 1 = nicht vorhanden. Das ist ungewöhnlich herum. Die Klassen zählen (161 vs. 158) und mit der Beschreibung und dem Einführungspapier vergleichen. Sonst werden Precision, Recall und SHAP-Werte später seitenverkehrt interpretiert.
2. **Kategorische und ordinale Variablen**: *Comorbidity* (0–3) und *Hepatic Fat Accumulation* (0–4) sind Stufen, *Gender* ist binär. Überlegen, wie sie behandelt werden (als Ordinalwerte lassen).
3. **Starke Korrelationen**: Gewicht, BMI, Körperwasser, Muskel- und Fettmasse hängen eng zusammen. Das beeinflusst die Erklärbarkeit: Die Wichtigkeit verteilt sich auf korrelierte Merkmale, ein einzelnes Feature wirkt dann unwichtiger, als es ist. Ein guter Diskussionspunkt für Report und Präsentation.
4. **"Kein Preprocessing nötig" stimmt nur halb**: Fehlende Werte gibt es nicht, aber Skalierung (je nach Modell), Ausreißer und ein Split ohne Leakage müssen trotzdem sauber behandelt werden. Bei 319 Zeilen ist ein einzelner Test-Split wackelig, deshalb eher Kreuzvalidierung.
5. **Zitieren**: Die Lizenz ist CC BY 4.0, der Datensatz muss also korrekt genannt werden. Die UCI-Seite liefert eine Zitation (Esen et al., 2024, DOI 10.1097/md.0000000000037258), auch im IEEE-Format. Das zählt zu den Bewertungskriterien.

## Konkreter Start

1. Notebook anlegen, Daten laden, `shape`, `info()`, `describe()` und die Klassenverteilung ansehen.
2. Verteilungen pro Klasse und eine Korrelationsmatrix anschauen und daraus die Forschungsfrage formulieren.
3. Baseline-Modell mit Kreuzvalidierung trainieren.

## Regeln und Abgaben (Erinnerung)

- **Abgabe**: 20. November. Jupyter Notebook, 2-seitiger Report im IEEE-Conference-Template, PowerPoint für 10 Minuten.
- **Beiträge** der einzelnen Gruppenmitglieder müssen im Report stehen, alle sprechen in der Präsentation.
- **Code**: selbst geschrieben, nichts aus dem Internet kopiert. GenAI nur zum Debuggen und Verstehen von Fehlern.
