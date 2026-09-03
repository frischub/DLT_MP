# Modulprojekt DLT – BERT-Finetuning (Starter-Kit)

Feintuning eines BERT-Modells für klassische NLP-Aufgaben. Das mitgelieferte Notebook zeigt die komplette Pipeline für **Sentiment-Klassifikation** auf dem
`cornell-movie-review-data/rotten_tomatoes`-Datensatz. Läuft auf der kostenlosen Colab-Stufe (oder CPU).

**Umfang:** ca. 2 ECTS (~60 Stunden Arbeitszeit).

## Inhalt

```
starter_kit/
├── finetune_starter.ipynb   # Colab-fertiges Notebook (die komplette Pipeline)
├── README.md                # diese Datei
├── RUBRIC.md                # Bewertungsraster
└── report/
    ├── report.tex           # Bericht in der ACL-Vorlage (vorausgefüllte Abschnitte)
    └── custom.bib           # Literaturverzeichnis
```

## Die Aufgabe

Das Projekt hat **zwei Teile**. Teil A ist das Gerüst, Teil B die eigentliche Leistung.

### Teil A – Vorlage nachvollziehen (Aufwärmen)

Arbeiten Sie das Notebook `finetune_starter.ipynb` für `rotten_tomatoes` vollständig durch: Daten inspizieren, Baselines, Feintuning, Evaluation, Fehleranalyse, LoRA, die Lernkurven-Untersuchung. **Verstehen** Sie jeden Schritt – Sie werden ihn in Teil B selbst anpassen müssen. Teil A allein ist wenig wert; er liefert die Grundlage für Teil B.

### Teil B – Übertragung auf eine **andere Aufgabenart** (Kern des Projekts)

Übertragen Sie die Pipeline auf einen zweiten Datensatz und wiederholen Sie dort die Untersuchungen. **Der zweite Datensatz muss eine andere Aufgabenart als die Einzelsatz-Klassifikation aus Teil A sein.** Wählen Sie eine der beiden Tiers:

**Tier 1 – Satzpaar-Klassifikation**
(`nyu-mll/glue` mit Konfiguration `mrpc`, oder ein Teil von `stanfordnlp/snli` bzw.
`nyu-mll/multi_nli`). Zwei Texte pro Beispiel. Sie müssen die **Tokenisierung** ändern (zwei Eingaben, `[SEP]`), und ggf. Metrik/Labelzahl anpassen. Konzeptuell reizvoll (Paraphrase, NLI). Ladebeispiel: `load_dataset("nyu-mll/glue", "mrpc")`.

**Tier 2 – Token-Klassifikation / NER** (`tomaarsen/conll2003`) *(anspruchsvoller)*
Ein anderer Modellkopf (`AutoModelForTokenClassification`), **Sub-Word-/Label-Alignment** und Evaluation mit `seqeval` (Entity-level F1). Deutlich mehr Eigenleistung – für ambitionierte Bearbeitungen empfohlen.

Was in Teil B verlangt ist:

- Datensatz inspizieren und beschreiben (Größe, Klassen, Längen).
- Beide Baselines übertragen (Majority + ein klassischer Baseline; bei NER z. B. ein
  einfacher Klassifikator auf Token-Ebene).
- BERT feintunen und **korrekt** evaluieren (passende Metrik; Test-Set nur einmal).
- **Mindestens zwei** der Untersuchungen aus Abschnitt 8 durchführen (z. B. Lernkurve
  **und** LoRA-Vergleich), sauber ausgewertet.
- Fehleranalyse für die neue Aufgabe.

## Was Sie abgeben

- Link zu **Code-Repository** (z. B. GitHub, Git.UP): darin **beide** ausgeführte Notebooks — auch das Teil-A-Notebook (`rotten_tomatoes`) mit Ihren initialen Untersuchungen — sowie das Teil-B-Notebook, `results/*.json`, `requirements.txt` und dieses README mit der genauen Reproduktionsanweisung. Das trainierte Modell **nicht** committen (zu groß). (Link in separate Text-Datei `repository.txt` einfügen und diese über Moodle einreichen.)
- **Bericht** (PDF, ACL-Vorlage, max. ~6 Seiten): siehe `report/report.tex`.
  Der Bericht behandelt **ausschließlich Teil B**. Teil A wird **nicht** im Bericht beschrieben, das Notebook aber trotzdem ausgeführt eingereicht. Über Moodle abgeben.

## Schnellstart

1. Öffnen Sie `finetune_starter.ipynb` in [Google Colab](https://colab.research.google.com/).
2. *Laufzeit → Laufzeittyp ändern → T4 GPU* (optional, aber schneller).
3. Zellen der Reihe nach ausführen. Der `pip install`-Schritt läuft nur einmal.

> **Colab-Hinweis:** Vorinstallierte Pakete kollidieren gelegentlich mit aktuellen Bibliotheksversionen (torchvision, torchao …). Die Einrichtungszelle (Abschnitt 0) behebt die bekannten Fälle.


## Pipeline (Notebook-Abschnitte)

0. Einrichtung · 1. Daten inspizieren · 2. Baselines (Majority, TF-IDF+LogReg) · 3. Tokenisierung · 4. Feintuning mit `Trainer` · 5. Test-Evaluation
(Accuracy + Macro-F1, Confusion-Matrix) · 6. Fehleranalyse · 7. LoRA · 8. Untersuchungen (Lernkurve u. a.) · 9. Ergebnisse speichern.

## Bewertung

Siehe `RUBRIC.md`. Kurz: Teil A ist Gerüst (wenige Punkte); die Punkte liegen in der **Übertragung (Teil B)**, den **Untersuchungen** und dem **Bericht**.

## ACL-Vorlage

Legen Sie auf Overleaf ein neues Projekt aus der offiziellen **ACL**-Vorlage an
(dort sind `acl.sty` und `acl_natbib.bst` enthalten) und ersetzen Sie die Haupt-`.tex`
durch `report/report.tex`. Style-Dateien alternativ:
<https://github.com/acl-org/acl-style-files>.

## Datensätze im Überblick

| Aufgabe | Datensatz-ID (Hugging Face) | Aufgabenart | Rolle |
|---|---|---|---|
| Sentiment | `cornell-movie-review-data/rotten_tomatoes` | Einzelsatz-Klassifikation | Teil A (Vorlage) |
| Paraphrase | `nyu-mll/glue` (Konfig. `mrpc`) | Satzpaar-Klassifikation | Teil B, Tier 1 |
| NLI | `stanfordnlp/snli` oder `nyu-mll/multi_nli` (Teilmenge) | Satzpaar-Klassifikation | Teil B, Tier 1 |
| NER | `tomaarsen/conll2003` | Token-Klassifikation | Teil B, Tier 2 |

> Bei `nyu-mll/glue` wird die Aufgabe über die Konfiguration gewählt, z. B.
> `load_dataset("nyu-mll/glue", "mrpc")`. `nyu-mll/multi_nli` hat keine
> `test`-Splits mit Labels – nutzen Sie `validation_matched` zum Testen.

```
requirements.txt:
transformers>=4.40
datasets>=2.19
evaluate
scikit-learn
peft
accelerate
seqeval        # nur für Teil B, Tier 2 (NER)
```



(Erstellt mit Hilfe von KI-Tools; gesteuert und durchgesehen von David Schlangen. Juli 2026.)
