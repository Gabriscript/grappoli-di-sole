# Grappoli di Sole: mockup identità

Mockup statico per agriturismograppolidisole.it. Italiano per i testi visibili; codice e commit in inglese.

- Stack: un solo `index.html` (HTML/CSS/JS vanilla inline). Nessuna libreria, nessun CDN, nessun Google Fonts.
- Preview: `preview_start` con nome `grappoli-di-sole` (voce in `MHW/.claude/launch.json`, porta 5500).
- Leggi prima `docs/SPEC.md` (direzione, token, contenuti) e `docs/PLAN.md`. `filemap.md` = indice dei file.

Regole non ovvie
- Contenuti: solo quelli di SPEC §6. Mai inventare prezzi, orari, recensioni, camere, cosa cresce in orto. Lacune = segnaposto `[... QUI]`.
- Un solo obiettivo: WhatsApp (`wa.me/393511700535`). Etichetta unica "Prenota".
- Palette e font solo quelli di SPEC §3. Vietati `#000`/`#fff`, Inter/Fraunces/Lora, gradient text, glass, fade-up per sezione, em dash/en dash nel testo visibile.
- Raggi: foto in lunetta, bottoni pill, resto angolo vivo.
- Foto in hotlink dal sito live (SPEC §5): non scaricarle nel repo.
- Un hook copia i file modificati in `backup/`: è in `.gitignore`, non committarlo né deployarlo.
- Non fare push. Commit solo su richiesta dell'orchestratore.
