# Ora 2: Lo Spettro dell'IA e il Context Engineering

---

## | [« Ora 1: Neurone Biologico e Reti Neurali](01-neurone-biologico-reti-neurali.md) | **Ora 2: Spettro IA e Context Engineering** | [Ora 3: AI-Driven SDLC e Setup](03-sdlc-ruoli-setup.md) » |

In questa seconda ora approfondiremo come dialogare con i modelli di linguaggio in modo disciplinato (Prompt Engineering), come gli agenti autonomi gestiscono il loro ciclo di lavoro, lo spettro che separa il "Vibe Coding" dall'ingegneria agentica ed effettueremo una sessione di prototipazione in Google AI Studio.

---

## 🔌 1. Tecniche di Prompt Engineering

Il Prompt Engineering è l'arte e la scienza di strutturare gli input per ottenere risposte ottimali e prevedibili da un LLM. Di seguito analizziamo le 4 tecniche principali con esempi pratici non legati allo sviluppo software.

### A. Role Prompting

Consiste nell'assegnare all'IA un ruolo, una personalità o un profilo professionale specifico prima di definire il compito. Questo aiuta il modello a restringere il dominio delle risposte e ad adottare la terminologia, il tono e il livello di dettaglio più appropriati.

- **❌ Prompt Sbagliato (Senza ruolo)**:

  ```text
  Spiegami come funziona l'inflazione economica.
  ```

  _Perché è inefficace_: L'IA risponderà in modo generico, rischiando di essere troppo tecnica (usando formule o gergo accademico) oppure troppo banale.

- **✅ Prompt Giusto**:

  ```text
  Ruolo: Sei un professore universitario di macroeconomia noto per la tua capacità di rendere i concetti complessi accessibili a chiunque.
  Compito: Spiegami come funziona l'inflazione economica.
  ```

### B. Zero-shot Prompting

Consiste nel chiedere all'IA di eseguire un compito senza fornirle alcun esempio precedente. Funziona bene per compiti semplici e per modelli molto potenti.

- **❌ Prompt Sbagliato (Troppo generico)**:

  ```text
  Riassumi questo testo storico sulle guerre puniche.
  [Testo Storico di 3 pagine]
  ```

  _Perché è inefficace_: Il modello non sa quale sia la lunghezza desiderata, il tono, il pubblico di riferimento o quali dettagli privilegiare. Genererà un testo di lunghezza casuale e con un focus arbitrario.

- **✅ Prompt Giusto (Specifico e vincolato)**:

  ```text
  Ruolo: Sei uno storico divulgatore per ragazzi delle scuole medie.
  Compito: Riassumi il testo storico fornito in un elenco puntato di massimo 5 punti.
  Vincoli: Focus esclusivamente sulle cause scatenanti del conflitto e sulle figure di Annibale e Scipione. Usa un tono avvincente ma rigoroso.
  Testo:
  [Testo Storico di 3 pagine]
  ```

### C. Few-shot Prompting

Consiste nel fornire al modello 2 o più esempi concreti di input e output attesi per addestrarlo al volo sul formato o sullo stile desiderato. È fondamentale quando si richiede una formattazione rigida o una classificazione specifica.

- **❌ Prompt Sbagliato**:

  ```text
  Classifica le recensioni dei libri in Positiva, Neutra o Negativa.
  Recensione: "Il libro parte bene ma si perde a metà, noioso."
  ```

  _Perché è inefficace_: Il modello potrebbe rispondere argomentando: _"Questa recensione è parzialmente negativa perché parla di noia, ma l'inizio era buono, quindi..."_ invece di restituire una singola parola.

- **✅ Prompt Giusto**:

  ```text
  Classifica le recensioni dei libri utilizzando esclusivamente una di queste etichette: POSITIVA, NEUTRA, NEGATIVA. Segui esattamente lo stile degli esempi.

  Input: "Un capolavoro assoluto, consigliato a tutti!"
  Output: POSITIVA

  Input: "La spedizione è stata rapida ma la copertina era leggermente graffiata."
  Output: NEUTRA

  Input: "Personaggi piatti e trama prevedibile. Non sono riuscito a finirlo."
  Output: NEGATIVA

  Input: "Il libro parte bene ma si perde a metà, noioso."
  Output:
  ```

### D. Chain of Thought (CoT) Prompting

Consiste nello spingere l'IA a scomporre un ragionamento complesso in passaggi logici intermedi prima di dare la risposta finale. Questo riduce drasticamente gli errori logico-matematici.

- **❌ Prompt Sbagliato**:

  ```text
  Un hotel ha 5 piani. Ogni piano ha 10 stanze. Metà delle stanze ha 2 letti singoli, l'altra metà ha 1 letto matrimoniale. Quanti letti ci sono in totale nell'hotel? Dimmi solo il numero.
  ```

  _Perché è inefficace_: Chiedere una risposta diretta costringe il modello a calcolare il token numerico successivo in un solo passaggio di attenzione, portando spesso a calcoli errati.

