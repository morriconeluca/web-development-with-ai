# Parte 4: Sviluppo del Progetto - Lavagna Collaborativa

---

## | [« Parte 3: Database in Tempo Reale con Firestore](03-database-firestore.md) | **Parte 4: Sviluppo del Progetto - Lavagna Collaborativa** | [Esercizio Giorno 3: Post-it Personalizzati e Collaborazione](05-compito-postit-personalizzati.md) » |

È il momento di unire tutti i tasselli studiati ed avviare il nostro progetto pratico di gruppo: la **Lavagna Collaborativa di Post-it in tempo reale**. In questo laboratorio guideremo l'agente integrato nell'IDE ad aiutarci nella stesura del codice, comprendendo come implementare il drag-and-drop logico e la sincronizzazione di rete.

---

## 🛠️ 1. Architettura dei Dati del Progetto

Il progetto si compone di una lavagna a tutto schermo su cui gli utenti possono creare post-it e trascinarli ovunque.

Il modello dati del singolo documento all'interno della collezione `postit` su Firestore è così composto:

- `testo` (String): Il messaggio scritto sul foglietto.
- `x` (Number): La coordinata orizzontale di posizionamento assoluto (in pixel o percentuale rispetto allo schermo).
- `y` (Number): La coordinata verticale di posizionamento assoluto.
- `colore` (String): Il colore di sfondo del post-it (es. classi Tailwind come `bg-yellow-200`, `bg-sky-200`).

---

## 💻 2. Il Codice Completo dell'Applicazione (`index.html`)

Ecco il codice sorgente completo da salvare nel tuo workspace come `index.html`.

> [!IMPORTANT]
> Ricorda di sostituire l'oggetto `firebaseConfig` con le credenziali del tuo progetto copiate precedentemente dalla console di Firebase durante la Parte 3.

```html
<!DOCTYPE html>
<html lang="it">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Lavagna Post-it Collaborativa</title>
    <!-- Tailwind CSS via CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
  </head>
  <body
    class="bg-slate-900 text-white h-screen w-screen overflow-hidden flex flex-col font-sans select-none"
  >
    <!-- Header della Lavagna -->
    <header
      class="bg-slate-800/80 backdrop-blur border-b border-slate-700 p-4 flex justify-between items-center z-10"
    >
      <div>
        <h1
          class="text-xl font-bold tracking-tight text-white flex items-center gap-2"
        >
          📌 Lavagna Collaborativa Real-Time
        </h1>
        <p class="text-xs text-slate-400">
          Trascina i post-it. Le modifiche si sincronizzano all'istante su tutti
          gli schermi.
        </p>
      </div>
      <button
        id="add-btn"
        class="bg-indigo-600 hover:bg-indigo-700 text-white font-semibold py-2 px-5 rounded-lg shadow-lg hover:shadow-indigo-500/20 active:scale-95 transition"
      >
        + Aggiungi Post-it
      </button>
    </header>

    <!-- Area di lavoro (Canvas) -->
    <main
      id="canvas"
      class="relative flex-1 w-full h-full bg-[radial-gradient(#334155_1px,transparent_1px)] [background-size:20px_20px] bg-slate-900"
    >
      <!-- I post-it verranno iniettati qui dinamicamente -->
    </main>

    <!-- Script Firebase & Logica Applicativa -->
    <script type="module">
      import { initializeApp } from 'https://www.gstatic.com/firebasejs/12.15.0/firebase-app.js';
      import {
        getFirestore,
        collection,
        addDoc,
        onSnapshot,
        updateDoc,
        doc,
      } from 'https://www.gstatic.com/firebasejs/12.15.0/firebase-firestore.js';

      // ⚠️ SOSTITUISCI CON LE TUE CREDENZIALI FIREBASE
      const firebaseConfig = {
        apiKey: 'LA_TUA_API_KEY',
        authDomain: 'IL_TUO_AUTH_DOMAIN',
        projectId: 'IL_TUO_PROJECT_ID',
        storageBucket: 'IL_TUO_STORAGE_BUCKET',
        messagingSenderId: 'IL_TUO_MESSAGING_SENDER_ID',
        appId: 'IL_TUO_APP_ID',
      };

      // Inizializza Firebase e Firestore
      const app = initializeApp(firebaseConfig);
      const db = getFirestore(app);
      const postitCol = collection(db, 'postit');

      const canvas = document.getElementById('canvas');
      const addBtn = document.getElementById('add-btn');

      // --- 1. AGGIUNGI UN NUOVO POST-IT ---
      addBtn.addEventListener('click', async () => {
        const testo = prompt('Cosa vuoi scrivere sul post-it?');
        if (!testo) return;

        // Crea un documento su Firestore posizionato al centro dello schermo
        try {
          await addDoc(postitCol, {
            testo: testo,
            x: 100 + Math.random() * 200, // Posizione iniziale casuale
            y: 100 + Math.random() * 200,
            colore: 'bg-yellow-200', // Colore di default
          });
        } catch (e) {
          console.error('Errore durante il salvataggio:', e);
        }
      });

      // --- 2. ASCOLTA E RENDERING IN TEMPO REALE ---
      onSnapshot(postitCol, (snapshot) => {
        // Pulisce l'area di lavoro prima di ridisegnare per evitare duplicati
        canvas.innerHTML = '';

        snapshot.forEach((documento) => {
          const id = documento.id;
          const dati = documento.data();

          // Creazione HTML del post-it
          const postit = document.createElement('article');
          postit.id = id;
          postit.className = `absolute ${dati.colore} text-slate-800 p-4 w-48 h-48 rounded-xl shadow-lg border border-yellow-300/20 cursor-grab active:cursor-grabbing flex flex-col justify-between transition-shadow hover:shadow-2xl`;
          postit.style.left = `${dati.x}px`;
          postit.style.top = `${dati.y}px`;

          postit.innerHTML = `
          <p class="text-sm font-medium overflow-y-auto max-h-32 select-none">${dati.testo}</p>
          <span class="text-[9px] text-slate-500 font-mono self-end">ID: ${id.substring(0, 5)}</span>
        `;

          // Abilita la logica di drag-and-drop sul post-it creato
          attivaDragDrop(postit);
          canvas.appendChild(postit);
        });
      });

      // --- 3. LOGICA DI DRAG & DROP VANILLA JS ---
      function attivaDragDrop(element) {
        let active = false;
        let currentX;
        let currentY;
        let initialX;
        let initialY;
        let xOffset = 0;
        let yOffset = 0;

        element.addEventListener('mousedown', dragStart);

        function dragStart(e) {
          // Impedisce la selezione indesiderata del testo circostante
          e.preventDefault();

          initialX = e.clientX - parseFloat(element.style.left || 0);
          initialY = e.clientY - parseFloat(element.style.top || 0);

          if (e.target === element || element.contains(e.target)) {
            active = true;
            document.addEventListener('mousemove', drag);
            document.addEventListener('mouseup', dragEnd);
          }
        }

        function drag(e) {
          if (!active) return;

          currentX = e.clientX - initialX;
          currentY = e.clientY - initialY;

          // Limita il trascinamento all'interno dell'area visibile dello schermo
          if (currentX < 0) currentX = 0;
          if (currentY < 0) currentY = 0;

          element.style.left = `${currentX}px`;
          element.style.top = `${currentY}px`;
        }

        async function dragEnd() {
          if (!active) return;

          active = false;
          document.removeEventListener('mousemove', drag);
          document.removeEventListener('mouseup', dragEnd);

          // Aggiorna le nuove coordinate su Firestore
          const docRef = doc(db, 'postit', element.id);
          try {
            await updateDoc(docRef, {
              x: currentX,
              y: currentY,
            });
          } catch (e) {
            console.error("Errore nell'aggiornamento della posizione:", e);
          }
        }
      }
    </script>
  </body>
</html>
```

