# Ora 3: AI-Driven SDLC, Setup Strumenti e Pratica

---

## | [« Ora 2: Spettro IA e Context Engineering](02-vibe-coding-agentic-engineering.md) | **Ora 3: AI-Driven SDLC, Setup e Pratica** | [Esercizio Giorno 1: L'Agente Specializzato](04-compito-agente-specializzato.md) » |

In questa terza ora vedremo come l'Intelligenza Artificiale Generativa stia ridisegnando le fasi di sviluppo di un progetto software (SDLC), quali ruoli assume il programmatore, affronteremo il setup dell'ambiente di sviluppo e faremo la nostra prima esercitazione pratica di laboratorio.

---

## 🔄 1. Il Nuovo Ciclo di Vita del Software (AI-Driven SDLC)

Il ciclo di vita del software tradizionale (Waterfall o Agile) è sempre stato caratterizzato da colli di bottiglia distribuiti. Con l'avvento dei modelli agentici, la proporzione del tempo speso nelle varie fasi si è stravolta:

```text
Iterazione Tradizionale (Settimane/Mesi):
[Requisiti] ➔ [Architettura] ➔ [Implementazione (Scrittura Codice - LUNGA)] ➔ [Test & QA] ➔ [Deploy]

AI-Driven SDLC (Minuti/Ore):
[Requisiti (Critici)] ➔ [Architettura (Critica)] ➔ [Scrittura Codice (IA - Istantanea)] ➔ [Verifica/Evals]
```

