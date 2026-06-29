# Riassunto del documento LLM Wiki di Karpathy

- **Il concetto centrale**: A differenza dei tradizionali sistemi RAG (Retrieval-Augmented Generation) — che analizzano i documenti da zero a ogni domanda senza accumulare conoscenza — questo approccio prevede che il LLM costruisca e mantenga una **wiki in formato markdown persistente e cumulativa**. Ogni nuova informazione viene letta, sintetizzata e integrata attivamente nel grafo di conoscenza già esistente.
- **La divisione dei ruoli**: L'utente si concentra sull'aspetto intellettuale (selezionare le fonti, guidare l'analisi, porre le domande), mentre il LLM si fa carico di tutto il lavoro ripetitivo e noioso di catalogazione, archiviazione e aggiornamento dei collegamenti incrociati.
- **Architettura a tre livelli**:
  1. _Fonti grezze_: I file originali immutabili (articoli, immagini, dati).
  2. _La wiki_: L'insieme di file markdown generati, strutturati e costantemente aggiornati dal LLM.
  3. _Lo schema_: Un file di configurazione contenente le regole e le istruzioni che guidano il LLM nella gestione della wiki.
- **Operazioni chiave**:
  - _Acquisizione (Ingest)_: Il LLM elabora una nuova fonte e aggiorna di conseguenza tutte le pagine della wiki collegate (concetti, entità, indici).
  - _Interrogazione (Query)_: L'utente interroga la wiki; le analisi o le risposte più utili possono essere salvate come nuove pagine per arricchire la base di conoscenza.
  - _Verifica (Lint)_: Controlli periodici in cui il LLM rileva contraddizioni, link interrotti o lacune informative da colmare.
- **Strumenti consigliati**: Il sistema si integra idealmente con **Obsidian** (sfruttando la vista a grafo, il controllo delle versioni tramite Git e plugin come Dataview o Marp) e può appoggiarsi a motori di ricerca locali (es. `qmd`) o a semplici file di indice e registro delle attività (`index.md` e `log.md`) per facilitare la navigazione del LLM.

In sintesi, il documento propone un metodo per ridurre a zero i costi di manutenzione di un archivio di conoscenza personale, delegando la burocrazia organizzativa all'intelligenza artificiale per tenere la wiki sempre aggiornata e coerente.
