# PLAN

Stato: bozza in attesa di approvazione. Specifiche in `docs/SPEC.md` (i worker lo leggono, non è nel loro contesto).

| # | Task | Tier | Dopo | Verifica |
|---|---|---|---|---|
| 1 | **Scaffold**: cartelle `assets/fonts`, `assets/brand`; copia dei 3 woff2 (SPEC §3); `.gitignore` con `backup/`; voce in `MHW/.claude/launch.json` (nome `grappoli-di-sole`, `npx --yes http-server grappoli-di-sole -p 5300 -c-1`, aggiungere senza toccare le altre); `index.html` minimo che carica | light | - | 3 woff2 presenti, `preview_start` serve la pagina |
| 2 | **Set SVG di brand** (SPEC §4): `emblem.svg`, `wordmark.svg`, `favicon.svg`, `botanical.svg` | careful | 1 | Aprire ogni SVG in browser a 32px e 400px: leggibile, 2 colori, nessun testo non convertito che dipenda da font di sistema |
| 3 | **Pagina completa** (SPEC §3, §5-§7): `index.html` con CSS e JS inline, sezioni 1-9, riferimenti agli SVG di task 2 ai percorsi di SPEC §4 | careful | 1 | Preview a 375px e 1280px, nessun errore in console, grep banditi/segnaposto, peso < 300 KB |
| 4 | **Revisione orchestratore**: screenshot, audit (`my-frontend/audit.md`), critica design, round di correzioni (max 2) | orchestratore | 2, 3 | checklist SPEC §8 |
| 5 | **Chiusura**: `filemap.md` aggiornato, commit finale | light | 4 | `git status` pulito |

I task 2 e 3 sono indipendenti (percorsi dei file fissati nello SPEC) e girano in parallelo.
Dopo ogni task accettato: commit (messaggi in inglese). Nessun push.
