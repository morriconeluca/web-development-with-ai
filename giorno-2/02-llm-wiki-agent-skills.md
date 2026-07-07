# Ora 2: LLM Wiki (Second Brain) e Agent Skills

---

## | [« Ora 1: Markdown, RAG e il System Prompt](01-markdown-rag-system-prompt.md) | **Ora 2: LLM Wiki e Agent Skills** | [Ora 3: Sviluppo Assistito, AI Pitfalls e Resa Cognitiva](03-sviluppo-assistito-linee-guida.md) » |

In questa seconda ora vedremo come strutturare la conoscenza a lungo termine e le istruzioni per i nostri agenti IA. Esploreremo il pattern dell'**LLM Wiki (Second Brain)** per creare una base di conoscenza cumulativa e persistente in Obsidian, ed approfondiremo la specifica e la creazione delle **Agent Skills**.

---

## 🧠 1. L'Alternativa al RAG: Il Pattern LLM Wiki (Second Brain)

Come abbiamo visto nell'Ora 1, l'architettura RAG classica è efficiente ma soffre di un limite: è _stateless_. Ogni volta che poniamo una domanda, l'LLM ricomincia la ricerca semantica da zero, estraendo frammenti scollegati e provando a ricostruire le relazioni concettuali al volo. Non c'è un accumulo stabile della conoscenza.

### L'Idea di Andrej Karpathy: La Wiki Cumulativa e Persistente

Andrej Karpathy (figura di spicco a livello mondiale nel campo dell'Intelligenza Artificiale, ex Direttore dell'IA presso Tesla, co-fondatore di OpenAI e rinomato divulgatore scientifico) è stato il primo a coniare e rendere celebre il concetto di **"Vibe Coding"** per descrivere lo sviluppo software assistito da modelli linguistici avanzati.

Per superare il limite _stateless_ della RAG classica, Karpathy ha proposto il pattern **LLM Wiki**: invece di delegare il reperimento a un database vettoriale opaco, usiamo l'agente intelligente per **creare e manutenere in modo incrementale una wiki in formato Markdown**.

```text
RAG Tradizionale:
[Domanda Utente] ➔ [Ricerca nel Vector DB] ➔ [Estrazione Chunks Sparsi] ➔ [Risposta LLM Monouso]

LLM Wiki (Second Brain):
[Nuova Fonte Raw] ➔ [L'agente legge, sintetizza e unisce] ➔ [Aggiornamento Pagine Concetti e Indici della Wiki Markdown]
[Domanda Utente] ➔ [L'agente naviga la Wiki interconnessa] ➔ [Risposta Coerente e Profonda]
```

- **Il Compounding Concettuale**: Quando si aggiunge una nuova fonte (un articolo, un PDF, un video), l'agente non si limita a indicizzarla. La legge, ne estrae i concetti chiave e **li integra attivamente** nelle pagine della wiki già esistenti. Se un concetto era già presente, l'agente ne espande la trattazione; se ci sono contraddizioni, le segnala; se nascono nuove relazioni, crea link ipertestuali.
- **Obsidian come Interfaccia**: I file markdown generati dall'agente sono ospitati in un archivio locale gestito tramite **Obsidian**. Questo ci permette di navigare graficamente nel nostro "Secondo Cervello" (Second Brain), seguendo le connessioni, i link interni e visualizzando la mappa relazionale (vista a grafo).

---

## 🛠️ 2. Pratica Parte 1: Creare un Second Brain con Obsidian

Mettiamo in pratica il pattern di Karpathy configurando una wiki personale per mappare le nostre ricerche.

### Istruzioni per la creazione della Wiki

1. Apri **Obsidian** e crea un nuovo archivio (vault) in una cartella locale dedicata, ad esempio `llm-wiki-sdlc`.
2. All'interno della cartella dell'archivio, crea una sottocartella chiamata `raw/` per le fonti grezze e una cartella `wiki/` per i file organizzati dall'agente.
3. Copia il file **[llm-wiki.md](llm-wiki/llm-wiki.md)** (il manifesto originale tratto dal [Gist di Andrej Karpathy](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)) all'interno della cartella dell'archivio.
4. Avvia il tuo agente di sviluppo (come Antigravity) all'interno di questa directory ed esegui il seguente prompt di avvio (Wiki Creation Prompt) incollando alla fine di esso anche il contenuto del file `llm-wiki.md` per consentire all'agente di leggerne le specifiche:

   ```text
   Agisci come un LLM Wiki Agent. Implementa queste idee di seguito per costruire una nuova LLM wiki. Guidami passo dopo passo. Ponimi solo le domande di dominio essenziali e che non riguardano aspetti tecnici o operativi, che sono tua responsabilità. Dopo aver ricevuto le risposte di base, crea il file `AGENTS.md` con le regole complete, configura `index.md` e `log.md` e infine definisci le convenzioni delle cartelle. Segui le regole descritte di seguito con rigore e precisione. Inoltre, tieni presente che la lingua della Wiki è l'italiano, e che ogni volta che termini di fare l'ingest di un file della raw, rinomina quel file aggiungendo un suffisso "_INGESTED".
   ```

