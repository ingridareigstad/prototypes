# Tripletex HTML/CSS Prototyping

This repo is a static HTML/CSS prototyping system for Tripletex. All prototypes use a shared design token system and component library — no frameworks, no build steps.

## Absolutte regler — bryt aldri disse

1. **Ingen hardkodede hex-farger** — aldri `#0a41fa`, alltid `var(--action-primary-rest)`
2. **Ingen hardkodede px-verdier** — aldri `padding: 16px`, alltid `var(--space-16)`
3. **Ikke bruk globale tokens direkte** — aldri `var(--global-blue-100)`, bare semantiske tokens
4. **Aldri bold skrift** — `font-weight: bold` og `700` er forbudt; `500` (medium) er maks
5. **Alltid systemklasser** — `btn`, `input`, `form-group`, `tx-table`, `status-dot`, `chip`, `alert`, `card` osv. — aldri egne varianter

## Systemfiler — rør ikke disse

```
_system/tokens.css       ← alle design tokens (farger, spacing, størrelser, radius)
_system/components.css   ← alle komponentklasser
_system/layout.css       ← app-shell, topbar, sidebar, page-layout
_system/REGLER.md        ← full referanse: token-oversikt, kodeeksempler, konvensjoner
```

**Les `_system/REGLER.md` for full komponentreferanse, kodeeksempler og mappekonvensjoner.**

## Maler — bruk alltid som startpunkt

| Mal | Bruk når |
|-----|----------|
| `_templates/side-med-tabell.html` | Siden viser en liste eller tabell |
| `_templates/side-med-skjema.html` | Siden har et skjema med felter og knapper |

Kopier riktig mal, legg filen i `prototyper/{kebab-case-navn}/`, og rett CSS-stiene til `../../_system/`.

## Slash-kommandoer

- `/start-session` — les inn systemfilene og bekreft at du er klar
- `/ny-prototype` — guided oppretting av ny prototype

## Preview

```
npx serve -l 4567 .
```
