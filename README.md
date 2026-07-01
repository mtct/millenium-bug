# millenium-bug

Retro banking vibes for your website.

A **classless-first** CSS library that recreates the look of late-'90s web banking back-offices: a near-white page, inset grey fields, cobalt-blue tabs, Courier-bold values, phosphor-yellow highlights and fire-red alerts. No border-radius. No transitions. No mercy.

## Installation

```html
<link rel="stylesheet" href="millenium-bug.css">
```

No dependencies, no build step. A single file, the way it used to be done.

## Philosophy: semantics first

Semantic HTML elements are styled directly — write correct HTML and you get the enterprise app. The `.mb-*` classes exist only as modifiers.

## Components

| Component | Semantic HTML |
| --- | --- |
| Dialog window | `<dialog open>` (or `.mb-window`) |
| Title bar | `<dialog> > <header>` with `<h1>` and `<button aria-label="Close">` |
| Tabs | `<nav>` with `<a>`/`<button>`; active tab via `aria-current` or `aria-selected="true"` |
| Content panel | `<section>` right after the `<nav>` (or `.mb-panel`) |
| Field row | `<p>` inside `<form>` (or `.mb-row`) — dense flex, inline label + fields |
| Fields | `<input>`, `<select>`, `<textarea>` — inset border, monospace bold value; `readonly`/`disabled` → grey background |
| Computed value | `<output>` |
| Dates and numbers | `<time>`, `<data>` → monospace |
| Yellow highlight (warning) | `<mark>` |
| Green highlight (ok) | `<ins>` or `<mark class="mb-ok">` |
| Cyan highlight (due date) | `<mark class="mb-due">` |
| Bold red alert | `<em>` (or `.mb-alert`) |
| 3D buttons | `<button>` — pressed on `:active`; `.mb-primary` for the cyan variant |
| Lookup button `…` | `<button class="mb-lookup">` |
| Button bar | `<menu>` with `<li><button>…</button></li>` |
| Data tables | `<table>` with `<th>`/`<td>` |
| Block progress | `<progress>` |

Highlighted fields: add `.mb-mark` (yellow), `.mb-ok` (green) or `.mb-due` (cyan) directly on the `<input>`.

Layout utilities for rows: `.mb-right` (pushes right with `margin-left: auto`), `.mb-grow` (takes the remaining space).

## Minimal example

```html
<dialog open>
  <header>
    <h1>-- Web page dialog window</h1>
    <button aria-label="Close">✕</button>
  </header>
  <form>
    <nav>
      <a href="#">Contact</a>
      <a href="#" aria-current="page">Event data</a>
    </nav>
    <section>
      <p>
        <label for="mezzo">Channel:</label>
        <input id="mezzo" size="2" value="7" readonly>
        <button class="mb-lookup" aria-label="Search"></button>
        <output>PEC</output>
        <span>In days:</span>
        <mark>not specified because already processed</mark>
      </p>
      <p><em>Possible statute of limitations!!</em></p>
    </section>
    <menu>
      <li><button type="submit">OK</button></li>
      <li><button class="mb-primary">Cancel</button></li>
    </menu>
  </form>
</dialog>
```

## Theming

All tokens are custom properties on `:root`, prefixed with `--mb-`:

```css
:root {
  --mb-window: #f5f4f1;     /* near-white window interior */
  --mb-face: #d8d4cf;       /* grey of fields and buttons */
  --mb-tab: #1058a8;        /* blue tab */
  --mb-tab-active: #e8501e; /* active orange tab */
  --mb-mark: #ffff00;       /* yellow highlight */
  --mb-ok: #39e639;         /* green highlight */
  --mb-due: #b8e2e2;        /* cyan highlight */
  --mb-alert: #e60000;      /* red alert */
  --mb-primary: #8ed8d8;    /* cyan primary button */
}
```

## Vibe coding

Feeding this style to an AI coding assistant (Claude Code, Cursor, v0, Copilot…) works best when you paste a short rules block instead of describing the look in prose. The library is classless-first, so the winning instruction is *"write semantic HTML, don't invent classes."*

**Drop-in system prompt** — paste this into your assistant's rules/system message:

```text
Style every UI with the "millenium-bug" CSS library (late-'90s banking back-office look).
Rules:
- Link it once: <link rel="stylesheet" href="millenium-bug.css">. Add no other CSS.
- Write SEMANTIC HTML and let it be styled: <dialog open> for windows, <header>+<h1>
  for title bars, <nav> for tabs (active tab = aria-current="page"), <section> for panels,
  <form> with each <p> as a dense row of <label>+<input>, <menu> for the button bar.
- Fields use the size attribute for width. Use <output> for decoded/computed values,
  <time>/<data> for dates and numbers, <mark> for warnings, <ins> for ok, <em> for alerts.
- Do NOT invent class names. The ONLY allowed classes are modifiers:
  .mb-primary, .mb-lookup, .mb-mark, .mb-ok, .mb-due, .mb-right, .mb-grow.
- No border-radius, no transitions, no gradients, no icons libraries. Keep it dense and flat.
```

**One-line prompt** — for a quick request:

> Build it as a '90s enterprise CRM screen using the millenium-bug CSS library: semantic HTML only (`<dialog>`, `<nav>` tabs, `<form>` rows of `<label>`+`<input>`, `<menu>` buttons), no custom classes except the `.mb-*` modifiers, no border-radius or transitions.

**Tips that keep the output on-model:**

- Point the assistant at the demos as reference: *"match the markup style of `demo/crm.html`."* Concrete examples beat adjectives.
- Ask for **dense, single-line form rows** — one `<p>` per row, labels and inputs inline. That single instruction is what sells the mainframe feel.
- If it starts adding utility classes or a component framework, remind it: *"classless-first — semantic tags only, `.mb-*` are the sole exception."*
- Want a different era or palette? Tell it to override the `--mb-*` custom properties on `:root` instead of editing the library.

## Demo

- [demo/index.html](demo/index.html) — **component guide**: interactive showcase with live examples and HTML snippets for every component
- [demo/crm.html](demo/crm.html) — **full example**: a record from a fictional secretariat CRM (case and appointment management) with every state in action

To serve them locally: `python3 -m http.server` from the project root, then open `http://localhost:8000/demo/`.

## License

MIT — see [LICENSE](LICENSE).
