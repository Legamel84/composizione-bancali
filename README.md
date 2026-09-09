# Composizione Bancali — Infermentum

App web per il reparto confezionamento: dall'ordine (pezzi / codici iMio) al piano di carico dei bancali.
Sito statico + Supabase (login team, salvataggio ordini, regole condivise).

## Cosa fa
- Inserimento ordine a mano, incollato o da Excel/CSV (riconosce i codici iMio: RI…, RP…, BB…, BA…, P…, EI…, BBM01)
- Conversione pezzi → scatole (pezzi/scatola per prodotto, da anagrafica)
- Composizione bancali: riempimento in altezza sul 120×80, combinazione dei resti, pedana piccola per i lievitati (scatola P ≤72 pz, scatola C ≤42 pz)
- Salvataggio/ricarica ordini e composizioni (Supabase)
- Regole (soglie, misure scatole, altezze bancali) modificabili e condivise con il team

## Accesso
- Password team attuale: **bancali2026** (modificabile — vedi sotto)

## Backend Supabase
- Progetto: **composizione-bancali** (org "Magazzino Reolto")
- URL: `https://kwqouuoyszpptrxktppk.supabase.co`
- Nel codice (`index.html`) sono usati l'URL e la **chiave pubblica** (publishable/anon): è pubblica per natura, protetta dalle regole di accesso (RLS) e dal login team. La password del team NON è nel codice: sta in una tabella non leggibile e si verifica via funzione sicura.

### Cambiare la password del team
Nel SQL editor di Supabase (progetto composizione-bancali):
```sql
update public.app_secrets set team_password = 'NUOVA_PASSWORD' where id = 1;
```

## Deploy su Netlify (via GitHub)
1. Crea un repository su GitHub (es. `composizione-bancali`) e carica questi file
   (`index.html`, `netlify.toml`, `README.md`). Da terminale:
   ```bash
   git init
   git add .
   git commit -m "Composizione Bancali"
   git branch -M main
   git remote add origin https://github.com/<tuo-utente>/composizione-bancali.git
   git push -u origin main
   ```
   (oppure trascina i file nella pagina "Add file → Upload files" di GitHub)
2. Su Netlify: **Add new site → Import an existing project → GitHub**, scegli il repo.
3. Build command: *(vuoto)* — Publish directory: `.` — poi **Deploy**.
4. Netlify ti dà un URL (`https://<nome>.netlify.app`): condividilo con i colleghi.
   Ogni push su GitHub aggiorna il sito da solo.

### Alternativa rapida (senza GitHub)
Trascina la cartella su https://app.netlify.com/drop — pubblica subito. (Gli aggiornamenti però vanno ricaricati a mano.)

## File
- `index.html` — l'app completa (HTML/CSS/JS, tutto in un file)
- `netlify.toml` — configurazione Netlify (sito statico)
