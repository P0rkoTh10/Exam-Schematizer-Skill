# Exam Schematizer Skill

Workflow riutilizzabile per categorizzare e schematizzare esami e lezioni di un corso in output strutturati per capitolo: **Quiz**, **Definizioni**, **Schemi** e **Flashcard**, con riferimenti tracciabili.

---

## Workflow Generale

```mermaid
graph LR
    User --> Input
    Input --> AIAgent[AI Agent]
    AIAgent --> Output
```

## Flusso Input/Output

```mermaid
graph LR
    %% Sezione Input
    Input --> Exams_In[- Exams]
    Input --> Lectures[- Lectures]
    Input --> List[- List of Chapters]

    %% Flusso Principale
    Output --> Exams_Out(Exams)

    %% Sotto-capitoli
    Exams_Out --> Ch1(Chapter 1)
    Exams_Out --> Ch2(Chapter 2)
    Exams_Out --> Ch3(Chapter 3)
    Exams_Out --> Ch4(Chapter 4...)

    %% File di output dal Capitolo 1
    Ch1 --> Q[Quizzes.md]
    Ch1 --> D[Definitions.md]
    Ch1 --> S[Schematics.md]
    Ch1 --> F[FlashCards.md]

    %% Destinazione finale
    F --> Anki((Anki))
```

## Struttura degli Schemi (Schematics.md)

```mermaid
graph LR
    %% Struttura principale di Schematics.md
    Schematics[Schematics.md] --> E1(Elemento 1)
    Schematics --> E2(Elemento 2)
    Schematics --> E3(Elemento 3...)

    %% Sotto-elementi dell'Elemento 1
    E1 --> Def[Definizione]
    E1 --> Ref[Reference]
    E1 --> QZ[Quiz]
    E1 --> FC[Flash card]

    %% Esplosione dei campi del Quiz
    QZ --> Title[title]
    QZ --> Quiz_Text[quiz.]
    QZ --> Source[Source]
    QZ --> Answer[Answer]
    QZ --> Expl[Explaination]
    QZ --> Ref_Quiz[Reference]
```

## Struttura dei Flashcard (Flashcards.md)

```mermaid
graph LR
    FC_MD[Flashcards.md] --> FC1(Flashcard 1)
    FC_MD --> FC2(Flashcard 2)
    FC_MD --> FC3(Flashcard 3...)

    %% Proprieta per Flashcard 1
    FC1 --> T1[title]
    FC1 --> I1[id]
    FC1 --> B1[back]

    %% Proprieta per Flashcard 2
    FC2 --> T2[title]
    FC2 --> I2[id]
    FC2 --> B2[back]

    %% Stile opzionale per evidenziare il file principale
    style FC_MD fill:#f9f9f9,stroke:#333,stroke-width:2px
```

---

## Struttura delle Cartelle

```
Input/
  Exams/
  Lectures/

Output/
  Exams/
    <Chapter 1>/
      Quizzes.md
      Definitions.md
      Schematics.md
      Flashcards.md
    <Chapter 2>/
      ...
```

## Dipendenze Esterne

- **Anki + AnkiConnect** per sincronizzare flashcard automaticamente
- **OCR tool** per PDF scansionati (Tesseract o EasyOCR)

## Skill Companion

- [mermaid-export](https://opencode.ai) — per esportare diagrammi in PNG/SVG/PDF
- [anki](https://opencode.ai) — per creare/verificare flashcard Anki
