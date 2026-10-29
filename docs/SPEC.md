# SPEC: mockup "Almanacco del Sole" per Agriturismo Grappoli di Sole

Mockup di identità per https://agriturismograppolidisole.it (sito attuale: landing Lovable, crema + verde oliva, Fraunces/Lora/Inter, logo clipart "casa + cipressi"). Non sostituisce il sito: serve a far vedere al cliente più identità, stessi contenuti reali.

## 1. Obiettivi e non obiettivi

Obiettivi
- Una home one-page, mobile-first, che il cliente riconosce come "sua" ma con un'identità forte e propria.
- Un solo obiettivo di conversione: **WhatsApp** `https://wa.me/393511700535?text=...` (testo precompilato, vedi §6). Telefono ed email solo in Contatti.
- Stessi contenuti reali del sito attuale (§6). Niente di inventato.

Non obiettivi
- Nessun backend, modulo, booking engine, calendario di disponibilità, analytics, embed (mappa = solo link).
- Nessun testo legale (Privacy/Cookie sono segnaposto etichettati).
- Nessuna foto nuova: si usano quelle del cliente (hotlink al sito live, vedi §5).
- Una sola lingua: italiano.

## 2. Stack

HTML + CSS + JS vanilla, **un solo `index.html`** con CSS e JS inline. Nessuna libreria, nessun CDN, nessun Google Fonts. Font woff2 self-hosted in `assets/fonts/`. SVG di brand in `assets/brand/`. Peso pagina escluse le foto hotlinkate: < 300 KB.

## 3. Direzione

```
Direzione: almanacco contadino solare, display condensato bold + sans rotonda leggibile, carta d'olivo / sole / uva / oliva / salvia
```

Lettura: brand/landing per chi cerca un pranzo o un evento fuori Roma, guarda dal telefono di giorno (scena: sabato mattina sulla Ardeatina, decide dove pranzare, luce piena). Tema **unico chiaro**.

Idea: il nome è una promessa ("grappoli di sole"). L'identità è un **almanacco / bustina di semi**: sole fatto di acini, etichette-cartellino, calendario della tavola con i giorni reali, foto "a lunetta" come finestre di pergola. Riferimenti da cui prendere lo spirito (non la struttura): le bustine di semi italiane d'epoca, i calendari da muro dell'ortolano. Voce: caldo, contadino, solare.

### Colori (strategia: Committed, il sole porta 30-40% della superficie)

| Token | Valore | Uso |
|---|---|---|
| `--carta` | `oklch(95.5% 0.025 110)` ~ #F0F1DC | sfondo base, tinta verde-oliva (non crema calda) |
| `--sole` | `oklch(82% 0.17 85)` ~ #F2B427 | superfici "sole" (hero, eventi, striscia contatti), **unico accento**, CTA su carta |
| `--uva` | `oklch(26% 0.06 330)` ~ #38203A | testo, inchiostro, CTA su sole |
| `--oliva` | `oklch(45% 0.08 125)` ~ #55662A | linee, illustrazioni, link, eco del verde del logo attuale |
| `--salvia` | `oklch(88% 0.04 120)` ~ #D9E0C0 | superficie di supporto (essenza, natura) |

Mai `#000`/`#fff`. Contrasto AA verificato su ogni coppia usata (uva su carta/sole/salvia; oliva su carta solo per testo ≥ 18px o linee).

### Tipografia (2 famiglie, 3 pesi)

- Display: **Barlow Condensed 700** normale + corsivo (solo questo peso), sentence case, line-height 0.95-1.05. File in `MHW/nordaurai/assets/fonts/barlow-condensed-latin-700-normal.woff2` e `...-700-italic.woff2` (OFL, copiare).
- Testo: **Lexend** variabile (pesi usati: 400, 600). File `MHW/nordaurai/assets/fonts/lexend-latin-wght-normal.woff2` (OFL, copiare).
- Scala rapporto 1.25 con `clamp()`: corpo 1rem (≥16px), h3 1.5rem, h2 `clamp(2.5rem, 8vw, 5rem)`, h1 `clamp(3.75rem, 15vw, 9.5rem)`.
- Enfasi dentro un titolo = corsivo Barlow, mai un secondo font né colore diverso.
- Preload solo del display normale. `font-display: swap`.

