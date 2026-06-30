# Ora 2: Frontend Rapido con Tailwind CSS (Sviluppo UI)

---

## | [« Ora 1: Le basi del Web](01-basi-web-architettura.md) | **Ora 2: Frontend Rapido con Tailwind CSS** | [Ora 3: Database Firestore](03-database-firestore.md) » |

In questa lezione impareremo le basi del frontend moderno. Vedremo come strutturare una pagina web per renderla facilmente leggibile sia dagli utenti che dagli agenti IA, come manipolare il DOM in JavaScript e come usare il framework Tailwind CSS per velocizzare lo sviluppo visuale.

---

## 🏗️ 1. L'HTML5 Semantico nell'Era dell'IA

La scrittura di codice HTML ordinato e semantico è una delle migliori pratiche per l'accessibilità (a11y) e per la SEO. Oggi, con l'avvento dei programmatori IA (agenti), assume un'importanza ancora maggiore.

Gli agenti IA leggono la struttura del tuo file HTML prima di decidere dove inserire un nuovo componente. Evita di creare pagine strutturate solo con tag generici `<div>` innestati. Utilizza invece tag semantici chiari:

- **`<header>`**: Contiene elementi di navigazione e introduzione della pagina.
- **`<main>`**: Delimita il contenuto informativo principale della pagina (deve essercene solo uno).
- **`<section>`**: Suddivide la pagina in sezioni tematiche logiche.
- **`<article>`**: Rappresenta un blocco di contenuto autonomo (es. una scheda post-it o un articolo di blog).
- **`<footer>`**: Contiene informazioni sul copyright, link utili o firme in fondo.

> [!TIP]
> Se il tuo HTML è semantico, l'agente IA riuscirà ad inserire nuovi elementi o fare modifiche con un tasso di successo molto più elevato, evitando di rompere la struttura visiva del tuo layout.

---

## ⚡ 2. JavaScript Moderno (ES6+) e Manipolazione del DOM

Il DOM (Document Object Model) è la rappresentazione strutturata ad albero del tuo documento HTML generata dal browser. JavaScript ci permette di modificarla dinamicamente per rendere la pagina interattiva.

I tre concetti chiave che useremo nel progetto sono:

### A. Selezione degli Elementi e Gestione degli Eventi

Selezioniamo gli elementi HTML usando `document.querySelector` e mettiamoci in ascolto di interazioni dell'utente (come i clic):

```javascript
const pulsante = document.querySelector('#my-btn');

pulsante.addEventListener('click', () => {
  console.log('Pulsante cliccato!');
});
```

### B. Iniezione Dinamica di Contenuto

