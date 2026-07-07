# Parte 3: Sviluppo Assistito, AI Pitfalls e Resa Cognitiva

---

## | [« Parte 2: LLM Wiki (Second Brain) e Agent Skills](02-llm-wiki-agent-skills.md) | **Parte 3: Sviluppo Assistito, AI Pitfalls e Resa Cognitiva** | [Giorno 3: Architettura Web »](../giorno-3/README.md) |

In questa terza parte integreremo una skill avanzata di apprendimento interattivo (`/teach`) ideata da Matt Pocock nel nostro workspace, analizzeremo criticamente l'evoluzione del ruolo dello sviluppatore software nell'era degli agenti autonomi esplorando lo **Spettro dello Sviluppo con IA**, discuteremo le insidie dello sviluppo assistito (**AI Pitfalls** di Andrej Karpathy) ed affronteremo il rischio psicologico ed operativo della **Resa Cognitiva** (Cognitive Surrender di Addy Osmani).

---

## 🛠️ 1. Pratica: Espandere l'LLM Wiki e integrare la Skill /teach

Riprendiamo il nostro progetto **LLM Wiki (Second Brain)** creato in Obsidian nella Parte 2. In questa sessione pratica vedremo come arricchire la nostra base di conoscenza con nuove specifiche tecniche e come integrare una skill avanzata per fare in modo che l'agente utilizzi quelle stesse informazioni per insegnarci ad implementare nuove funzionalità.

### A. Istruzioni Aggiuntive: Aggiungere le Fonti sulle Skills

Vogliamo che il nostro Second Brain acquisisca conoscenza su come sono strutturate le Agent Skills. Per farlo, delegheremo all'agente il download e il caricamento dei file di specifica della repository ufficiale all'interno della nostra cartella delle fonti grezze (`raw/`).

1. Ordina all'agente di scaricare il repository che contiene le specifiche delle skill e di rilevare e aggiungere nella directory raw i file della specifica inviando questo prompt:

   ```text
   Aggiungi nella raw i file markdown che descrivono la specifica delle SKILLS in https://github.com/agentskills/agentskills/tree/main
   ```

2. Procedi con l'ingestione delle nuove fonti ordinando all'agente:

   ```text
   Procedi con l'ingest delle nuove fonti
   ```

L'agente elaborerà i nuovi file markdown delle specifiche, aggiornerà le pagine collegate in `wiki/` e registrerà l'operazione in `log.md` e `index.md`.

### B. Il Progetto Skills di Matt Pocock e l'Integrazione di `/teach`