### Forma e movimento

- Regola raggi: **foto = lunetta (arco in alto, `border-radius: 999px 999px 0 0`)**, bottoni pill, tutto il resto angolo vivo. Niente altro raggio.
- Spaziature da scala 8px, sezioni generose (`clamp(4rem, 10vw, 8rem)` verticale).
- Ombre: nessuna. Bordi: 2px `--uva` su pochi elementi (celle calendario, cartellini).
- Movimento solo CSS, `transform`/`opacity`, easing unico `cubic-bezier(0.16, 1, 0.3, 1)`, 150-400 ms:
  1. **Momento firma, solo hero:** l'emblema-sole sale da dietro la riga d'orizzonte (translateY 30% → 0, opacity 0 → 1, 400 ms) all'apertura. Su mobile e con `prefers-reduced-motion` è statico.
  2. Risposta ad azione: hover/focus bottoni e righe menù, apertura del menù mobile (`<details>`).
- Vietati fade-up per sezione, parallax, cursori, gradient text, glass.

## 4. Asset di brand (`assets/brand/`, SVG inline-friendly, `currentColor` dove possibile)

| File | Contenuto |
|---|---|
| `emblem.svg` | Emblema "grappolo di sole": disco solare con raggi corti (12-16 trattini) e, dentro/sotto il disco, un grappolo di acini (cerchi in file triangolari, 15-21 acini) con picciolo e una foglia di vite. Geometrico, tratto 4px su viewBox 200, 2 colori (uva + sole), leggibile a 32px. |
| `wordmark.svg` | Lockup orizzontale: emblema + "Grappoli di Sole" (testo convertito in path o `<text>` con font Barlow Condensed) + piccola riga "Agriturismo, Via Ardeatina 1943". |
| `favicon.svg` | Solo disco + 3 acini, leggibile a 16px. |
| `botanical.svg` | Sprite `<symbol>`: `grape` (grappolo a tratto), `vine-leaf`, `olive-branch`, `divider` (filare orizzontale ripetibile). Tratto 2px `currentColor`, stile incisione semplificata. Nessun animale, nessun ortaggio (non inventiamo cosa cresce in orto). |

## 5. Foto (hotlink, nessun download in repo)

Base URL `https://agriturismograppolidisole.it/__l5e/assets-v1/`. Tutte 1280x1920 (verticali 2:3). Trattamento coerente: **sempre in lunetta, crop 4:5 con `object-fit: cover`**, stesso `object-position` indicato, nessun filtro (già calde), `width="1280" height="1920"` sugli `<img>`, `loading="lazy"` tranne l'hero.

| Chiave | Percorso | Alt reale | Uso |
|---|---|---|---|
| `uliveto` | `73a80832-ba64-490b-afd2-0e4f1afb036d/DSC04565.jpg` | Uliveto e vigna dell'agriturismo Grappoli di Sole alle porte di Roma | hero |
| `ruota` | `f42a02db-187f-46cb-a683-810303b9a60d/DSC04562.jpg` | Filari della vigna in autunno con vecchia ruota di carro | essenza |
| `asini` | `cd9e5bed-2d5d-41d3-8606-632da7f57924/DSC00085.jpg` | Asini al pascolo nel prato dell'agriturismo | essenza |
| `pasta` | `a2c9f2d5-daec-43ab-b965-89693a907d87/DSC00075.jpg` | Pasta fresca fatta a mano con crema di zucchine e zucchine croccanti | cucina |
| `tagliere` | `ca5425a9-39dc-4e51-8d52-24a48f1e30b6/DSC00059.jpg` | Tagliere di salumi, prosciutto e polpette della casa | cucina |
| `alpaca` | `63b88f29-3490-43ef-9656-5a90d8cb286d/DSC04512.jpg` | Alpaca tra i filari della vigna al tramonto | natura |