- **✅ Prompt Giusto**:

  ```text
  Risolvi il seguente problema logico-matematico. Pensa e ragiona passo dopo passo, spiegando ogni passaggio logico prima di fornire il risultato finale.
  Problema: Un hotel ha 5 piani. Ogni piano ha 10 stanze. Metà delle stanze ha 2 letti singoli, l'altra metà ha 1 letto matrimoniale. Quanti letti ci sono in totale nell'hotel?
  ```

---

## 🌐 2. Dal Prompt Engineering al Context Engineering

Mentre il **Prompt Engineering** si concentra su _come_ formulare una domanda o un'istruzione (sintassi, regole, esempi e struttura del prompt), il **Context Engineering** rappresenta la sua naturale evoluzione. Questo approccio sposta l'attenzione su _quali informazioni_ circondano la richiesta e su come esse vengano selezionate e fornite all'IA.

### Cos'è il Contesto?

Il **contesto** è l'insieme di tutti i dati che un modello di linguaggio (LLM) ha a disposizione per generare la risposta in un determinato momento. Include le istruzioni di sistema (System Prompt), la cronologia dei messaggi precedenti e tutte le risorse caricate nella conversazione (file di codice, documentazione, regole di stile).

### Il Context Engineering come Evoluzione del Prompting

Nei progetti reali, l'ostacolo principale per un'IA non è la comprensione del comando singolo, bensì la mancanza di conoscenza specifica sul progetto (il codice già scritto, le librerie in uso, le convenzioni del team). Il **Context Engineering** consiste nell'ingegnerizzare attivamente questa base di conoscenza per ottimizzare l'output:

- **Contesto Statico**: Regole stabili e persistenti (es. file di configurazione `AGENTS.md`, linee guida del progetto, documentazione architetturale).
- **Contesto Dinamico**: Il recupero automatico e mirato delle sole porzioni di codice o informazioni necessarie per risolvere il sotto-compito corrente (ad esempio tramite sistemi RAG o strumenti di scansione del workspace).

In questo modo, se il Prompt Engineering indica al modello _come_ rispondere, il Context Engineering seleziona e organizza _su cosa_ deve rispondere, riducendo drasticamente le allucinazioni.

---

## 📦 3. I Limiti del Contesto negli LLM ("Lost in the Middle")

Sebbene i modelli di linguaggio moderni vantino finestre di contesto enormi (fino a milioni di token), la loro capacità reale di elaborare le informazioni decade all'aumentare dei dati inseriti.

- **Position Bias (Lost in the Middle)**: Studi empirici hanno dimostrato che gli LLM tendono a ricordare con alta precisione le informazioni collocate **all'inizio** del prompt (istruzioni di sistema) e **alla fine** (le ultime frasi inserite), mentre tendono a ignorare o confondere le informazioni poste nel **mezzo** di un contesto molto lungo.
- **Miglioramenti Continui**: I modelli moderni stanno riducendo questo gap, ma il limite fisico della densità informativa permane.
- **Soluzione didattica**: Non caricare interi archivi inutilmente. Pratica il **Context Engineering dinamico**, fornendo all'agente solo i file e le informazioni strettamente necessari per il sotto-compito corrente.

---

## 🧪 4. Il Ruolo Fondamentale della Verifica

La differenza principale tra un programmatore amatoriale e un ingegnere del software nell'era dell'IA risiede nella **verifica**.

- **I Test deterministici**: Verificano che a parità di input, una determinata funzione produca lo stesso output (es. `somma(2, 3) == 5`).
- **Le Valutazioni (Evals)**: Poiché gli LLM sono non-deterministici, le Evals verificano la qualità dell'output complessivo (es. _"L'agente ha seguito le linee guida di sicurezza?"_, _"Il codice generato contiene dipendenze allucinate?"_).

> [!CAUTION]
> Scrivere codice con l'IA senza avere una suite di test o un criterio di verifica rigoroso è puro **Vibe Coding ad alto rischio**. Lo sviluppatore deve scrivere i test _prima_ che l'agente scriva il codice applicativo.

---

## 🤖 5. Cos'è un Agente IA?

Un **Agente IA** non è una semplice chat che attende passivamente un prompt per rispondere. È un sistema software autonomo che opera all'interno di un loop continuo:

