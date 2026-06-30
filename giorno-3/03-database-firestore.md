# Ora 3: Database in Tempo Reale con Firestore

---

## | [« Ora 2: Frontend Rapido con Tailwind CSS](02-frontend-rapido-tailwind.md) | **Ora 3: Database Firestore** | [Ora 4: Sviluppo del Progetto - Lavagna Collaborativa](04-progetto-lavagna-collaborativa.md) » |

Nelle prime due ore abbiamo visto come strutturare l'interfaccia (client) e come i dati viaggiano sul web. Ora collegheremo la nostra applicazione a un database in cloud di tipo NoSQL, imparando a configurare Firebase Firestore ed a sfruttare la sincronizzazione dati in tempo reale per abilitare la collaborazione tra diversi utenti.

---

## 🔋 1. Database Relazionali (SQL) vs Documentali (NoSQL)

I database tradizionali (SQL) organizzano i dati in tabelle rigide composte da righe e colonne predefinite (es. MySQL, PostgreSQL). Per collegare i dati occorre effettuare operazioni di relazione (JOIN).

I database moderni in cloud di tipo **NoSQL orientati ai documenti** (come MongoDB o Firebase Firestore) scartano le tabelle rigide a favore di una struttura gerarchica basata su **Collezioni** e **Documenti**:

```text
Database Firestore
 └── 📂 Collezione (es. "postit")   <── Insieme omogeneo di oggetti
      ├── 📄 Documento (id: "1")     <── Oggetto singolo (in formato JSON-like)
      │    ├── testo: "Fare la spesa"
      │    ├── x: 120
      │    └── colore: "giallo"
      └── 📄 Documento (id: "2")
           ├── testo: "Studiare Firebase"
           ├── x: 250
           └── colore: "azzurro"
```

- **Collezione**: È un raccoglitore (una cartella) che contiene diversi elementi individuali.
- **Documento**: È l'elemento singolo. Si presenta come una mappa di coppie chiave-valore (molto simile a un oggetto JSON). Ciascun documento all'interno della stessa collezione può avere campi differenti, garantendo massima flessibilità nello sviluppo iniziale.

---

## 🛠️ 2. Setup della Firebase Console

**Firebase** è una piattaforma di sviluppo di Google che fornisce servizi backend già pronti (database, autenticazione, hosting) senza la necessità di configurare un server fisico. Useremo **Cloud Firestore**, il suo database NoSQL flessibile e scalabile.

### Guida Passo-Passo per la Configurazione

1. Visita la [Firebase Console](https://console.firebase.google.com/) ed esegui l'accesso con il tuo account Google.
2. Fai clic su **Aggiungi progetto (Create a project)**:
   - Assegna un nome al progetto (es. `webdev-corso`).
   - Disabilita Google Analytics per questo progetto didattico (velocizza la creazione) e fai clic su _Crea_.
3. Una volta creato il progetto, abilita la Web App:
   - Fai clic sull'icona Web (`</>`) nella dashboard centrale.
   - Registra l'app (es. `lavagna-postit`).
   - Firebase ti mostrerà il codice di configurazione contenente le tue chiavi API (`firebaseConfig`). **Copia queste righe**, ci serviranno a breve!
4. Abilita il Database:
   - Nel menu laterale sinistro, seleziona **Firestore Database** e fai clic su **Crea database**.
   - Imposta la posizione del server (es. `europe-west8` per l'Italia).
   - Seleziona **Inizia in modalità test (Start in test mode)**.

> [!WARNING]
> La _modalità test_ disabilita temporaneamente i controlli di sicurezza, consentendo a chiunque conosca la tua configurazione di leggere e scrivere sul database per i primi 30 giorni. È utilissima in fase didattica, ma in produzione è obbligatorio configurare le _Regole di Sicurezza_ (Security Rules) per proteggere i dati.

---

## ⚡ 3. Integrazione dell'SDK Firebase

Per connettere il nostro file HTML a Firebase, importeremo l'SDK ufficiale di Firebase tramite CDN utilizzando il tag script in modalità **modulo JavaScript (`type="module"`)**. Questo ci consente di utilizzare i costrutti moderni `import` ed `export` per importare solo le funzioni di cui abbiamo bisogno:

```html
<script type="module">
  // Importa le funzioni necessarie dagli SDK Firebase
  import { initializeApp } from 'https://www.gstatic.com/firebasejs/12.15.0/firebase-app.js';
  import {
    getFirestore,
    collection,
    addDoc,
  } from 'https://www.gstatic.com/firebasejs/12.15.0/firebase-firestore.js';

  // Configurazione del tuo progetto Firebase (incollata dalla Console)
  const firebaseConfig = {
    apiKey: 'LA_TUA_API_KEY',
    authDomain: 'TUTTO_IL_RESTO_COPIATO',
    projectId: '...',
    storageBucket: '...',
    messagingSenderId: '...',
    appId: '...',
  };

  // Inizializza l'applicazione Firebase
  const app = initializeApp(firebaseConfig);
  // Ottieni il riferimento al database Firestore
  const db = getFirestore(app);
</script>
```

---

## 🔄 4. La Sincronizzazione in Tempo Reale: `onSnapshot()`

La maggior parte dei database tradizionali richiede che il client interroghi periodicamente il server per sapere se ci sono nuovi dati (polling). Questo processo è lento e consuma risorse di rete.

Firestore implementa un meccanismo nativo basato su connessioni persistenti (WebSocket). Invece di chiedere i dati una sola volta tramite `getDocs()`, ci mettiamo "in ascolto" di una collezione utilizzando la funzione **`onSnapshot()`**:

```javascript
import {
  collection,
  onSnapshot,
} from 'https://www.gstatic.com/firebasejs/12.15.0/firebase-firestore.js';

// Riferimento alla collezione "postit"
const colRef = collection(db, 'postit');

// Ascolta le modifiche in tempo reale
onSnapshot(colRef, (snapshot) => {
  console.log('Il database è cambiato!');

  snapshot.forEach((doc) => {
    // Stampa i dati di ciascun documento
    console.log(doc.id, doc.data());
  });
});
```

### Come Funziona `onSnapshot`?

1. Il client si collega a Firestore e scarica i dati correnti.
2. Firestore tiene aperta la connessione.
3. Non appena un utente (anche da un altro computer) aggiunge, modifica o elimina un documento nella collezione, Firestore invia istantaneamente l'aggiornamento a tutti i client connessi.
4. La callback all'interno di `onSnapshot()` viene eseguita automaticamente sul browser degli utenti, aggiornando l'interfaccia senza ricaricare la pagina.

---

[« Ora 2: Frontend Rapido con Tailwind CSS](02-frontend-rapido-tailwind.md) | **Ora 3: Database Firestore** | [Ora 4: Sviluppo del Progetto - Lavagna Collaborativa](04-progetto-lavagna-collaborativa.md) » |
