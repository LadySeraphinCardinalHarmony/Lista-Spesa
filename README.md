# Lista della Spesa (versione offline)

App web per creare e gestire liste della spesa: prezzi, sconti, colori, emoji, punti e
personalizzazioni. Questa versione **non dipende da nessun servizio esterno**: React,
ReactDOM e le icone sono compilati dentro `bundle.js`, quindi dopo la prima apertura
online l'app funziona anche senza connessione.

## Pubblicarla su GitHub Pages

**Dal sito, senza Git (funziona anche da telefono):**
1. Su github.com → **New repository** → nome senza spazi → **Public** (obbligatorio per le
   Pages gratuite).
2. **Add file › Upload files** → trascina dentro TUTTO il contenuto di questa cartella
   (`index.html`, `bundle.js`, `manifest.webmanifest`, `sw.js`, `.nojekyll`, la cartella
   `assets/`). `index.html` deve stare nella radice del repository.
3. **Commit changes**.
4. **Settings › Pages** → *Deploy from a branch* → ramo `main`, cartella `/ (root)` → **Save**.
5. Dopo circa un minuto il sito è online su `https://TUONOME.github.io/NOMEREPO/`.

## Installarla e usarla offline

1. Apri l'indirizzo **almeno una volta con connessione attiva** (iPhone: Safari →
   Condividi → Aggiungi a schermata Home. Android: Chrome → Installa app / Aggiungi a
   schermata Home). Questo passaggio è necessario: scarica e mette in cache `bundle.js`,
   le icone e l'app stessa.
2. Da quel momento in poi l'app si apre e funziona **anche senza internet**: crei liste,
   aggiungi articoli, spunti, spendi punti — tutto resta salvato sul telefono.
3. Quando torni online, se hai pubblicato un aggiornamento il service worker lo scarica
   automaticamente al successivo avvio.

## Perché prima non funzionava offline

Le versioni precedenti caricavano React, le icone e il traduttore JSX da internet
(esm.sh, unpkg, Google Fonts) a ogni apertura: utili per svilupparla rapidamente, ma
inutilizzabili senza connessione. In questa versione:
- React, ReactDOM e le icone sono **compilati dentro `bundle.js`** (nessuna chiamata a
  CDN in fase di esecuzione).
- I caratteri Google Fonts sono stati rimossi: l'app usa i font già presenti sul
  telefono (Georgia, il sans-serif di sistema, un monospace) — la differenza estetica è
  minima ed è il prezzo per non dipendere da internet.
- Il service worker mette in cache anche `bundle.js`, non solo `index.html` e le icone.

## Cose da sapere

- **I dati (liste, punti, impostazioni) restano sul singolo dispositivo**, salvati nel
  browser: telefono e computer avranno liste separate, e cancellare i dati del sito le
  azzera.
- **La primissima apertura richiede connessione**: serve a scaricare l'app una volta.
  Da lì in poi funziona offline.
- **Dopo un aggiornamento** pubblicato online, il service worker scarica la nuova
  versione la prossima volta che apri l'app con connessione attiva.
- Le chiavi di salvataggio locale (`grocery-lists-v3`, `grocery-settings-v3`,
  `grocery-gamification-v1`) sono le stesse di sempre: se pubblichi dallo stesso
  indirizzo di prima, le liste già create non vengono perse.
