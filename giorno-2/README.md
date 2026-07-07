# Giorno 2: Documentazione e Sviluppo Assistito da Agent Skills e LLM Wiki

---

## | [« Parte 3: AI-Driven SDLC e Setup Strumenti](../giorno-1/03-sdlc-ruoli-setup.md) | **Introduzione Giorno 2** | [Parte 1: Markdown, RAG e il System Prompt](01-markdown-rag-system-prompt.md) » |

Benvenuto nella seconda giornata del corso! L'obiettivo di oggi è comprendere l'importanza di una documentazione formale e strutturata nello sviluppo guidato dall'Intelligenza Artificiale. Esploreremo come il Markdown funge da interfaccia di precisione per i modelli, confronteremo l'architettura di recupero RAG con il pattern cumulativo e persistente di un **LLM Wiki (Second Brain)** gestito su Obsidian, impareremo a ingegnerizzare le **Agent Skills** per guidare gli agenti in modo dichiarativo e discuteremo criticamente i concetti di **AI Pitfalls** e **Resa Cognitiva** (Cognitive Surrender).

## 🎯 Obiettivi della Giornata

- **Documentazione Strutturata e Intento**:
  - Imparare ad utilizzare la sintassi Markdown in modo ottimale per definire regole, contesti e specifiche chiare e leggibili per i linter e per l'IA.
  - Comprendere i limiti di memoria dell'LLM ed analizzare il funzionamento generale del RAG.
- **LLM Wiki (Second Brain)**:
  - Comprendere il pattern cumulativo e persistente dell'LLM Wiki ideato da Andrej Karpathy e le differenze architetturali con il RAG tradizionale.
  - Creare e utilizzare attivamente un Second Brain su Obsidian, effettuando l'ingestione e la query di file raw.
- **Agent Skills & Ingegnerizzazione dell'Intento**:
  - Comprendere la struttura e la specifica delle Agent Skills (`agentskills.io` e la specifica YAML/Markdown con frontmatter).
  - Scrivere una skill personalizzata (`stil-novo`) e comprendere l'attivazione automatica o manuale tramite il parametro `disable-model-invocation: true`.
- **Sviluppo Assistito e Presidio dell'Uomo**:
  - Distinguere tra Vibe Coding, Sviluppo Assistito ed Agentic Engineering.
  - Analizzare le euristiche di presidio intellettuale sul codice generate da Karpathy (AI Pitfalls) e Addy Osmani (Cognitive Surrender vs Cognitive Offloading) per evitare l'accumulo di "debito di comprensione".

---

La seconda giornata è organizzata in tre parti principali.

### 📝 [Parte 1: Markdown, RAG e il System Prompt](01-markdown-rag-system-prompt.md)

- _Cosa imparerai_: Il video di ispirazione di Salvatore Sanfilippo (antirez) sui pericoli dell'uso passivo dell'IA, l'utilizzo del Markdown per allineare l'intento uomo-macchina, la differenza tra prompt monouso e System Prompt (`AGENTS.md`) con la realizzazione di un esempio in stile stilnovista, il problema della memoria nei modelli e il funzionamento fondamentale del RAG.

### 🌐 [Parte 2: LLM Wiki (Second Brain) e Agent Skills](02-llm-wiki-agent-skills.md)

- _Cosa imparerai_: Il pattern cumulativo dell'LLM Wiki, la configurazione pratica di un Second Brain su Obsidian per ingurgitare e sintetizzare informazioni (ingest e query), e la specifica delle Agent Skills. Trasformerai il System Prompt in stile stilnovista in una skill riutilizzabile.

### ⚖️ [Parte 3: Sviluppo Assistito, AI Pitfalls e Resa Cognitiva](03-sviluppo-assistito-linee-guida.md)

- _Cosa imparerai_: L'utilizzo del framework delle Agent Skills di Matt Pocock (come la skill `/teach`) per guidare l'apprendimento, lo Spettro dello Sviluppo con IA (Vibe Coding vs Agentic Engineering), le insidie dello sviluppo assistito (le AI Pitfalls di Karpathy) e il concetto neurale ed operativo di "Resa Cognitiva" (Cognitive Surrender di Addy Osmani) con relative letture di approfondimento.

---

[« Parte 3: AI-Driven SDLC e Setup Strumenti](../giorno-1/03-sdlc-ruoli-setup.md) | **Introduzione Giorno 2** | [Parte 1: Markdown, RAG e il System Prompt](01-markdown-rag-system-prompt.md) » |