Matt Pocock (noto educatore ed esperto di TypeScript) ha ideato una collezione di skill rilasciate con licenza open source ([mattpocock/skills](https://github.com/mattpocock/skills)).

Tra queste vogliamo integrare la skill `/teach` direttamente **all'interno del nostro progetto LLM Wiki** in Obsidian, in modo che l'agente possa consultare la conoscenza della wiki sulle specifiche e insegnarci passo dopo passo.

1. All'interno della cartella principale del tuo archivio Obsidian (`llm-wiki-sdlc`), crea la cartella `.agents/skills/teach/` (il customization root locale dell'archivio).
2. Copia all'interno di questa cartella tutti i file di supporto della skill `teach` che trovi in `[materiali/skills/teach/](../materiali/skills/teach/)`:
   - `GLOSSARY-FORMAT.md`
   - `LEARNING-RECORD-FORMAT.md`
   - `MISSION-FORMAT.md`
   - `RESOURCES-FORMAT.md`
   - `SKILL.md`

### C. Utilizzo della Skill `/teach` per lo Studio

Ora che la skill è stata caricata all'interno del progetto, ordina al tuo agente di avviarla eseguendo questo comando:

```text
/teach Fai una query e insegnami a scrivere una skill
```

L'agente inizializzerà un vero e proprio "ambiente didattico" all'interno dell'archivio Obsidian creando i file `MISSION.md` e `RESOURCES.md` per tracciare il tuo apprendimento. Invece di darti il codice pronto, l'agente:

- Interrogherà il Second Brain per ricavare le specifiche delle Agent Skills appena importate.
- Ti porrà domande per comprendere il tuo obiettivo didattico.
- Creerà micro-lezioni HTML in una cartella `./lessons/` per spiegarti passo passo come strutturare una skill.
- Ti sottoporrà piccoli quiz e test interattivi per misurare la tua reale comprensione del codice, forzando un'interazione basata sull'**amplificazione reciproca** (cooperazione attiva) anziché sulla delega passiva.

---

## ⚖️ 2. Lo Spettro dello Sviluppo con IA

Lavorare con l'IA nella programmazione non è una scelta binaria (usarla o non usarla). Si tratta di uno **spettro operativo** definito dal livello di struttura, disciplina e verifica applicati:

| Dimensione                      | Vibe Coding                                                                 | Sviluppo Assistito Strutturato                                                     | Agentic Engineering                                                                                  |
| :------------------------------ | :-------------------------------------------------------------------------- | :--------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------- |
| **Specificazione dell'Intento** | Prompt rapidi e informali in linguaggio naturale.                           | Prompt dettagliati con regole, esempi e contesti circoscritti.                     | Specifiche formali, schemi di architettura e file di regole stabili (es. `AGENTS.md` o `CLAUDE.md`). |
| **Verifica**                    | _"Sembra funzionare"_ (test a vista dell'interfaccia).                      | Test manuali mirati ed esecuzione controllata.                                     | Test suite automatizzate, pipeline CI/CD e validazioni programmate (Evals).                          |
| **Comprensione del Codice**     | Minima: lo sviluppatore spesso copia e incolla senza leggere il codice.     | Selettiva: analisi approfondita dei moduli critici modificati dall'IA.             | Architetturale: l'uomo presidia la logica di sistema, l'agente gestisce i dettagli.                  |
| **Gestione Errori**             | Copia e incolla dei messaggi di errore restituiti dall'IDE all'IA.          | Lo sviluppatore analizza il bug, individua la causa e guida l'IA nella correzione. | L'agente esegue i test, legge i log di errore e si corregge in autonomia nella sandbox.              |
| **Scopo Appropriato**           | Prototipi rapidi, script personali, hackathon, esplorazione.                | Nuove funzionalità all'interno di codebase già esistenti e stabili.                | Sistemi di produzione complessi, refactoring di massa, migrazioni stabili.                           |
| **Profilo di Rischio**          | **Alto**: codice instabile, potenziale debito tecnico e falle di sicurezza. | **Moderato**: presidiato da checkpoint decisionali umani.                          | **Basso**: ogni modifica è validata da test deterministici e di qualità.                             |

---

## 🔬 3. AI Pitfalls: Le Insidie del Coding con IA (di Andrej Karpathy)

Per comprendere a fondo come posizionarsi all'interno dello **Spettro dello Sviluppo con IA** appena analizzato — e soprattutto come superare le trappole del puro _Vibe Coding_ per migrare verso la stabilità dell'_Agentic Engineering_ — è utile esaminare l'esperienza sul campo di chi ha coniato e vissuto in prima persona questi concetti.

In questa riflessione, Karpathy descrive la transizione personale a un workflow di sviluppo guidato per l'80% da agenti autonomi. Evidenzia l'importanza di cambiare l'approccio da _imperativo_ (istruire l'agente su ogni singolo passaggio) a _dichiarativo_ (definire criteri di successo e test prima della generazione). Al contempo, solleva interrogativi cruciali sulla tendenza dei modelli a complicare le astrazioni generando codice ridondante ("slop"), e sul rischio a lungo termine di atrofizzare le competenze manuali di programmazione a causa dello sbilanciamento tra la lettura del codice (discriminazione) e la sua scrittura (generazione).

- **Post originale su X**: [Karpathy on X](https://x.com/karpathy/status/2015883857489522876)

```markdown
# Alcune note sparse dopo aver programmato parecchio con Claude nelle ultime settimane

di Andrej Karpathy

**Workflow di programmazione.** Dato il recente salto di qualità nelle capacità di programmazione dei LLM, come molti altri sono passato rapidamente da circa l'80% di programmazione manuale + autocompletamento e il 20% di agenti a novembre, all'80% di programmazione tramite agenti e il 20% di modifiche e ritocchi a dicembre. In altre parole, ora programmo davvero per lo più in inglese, dicendo quasi con un po' di imbarazzo all'LLM quale codice scrivere... a parole. Ferisce un po' l'orgoglio, ma il potere di operare sul software attraverso ampie "azioni di codice" è semplicemente troppo utile nel complesso, specialmente dopo che ci si adatta, lo si configura, si impara a usarlo e si comprende bene cosa può e non può fare. Questo è senza dubbio il cambiamento più grande nel mio workflow di programmazione di base in circa vent'anni di carriera, ed è avvenuto nel giro di poche settimane. Mi aspetterei che stia accadendo qualcosa di simile a una percentuale di ingegneri a doppia cifra abbondante là fuori, mentre la consapevolezza di ciò nella popolazione generale sembra essere decisamente a una cifra percentuale molto bassa.

**IDE / swarm di agenti / fallibilità.** Sia l'hype sul "non c'è più bisogno dell'IDE" sia quello sugli "swarm (sciami) di agenti" sono, a mio parere, eccessivi per il momento. I modelli commettono sicuramente ancora degli errori e, se avete del codice a cui tenete davvero, vi consiglierei di sorvegliarli come un falco, tenendo a fianco un bell'IDE di grandi dimensioni. Gli errori sono cambiati molto: non sono più semplici errori di sintassi, ma sottili errori concettuali che potrebbe commettere uno sviluppatore junior un po' trasandato e sbrigativo. La categoria più comune è quella in cui i modelli fanno supposizioni errate per conto vostro e procedono dritti per la loro strada senza verificare. Inoltre, non gestiscono la propria confusione, non cercano chiarimenti, non fanno emergere le incongruenze, non presentano i compromessi, non si oppongono quando dovrebbero e sono ancora un po' troppo compiacenti. Le cose migliorano nella modalità pianificazione ("plan mode"), ma ci sarebbe bisogno di una modalità di pianificazione inline più leggera. Amano anche complicare eccessivamente il codice e le API, gonfiano le astrazioni, non ripuliscono il codice morto che si lasciano alle spalle, ecc. Implementeranno una struttura inefficiente, gonfia e fragile di oltre 1000 righe di codice, e spetterà a voi dire qualcosa come: "Ehm, non potresti fare semplicemente così invece?" e loro risponderanno: "Certamente!" riducendola immediatamente a 100 righe. A volte continuano a modificare o rimuovere, come effetti collaterali, commenti e porzioni di codice che non gradiscono o non comprendono a sufficienza, anche se ciò è del tutto ortogonale rispetto al compito da svolgere. Tutto questo accade nonostante alcuni semplici tentativi di risolverlo tramite istruzioni nel file `CLAUDE.md`. Nonostante tutti questi problemi, si tratta comunque di un enorme miglioramento netto ed è difficilissimo immaginare di tornare alla programmazione manuale. In sintesi (TLDR): ognuno ha il proprio flusso di sviluppo; il mio attuale consiste in alcune sessioni di Claude Code (CC) sulla sinistra in finestre/tab di Ghostty e un IDE sulla destra per visualizzare il codice ed effettuare modifiche manuali.

**Tenacia.** È estremamente interessante guardare un agente lavorare instancabilmente a qualcosa. Non si stancano mai, non si demoralizzano mai, continuano semplicemente ad andare avanti e a provare soluzioni in situazioni in cui un essere umano si sarebbe arreso da tempo per riprovarci un altro giorno. È un momento in cui si "percepisce l'AGI" (feel the AGI) vederlo lottare con un problema per molto tempo, per poi vederlo uscirne vittorioso 30 minuti dopo. Ci si rende conto che la resistenza è un collo di bottiglia fondamentale per il lavoro e che, con gli LLM a portata di mano, questa è stata aumentata drasticamente.

**Incrementi di velocità.** Non è chiaro come misurare l'accelerazione dovuta all'assistenza degli LLM. Sicuramente mi sento nettamente più veloce in quello che avevo intenzione di fare, ma l'effetto principale è che faccio molto più di quanto avessi pianificato perché: 1) posso programmare ogni genere di cosa che prima semplicemente non sarebbe valsa la pena di scrivere e 2) posso approcciare porzioni di codice su cui prima non avrei potuto lavorare per mancanza di conoscenze o competenze. Quindi si tratta certamente di un'accelerazione, ma è probabilmente molto più un'espansione.

**Effetto leva.** I modelli linguistici (LLM) sono eccezionalmente bravi a eseguire cicli iterativi fino a raggiungere obiettivi specifici, ed è proprio qui che si trova la maggior parte della magia del "percepire l'AGI". Non ditegli cosa fare, dategli dei criteri di successo e guardatelo agire. Fate in modo che scriva prima i test e poi che li superi. Mettetelo nel loop con un browser MCP. Scrivete prima voi l'algoritmo ingenuo (naive) che è molto probabilmente corretto, poi chiedetegli di ottimizzarlo preservandone la correttezza. Cambiate il vostro approccio da imperativo a dichiarativo per far sì che gli agenti iterino più a lungo e possiate ottenere un maggiore effetto leva.

**Divertimento.** Non avevo previsto che con gli agenti programmare sarebbe sembrato _più_ divertente, perché gran parte della fatica ripetitiva di "riempire i vuoti" viene rimossa e ciò che resta è la parte creativa. Mi sento anche meno bloccato (il che non è divertente) e sperimento molto più coraggio, perché c'è quasi sempre un modo per lavorare mano nella mano con l'IA per fare qualche progresso positivo. Ho visto anche il sentimento opposto in altre persone; la programmazione con gli LLM dividerà gli ingegneri tra coloro a cui piaceva principalmente scrivere codice (coding) e coloro a cui piaceva principalmente creare (building).

**Atrofia.** Ho già notato che sto iniziando lentamente ad atrofizzare la mia capacità di scrivere codice manualmente. La generazione (scrivere codice) e la discriminazione (leggere/valutare il codice) sono abilità diverse nel cervello. In gran parte a causa di tutti i piccoli dettagli, per lo più sintattici, coinvolti nella programmazione, si può revisionare il codice benissimo anche se si fa fatica a scriverlo.

**Slopocalisse.** Mi sto preparando al 2026 come l'anno della "slopocalisse" su GitHub, Substack, arXiv, X/Instagram e in generale su tutti i media digitali. Vedremo anche molto più "teatro della produttività" basato sull'hype dell'IA (è mai possibile?), a fianco di miglioramenti effettivi e reali.

**Domande.** Alcune delle domande che mi frullano in testa:

- Cosa succede all' "ingegnere 10x" – ovvero al rapporto di produttività tra l'ingegnere medio e quello massimo? È del tutto possibile che questo cresca _moltissimo_.
- Armati di LLM, i generalisti supereranno sempre di più gli specialisti? Gli LLM sono molto più bravi a riempire i vuoti (il micro) che nella grande strategia (il macro).
- Come sarà programmare con gli LLM in futuro? Sarà come giocare a StarCraft? Giocare a Factorio? Suonare musica?
- Quanta parte della società è frenata dal collo di bottiglia del lavoro intellettuale digitale?

**TLDR (In sintesi): Dove ci lascia tutto questo?** Le capacità degli agenti LLM (specialmente Claude e Codex) hanno superato una sorta di soglia di coerenza intorno a dicembre 2025, provocando una transizione di fase nell'ingegneria del software e nei settori strettamente correlati. La componente legata all'intelligenza sembra improvvisamente parecchio più avanti rispetto a tutto il resto: integrazioni (strumenti, conoscenza), necessità di nuovi flussi di lavoro organizzativi, processi e diffusione più in generale. Il 2026 sarà un anno ad altissima energia mentre l'industria metabolizza questa nuova capacità.
```

---

## 🚫 4. La Resa Cognitiva: Evitare il Debito di Comprensione (di Addy Osmani)

Se le osservazioni pratiche di Karpathy mettono in guardia dalle prime insidie tecniche dello sviluppo delegato all'agente (come l'inizio dell'atrofia delle competenze e l'approvazione frettolosa di modifiche non comprese), Addy Osmani spinge l'analisi su un piano cognitivo e psicologico più profondo. Osmani affronta il rischio che il risparmio di fatica immediata si trasformi in una totale **Resa Cognitiva (Cognitive Surrender)**, in cui il programmatore smette di formulare un modello mentale autonomo del software, accumulando un pericoloso _debito di comprensione_ destinato a paralizzare il progetto al verificarsi del primo bug complesso.

In questo saggio, Osmani analizza la differenza fondamentale tra delegare all'IA compiti ripetitivi mantenendo il controllo e la comprensione logica (_Scaricamento Cognitivo_) e accettare ciecamente l'output del modello per pigra compiacenza, accumulando un debito tecnico e cognitivo che renderà il programmatore incapace di comprendere o riparare il sistema nel lungo periodo.

- **Post originale**: [Cognitive Surrender - Addy Osmani](https://addyosmani.com/blog/cognitive-surrender/)

---

```markdown
# La Resa Cognitiva (Cognitive Surrender)

di Addy Osmani

Il _cognitive offloading_ (lo scaricamento cognitivo) consiste nel delegare all'IA pur rimanendo proprietari della risposta. La _resa cognitiva_ si verifica quando l'output dell'IA diventa silenziosamente il tuo output e ritieni che non sia rimasto nulla da verificare. Per gli ingegneri del software, il confine tra queste due condizioni si sposta sotto i piedi quasi ogni giorno, e la maggior parte di noi lo sta superando senza rendersene conto.

C'è un termine che ho sentito ieri e di cui volevo discutere: _resa cognitiva_. Proviene da un recente articolo della Wharton School della UPenn, firmato da Steven Shaw e Gideon Nave: _“Thinking - Fast, Slow, and Artificial: How AI is Reshaping Human Reasoning and the Rise of Cognitive Surrender”_ (Pensare - Veloce, Lento e Artificiale: Come l'IA sta rimodellando il ragionamento umano e l'ascesa della resa cognitiva). L'espressione ha radici teologiche più antiche, ma la sua applicazione al contesto dell'IA è nuova e colpisce duramente chiunque rilasci codice avendo un agente al proprio fianco.

La distinzione che propongono è la parte che vale la pena memorizzare:

> Il _cognitive offloading_ è la calcolatrice, il motore di ricerca, il GPS. Deleghi il _come_ e mantieni il _cosa_. Valuti comunque se il risultato è sensato e intervieni quando non lo è. La _resa cognitiva_ è ciò che accade quando smetti del tutto di costruire la risposta. L'output dell'IA diventa il tuo output. Non c'è nulla da correggere, perché non hai mai elaborato un'opinione indipendente con cui confrontarlo.

Attraverso tre esperimenti e 1.372 partecipanti, Shaw e Nave hanno scoperto che la semplice disponibilità di un'IA era sufficiente a spingere le persone ad arrendersi. Nelle prove in cui l'IA si sbagliava, il 73% delle volte i partecipanti hanno accettato la risposta errata. Peggio ancora: la loro sicurezza aumentava quando l'IA era disponibile, anche se metà delle risposte erano deliberatamente errate. Prendevano in prestito la sicurezza del modello (che è sempre piuttosto elevata) e la consideravano propria.

Questo effetto di sicurezza presa in prestito è il punto in cui questa smette di essere una storia di cognizione generale e inizia a riguardare l'ingegneria del software.

---

## Dove si manifesta la resa nel nostro lavoro

La maggior parte di noi non si arrende sulle cose facili. Ci accorgiamo se un agente inventa un'API o fabbrica un import. La resa avviene più in basso nello stack, nei momenti in cui il costo di formulare un'opinione indipendente sembra sproporzionato rispetto al compito da svolgere.

Alcuni ambiti in cui l'ho visto accadere, per lo più a me stesso:

- **Leggere le differenze (il _diff_):** L'agente produce una pull request (PR) da 600 righe. La scorri rapidamente. I nomi delle variabili sono ragionevoli. I test sono verdi. Approvi. Da qualche parte nel mezzo c'è un sottile cambiamento nell'ordine in un confine di transazione, o un valore predefinito che si inverte per un caso limite che non hai pensato di controllare. Non hai revisionato il codice. Lo hai ratificato. La resa è stata l'assenza di una decisione.
- **Risolvere un errore (_debug_) che non comprendi appieno:** Lo stack trace sembra spaventoso. Lo incolli nell'agente. Ti restituisce una soluzione. Funziona. Vai avanti. Due settimane dopo riaffiora un sintomo correlato e ti rendi conto di non aver mai compreso davvero il bug originale. Ne hai solo rimosso la manifestazione visibile. Il modello mentale che hai del sistema nella tua testa è ora errato in un punto che non sai nemmeno individuare.
- **Prendere una decisione di progettazione (_design_):** Non sei sicuro se utilizzare una coda o una chiamata diretta tra due servizi. Chiedi all'agente. Sceglie un'opzione fornendo un paragrafo di giustificazione che suona molto sicuro. Ti adegui. Non hai ragionato sul throughput, sulle modalità di guasto o sulla semantica di riproduzione (_replay_). Hai accolto l'inquadramento del problema fatto dal modello e la sua risposta con lo stesso identico gesto.
- **Imparare qualcosa di nuovo:** Questo è l'aspetto su cui il documento di Anthropic sulla formazione delle competenze (_skill-formation_) fornisce dati numerici. Gli ingegneri che hanno usato l'IA per generare codice durante l'apprendimento di una nuova libreria hanno ottenuto un punteggio inferiore del 17% in un quiz di comprensione successivo rispetto al gruppo di controllo. Gli ingegneri che hanno usato l'IA per un'indagine concettuale (facendo domande, esplorando i compromessi) hanno tenuto testa. Stesso strumento. L'atteggiamento ha cambiato il risultato.

Il filo conduttore di tutte queste situazioni è lo stesso: il modello ha offerto una risposta completa e noi l'abbiamo accettata invece di elaborare una nostra visione parallela. A volte è corretto così. Altre volte è una resa. Le due cose sembrano identiche viste dall'interno.

---

## Il legame con il debito di comprensione

Ho già scritto in passato del _debito di comprensione_ — il divario crescente tra la quantità di codice esistente nel sistema e quanto di esso sia effettivamente compreso da un essere umano. La resa cognitiva è il meccanismo attraverso il quale si accumula questo debito di comprensione.

Ogni atto di resa è un piccolo prestito. La base di codice cresce di un'altra patch che non comprendi appieno. L'architettura assorbe un'altra decisione che non hai preso. La suite di test acquisisce un test che non hai pensato di specificare. Nessuno di questi sembra un problema il giorno in cui avviene. Si accumulano con interessi composti.

La ricerca del MIT _“Your Brain on ChatGPT”_ ha mostrato lo stesso schema a livello neurale: gli scrittori che si affidavano all'IA mostravano una connettività neurale misurabilmente ridotta, una memoria più debole di ciò che avevano appena prodotto e difficoltà a ricostruire il proprio ragionamento. Gli autori lo hanno definito _debito cognitivo_, termine mutuato dal concetto di debito tecnico: guadagno a breve termine, costo a lungo termine con interessi composti.

Metti insieme le due prospettive. La resa cognitiva è il modo in cui ti carichi di debito cognitivo. Il debito di comprensione è la fattura, denominata in termini di modello mentale perduto. Gli interessi si pagano la volta successiva in cui qualcosa va storto e nessuno nel team è in grado di ricostruire il sistema a partire dai principi fondamentali.

L'IA non crea il debito. È l'atteggiamento che adotti nei suoi confronti a farlo. Lo stesso modello che svuota il modello mentale di un ingegnere può affinare quello di un altro, a seconda che lo si utilizzi per pensare o per evitare di farlo.

---

## Perché gli ingegneri del software sono particolarmente esposti

Alcune caratteristiche del nostro lavoro ci rendono più vulnerabili rispetto alla media dei lavoratori della conoscenza.

- **I segnali superficiali sembrano corretti per impostazione predefinita:** Il codice generato si compila. Supera il linter. Funziona. Somiglia al resto del file. La maggior parte degli altri ambiti non ha un filtro così forte di "sembra plausibile" per l'output dell'IA. Il nostro sì, ed è il filtro sbagliato. La correttezza superficiale non è correttezza sistemica, e il divario tra le due è proprio dove si nasconde la resa.
- **La produttività (_throughput_) è la metrica visibile:** PR unite, funzionalità rilasciate, ticket chiusi. Nessuno di questi dati distingue tra "l'ho creato io e lo capisco" e "l'agente lo ha creato e io l'ho approvato". L'organizzazione premia entrambi allo stesso modo nel breve periodo. La resa è invisibile ai grafici di controllo (_dashboard_).
- **La sicurezza si trasmette in modo pulito:** I modelli parlano con frasi dichiarative. Chi effettua le revisioni del codice tende a interpretare le dichiarazioni come espressione di autorità. Quando l'agente scrive _"qui usiamo un debounce di 300 ms per evitare rallentamenti (jank)"_, suona come una conoscenza istituzionale consolidata, anche se il modello ha inventato quel numero sul momento. Ne erediti la certezza senza ereditarne il ragionamento (inesistente).
- **Il lavoro si compone:** Ogni resa facilita la successiva. Una volta che hai accettato un blocco di codice che non comprendi appieno, la modifica successiva a quel blocco sarà quasi certamente un altro atto di resa, perché elaborare una visione indipendente ora richiederebbe la ricostruzione della parte che hai saltato prima. La resa dipende dal percorso intrapreso (_path-dependent_).

Non sto argomentando contro gli strumenti di programmazione basati sull'IA. L'atteggiamento conta più dello strumento, e non abbiamo ancora sviluppato molte delle abitudini di cui avremmo bisogno.

---

## La questione della calibrazione

Lo stesso Shaw è attento a non fare allarmismo su questo tema. La sua impostazione è quella che ripeterei a chiunque utilizzi seriamente questi strumenti:

> "La resa cognitiva non equivale a dire che l'IA sia un male o che usarla sia irrazionale; in molti contesti, l'IA può migliorare la capacità di giudizio. Il problema chiave è la calibrazione: sapere quando l'IA ti sta aiutando a pensare e quando sta silenziosamente pensando al posto tuo."

La domanda da porsi continuamente è: sto elaborando un'opinione indipendente su questa risposta, o sto semplicemente adottando in toto la visione dell'agente? Si tratta di atti psicologici differenti che appaiono identici dall'esterno.

Alcune euristiche che ho iniziato a usare per mantenermi dal lato corretto della linea, ovvero quello del _cognitive offloading_:

- **Formulare un'aspettativa prima di leggere l'output:** Prima di avviare l'agente su un compito non banale, metto per iscritto (anche solo nella mia testa) come penso dovrebbe apparire la risposta. Tre righe o cinquanta. Una coda o una chiamata diretta. Se il bug si trova in questo modulo o in quello. Quando la risposta dell'agente coincide con la mia aspettativa, sono calibrato. Quando non coincide, ho una vera scelta da compiere: ho sbagliato io o ha sbagliato l'IA? Questa scelta è l'elemento che la resa evita.
- **Leggere le modifiche (il _diff_) come se non le avesse scritte l'IA:** Fai finta che sia stato un ingegnere junior del tuo team a presentare la PR. La uniresti solo sulla base del fatto che "i test passano"? Sicuramente no. Lo stesso standard dovrebbe applicarsi quando l'autore è un modello. Il lavoro non è cambiato; è cambiato l'autore. "Sembra a posto" continua a non essere una vera revisione.
- **Chiedere al modello di argomentare contro se stesso:** La maggior parte dei modelli produrrà una risposta sicura e poi, se sollecitata, produrrà un contro-argomento altrettanto sicuro. Questo secondo passaggio costa poco e spezza l'effetto della certezza presa in prestito. Se non riesci a decidere con logica quale delle due risposte sia corretta, hai trovato un punto in cui stavi per arrenderti.
- **Accorgersi di quando si è stanchi:** La resa è un fenomeno legato alla fatica. La prima PR del giorno riceve una vera revisione; la quinta riceve solo un'occhiata rapida. Gli ingegneri senior di cui mi fido sono tutti giunti alla stessa conclusione: _"Smettere di far generare codice all'agente quando si è troppo stanchi per valutarlo"_. Questa autoconsapevolezza fa parte del lavoro adesso.
- **Osservare da dove proviene la sicurezza:** Se ti ritrovi a difendere una scelta di progettazione in una riunione e non riesci effettivamente a ricostruire il motivo per cui è stata presa, se non per il fatto che l'agente l'ha suggerita e sembrava ragionevole, hai ereditato la sicurezza del modello senza possedere il ragionamento sottostante. Questo è un artefatto della resa. Torna al codice e ricostruisci il _perché_ prima che la discussione continui.

---

## Scelte ingegneristiche per resistere alla resa

Le euristiche personali sono importanti, ma esiste anche una versione strutturale di tutto questo. La maggior parte delle cose di cui ho scritto negli ultimi mesi (_Agent Skills_, ingegnerizzazione dell'imbracatura degli agenti, l'articolo sul debito di comprensione) riguarda la costruzione di un'impalcatura che renda più difficile la resa.

Un breve elenco di strategie che funzionano:

- **La verifica come criterio di uscita tassativo:** Ogni compito completato dall'agente dovrebbe concludersi con una prova concreta: un test che viene eseguito, uno screenshot, un registro (_log_), una traccia di runtime o l'approvazione di un revisore. "Sembra finito" è l'approccio favorevole alla resa. "Ecco la prova che funziona" è quello resistente alla resa. Integra l'obbligo di fornire prove nel flusso di lavoro per eliminare la via di fuga più facile verso la resa.
- **Tabelle anti-razionalizzazione:** La scelta di progettazione più distintiva in _Agent Skills_ consiste nel dotare ogni scusa comune utilizzata per saltare una fase del flusso di lavoro di una confutazione scritta. Questo funge anche da meccanismo di resistenza alla resa. _"Questo compito è troppo semplice per richiedere una specifica"_ $\rightarrow$ _"I criteri di accettazione si applicano comunque"_. In questo modo si scrive in anticipo la confutazione a una razionalizzazione che il modello (o la tua versione stanca del venerdì pomeriggio) non ha ancora elaborato. I modelli sono eccezionali nel generare motivi plausibili per saltare i passaggi rigorosi. Le tabelle anti-razionalizzazione si rifiutano di scendere a patti sul momento.
- **Ambito d'azione più ridotto, PR più piccole:** La resa aumenta proporzionalmente alle dimensioni. Una modifica di 50 righe si riesce a leggere davvero; una di 600 righe no. La norma di Google di mantenere le PR intorno alle 100 righe esiste per ragioni umane, ma funziona contro la resa all'IA per gli stessi identici motivi. L'unità di revisione è l'unità di comprensione. Rendi l'unità abbastanza piccola da poter essere realmente compresa.
- **Indagine concettuale anziché generazione, durante l'apprendimento:** Questa è la scoperta dello studio sulla formazione delle competenze riformulata sotto forma di abitudine. Quando affronti per la prima volta una libreria o un sistema, chiedi all'agente di spiegarti il funzionamento prima di chiedergli di generare. Lo stesso strumento, usato per interrogare anziché per produrre, costruisce il tuo modello mentale invece di eroderlo. I dati su questo punto sono inequivocabili e il costo del cambio di modalità è irrilevante.
- **Attrito intenzionale (_friction by design_):** L'articolo di arXiv _“Cognitive Agency Surrender”_ propone la _Scaffolded Cognitive Friction_ (attrito cognitivo strutturato): introdurre deliberatamente momenti di resistenza per interrompere l'accettazione euristica. In termini ingegneristici: un documento di progettazione richiesto prima della generazione, una fase di conferma prima dell'unione (_merge_), una lista di controllo prima del rilascio (_deploy_). L'attrito ha una cattiva reputazione nei discorsi sulla produttività, eppure è esattamente ciò che si frappone tra lo scaricamento e la resa.
- **Tempo da soli alla tastiera:** Scrivi del codice senza l'agente, ogni settimana. Non come esercizio morale, ma come esercizio di calibrazione. Il giorno in cui non riuscirai a costruire comodamente qualcosa di semplice senza l'assistenza dell'IA sarà il giorno in cui lo scaricamento si sarà trasformato in resa a tua insaputa.

---

## Amplificazione reciproca, non delega

La prospettiva con cui voglio concludere non è cupa. Andy Clark, citato dal _Time_ a proposito di questa ricerca, fa la distinzione corretta: c'è differenza tra delegare a un sistema di IA e cooperare con esso. La delega produce resa. La cooperazione produce ciò che lui chiama _amplificazione reciproca_: un ciclo in cui i tuoi prompt affinano l'output del modello, il che a sua volta affina i tuoi prompt successivi, che di conseguenza affinano il tuo modello concettuale del problema.

È una differenza percepibile. Con l'amplificazione reciproca ti ritrovi a imparare il dominio d'applicazione attraverso la conversazione, e non a scapito di essa. Termini la sessione con un modello mentale più nitido rispetto a quello di partenza, non più confuso. Sei ancora in grado di costruire il sistema da solo; hai semplicemente scelto una strada più veloce. L'agente è il secondo ingegnere nella stanza, non l'unico.

L'atteggiamento di resa è l'opposto. L'agente termina con un modello del problema più nitido del tuo. Non riesci a ricostruire la progettazione. Non riesci a fare il debug del codice senza l'aiuto dell'agente. Hai esternalizzato proprio la parte di lavoro che avrebbe dovuto renderti migliore.

Entrambi gli approcci utilizzano gli stessi strumenti. Entrambi producono codice che viene rilasciato. Dall'esterno, nell'arco di un singolo sprint, sembrano identici. La differenza si nota sei mesi dopo, quando qualcosa si rompe e uno dei due ingegneri è in grado di risolverlo partendo dai principi fondamentali, mentre l'altro no.

---

## Cosa vorrei principalmente ottenere con questo articolo

Non intendo spaventare nessuno o allontanarlo da questi strumenti. Li uso ogni giorno. Ho rilasciato più codice negli ultimi dodici mesi che in qualsiasi altro periodo analogo in precedenza, e penso che chi ne rimane fuori stia commettendo un errore molto più grande rispetto a chi vi si affida.

Tuttavia, l'atteggiamento è importante e non se ne parla abbastanza. Il dibattito verte soprattutto su ciò che i modelli sanno fare. Dovrebbe invece riguardare almeno altrettanto ciò che noi stiamo facendo con essi, e se la risposta sia pensare _con_ l'IA o smettere del tutto di pensare.

Lo scaricamento cognitivo (_cognitive offloading_) è un superpotere. La resa cognitiva è la modalità di errore (_failure mode_) che si verifica quando lo si usa senza notare la linea di confine tra i due stati. Il lavoro consiste sempre più nel rimanere calibrati su quale lato di quella linea ci si trovi in ogni singolo momento.

Se il tuo codice viene rilasciato ma la tua comprensione del sistema si riduce, stai pagando sotto forma di debito cognitivo. Se il tuo codice viene rilasciato e la tua comprensione del sistema cresce, stai facendo il vero lavoro, semplicemente più velocemente di prima.

Gli strumenti sono gli stessi in entrambi i casi. È l'atteggiamento ad essere diverso. Questa è la parte che rimane interamente tua.
```

---

[« Parte 2: LLM Wiki (Second Brain) e Agent Skills](02-llm-wiki-agent-skills.md) | **Parte 3: Sviluppo Assistito, AI Pitfalls e Resa Cognitiva** | [Giorno 3: Architettura Web »](../giorno-3/README.md) |
