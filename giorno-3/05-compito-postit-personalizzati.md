# Esercizio Giorno 3: Post-it Personalizzati e Collaborazione

---

## | [« Parte 4: Sviluppo del Progetto - Lavagna Collaborativa](04-progetto-lavagna-collaborativa.md) | **Esercizio Giorno 3: Post-it Personalizzati e Collaborazione** | [Messa in Produzione: GitHub e Deploy su Netlify](06-deploy-netlify-github.md) » |

L'obiettivo di questo compito è consolidare le competenze acquisite sull'interazione tra codice Javascript (client) e database Firebase (server), spingendoti ad estendere l'applicazione con nuove funzionalità e a pubblicare il risultato tramite Git.

## 📝 Traccia dell'Esercizio

Estendi l'applicazione `index.html` realizzata in classe implementando **almeno una (1)** delle seguenti tre opzioni a scelta.

> [!TIP]
> Se vuoi metterti alla prova ed ottenere una valutazione eccellente, prova ad implementarne più di una!

### Opzione A: Palette di Colori per i Post-it

Attualmente, tutti i post-it creati sono di colore giallo (`bg-yellow-200`).

- **Cosa fare**: Modifica la finestra di creazione del post-it (o aggiungi dei piccoli cerchi colorati all'interno di ciascun post-it) per consentire all'utente di scegliere il colore.
- **Dettagli tecnici**: Assicurati che all'atto del salvataggio su Firestore venga salvata la stringa di classe Tailwind corretta (es. `bg-pink-200`, `bg-emerald-200`, `bg-sky-200`, `bg-yellow-200`). L'interfaccia deve aggiornarsi dinamicamente per mostrare il colore scelto.

### Opzione B: Firma dell'Autore

- **Cosa fare**: Aggiungi la possibilità per l'utente di firmare il post-it con il proprio nome.
- **Dettagli tecnici**:
  - Quando l'utente fa clic su "+ Aggiungi Post-it", richiedi (tramite un secondo `prompt` o un form) il nome dell'autore.
  - Salva il campo `autore` nel documento Firestore.
  - Aggiorna la funzione di rendering per mostrare in calce al post-it il nome dell'autore in piccolo (es. _"Scritto da: Marco"_).

### Opzione C: Eliminazione dei Post-it

Attualmente, i post-it rimangono memorizzati sulla lavagna all'infinito.

- **Cosa fare**: Aggiungi un pulsante di cancellazione (es. un'emoji di un cestino 🗑️ o una `❌`) in alto a destra su ogni post-it. Cliccando sul pulsante, il post-it deve essere eliminato definitivamente dal database (e quindi scomparire istantaneamente dagli schermi di tutti gli utenti).
- **Dettagli tecnici**:
  - Importa la funzione `deleteDoc` dall'SDK Firestore:
    `import { deleteDoc, doc } from "https://www.gstatic.com/firebasejs/12.15.0/firebase-firestore.js";`
  - Aggiungi un addEventListener sul clic del pulsante che richiama `await deleteDoc(doc(db, "postit", id))`.
  - **Suggerimento**: Ricordati di usare `e.stopPropagation()` sull'evento del pulsante di eliminazione per evitare che il clic sul pulsante attivi accidentalmente la logica di inizio del drag-and-drop del post-it!

---

[« Parte 4: Sviluppo del Progetto - Lavagna Collaborativa](04-progetto-lavagna-collaborativa.md) | **Esercizio Giorno 3: Post-it Personalizzati e Collaborazione** | [Messa in Produzione: GitHub e Deploy su Netlify](06-deploy-netlify-github.md) » |