5. L'agente ti porrà alcune domande iniziali sul dominio della wiki. Rispondi incollando la seguente configurazione:

   ```text
   L'argomento della wiki sarà "Il Nuovo Ciclo di Vita dello Sviluppo del Software (SDLC) guidata dall'Intelligenza Artificiale". Si tratta di una ricerca scientifica su questo argomento. Userò come fonti: articoli web clippati, paper scientifici in PDF, trascrizioni di video, appunti personali. Non conosco ancora quali saranno le categorie, entità o concetti che vorrò tracciare.
   ```

A questo punto, l'agente inizializzerà i file di controllo `index.md` (l'indice semantico delle pagine), `log.md` (il diario cronologico delle attività) e il file `AGENTS.md` contenente le regole per la manutenzione.

### Il Primo Ingest

1. Scarica e copia il whitepaper **[the-new-sdlc-with-vibe-coding.pdf](llm-wiki/the-new-sdlc-with-vibe-coding.pdf)** all'interno della cartella `raw/`.
2. Ordina all'agente di eseguire l'ingestione tramite il prompt:

```text
Esegui l'ingest del primo file che ho aggiunto nella raw
```

L'agente analizzerà il PDF e creerà automaticamente le prime pagine della wiki in `wiki/` (ad esempio, le schede relative a "Vibe Coding", "Agentic Engineering", "Harness" e "Context Engineering"), inserendo i collegamenti reciproci e rinominando il PDF di origine in `the-new-sdlc-with-vibe-coding_INGESTED.pdf`.

### Esecuzione della prima Query

Metti alla prova il Second Brain ponendo una domanda di sintesi:

```text
Fai una query: qual'è il nuovo ciclo di vita dello sviluppo del software guidato dall'Intelligenza Artificiale?
```

L'agente non leggerà il PDF originale da zero, ma interrogherà le schede già strutturate e collegate all'interno della cartella `wiki/`, componendo una risposta ricca di citazioni e link alle singole pagine.

---

## 🔌 3. Cosa sono le Agent Skills?

Un System Prompt generico (come quello creato nell'Ora 1) indica all'agente come comportarsi in _ogni_ circostanza. Tuttavia, man mano che un progetto cresce, l'agente deve acquisire competenze specifiche che non devono appesantire costantemente la finestra di contesto. Per fare questo si utilizzano le **Agent Skills**.

Una **Agent Skill** è un modulo autonomo costituito da istruzioni, script o configurazioni che l'agente carica in memoria solo quando necessario.

### La Specifica delle Skills (agentskills.io)

Una skill è rappresentata da un file Markdown (`SKILL.md`) che segue regole precise:

1. **Frontmatter YAML**: Contiene i metadati identificativi della skill, come il nome, la descrizione e i parametri operativi.
2. **Attivazione Manuale vs Automatica**:
   - Per impostazione predefinita, l'agente scansiona il prompt dell'utente e attiva automaticamente le sue skill se rileva parole chiave correlate alla descrizione della skill stessa.
   - Se inseriamo il parametro **`disable-model-invocation: true`** nel frontmatter, la skill **non si attiverà mai da sola**. L'utente deve invocarla esplicitamente nella chat facendo riferimento al nome della skill stessa.
3. **Istruzioni (Markdown)**: Il corpo del file definisce le istruzioni operative dettagliate che l'agente deve seguire una volta caricata la skill.

---

## 🛠️ 4. Pratica Parte 2: Creare una Skill Personalizzata (stil-novo)

Trasformiamo il comportamento poetico dell'agente creato nell'Ora 1 in una skill formale riutilizzabile, che l'utente può richiamare a comando.

1. Torna alla cartella `poetry` creata nell'Ora 1 ed elimina il file `AGENTS.md` (questo disabiliterà il comportamento poetico permanente dell'agente in quella directory, facendolo tornare a rispondere normalmente).
2. Dentro la cartella `poetry`, crea la sottocartella `.agents/skills/stil-novo/` (il customization root locale).
3. All'interno di questa cartella, crea il file `SKILL.md` e incolla il seguente codice:

```markdown
---
name: stil-novo
description: Risponde in rima in stile stilnovista.
disable-model-invocation: true
---

# Dolce Stil Novo

Rispondi sempre in rima, come un poeta dello Stil Novo.

## Regola Fondamentale

- **Rima e Stile**: Esprimiti esclusivamente in versi rimati, impiegando il volgare illustre e i temi tipici della nobiltà d'animo e del parlar leggiadro dei poeti stilnovisti.
```

### Come testare la Skill

Dato che abbiamo impostato `disable-model-invocation: true`, l'agente non risponderà in rima se gli scriviamo un messaggio generico. Per attivare la skill, dobbiamo richiamarla esplicitamente.

**Prompt di esempio per i test**:

> _"Usa la skill `stil-novo` per rispondermi alla domanda: chi era Beatrice?"_

Oppure:

> _"Attiva la skill `stil-novo` e spiegami cos'è l'amore secondo i poeti fiorentini."_

L'agente caricherà temporaneamente la skill, applicherà le istruzioni del file `SKILL.md` solo per questa risposta e genererà i suoi versi in rima. Nelle risposte successive tornerà al suo comportamento normale, dimostrando come le Agent Skills consentano di espandere le capacità dell'agente senza inquinare permanentemente il contesto.

---

[« Ora 1: Markdown, RAG e il System Prompt](01-markdown-rag-system-prompt.md) | **Ora 2: LLM Wiki e Agent Skills** | [Ora 3: Sviluppo Assistito, AI Pitfalls e Resa Cognitiva](03-sviluppo-assistito-linee-guida.md) » |
