---
name: ny-prototype
description: >
  Lag en ny HTML/CSS-prototype i dette prosjektet. Bruk denne skillet når
  brukeren vil lage en ny prototype, nytt skjermbilde, ny side eller ny
  seksjon i prototyping-systemet. Trigger på fraser som "lag en ny prototype",
  "ny prototype", "legg til prototype", "opprett prototype" eller når brukeren
  beskriver en ny del av Tripletex de vil prototype.
---

# Lag ny prototype

Du hjelper brukeren med å opprette en ny prototype i dette Tripletex-prototyping-prosjektet. Målet er at alt følger eksisterende mønstre fra `_templates/` og `_system/`, slik at prototypen ser riktig ut fra første stund.

## Steg 1: Samle informasjon

Spør brukeren om følgende med `AskUserQuestion`:

- **Navn** (kebab-case, f.eks. `faktura-v1`) — brukes som mappenavn og filnavn
- **Visningsnavn** (f.eks. `Faktura`) — vises i nav og dashbord
- **Beskrivelse** — kort setning om hva prototypen dekker, til dashbordet
- **Sider** — liste over sider som skal inngå, f.eks. `oversikt (tabell), ny-faktura (skjema)`

For "Sider": be brukeren skrive sidenavn og type (tabell/skjema) for hver side. Hvis de er usikre, foreslå `index (tabell)` som default startpunkt.

## Steg 2: Opprett mappestruktur

Opprett mappen:
```
prototyper/{navn}/
```

Rotet til prosjektet er `/Users/ingridreigstad/Documents/GitHub/absence-prototypeV1/`.

## Steg 3: Kopier og tilpass maler

For **hver side** brukeren har spesifisert:

### Velg mal
- Side med liste/tabell → `_templates/side-med-tabell.html`
- Side med skjema/formular → `_templates/side-med-skjema.html`

### Kopier og gi nytt navn
Filnavn = sidenavn i kebab-case + `.html`, f.eks. `oversikt.html`, `ny-faktura.html`.

### Tilpass innholdet
Gjør disse endringene i den kopierte filen:

1. **`<title>`** — oppdater til `{Sidetittel} – Tripletex`

2. **CSS-stier** — malen bruker `../_system/`, men prototyper ligger ett nivå dypere. Rett til:
   ```html
   ../../_system/tokens.css
   ../../_system/components.css
   ../../_system/layout.css
   ```

3. **Sidebar-navigasjon** — finn riktig `nav-item` og merk den aktiv:
   ```html
   <div class="nav-item nav-item--active">
     <span class="nav-icon">…</span>
     {Visningsnavn}
   </div>
   ```
   Hvis prototypen har undersider i nav, legg til `nav-sub`-lenker under og merk aktiv side med `nav-sub--active`.

4. **Sidetittel** — oppdater `<h1>` og eventuelt undertittel til noe meningsfullt.

5. **Lenker mellom sider** — bruk relative stier innen samme mappe, f.eks. `href="ny-faktura.html"`.

6. **Dummy-innhold** — fyll inn realistisk eksempelinnhold tilpasset prototype-temaet. Ikke la stå generisk placeholder-tekst fra malen.

## Steg 4: Oppdater dashbordet (index.html)

Legg til et nytt `proto-card` i `index.html` i rotet. Kopier mønsteret fra eksisterende kort og fyll inn:

```html
<div class="proto-card">
  <div class="proto-card-header">
    <div>
      <div class="proto-card-title">{Visningsnavn}</div>
      <div class="proto-card-desc">{Beskrivelse}</div>
    </div>
    <div class="proto-card-meta">
      <span class="status-badge status-badge--wip">Under arbeid</span>
      <span class="proto-date">Opprettet {dagens dato, f.eks. "5. juni 2026"}</span>
    </div>
  </div>
  <div class="proto-pages">
    <!-- én lenke per side -->
    <a class="proto-page-link" href="prototyper/{navn}/{filnavn}.html" target="_blank">
      <svg …pil-ikon…></svg>
      {Sidevisningsnavn}
    </a>
  </div>
</div>
```

Bruk pil-SVG-ikonet fra eksisterende lenker i index.html.

## Steg 5: Bekreft

Gi brukeren en kort oppsummering:
- Hvilke filer som ble opprettet
- At dashbordet er oppdatert
- Påminn om at de kan pushe via GitHub Desktop

## Steg 6: Kjør linter og rett feil

Kjør linting-scriptet på de nyopprettede filene:

```bash
node _system/lint.js prototyper/{navn}/
```

Les output nøye. Rett **alle feil** (`✖`) før du er ferdig:
- Hex-farger → erstatt med semantisk token (`var(--action-primary-rest)` osv.)
- Hardkodet `padding`/`margin`/`gap` i px → erstatt med `var(--space-*)` 
- `font-weight: bold` / `700` → endre til `500`
- `var(--global-*)` → erstatt med semantisk token

Kjør lintere på nytt etter rettinger og bekreft at output er `✅ Ingen regelbrudd funnet.`

---

## Viktige regler som gjelder for alle prototyper

- Ingen hardkodede hex-farger — alltid `var(--token-navn)`
- Ingen hardkodede px-verdier — alltid `var(--space-*)`
- `font-weight: bold` / `700` er forbudt — bruk maks `500` (medium)
- Lenker: blå tekst (`color: var(--text-link)`), regular vekt, ingen underline
- Bruk alltid system-komponentklasser: `btn btn-primary`, `table-container`, `form-group`, `input`, `status-dot`, `chip` osv. — aldri egne varianter
- Topbar og sidebar kopier alltid fra mal eller eksisterende prototype, ikke skriv fra scratch
- Se `_system/REGLER.md` for full oversikt
