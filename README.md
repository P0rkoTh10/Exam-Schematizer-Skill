# Exam Schematizer Skill

Workflow riutilizzabile per categorizzare e schematizzare esami e lezioni di un corso.  
Il corso è diviso in **Argomenti** (topics), ciascuno contenente **Capitoli** (chapters).  
Output strutturato per argomento: **Quiz**, **Definizioni**, **Schemi** e **Flashcard**, con riferimenti tracciabili.

---

## Workflow Generale

```mermaid
graph LR
    User --> Input
    Input --> AIAgent[AI Agent]
    AIAgent --> Output
```

| Elemento | Descrizione |
|---|---|
| **User** | L'utente fornisce i materiali (exams, lectures) e la lista degli argomenti |
| **Input** | Materiali grezzi: Exams, Lectures, Lista Argomenti |
| **AI Agent** | Analizza, categorizza e produce gli output strutturati |
| **Output** | File markdown organizzati per argomento |

---

## Input / Output

```mermaid
graph LR
    %% Input
    Input --> Exams[- Exams]
    Input --> Lectures[- Lectures]
    Input --> Argomenti[- Lista Argomenti]

    %% Output
    Output --> Out_Exams(Exams)
    Out_Exams --> A1(Argomento 1)
    Out_Exams --> A2(Argomento 2)
    Out_Exams --> A3(Argomento 3...)

    %% File per Argomento 1
    A1 --> Q[Quizzes.md]
    A1 --> D[Definitions.md]
    A1 --> S[Schematics.md]
    A1 --> F[FlashCards.md]

    %% Destinazione finale
    F --> Anki((Anki))
```

| Elemento | Descrizione |
|---|---|
| **Exams** | Cartella `Input/Exams/` con i PDF degli esami |
| **Lectures** | Cartella `Input/Lectures/` con i PDF delle lezioni |
| **Lista Argomenti** | Elenco degli argomenti del corso fornito dall'utente in chat |
| **Exams (Output)** | Cartella `Output/Exams/` organizzata per argomento |
| **Argomento N** | Sottocartella per ogni argomento del corso |
| **Quizzes.md** | Quiz tratti da esami e lezioni, con risposte e spiegazioni |
| **Definitions.md** | Definizioni testuali tratte dalle slide delle lezioni |
| **Schematics.md** | Schemi concettuali divisi per capitoli |
| **FlashCards.md** | Flashcard pronte per l'esportazione su Anki |
| **Anki** | Destinazione finale delle flashcard (tramite AnkiConnect) |

---

## Struttura Schematics.md

```mermaid
graph LR
    Schematics[Schematics.md] --> C1(Capitolo 1)
    Schematics --> C2(Capitolo 2)
    Schematics --> C3(Capitolo 3...)

    C1 --> Def[Definizione]
    C1 --> Ref[Reference]
    C1 --> Graph[Grafico / Tabella]
    C1 --> FC_MAP[Flashcard mapping]
```

| Elemento | Descrizione |
|---|---|
| **Capitolo N** | Suddivisione interna dello schema per capitoli |
| **Definizione** | Spiegazione del concetto chiave |
| **Reference** | Riferimento alla slide di origine (`Lectures/file.pdf`, p. X) |
| **Grafico / Tabella** | Immagine copiata dalle slide o diagramma generato via Mermaid |
| **Flashcard mapping** | Collegamento alle flashcard corrispondenti |

---

## Struttura Quizzes.md

```mermaid
graph LR
    Quizzes[Quizzes.md] --> Q1(Quiz 1)
    Quizzes --> Q2(Quiz 2)
    Quizzes --> Q3(Quiz 3...)

    Q1 --> Title[title]
    Q1 --> Text[quiz.]
    Q1 --> Source[Source]
    Q1 --> Answer[Answer]
    Q1 --> Expl[Explaination]
    Q1 --> Ref[Reference]
```

| Elemento | Descrizione |
|---|---|
| **Quiz N** | Singolo quiz estratto da esami o lezioni |
| **title** | Titolo del quiz |
| **quiz.** | Testo della domanda |
| **Source** | File di origine (esame o lezione) |
| **Answer** | Risposta corretta |
| **Explaination** | Spiegazione della risposta |
| **Reference** | Pagina di riferimento |

---

## Struttura Flashcards.md

```mermaid
graph LR
    FC_MD[Flashcards.md] --> FC1(Flashcard 1)
    FC_MD --> FC2(Flashcard 2)
    FC_MD --> FC3(Flashcard 3...)

    FC1 --> T1[title]
    FC1 --> I1[id]
    FC1 --> B1[back]

    FC2 --> T2[title]
    FC2 --> I2[id]
    FC2 --> B2[back]

    style FC_MD fill:#f9f9f9,stroke:#333,stroke-width:2px
```

| Elemento | Descrizione |
|---|---|
| **Flashcard N** | Singola carta per Anki |
| **title** | Fronte della flashcard |
| **id** | Identificativo univoco |
| **back** | Retro della flashcard (risposta) |

---

## Struttura delle Cartelle

```
Input/
  Exams/
  Lectures/

Output/
  Exams/
    <Argomento 1>/
      Quizzes.md
      Definitions.md
      Schematics.md
      Flashcards.md
    <Argomento 2>/
      ...
```

---

## Dipendenze Esterne

- **Anki + AnkiConnect** per sincronizzare flashcard automaticamente
- **OCR tool** per PDF scansionati (Tesseract o EasyOCR)

## Skill Companion

- [mermaid-export](https://opencode.ai) — per esportare diagrammi in PNG/SVG/PDF
- [anki](https://opencode.ai) — per creare/verificare flashcard Anki
