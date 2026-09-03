# Bewertungsraster – Modulprojekt DLT (BERT-Finetuning)

Gesamt: **100 Punkte**, verteilt auf Teil A (10), Teil B (45), Bericht (45).
Richtwert; Gewichtung kann noch angepasst werden. Umfang: ca. 2 ECTS (~60 h).

## Teil A – Vorlage nachvollziehen (10 P)

Reines Gerüst; hier gibt es nicht viele Punkte zu holen.

| Kriterium | Punkte | Erwartung |
|---|---:|---|
| Notebook lauffähig durchgearbeitet | 6 | `rotten_tomatoes`-Notebook läuft von oben nach unten; Ergebnisse plausibel; BERT schlägt beide Baselines. |
| Verständnis erkennbar | 4 | Kurze eigene Kommentare/Notizen zeigen, dass die Schritte verstanden wurden (nicht nur ausgeführt). |

## Teil B – Übertragung auf eine andere Aufgabenart (45 P)

Der Kern des Projekts. **Voraussetzung:** der zweite Datensatz ist eine *andere
Aufgabenart* (Satzpaar- oder Token-Klassifikation). Gleiche Aufgabenart wie Teil A
→ Teil B gilt als nicht erfüllt.

| Kriterium | Punkte | Erwartung |
|---|---:|---|
| Korrekte Übertragung der Pipeline | 12 | Tokenisierung/Modellkopf/Datenformat an die neue Aufgabenart angepasst; läuft sauber. |
| Baselines | 6 | Majority **und** eine sinnvolle klassische Baseline übertragen; BERT schlägt beide. |
| Korrekte Evaluation | 8 | Zur Aufgabe passende Metrik (z. B. Macro-F1; bei NER Entity-F1 via `seqeval`); Test-Set genau **einmal** benutzt. |
| Zwei Untersuchungen | 12 | Mind. zwei aus Abschnitt 8 (z. B. Lernkurve **und** LoRA), sauber aufgesetzt und ausgewertet. |
| Reproduzierbarkeit & Code | 7 | Fester Seed; beide Notebooks + `results/*.json` + `requirements.txt`; README mit exakter Reproduktionsanweisung; großes Modell **nicht** eingecheckt. |

## Bericht (45 P)

ACL-Vorlage, ≤ ~6 Seiten. Behandelt **ausschließlich Teil B**; Teil A wird nicht
im Bericht beschrieben (aber als ausgeführtes Notebook mit eingereicht).

| Kriterium | Punkte | Erwartung |
|---|---:|---|
| Struktur & ACL-Format | 6 | Vorlage korrekt genutzt, alle Abschnitte vorhanden, im Seitenlimit. |
| Daten & Methode | 8 | Beide Datensätze beschrieben; Anpassungen an die neue Aufgabenart klar und reproduzierbar dargestellt. |
| Ergebnisse | 12 | Mind. 1 Tabelle + 1 Abbildung; Vergleich zu **beiden** Baselines; Zahlen stimmen mit `results/*.json` überein. |
| Diskussion der Untersuchungen | 10 | Die zwei Untersuchungen interpretiert, nicht nur berichtet. |
| Fehleranalyse | 5 | Konkrete Fehlerbeispiele + nachvollziehbare Hypothesen für die neue Aufgabe. |
| Diskussion & Limitationen | 4 | Ehrliche Einordnung (kleiner Datensatz, wenige Seeds, kein Sweep); kurzer Ausblick. |

## Bonus (bis +10 P)

- Mehrere Seeds gemittelt (Fehlerbalken/Streuung) in den Untersuchungen.
- Beide Tiers bearbeitet (Satzpaar **und** Token-Klassifikation).
- Sauberer Modellvergleich (DistilBERT vs. BERT-base vs. `bert-mini`) mit Kosten/Nutzen.

## Notenschlüssel

90–100 = 1,0–1,3 · 80–89 = 1,7–2,0 · 70–79 = 2,3–2,7 · 60–69 = 3,0–3,3 ·
50–59 = 3,7–4,0 · < 50 = nicht bestanden.

## Häufige Fehler (Abzug)

- Zweiter Datensatz ist doch nur Einzelsatz-Klassifikation → Teil B nicht erfüllt.
- Test-Set mehrfach / zum Tuning benutzt.
- Falsche Metrik (z. B. Token-Accuracy statt Entity-F1 bei NER; nur Accuracy bei
  unbalancierten Klassen).
- Kein Baseline-Vergleich ("BERT erreicht 0,84" ohne Referenz).
- Kein fester Seed; Ergebnisse nicht reproduzierbar.
- Bericht = Notebook-Dump statt eigenständiger Text.


(Erstellt mit Hilfe von KI-Tools; gesteuert und durchgesehen von David Schlangen. Juli 2026.)