Non usare il logo PNG attuale: il mockup propone il nuovo emblema (decisione da far approvare al cliente).

## 6. Contenuti reali (unici ammessi)

Navigazione (voci invariate): La Tenuta `#storia`, La Tavola `#cucina`, Menù `#menu`, Eventi `#eventi`, Natura `#esperienze`, Contatti `#contatti`. CTA unica con etichetta **"Prenota"** ovunque (WhatsApp). Eccezione di intento diverso: "Richiedi un preventivo" in Eventi (stesso link WhatsApp, testo precompilato diverso).

Testi del sito attuale da riusare: Hero "Il ritmo dolce della terra." + riga "Un vero agriturismo a due passi dal caos di Roma." (≤ 20 parole, parafrasi del testo reale). Essenza: titolo "Oltre la città, dentro la natura più vera.", citazione "C'è un'onestà profonda nel veder crescere ciò che si mangia.", il nome come promessa. Cucina: "Ingredienti a metro zero, ricette tramandate, fuoco vivo." con tre voci: "Primi e Secondi da acquolina di bocca" (tonnarelli, strozzapreti e gnocchi preparati ogni mattina con le verdure dell'orto), "Taglieri ricchi e con prodotti locali" (salumi e formaggi dell'agro romano, composte e fritti di stagione), "Dalla natura al piatto". Eventi: "Organizza il tuo evento privato." con comunioni e cresime, battesimi, anniversari, compleanni, pranzi e cene di famiglia, formule su misura. Natura: "Incontri inaspettati." con visita a orto, uliveto e vigna; incontro con gli animali della fattoria (tra cui alpaca); pernottamento su richiesta.

Menù e prezzi (reali):
- Mer-ven, pranzo: Insalatona €10; Primo €12; Antipasto e Primo €15; Antipasto e Secondo €17.
- Ven sera, sab pranzo e cena, dom pranzo: Menù Completo €30,00 a persona (3 antipasti, scelta tra 3 primi, secondo con contorno, acqua, vino della casa in ragione di una bottiglia ogni 5 persone, dolce della casa).
- Bambini: €12,00 (un primo o un secondo, acqua) oppure €15,00 (primo + secondo, bibita).
- "Prenotazione consigliata", tel. 346 661 3687.

Contatti: Via Ardeatina, 1943, 00134 Roma RM. WhatsApp +39 351 170 0535. Tel 346 661 3687. Email agriturismograppolidisole@gmail.com. Link "Trova la strada" = `https://www.google.com/maps/search/?api=1&query=Via+Ardeatina+1943+00134+Roma`. P.IVA 18014771002. "Disponibilità alloggio su richiesta".

Testo WhatsApp precompilato (mock, da far approvare): prenota = `Ciao, vorrei prenotare da Grappoli di Sole. Giorno, orario e numero di persone: `; preventivo = `Ciao, vorrei un preventivo per un evento privato da Grappoli di Sole. Tipo di evento e numero di persone: `.

**Segnaposto etichettati da lasciare** (elencare nel report): `[PRIVACY POLICY DEL CLIENTE QUI]`, `[COOKIE POLICY DEL CLIENTE QUI]`, `[ORARI DI APERTURA DA CONFERMARE]`, `[RECENSIONI REALI QUI]` (solo se la sezione esiste; altrimenti ometterla).

**Vietato inventare:** piscina, camere, orari, recensioni, "cosa cresce a stagione", numeri, statistiche, premi.

## 7. Sezioni (mobile 360-390 poi desktop 1280)

Ogni famiglia di layout compare una sola volta.