```mermaid
graph TD
    A["Percepisci Goal<br>(Analizza l'obiettivo dell'utente)"] --> B["Pianifica Step<br>(Scompone il lavoro in sotto-compiti)"]
    B --> C["Agisci (Uso Strumenti)<br>(Scrive file, esegue comandi, cerca sul web)"]
    C --> D["Osserva Risultati<br>(Verifica output dei comandi o test)"]
    D --> E{"Obiettivo Raggiunto?"}
    E -- No --> B
    E -- Sì --> F["Consegna Output"]
    style A fill:#333,stroke:#ccc,stroke-width:1px
    style B fill:#333,stroke:#ccc,stroke-width:1px
    style C fill:#333,stroke:#ccc,stroke-width:1px
    style D fill:#333,stroke:#ccc,stroke-width:1px
    style E fill:#333,stroke:#ccc,stroke-width:1px
    style F fill:#333,stroke:#ccc,stroke-width:1px
```

### I 5 Componenti Chiave di un Agente

Ogni agente moderno è costituito da 5 parti fondamentali:

1. **Il Modello (LLM)**: Il motore di ragionamento e decisione. Legge il contesto e decide quale azione intraprendere.
2. **Gli Strumenti (Tools)**: Ciò che connette il modello al mondo esterno (es. lettori di file, compilatori, browser web, server MCP).
3. **La Memoria (Memory)**: Mantiene lo stato (i log dei tentativi precedenti, le linee guida di progetto, le regole persistenti).
4. **L'Orchestra (Orchestration)**: Il codice logico che gestisce il ciclo continuo dell'agente (il motore del loop).
5. **Il Runtime (Deployment)**: L'ambiente sicuro (sandbox) all'interno del quale l'agente esegue fisicamente il codice.

---

## 🛠️ 6. Demo Google AI Studio & Prototipizzazione Rapida

Ora metteremo in pratica i concetti di Prompting e Intent Specification usando [Google AI Studio](https://aistudio.google.com/), l'ambiente di prototipazione ufficiale di Google per interagire con i modelli Gemini.

### I 5 Prompt in Italiano per gli Studenti

Utilizza i prompt seguenti all'interno della chat di AI Studio per vedere come Gemini traduce istantaneamente il tuo intento in codice HTML/CSS/JS funzionante in una sola sessione:

#### 1. Fiocchi di Neve e Palloncini

> "Crea un'applicazione frontend dall'aspetto formale che ha due pulsanti: "Snowflakes" e "Balloons". Se l'utente fa clic sul pulsante "Snowflakes", fiocchi di neve di medie dimensioni dovrebbero iniziare a cadere sullo schermo dall'alto verso il basso per 5 secondi. Se l'utente fa clic sul pulsante "Balloons", palloncini di medie dimensioni dovrebbero iniziare a fluttuare dal fondo dello schermo verso l'alto per 5 secondi."

#### 2. Pomodoro Timer

> "Crea un'applicazione web minimale per un Pomodoro Timer. L'interfaccia deve mostrare un timer circolare che parte da 25:00 minuti. Includi tre pulsanti ben stilizzati: Start, Pausa e Reset. Quando il timer scade, lo sfondo dello schermo deve lampeggiare delicatamente di rosso e deve essere riprodotto un suono acustico sintetico creato tramite la Web Audio API (senza caricare file audio esterni)."

#### 3. Clicker Counter con Emoji

> "Crea un'applicazione con un contatore numerico al centro. Fornisci due pulsanti: '+' (Incrementa) e '-' (Decrementa). In base al valore del contatore, cambia lo sfondo della pagina: verde se positivo, rosso se negativo, grigio se zero. Inoltre, mostra un'emoji diversa sopra il numero (es. 🙂 se positivo, 😢 se negativo, 😐 se zero)."

#### 4. Generatore Casuale di Citazioni e Gradienti

> "Crea un'applicazione web composta da una scheda centrale contenente una citazione motivazionale e un pulsante 'Nuova Citazione'. Ogni volta che l'utente preme il pulsante, l'applicazione deve: 1) Mostrare una nuova citazione casuale da una lista interna di almeno 10 citazioni celebri. 2) Cambiare lo sfondo della pagina applicando un gradiente CSS lineare a due colori generato casualmente ad ogni clic."

#### 5. Generatore di Palette di Colori con tasto Copia

> "Crea un'applicazione che mostra una palette di 5 colori casuali ma cromaticamente armoniosi (es. toni pastello o monocromatici). Sotto ogni colore deve esserci il relativo codice esadecimale (es. #FF5733) e un piccolo pulsante 'Copia'. Cliccando sul pulsante 'Copia', il codice esadecimale di quel colore deve essere copiato negli appunti dell'utente e deve apparire una notifica temporanea di successo sullo schermo."

---

[« Ora 1: Neurone Biologico e Reti Neurali](01-neurone-biologico-reti-neurali.md) | **Ora 2: Spettro IA e Context Engineering** | [Ora 3: AI-Driven SDLC e Setup](03-sdlc-ruoli-setup.md) » |
