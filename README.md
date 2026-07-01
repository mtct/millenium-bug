# millenium-bug

Retro banking vibes for your website.

Una libreria CSS **classless-first** che replica l'estetica dei gestionali bancari web di fine anni '90: pagina quasi bianca, campi grigi a bordo incassato, tab blu cobalto, valori in Courier bold, evidenziazioni giallo fosforescente e alert rosso fuoco. Niente border-radius. Niente transizioni. Niente pietà.

## Installazione

```html
<link rel="stylesheet" href="millenium-bug.css">
```

Nessuna dipendenza, nessun build step. Un file solo, come si faceva una volta.

## Filosofia: semantica prima di tutto

Gli elementi HTML semantici vengono stilati direttamente — scrivi HTML corretto e ottieni il gestionale. Le classi `.mb-*` esistono solo come modificatori.

## Componenti

| Componente | HTML semantico |
| --- | --- |
| Finestra di dialogo | `<dialog open>` (o `.mb-window`) |
| Barra del titolo | `<dialog> > <header>` con `<h1>` e `<button aria-label="Chiudi">` |
| Tab | `<nav>` con `<a>`/`<button>`; tab attivo via `aria-current` o `aria-selected="true"` |
| Pannello contenuto | `<section>` subito dopo il `<nav>` (o `.mb-panel`) |
| Riga di campi | `<p>` dentro `<form>` (o `.mb-row`) — flex denso, label + campi inline |
| Campi | `<input>`, `<select>`, `<textarea>` — bordo inset, valore monospace bold; `readonly`/`disabled` → sfondo grigio |
| Valore calcolato | `<output>` |
| Date e numeri | `<time>`, `<data>` → monospace |
| Evidenza gialla (warning) | `<mark>` |
| Evidenza verde (ok) | `<ins>` o `<mark class="mb-ok">` |
| Evidenza ciano (scadenza) | `<mark class="mb-due">` |
| Alert rosso bold | `<em>` (o `.mb-alert`) |
| Bottoni 3D | `<button>` — pressed su `:active`; `.mb-primary` per la variante ciano |
| Bottone lookup `…` | `<button class="mb-lookup">` |
| Bottoniera | `<menu>` con `<li><button>…</button></li>` |
| Tabelle dati | `<table>` con `<th>`/`<td>` |
| Avanzamento a blocchi | `<progress>` |

Campi evidenziati: aggiungi `.mb-mark` (giallo), `.mb-ok` (verde) o `.mb-due` (ciano) direttamente sull'`<input>`.

Utilities di layout per le righe: `.mb-right` (spinge a destra con `margin-left: auto`), `.mb-grow` (occupa lo spazio residuo).

## Esempio minimo

```html
<dialog open>
  <header>
    <h1>-- Finestra di dialogo pagina Web</h1>
    <button aria-label="Chiudi">✕</button>
  </header>
  <form>
    <nav>
      <a href="#">Cliente</a>
      <a href="#" aria-current="page">Dati evento</a>
    </nav>
    <section>
      <p>
        <label for="mezzo">Mezzo:</label>
        <input id="mezzo" size="2" value="7" readonly>
        <button class="mb-lookup" aria-label="Cerca"></button>
        <output>PEC</output>
        <span>Tra gg:</span>
        <mark>non indicato perché già esitato</mark>
      </p>
      <p><em>Possibili pietre prescritte!!</em></p>
    </section>
    <menu>
      <li><button type="submit">OK</button></li>
      <li><button class="mb-primary">Annulla</button></li>
    </menu>
  </form>
</dialog>
```

## Theming

Tutti i token sono custom properties su `:root`, prefisso `--mb-`:

```css
:root {
  --mb-window: #f5f4f1;     /* interno finestra quasi bianco */
  --mb-face: #d8d4cf;       /* grigio di campi e bottoni */
  --mb-tab: #1058a8;        /* tab blu */
  --mb-tab-active: #e8501e; /* tab attivo arancio */
  --mb-mark: #ffff00;       /* evidenza gialla */
  --mb-ok: #39e639;         /* evidenza verde */
  --mb-due: #b8e2e2;        /* evidenza ciano */
  --mb-alert: #e60000;      /* alert rosso */
  --mb-primary: #8ed8d8;    /* bottone primario ciano */
}
```

## Demo

- [demo/index.html](demo/index.html) — **guida ai componenti**: showcase interattivo con esempi live e snippet HTML per ogni componente
- [demo/crm.html](demo/crm.html) — **esempio completo**: scheda di un CRM di segreteria fittizio (gestione pratiche e appuntamenti) con tutti gli stati in azione

Per servirle in locale: `python3 -m http.server` dalla root del progetto, poi apri `http://localhost:8000/demo/`.

## Licenza

MIT — vedi [LICENSE](LICENSE).
