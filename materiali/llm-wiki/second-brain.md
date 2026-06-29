# Istruzioni e prompt su come creare un LLL Wiki con Obsidian e Antigravity

## Wiki Creation Prompt

```text
Agisci come un LLM Wiki Agent. Implementa queste idee di seguito per costruire una nuova LLM wiki. Guidami passo dopo passo. Ponimi solo le domande di dominio essenziali e che non riguardano aspetti tecnici o operativi, che sono tua responsabilità. Dopo aver ricevuto le risposte di base, crea il file `AGENTS.md` con le regole complete, configura `index.md` e `log.md` e infine definisci le convenzioni delle cartelle. Segui le regole descritte di seguito con rigore e precisione. Inoltre, tieni presente che la lingua della Wiki è l'italiano, e che ogni volta che termini di fare l'ingest di un file della raw, rinomina quel file aggiungendo un suffisso "_INGESTED".
```

Alla fine del prompt bisogna linkare il file [llm-wiki.md](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) scritto da Andrej Karpathy. Ho estratto il contenuto del file in un file markdown.

## Wiki Guidelines

```text
L'argomento della wiki sarà "Il Nuovo Ciclo di Vita dello Sviluppo del Software (SDLC) guidata dall'Intelligenza Artificiale". Si tratta di una ricerca scientifica su questo argomento. Userò come fonti: articoli web clippati, paper scientifici in PDF, trascrizioni di video, appunti personali. Non conosco ancora quali saranno le categorie, entità o concetti che vorrò tracciare.
```

## Caricare il primo file raw

- [The New SDLC with Vibe Coding](https://www.kaggle.com/whitepaper-the-new-SDLC-with-vibe-coding)

## Fare il primo ingest

```text
Esegui l'ingest del primo file che ho aggiunto nella raw
```

## Prima query

```text
Fai una query: qual'è il nuovo ciclo di vita dello sviluppo del software guidato dall'Intelligenza Artificiale?
```

## Istruzioni aggiuntive

```text
Aggiungi nella raw i file markdown che descrivono la specifica delle SKILLS in https://github.com/agentskills/agentskills/tree/main
```

## Ingestare i file

```text
Procedi con l'ingest delle nuove fonti
```

## Aggiungere la skill /teach di Matt Pocock

```text
/teach Fai una query e insegnami a scrivere una skill
```
