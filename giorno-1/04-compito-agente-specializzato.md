# Esercizio Giorno 1: L'Agente Specializzato

---

## | [« Ora 3: AI-Driven SDLC, Setup e Pratica](03-sdlc-ruoli-setup.md) | **Esercizio Giorno 1: L'Agente Specializzato** | [« Indice del Corso](../README.md) |

L'obiettivo di questo primo compito è valutare la tua comprensione pratica del Prompt Engineering e del Context Engineering, la tua capacità di analizzare criticamente i limiti logici dei modelli linguistici, e l'utilizzo corretto di Markdown e Git per la documentazione e la condivisione del lavoro.

---

## 📝 Istruzioni Passo-Passo

Segui attentamente le indicazioni sottostanti per completare e consegnare l'esercizio.

### 1. Creazione del File di Compito

All'interno del repository che hai clonato sul tuo computer durante l'Ora 3 (`webdev-ai-corso`), crea un nuovo file intitolato **`compito_giorno1.md`** (scritto rigorosamente in formato Markdown).

---

### 2. Documentazione del Limite Logico / Allucinazione

Effettua dei test con un LLM (tramite la chat dell'IDE o in Google AI Studio) cercando di portarlo all'errore, all'allucinazione o a un cortocircuito logico (paradossi, calcoli fuorvianti, domande trabocchetto).
Nel tuo file `compito_giorno1.md`, inserisci una sezione intitolata `## Analisi del Limite Logico` contenente:

- **Il prompt che hai inviato**: Il testo esatto che ha scatenato l'errore.
- **La risposta dell'IA**: La risposta errata o allucinata generata dal modello.
- **La tua riflessione (2-3 righe)**: Una breve spiegazione sul _perché_ l'IA ha fallito. Fai riferimento al fatto che i modelli non possiedono coscienza o reale comprensione del mondo, ma sviluppano traiettorie probabilistico-statistiche basate sui dati storici e sulla predizione del token successivo, risultando a volte vulnerabili a tranelli logici.

---

### 3. Progettazione del System Prompt per un Sub-Agente

Immagina di dover configurare un sub-agente specializzato all'interno di un team di sviluppo o di automazione personale.
Crea una sezione intitolata `## System Prompt del Sub-Agente` e scrivi il prompt di sistema per un agente immaginario a tua scelta (es. _un revisore di codice super pignolo che risponde solo con critiche costruttive ed emoji_, _un traduttore in gergo piratesco_, _un assistente culinario che progetta ricette basandosi solo sugli ingredienti rimasti in frigo_).

Il System Prompt deve essere strutturato applicando le regole di **Context Engineering** studiate durante l'Ora 2:

1. **Ruolo & Obiettivo (Instructions)**: Definisci con chiarezza chi è l'agente e cosa deve fare.
2. **Regole & Limitazioni (Guardrails)**: Inserisci vincoli espliciti su cosa l'agente **non** deve fare (es. _"Non suggerire mai ricette che richiedano la cottura in forno"_, _"Rispondi sempre con un massimo di due frasi"_).
3. **Formato dell'Output**: Specifica la struttura della risposta (es. JSON, elenchi puntati, uso di tabelle, toni formali o informali).

---

### 4. Consegna tramite Git e GitHub

Una volta completato il file `compito_giorno1.md`:

1. Salva il file.
2. Apri il terminale del tuo Antigravity IDE nella cartella del progetto.
3. Aggiungi il file all'area di staging:

   ```bash
   git add compito_giorno1.md
   ```

4. Crea un commit con un messaggio descrittivo:

   ```bash
   git commit -m "Aggiunto compito giorno 1 - L'Agente Specializzato"
   ```

5. Esegui il push del codice sul tuo repository GitHub personale:

   ```bash
   git push origin main
   ```

6. Copia il link del file `compito_giorno1.md` direttamente dal tuo repository GitHub pubblico e invialo al docente per la valutazione.

---

## 🎯 Criteri di Valutazione

Il docente valuterà il tuo compito basandosi sui seguenti punti:

- **Uso di Git/GitHub**: Consegna puntuale tramite repository remoto (superamento dello scoglio dell'autenticazione ed esecuzione dei comandi di base).
- **Formattazione in Markdown**: Utilizzo corretto di titoli, elenchi puntati, blocchi di codice, evidenziazioni e tabelle.
- **Profondità della Riflessione**: Capacità di identificare e motivare l'errore o l'allucinazione dell'IA senza antropomorfizzare il modello.
- **Ingegnerizzazione del System Prompt**: Efficacia e completezza del System Prompt progettato, con particolare attenzione alla presenza di istruzioni chiare e guardrail vincolanti.

---

[« Ora 3: AI-Driven SDLC, Setup e Pratica](03-sdlc-ruoli-setup.md) | **Esercizio Giorno 1: L'Agente Specializzato** | [« Indice del Corso](../README.md) |