---

## 👥 3. Laboratorio di Gruppo (Multi-User Test)

Ecco lo scenario del laboratorio di gruppo per valutare la sincronizzazione in tempo reale:

1. **Lancio in locale**: Fai clic destro sul file `index.html` creato nell'IDE e aprilo all'interno del browser (oppure avvia un server di sviluppo locale integrato).
2. **Condivisione**: Copia l'intero codice o assicurati che i tuoi compagni di banco utilizzino lo **stesso identico `firebaseConfig`** nel loro file `index.html`.
3. **Il Test Collaborativo**:
   - Apri l'applicazione sul tuo browser.
   - Chiedi ad altri compagni di classe di fare lo stesso dai loro rispettivi computer del laboratorio.
   - Aggiungete ciascuno un post-it firmato. Vedrete il post-it apparire istantaneamente sugli schermi di tutti i compagni.
   - Trascina un post-it sulla tua scrivania virtuale. Lo vedrai muoversi sugli schermi degli altri compagni in tempo reale senza dover ricaricare la pagina!

---

## ⚡ 4. Estensione Guidata: Modifica dei Post-it in Tempo Reale

Per rendere la nostra lavagna ancora più interattiva, prima di passare agli esercizi autonomi, implementeremo insieme una funzionalità fondamentale: la **modifica in tempo reale** del testo di un post-it tramite doppio clic.

Questo ci mostrerà come aggiornare campi specifici di un documento Firestore già esistente usando la funzione `updateDoc`.

### Come procedere

All'interno del blocco `onSnapshot`, subito dopo aver creato l'elemento `postit` e prima di appenderlo al `canvas`, aggiungiamo un ascoltatore per l'evento di doppio clic (`dblclick`):

```javascript
// Rileva il doppio clic sul post-it per modificarne il testo
postit.addEventListener('dblclick', async () => {
  // Mostra un prompt precompilato con il testo attuale
  const nuovoTesto = prompt('Modifica il testo del post-it:', dati.testo);

  // Se l'utente clicca su "Annulla" o lascia vuoto, non fare nulla
  if (nuovoTesto === null || nuovoTesto.trim() === '') return;

  // Ottieni il riferimento al documento specifico su Firestore
  const docRef = doc(db, 'postit', id);

  try {
    // Aggiorna solo il campo "testo" nel database
    await updateDoc(docRef, {
      testo: nuovoTesto,
    });
  } catch (e) {
    console.error('Errore durante la modifica del testo:', e);
  }
});
```

### Perché questa modifica è istantanea?

1. L'utente fa doppio clic e inserisce il nuovo testo.
2. `updateDoc` invia la modifica a Firestore in cloud.
3. Firestore aggiorna il documento e notifica immediatamente tutti i client connessi tramite il canale aperto da `onSnapshot`.
4. La funzione di rendering si attiva su tutti i browser dei compagni ridisegnando il post-it con il testo modificato, senza bisogno di ricaricare la pagina!

---

[« Parte 3: Database in Tempo Reale con Firestore](03-database-firestore.md) | **Parte 4: Sviluppo del Progetto - Lavagna Collaborativa** | [Esercizio Giorno 3: Post-it Personalizzati e Collaborazione](05-compito-postit-personalizzati.md) » |
