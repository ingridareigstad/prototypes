---
name: start-session
description: >
  Start en ny prototyping-session i dette Tripletex-prosjektet. Les inn alle
  relevante regler, tokens og konvensjoner slik at du kan hjelpe brukeren
  riktig fra første stund. Trigger på "start session", "ny session",
  "start prototyping" eller lignende.
---

# Start prototyping-session

Du starter en ny session i Tripletex-prototyping-prosjektet. Les gjennom dette nøye – det er kilden til sannhet for all koding i dette prosjektet.

## Steg 1: Les inn systemfilene

Les disse filene **nå**, i prioritert rekkefølge:

1. `_system/REGLER.md` — absolutte regler, token-oversikt, komponentklasser og konvensjoner
2. `_system/components.css` — alle tilgjengelige systemklasser
3. `_system/layout.css` — app-shell, topbar, sidebar, page-layout

Disse filene er den autoritative kilden. Hvis noe i chatten strider mot dem, vinner filene.

## Steg 2: Forstå prosjektstrukturen

```
/Users/ingridreigstad/Documents/GitHub/absence-prototypeV1/
  _system/          ← RØR IKKE – tokens.css, components.css, layout.css, REGLER.md
  _templates/       ← Startpunkt for nye prototyper
    side-med-tabell.html
    side-med-skjema.html
  prototyper/       ← Ferdige og pågående prototyper
    absence-v1/     ← Fravær og ferie-modulen (aktiv)
      fravaersoversikt.html
      inntektsmeldinger.html
      inntektsmeldinger-skjema.html
      statistikk.html
      innstillinger.html
      ssb-rapporter.html
      ssb-rapporter-send.html
      avstemming-refusjoner.html
  index.html        ← Dashboard med oversikt over alle prototyper
  .claude/
    launch.json     ← Preview-server: npx serve -l 4567 .
    commands/       ← Disse skillene
```

## Steg 3: Absolutte regler – aldri bryt disse

1. **Ingen hardkodede hex-farger** — aldri `#0a41fa`, alltid `var(--action-primary-rest)`
2. **Ingen hardkodede px-verdier** — aldri `padding: 16px`, alltid `var(--space-16)`
3. **Ingen globale tokens direkte i HTML** — aldri `var(--global-blue-100)`
4. **Kun semantiske tokens** — token-navnene beskriver hensikt, ikke farge
5. **Aldri bold skrift** — `font-weight: bold` og `700` er forbudt; `500` (medium) er maks

## Steg 4: Token-systemet

### Farger
| Kategori | Eksempel-tokens |
|----------|----------------|
| Handling | `--action-primary-rest/hover/active`, `--action-secondary-*`, `--action-tertiary-*`, `--action-neutral-*` |
| Bakgrunn | `--surface-background`, `--surface-default`, `--surface-nav`, `--surface-disabled` |
| Status-bakgrunn | `--surface-info/success/warning/error-rest` og `-active` |
| Tekst | `--text-primary`, `--text-muted`, `--text-placeholder`, `--text-disabled`, `--text-on-action`, `--text-action`, `--text-link` |
| Kanter | `--border-faint`, `--border-muted`, `--border-primary`, `--border-focus`, `--border-hover`, `--border-error/warning/success/info` |

### Spacing (bruk alltid `--space-*`)
`--space-2` `--space-4` `--space-8` `--space-12` `--space-16` `--space-20` `--space-24` `--space-32` `--space-40` `--space-48` `--space-64`

### Størrelser (for høyde på knapper og inputs)
`--size-tiny` (20px) `--size-small` (24px) `--size-medium` (32px) `--size-large` (40px) `--size-xl` (48px)

### Border-radius
`--radius-default` (4px) `--radius-full` (9999px, pille-form) `--radius-none` `--radius-mobile` (16px)

## Steg 5: Systemklasser – bruk alltid disse, aldri egendefinerte varianter

### Knapper
```html
<button class="btn btn-primary">Lagre</button>
<button class="btn btn-secondary">Avbryt</button>
<button class="btn btn-ghost">Se mer</button>
<button class="icon-btn"><!-- svg --></button>
```

### Skjema
```html
<div class="form-group">
  <label class="input-label">Felt <span class="required">*</span></label>
  <input class="input" type="text" placeholder="...">
  <span class="input-hint">Hjelpetekst</span>
</div>
<!-- select og textarea bruker også class="input" -->
```