Possiamo creare nuovi tag HTML via Javascript e appenderli alla pagina usando i **Template Literals** (stringhe racchiuse tra apici inversi `` ` `` che supportano variabili interne tramite `${}`):

```javascript
const contenitore = document.querySelector('#contenitore');

// Creazione dinamica di una scheda
const nuovaCard = document.createElement('div');
nuovaCard.className = 'card';
nuovaCard.innerHTML = `
  <h3>Titolo Dinamico</h3>
  <p>Questo testo è inserito via JS.</p>
`;

contenitore.appendChild(nuovaCard);
```

### C. Programmazione Asincrona (`async/await`)

Quando leggiamo o scriviamo dati su un server o database remoto (come Firebase), l'operazione non è immediata (dipende dalla connessione). Utilizziamo quindi la sintassi asincrona per evitare di "bloccare" l'interfaccia utente durante l'attesa:

```javascript
async function caricaDatiDalDatabase() {
  try {
    const dati = await fetch('https://api.esempio.com/dati');
    const json = await dati.json();
    console.log(json);
  } catch (errore) {
    console.error('Si è verificato un errore:', errore);
  }
}
```

---

## 🎨 3. Tailwind CSS: Il Framework Utility-First

**Tailwind CSS** è un framework CSS che ti consente di stilizzare la tua pagina web senza scrivere un solo foglio di stile esterno (`.css`). Fornisce migliaia di classi predefinite (utility classes) focalizzate su singole proprietà (es. `p-4` per padding, `bg-blue-500` per il colore di sfondo, `rounded-lg` per i bordi arrotondati).

### A. Integrazione Rapida (CDN)

Durante il laboratorio integreremo Tailwind inserendo questo semplice script all'interno del tag `<head>` del file `index.html`:

```html
<script src="https://cdn.tailwindcss.com"></script>
```

### B. Perché Tailwind CSS è perfetto per lo sviluppo assistito da IA?

Quando sviluppi un'interfaccia in tandem con un agente IA:

1. **Nessun file CSS separato**: Tutti gli stili risiedono direttamente nelle classi dei tag HTML nel file `index.html`. L'agente non deve saltare tra file diversi per modificare lo stile, riducendo gli errori di sincronizzazione.
2. **Standardizzazione**: Le classi di Tailwind (`shadow-md`, `flex`, `items-center`, `text-xl`) sono standard, uniformi e ampiamente documentate sul web. L'agente IA le conosce alla perfezione e genera layout moderni ed eleganti con pochissimo margine di errore, evitando di inventare classi CSS non esistenti.

---

## 🔬 4. Laboratorio Pratico: Card Profilo Interattiva

Creiamo la nostra prima pagina interattiva stilizzata con Tailwind CSS.

### Codice di Esempio (`index.html`)

Crea un file locale sul tuo computer con questo codice e aprilo nel browser:

```html
<!DOCTYPE html>
<html lang="it">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Card Profilo Interattiva</title>
    <!-- Script Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
  </head>
  <body class="bg-slate-100 flex items-center justify-center min-h-screen">
    <main
      class="bg-white p-8 rounded-2xl shadow-xl max-w-sm w-full text-center border border-slate-200"
    >
      <!-- Immagine Profilo -->
      <div
        class="w-24 h-24 bg-gradient-to-tr from-sky-400 to-indigo-500 rounded-full mx-auto flex items-center justify-center text-white text-3xl font-bold shadow-inner"
      >
        LM
      </div>

      <!-- Info Utente -->
      <h1 class="text-2xl font-bold text-slate-800 mt-4">Luca Morricone</h1>
      <p
        class="text-sm font-semibold text-indigo-600 uppercase tracking-wider mt-1"
      >
        Docente Web Dev
      </p>
      <p class="text-slate-500 mt-3 text-sm leading-relaxed">
        Appassionato di programmazione web, intelligenza artificiale generativa
        e architetture cloud real-time.
      </p>

      <!-- Statistiche -->
      <div
        class="flex justify-around my-6 py-4 bg-slate-50 rounded-xl border border-slate-100"
      >
        <div>
          <span class="block text-lg font-bold text-slate-700">12</span>
          <span class="text-xs text-slate-400 uppercase font-semibold"
            >Progetti</span
          >
        </div>
        <div>
          <span class="block text-lg font-bold text-slate-700">1.4k</span>
          <span class="text-xs text-slate-400 uppercase font-semibold"
            >Studenti</span
          >
        </div>
      </div>

      <!-- Pulsante Interattivo -->
      <button
        id="follow-btn"
        class="w-full bg-indigo-600 hover:bg-indigo-700 active:bg-indigo-800 text-white font-semibold py-3 px-6 rounded-xl transition duration-200 shadow-md shadow-indigo-100"
      >
        Segui
      </button>
    </main>

    <script>
      // Codice Javascript per l'interazione
      const followBtn = document.querySelector('#follow-btn');
      let isFollowing = false;

      followBtn.addEventListener('click', () => {
        isFollowing = !isFollowing;

        if (isFollowing) {
          followBtn.textContent = 'Seguito ✔️';
          followBtn.classList.replace('bg-indigo-600', 'bg-emerald-600');
          followBtn.classList.replace(
            'hover:bg-indigo-700',
            'hover:bg-emerald-700',
          );
        } else {
          followBtn.textContent = 'Segui';
          followBtn.classList.replace('bg-emerald-600', 'bg-indigo-600');
          followBtn.classList.replace(
            'hover:bg-emerald-700',
            'hover:bg-indigo-700',
          );
        }
      });
    </script>
  </body>
</html>
```

---

[« Ora 1: Le Basi del Web](01-basi-web-architettura.md) | **Ora 2: Frontend Rapido con Tailwind CSS** | [Ora 3: Database Firestore](03-database-firestore.md) » |