1. **Header**: wordmark a sinistra; desktop = nav in una riga (64-72px) + bottone Prenota; mobile = wordmark + `<details>` "Menu" (voci a tutta larghezza, tap ≥ 44px). Link "Salta al contenuto".
2. **Hero** (famiglia: split asimmetrico drenched). Sfondo `--sole`, linea d'orizzonte `--uva` 2px. Testo: H1 + riga + bottone Prenota (uva su sole). Visual: emblema grande che sorge dietro la lunetta `uliveto`. Mobile: H1 sopra, lunetta sotto con emblema dietro in alto a destra; nessun altro elemento. Altezza `min-height: 100dvh`, CTA visibile senza scroll.
3. **La Tenuta #storia** (famiglia: tipografica + foto sfalsate). Sfondo `--carta`. Citazione grande Barlow a sinistra; due lunette `ruota` e `asini` sfalsate in verticale, con cartellini-didascalia ("Filari in autunno", "Gli asini al pascolo", dalle alt reali). Mobile: citazione, poi lunette in due colonne sfalsate o una sotto l'altra. Divider `botanical` sopra.
4. **La Tavola #cucina** (famiglia: riga scroll-snap). Sfondo `--salvia`. Titolo + sottotitolo; tre voci con larghezze diverse (non tre card uguali): `pasta` (larga), `tagliere` (media), terza "Dalla natura al piatto" = tipografica su sole con grappolo botanico (niente foto inventata). Mobile: scroll-snap orizzontale con indizio della card successiva; desktop: griglia 5/4/3.
5. **Il calendario della tavola #menu** (famiglia: griglia-calendario). Sfondo `--carta`. Griglia Mer-Dom x Pranzo/Cena con soli dati reali: Mer-Ven pranzo = menù pranzo; Ven cena, Sab pranzo, Sab cena, Dom pranzo = Menù Completo; celle senza dati = vuote a tratteggio con legenda "Altri giorni e orari: `[ORARI DI APERTURA DA CONFERMARE]`". Sotto: elenco prezzi come "etichetta d'almanacco" (voce, dotted leader, prezzo). Bambini a parte. JS (≤ 15 righe, progressive enhancement): evidenzia la colonna del giorno corrente se ha dati, con tag "oggi"; senza JS niente cambia. Non dire mai aperto/chiuso. Mobile: ogni giorno = riga impilata con le sue fasce, non tabella compressa.
6. **Eventi #eventi** (famiglia: banda sole piena, lista tipografica). Sfondo `--sole`. Titolo "Organizza il tuo evento privato." e l'elenco occasioni come riga gigante di testo a capo libero; bottone "Richiedi un preventivo" (uva su sole).
7. **Natura #esperienze** (famiglia: foto + lista a sentiero). Sfondo `--salvia`. Lunetta `alpaca` con tre voci su linea verticale/orizzontale `--oliva`: orto uliveto e vigna; animali della fattoria (alpaca incluso); pernottamento su richiesta. Titolo "Incontri inaspettati."
8. **Contatti #contatti + footer** (famiglia: indirizzo-timbro). Sfondo `--carta`, blocco indirizzo come timbro/cartellino bordo 2px. Bottone Prenota (sole su carta, testo uva) primo; poi tel, email, "Trova la strada". Footer: P.IVA, © 2026 Grappoli di Sole, segnaposto Privacy e Cookie.
9. **Barra fissa mobile** (< 768px): bottone "Prenota" a tutta larghezza, ≥ 48px, safe-area-inset-bottom; sparisce quando #contatti è in vista (IntersectionObserver, facoltativo).

## 8. Definition of done

- Funziona da 360px a 1440px, senza scroll orizzontale della pagina.
- Leggibile senza JS e con `prefers-reduced-motion`.
- Focus visibile, contrasto AA, target ≥ 44px, un solo H1, `lang="it"`, title, meta description, Open Graph; **nessun** JSON-LD con dati non forniti (al più `LocalBusiness` con indirizzo, telefono, email reali).
- Nessuna riga "—" o "–" nel testo visibile; nessun em dash.
- `grep "QUI\]"` elenca solo i segnaposto del §6.
- Lighthouse mobile ≥ 90 su accessibilità, SEO, best practices (prestazioni: foto hotlinkate escluse dal giudizio, annotare).
- Screenshot a 375px e 1280px controllati dall'orchestratore.