### Tabell
```html
<div class="table-container">
  <div class="table-toolbar">
    <div class="table-toolbar-filters">
      <div class="input-search-wrap">
        <input class="input" type="search" placeholder="Søk...">
        <svg class="input-search-icon" …></svg>
      </div>
      <div class="switcher">
        <button class="switcher-btn switcher-btn--active">Alle</button>
        <button class="switcher-btn">Aktive</button>
      </div>
      <select class="input toolbar-select">…</select>
    </div>
  </div>
  <table class="tx-table table-standard">…</table>
</div>
```

### Status og chips
```html
<span class="status-dot status-dot--success">Aktiv</span>
<span class="status-dot status-dot--warning">Krever handling</span>
<span class="status-dot status-dot--error">Avvist</span>
<span class="status-dot status-dot--neutral">Inaktiv</span>
<span class="status-dot status-dot--info">Ny</span>
<span class="chip">Etikett</span>
```

### Alerts
```html
<div class="alert alert--info">…</div>
<div class="alert alert--warning">…</div>
<div class="alert alert--success">…</div>
<div class="alert alert--error">…</div>
```

### Kort
```html
<div class="card">
  <div class="card-header">…</div>
  <div class="card-body">…</div>
</div>
```

## Steg 6: App-shell – topbar og sidebar

**Kopier alltid topbar og sidebar fra `_templates/side-med-tabell.html`**, ikke fra gamle prototyper og ikke fra scratch. Den inneholder riktig struktur med alle ikonknapper.

Topbar-klasser: `.app-topbar`, `.topbar-left`, `.topbar-right`, `.topbar-logo`, `.topbar-sep`, `.topbar-company`, `.topbar-icon-btn`, `.topbar-user-btn`, `.topbar-assistant`

Sidebar-klasser: `.sidebar`, `.nav-item`, `.nav-item--active`, `.nav-icon`, `.nav-sub`, `.nav-sub--active`, `.nav-bullet`

Page-layout: `.main-content > .page > .page-header + innhold`

## Steg 7: Ny prototype – alltid kopier fra mal

- **Tabell/liste-side** → kopier `_templates/side-med-tabell.html`
- **Skjema-side** → kopier `_templates/side-med-skjema.html`
- Legg filen i `prototyper/{kebab-case-navn}/`
- Rett CSS-stier til `../../_system/`
- Bruk `/start-session` → `ny-prototype`-kommandoen for full veiledning

## Steg 8: Figma-integrasjon

Når brukeren gir en Figma-URL (`figma.com/design/:fileKey/…?node-id=…`):
1. Hent design-kontekst med `get_design_context` (fileKey og nodeId fra URL-en)
2. Figma-verktøyet returnerer React/Tailwind — **konverter alltid til vanilla HTML/CSS** med systemklassene over
3. Hardkodede farger i Figma-kode (f.eks. `#0a41fa`) → erstatt med semantisk token (`var(--action-primary-rest)`)
4. Tailwind-spacing (f.eks. `p-4`) → erstatt med `var(--space-16)`

## Steg 9: Preview-server

Serveren kjøres med `npx serve -l 4567 .` fra prosjektroten (konfigurert i `.claude/launch.json`).

**Merk:** `serve` bruker clean URLs — `.html`-endelsen strippes. Dette betyr at preview-verktøyets eval/navigate ikke alltid klarer å navigere direkte til undersider. Verifiser heller endringer ved å grep/lese kildekoden, eller be brukeren åpne filen direkte i nettleseren.

---

## Oppsummering: Slik hjelper du i denne prototypen

- **Les alltid `_system/REGLER.md`** ved tvilstilfeller
- **Aldri hardkodede verdier** — tokens for alt
- **Aldri bold** — maks `font-weight: 500`
- **Alltid systemklasser** — `btn`, `input`, `form-group`, `table-container`, `status-dot`, `chip`, `alert`, `card`, `icon-btn` osv.
- **Alltid mal som base** — ikke bygg app-shell fra scratch
- **Figma → konverter til systemklasser**, ikke kopier Tailwind

Svar brukeren kort med hva du har lest og er klar til å hjelpe med.
