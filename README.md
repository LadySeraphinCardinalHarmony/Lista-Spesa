# Lista della Spesa

App web per creare e gestire liste della spesa: prezzi, sconti, colori, emoji, punti e
personalizzazioni. Progetto pronto per GitHub Pages e per l'installazione sul telefono
come un'app vera (icona, schermo intero, offline parziale).

## Pubblicarla su GitHub Pages

**Dal sito, senza Git (funziona anche da telefono):**
1. Su github.com → **New repository** → nome senza spazi → **Public** (obbligatorio per le
   Pages gratuite).
2. **Add file › Upload files** → trascina dentro TUTTO il contenuto di questa cartella
   (`index.html`, `manifest.webmanifest`, `sw.js`, `.nojekyll`, la cartella `assets/`).
   `index.html` deve stare nella radice del repository, non in una sottocartella.
3. **Commit changes**.
4. **Settings › Pages** → *Deploy from a branch* → ramo `main`, cartella `/ (root)` → **Save**.
5. Dopo circa un minuto il sito è online su `https://TUONOME.github.io/NOMEREPO/`. Se compare
   404 la prima volta, aspetta un minuto e ricarica.

## Installarla sul telefono

**iPhone:** apri l'indirizzo **in Safari** (Chrome su iOS non installa le web app) → icona
Condividi → **Aggiungi alla schermata Home**.

**Android:** apri l'indirizzo in Chrome. Di solito compare da sola la proposta
**"Installa app"**; se non compare, usa il menu ⋮ → **Aggiungi a schermata Home**. Il
comportamento è lo stesso di iPhone: icona propria, schermo intero, nessuna barra del browser.

## Cose da sapere

- **I dati (liste, punti, impostazioni) restano sul singolo dispositivo**, salvati nel
  browser: telefono e computer avranno liste separate, e cancellare i dati del sito le
  azzera.
- **Non è offline al 100%**: React, le icone e i font vengono caricati da internet
  (esm.sh, unpkg, fonts.googleapis.com) al primo avvio di ogni sessione; il service worker
  mette in cache solo i file dell'app stessa (`index.html`, icone).
- **Dopo un aggiornamento** il service worker può continuare a servire la versione vecchia
  finché la cache non si aggiorna. Rilanciando `make_pwa.py` la versione si aggiorna da
  sola; se modifichi i file a mano, cambia tu la stringa `CACHE` in cima a `sw.js`. Sul
  telefono, chiudere del tutto l'app e riaprirla forza l'aggiornamento.
- Le chiavi di salvataggio locale (`grocery-lists-v3`, `grocery-settings-v3`,
  `grocery-gamification-v1`) sono le stesse di sempre: se pubblichi sempre dallo stesso
  indirizzo, le liste già create non vengono perse.
