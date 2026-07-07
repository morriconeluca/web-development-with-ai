# Messa in Produzione: GitHub e Deploy su Netlify

---

## | [« Esercizio Giorno 3: Post-it Personalizzati e Collaborazione](05-compito-postit-personalizzati.md) | **Messa in Produzione: GitHub e Deploy su Netlify** | [Indice Giorno 3](README.md) |

Al termine del nostro percorso pratico, dopo aver sviluppato ed esteso l'applicazione "Lavagna Post-it Collaborativa", il passo finale è pubblicarla online. In questa lezione vedremo come creare il repository su GitHub, sincronizzare i nostri file locali in cloud ed effettuare il deploy gratuito su Netlify per rendere il progetto accessibile a chiunque.

---

## 📂 1. Creazione del Repository su GitHub

Per salvare il codice online ed abilitare il deploy automatico, dobbiamo creare uno spazio (repository) su GitHub:

1. Accedi a [GitHub](https://github.com) ed effettua l'accesso.
2. In alto a destra, clicca sul pulsante **+** e seleziona **New repository**.
3. Configura il repository:
   - **Repository name**: `post-it`
   - **Public/Private**: Scegli in base alle tue preferenze (es. _Public_ per mostrarlo facilmente).
   - **ATTENZIONE**: Lascia deselezionate tutte le opzioni di inizializzazione ("Add a README file", "Add .gitignore", "Choose a license"). Avendo già questi file nella nostra cartella di lavoro locale, crearli su GitHub causerebbe dei conflitti di sincronizzazione.
   - Clicca sul pulsante verde **Create repository** in fondo.

---

## ⚡ 2. Collegamento del Repository Locale a GitHub

Ora dobbiamo indicare al nostro Git locale (configurato nel Giorno 1) dove inviare i file su internet:

1. Apri il terminale dell'IDE all'interno della cartella radice del tuo progetto.
2. Associa l'indirizzo remoto del repository GitHub appena creato eseguendo:

   ```bash
   git remote add origin https://github.com/IL_TUO_USERNAME/post-it.git
   ```

   _(Sostituisci `IL_TUO_USERNAME` con il tuo effettivo nome utente di GitHub)._

3. Assicurati che il branch principale sia rinominato correttamente in `main`:

   ```bash
   git branch -M main
   ```

4. Carica tutti i tuoi file locali (incluso il compito del Giorno 3) su GitHub ed imposta il tracciamento remoto:

   ```bash
   git push -u origin main
   ```

5. Ricarica la pagina del tuo repository su GitHub: vedrai apparire tutti i file del corso online!

---

## 🚀 3. Deploy dell'Applicazione su Netlify

Per ospitare l'applicazione in cloud in modo gratuito, utilizzeremo **Netlify**, una piattaforma che si collega direttamente a GitHub ed aggiorna il sito ogni volta che eseguiamo un push.

1. Visita [Netlify.com](https://www.netlify.com/) e fai clic su **Sign Up** (Registrati).
2. Seleziona **GitHub** come metodo di registrazione per collegare i due account.
3. Nella dashboard principale di Netlify, clicca sul pulsante **Add new site** (Aggiungi nuovo sito) e seleziona **Import an existing project** (Importa un progetto esistente).
4. Seleziona nuovamente **GitHub** come provider Git. Se richiesto, autorizza Netlify ad accedere ai tuoi repository.
5. Cerca e seleziona dall'elenco il tuo repository `post-it`.
6. Nella schermata di configurazione dei parametri di pubblicazione, lascia le impostazioni predefinite:
   - **Branch to deploy**: `main`
   - **Build command**: (lascialo vuoto, la nostra app è statica e non ha compilazione).
   - **Publish directory**: `.` (il punto indica la cartella radice dove risiede il nostro file `index.html`).
7. Fai clic su **Deploy site** (o **Deploy post-it**).
8. Attendi circa 10-15 secondi. Netlify completerà la pubblicazione e ti fornirà un link pubblico (es. `https://super-cookie-12345.netlify.app`).

Cliccando su quel link vedrai la tua lavagna di post-it collaborativa online! Condividi l'indirizzo con i tuoi amici e compagni di classe: chiunque si collegherà potrà interagire inserendo, spostando o eliminando post-it in tempo reale sul tuo schermo.

---

## 🛠️ 4. Guida alla Consegna

Una volta completato l'Esercizio del Giorno 3 e verificato che il deploy su Netlify sia andato a buon fine, procedi con la consegna finale del tuo lavoro:

1. Apri il terminale dell'IDE nella cartella radice del progetto.
2. Aggiungi il file `index.html` (contenente il tuo esercizio) in staging:

   ```bash
   git add index.html
   ```

3. Esegui il commit locale descrivendo l'estensione che hai sviluppato:

   ```bash
   git commit -m "Compito Giorno 3 - Sviluppata estensione post-it"
   ```

4. Invia tutti i cambiamenti sul tuo repository remoto su GitHub:

   ```bash
   git push origin main
   ```

5. Invia al docente:
   - Il link del tuo **repository GitHub** (es. `https://github.com/tuo-username/post-it`).
   - Il link dell'applicazione **pubblicata online su Netlify** (es. `https://nome-casuale.netlify.app`).

---

[« Esercizio Giorno 3: Post-it Personalizzati e Collaborazione](05-compito-postit-personalizzati.md) | **Messa in Produzione: GitHub e Deploy su Netlify** | [Indice Giorno 3](README.md) |