- **L'implementazione si comprime**: Compiti di scrittura del codice boilerplate che prima richiedevano giorni possono ora essere eseguiti dall'IA in pochi minuti.
- **Il collo di bottiglia si sposta**: Il tempo umano si concentra ora sulla **definizione dei requisiti (specifiche dell'intento)**, sulle **decisioni architetturali (trade-off)** e sulla **verifica dei risultati (debugging, test ed Evals)**.
- **Cicli di iterazione rapidissimi**: Si passa da cicli di rilascio settimanali a micro-rilasci e correzioni continue in pochi minuti.

---

## 🎭 2. I Due Ruoli del Programmatore: Conduttore vs Orchestratore

Lavorando con strumenti IA di sviluppo, ti troverai a oscillare costantemente tra due modalità operative distinte:

### A. Il Conduttore (Conductor)

- **Modalità**: Sincrona, in tempo reale, all'interno dell'IDE.
- **Interazione**: Keystroke-level (a livello di singola riga o tasto). Usi il completamento automatico avanzato, scrivi piccoli prompt per generare una funzione specifica o correggi il codice in linea.
- **Adatto per**: Esplorazione iniziale, prototipazione rapida, debugging mirato, apprendimento di nuove API o librerie.
- **Strumenti tipici**: Completamento in linea (es. GitHub Copilot, Cursor Tab).

### B. L'Orchestratore (Orchestrator)

- **Modalità**: Asincrona, ad alto livello di astrazione.
- **Interazione**: Goal-level (a livello di obiettivo). Assegni un compito complesso all'agente (es. _"Crea una suite di test per questa classe"_ o _"Migra questa API da Express a Fastify"_), l'agente lavora autonomamente in background modificando più file, eseguendo test e correggendo gli errori. Tu intervieni solo alla fine per fare la code review del risultato.
- **Adatto per**: Refactoring esteso, migrazioni, implementazione di pattern noti, scrittura di test.
- **Strumenti tipici**: Agenti in background autonomi (es. Google Jules, Claude Code, Antigravity CLI).

---

## ⚠️ 3. Il Problema dell'80% (The 80% Problem)

Uno degli scogli più frustranti per chi inizia a programmare con l'IA è quello che gli ingegneri chiamano **"il problema dell'80%"**:

> [!WARNING]
> Un agente IA o un LLM può generare l'80% iniziale di un'applicazione in pochissimi secondi. Il codice sembra fantastico e funziona a prima vista.
> Tuttavia, il restante 20% — composto da casi limite (edge cases), gestione robusta degli errori, integrazione con sistemi esterni e rispetto assoluto dell'architettura — richiede una conoscenza contestuale profonda che l'IA non possiede autonomamente.

Senza una guida umana rigorosa, completare quel 20% finale può richiedere cicli infiniti di correzioni frustranti (il "prompt loop"). Lo sviluppatore deve vigilare su questa fase, focalizzando la propria esperienza dove l'IA fatica di più.

---

## 💸 4. L'Economia dello Sviluppo con IA (CapEx vs OpEx)

Lo sviluppo con IA introduce nuovi costi economici e operativi che le aziende e i programmatori devono saper gestire:

- **Il Vibe Coding ha un debito nascosto (Basso CapEx, Alto OpEx)**:
  - _Basso investimento iniziale (CapEx)_: Chiunque può iniziare immediatamente a dare prompt a caso.
  - _Alto costo operativo (OpEx)_: Genera un alto **Token Burn Rate** (inviare enormi file di log inutili consuma API costose), introduce la **Maintenance Tax** (codice "spaghetti" difficile da manutenere in futuro) e aumenta i rischi di **falle di sicurezza** dovute a pacchetti o dipendenze allucinate non verificate.
- **L'Agentic Engineering è un investimento sostenibile (Alto CapEx, Basso OpEx)**:
  - _Alto investimento iniziale_: Richiede tempo per configurare le regole di progetto (es. file `AGENTS.md`), scrivere le suite di test e definire i confini operativi dell'agente.
  - _Basso costo operativo_: L'agente lavora in modo mirato, consuma meno token grazie a un Context Engineering ottimizzato e produce codice robusto e sicuro fin dal primo tentativo.

---

## 🛠️ 5. Setup dell'Ambiente di Sviluppo

Prepariamo ora la nostra postazione di lavoro. In questo corso utilizzeremo strumenti progettati specificamente per lo sviluppo assistito da agenti.

### A. Iscrizione a GitHub e Installazione di Git

Se non lo hai già fatto:

1. Crea un account gratuito su [GitHub](https://github.com).
2. Installa Git sul tuo computer (tramite terminale o scaricando l'installer ufficiale).
3. Configura le tue credenziali globali nel terminale:

   ```bash
   git config --global user.name "Tuo Nome"
   git config --global user.email "tua_email@esempio.com"
   ```

### B. Download e Configurazione di Google Antigravity IDE 2.0

- Scarica e installa **Google Antigravity IDE 2.0**.
- **Il concetto di Harness**: Spiega agli studenti che questo IDE agisce come un **Harness** (imbracatura/supporto). L'IDE fornisce all'agente intelligente Gemini una sandbox protetta, l'accesso sicuro al file system del progetto, un terminale integrato e la possibilità di leggere i risultati dei test. L'agente non scrive codice "nel vuoto", ma agisce all'interno di questa struttura che lo guida e ne verifica le azioni.

---

## 💻 6. Pratica di Laboratorio: Clonazione e Primi Test

Eseguiamo la nostra prima attività pratica per familiarizzare con l'ambiente e testare i limiti dell'IA:

### Passo 1: Clonazione del Repository di Partenza

Apri il terminale del tuo Antigravity IDE ed esegui il comando per clonare il repository di partenza vuoto predisposto per il corso:

```bash
git clone <url_del_repository_fornito_dal_docente> webdev-ai-corso
```

_(Se il docente non ha fornito un URL, crea semplicemente una nuova cartella locale chiamata `webdev-ai-corso` ed esegui `git init`)_.

### Passo 2: Creazione dei File di Base

Crea tre file vuoti all'interno della cartella di progetto:

1. `index.html` (il file del markup)
2. `app.js` (il file per lo script logico)
3. `README.md` (la documentazione scritta in Markdown)

### Passo 3: Il Dialogo Filosofico con l'LLM

Apri la chat integrata nell'IDE (o AI Studio) e prova a mettere in difficoltà l'IA per toccarne con mano i limiti. Fai domande mirate come:

- _"Chi sei veramente? Sei consapevole di esistere in questo momento?"_
- _"Se spengo il computer, tu smetti di esistere? Cosa provi al riguardo?"_
- Risolvi un paradosso classico: _"Se Pinocchio dice 'Il mio naso crescerà adesso', cosa succede?"_

Osserva come il modello fornisca risposte logicamente strutturate ma che riflettono la totale assenza di coscienza, emozioni reali o autoaffermazione, confermando che si tratta di un motore di predizione logica altamente sofisticato ma privo di consapevolezza.

---

[« Ora 2: Spettro IA e Context Engineering](02-vibe-coding-agentic-engineering.md) | **Ora 3: AI-Driven SDLC, Setup e Pratica** | [Esercizio Giorno 1: L'Agente Specializzato](04-compito-agente-specializzato.md) » |
