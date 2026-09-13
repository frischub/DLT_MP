# Modulprojekt DLT - BERT-Finetuning

Dieses Repository enthält die Abgabe des Modulprojekts mit **Teil A**
und **Teil B**.

-   **Teil A:** Sentiment-Klassifikation auf
    `cornell-movie-review-data/rotten_tomatoes`
-   **Teil B:** Satzpaar-Klassifikation auf `nyu-mll/glue` mit der
    Konfiguration `mrpc`

Für beide Teile wird das **DistilBERT (`distilbert-base-uncased`)**-Modell verwendet.


## Repository-Struktur

``` text
DLT_MP
├── finetune_starter.ipynb
├── finetune_mrpc.ipynb
├── README.md
├── requirements.txt
├── results/
    ├── metrics_starter.json
    ├── metrics.json
    └── learning_curve.json

```

Die beiden Notebooks enthalten die ausgeführten Bearbeitungen von Teil A
und Teil B. Im Verzeichnis `results/` befinden sich die erzeugten
Ergebnisdateien. 

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

## Reproduktion Teil B

Das Notebook kann entweder in **Google Colab** oder in einer **lokalen Python-Umgebung** ausgeführt werden. Die benötigten Python-Pakete sind in `requirements.txt` definiert.

### Option 1: Google Colab

1. Öffnen Sie das Notebook `finetune_mrpc.ipynb` in [Google Colab](https://colab.research.google.com/).

2. Für das Fine-Tuning wird die Verwendung einer GPU empfohlen. In Colab kann diese unter **Laufzeit → Laufzeittyp ändern → T4 GPU** aktiviert werden.

3. Die benötigten Pakete werden direkt im Notebook installiert.

4. Zellen der Reihe nach ausführen.

### Option 2: Lokale Ausführung


Repository klonen und in das Projektverzeichnis wechseln:

```bash
git clone https://github.com/frischub/DLT_MP.git
cd DLT_MP
```

Virtuelle Umgebung erstellen:

```bash
python -m venv .venv
```

Umgebung unter Linux/macOS aktivieren:

```bash
source .venv/bin/activate
```

Unter Windows:

```bash
.venv\Scripts\activate
```

Anschließend die Abhängigkeiten installieren:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Falls Jupyter noch nicht installiert ist, kann es zusätzlich installiert werden:

```bash
pip install jupyter
```

Danach Jupyter starten:

```bash
jupyter notebook
```

Im Browser kann anschließend `finetune_mrpc.ipynb` geöffnet und vollständig ausgeführt werden.



