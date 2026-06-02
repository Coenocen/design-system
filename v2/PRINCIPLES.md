# Coen Design System — Principes (v2)

Gedeeld, app-agnostisch design system voor alle projecten van Coen.
Versie 2.0.

## Kernregels

### 1. Consistentie boven creativiteit
Nieuwe componenten sluiten aan bij bestaande. Nooit een nieuwe kleur, radius of
spacing-waarde introduceren tenzij er écht een goede reden is. Ontbreekt iets?
Voeg het toe aan `tokens.css` — niet ad-hoc in een app.

### 2. Altijd tokens gebruiken
Nooit hardcoded kleuren (`#e33b2a`), afmetingen (`8px`) of fonts in componenten.
Gebruik `var(--accent)`, `var(--radius)`, `var(--font)`, etc.

Uitzondering: alpha-variaties van een bestaande kleur mogen hardcoded
(`rgba(0,0,0,.05)`) als ze niet los als token gedefinieerd zijn.

### 3. Semantic tokens > primitieven in componenten
Gebruik `--text-primary`, `--surface`, `--border-subtle` in componenten.
Laat primitieven (`--ink`, `--paper`, `--line`) alleen voorkomen in `tokens.css`.
Dit maakt dark-mode-support straks triviaal: je overschrijft alleen de semantic
layer.

### 4. Leesbare classnames
Componenten hebben beschrijvende klassen: `.btn-primary`, `.nav-item`,
`.page-header`. Geen cryptische afkortingen zoals `.bp` of `.ni`.
Modifiers als losse klassen: `.btn-sm` (niet `.btn.sm`).

### 5. 8px radius overal
Kaarten, knoppen, inputs, panels: `var(--radius-md)` = 8px.
Modals iets ronder (`--radius-lg` = 12px). Badges/tags strakker
(`--radius-sm` = 4px). Pills volrond (`--radius-pill` = 999px).

### 6. Glass-look is optioneel, niet signature
De `.surface-glass` class blijft beschikbaar voor apps die een glas/gradient-
esthetiek willen (zoals MijnCRM), maar is geen standaardelement meer. De
standaardoppervlakte is solid wit (`--surface`) met `.card`.

Apps kiezen zelf hun achtergrond — het design system zet geen body-gradient meer.

### 7. Nederlandse UI-copy
Alle labels, knoppen, foutmeldingen, toasts in het Nederlands.
Toon is zakelijk maar menselijk — geen "Oeps!" of overdreven enthousiasme.

### 8. Kleurgebruik
- **Accent (rood-oranje `#e33b2a`):** primaire actieknoppen, links, focus-state
- **Green:** success, uren, online-status
- **Amber:** waarschuwingen, planning
- **Blue:** info, neutrale statussen
- **Danger (= accent):** errors, gevaarzone, verwijderen
- **Purple:** reserve (dashboards, data-viz)

Business-specifieke kleuren (bijv. MijnCRM's dienst/product/inkoop) horen
NIET in dit design system. Die definieert elke app zelf.

### 9. Typografie
- Font: **Work Sans** (via Google Fonts)
- Document-base 16px, UI-body `--fs-sm` (13px), meta/labels `--fs-xs` (11.5px)
- Koppen: `--fs-lg` (h3), `--fs-xl` (h2), `--fs-2xl` (h1)
- Gewichten: 400 (body), 500 (labels/buttons), 600 (koppen/strong), 700 (uppercase labels)

### 10. Spacing-schaal
4, 8, 12, 16, 20, 24, 32, 40 (de `--sp-1` t/m `--sp-8` tokens).
Gebruik géén ad-hoc waarden zoals 10px, 14px, 18px.

### 11. Knoppen
- Default hoogte 32px (`--h-btn`)
- Kleinere: `.btn-sm` (26px). Grotere: `.btn-md` (34px), `.btn-lg` (40px)
- Primair: `.btn-primary` (accent)
- Secundair: `.btn-secondary` (wit + grijze border)
- Ghost/add: `.btn-ghost` (dashed border, transparant)
- Destructief: `.btn-danger` (rood)
- Icon-only: `.btn-icon`

### 12. Formulieren
- Label boven het veld, 11.5px grijs (`--text-muted`)
- Inputs 36px hoog, 8px radius, focus = accent border + focus-ring
- Twee kolommen: wrap in `.field-row`

### 13. Focus altijd zichtbaar
Elk interactief element toont bij toetsenbordfocus een `--focus-ring` box-shadow.
Nooit `outline: none` zonder vervanging.

## Anti-patronen

- Gebruik geen box-shadow op buttons — shadows horen bij kaarten en overlays
- Geen hover-animaties langer dan 200ms
- Geen emoji in UI-teksten (tenzij expliciet gevraagd)
- Geen dropdowns zonder z-index-management in panels met `backdrop-filter`
  (backdrop-filter creëert een eigen stacking context)
- Geen inline styles voor iets dat een token heeft
- Geen primitieve tokens direct gebruiken in componenten — altijd via semantic
  tokens

## Setup in een nieuwe app

```html
<!DOCTYPE html>
<html lang="nl">
<head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
  <link href="https://fonts.googleapis.com/icon?family=Material+Symbols+Rounded" rel="stylesheet">
  <link rel="stylesheet" href="./styles/tokens.css">
  <link rel="stylesheet" href="./styles/base.css">
  <link rel="stylesheet" href="./styles/components.css">
</head>
```

Kopieer de CSS-bestanden in `styles/` of symlink ze:
```bash
mkdir -p styles
ln -s ~/design-system/v2/tokens.css     styles/tokens.css
ln -s ~/design-system/v2/base.css       styles/base.css
ln -s ~/design-system/v2/components.css styles/components.css
```

Met symlink krijg je automatisch alle design-updates mee. Met kopiëren heb je
app-specifieke vrijheid maar moet je zelf bijhouden. Voor productie-apps:
kopieer en lock de versie. Voor snel schakelen tussen apps: symlink.

## Updates en versioning

Wijzigingen aan `tokens.css` of `components.css` bump de minor/patch-versie in
de header-comment. Breaking changes documenteren in deze file:

### v2.0 (2026-04-23)
- App-agnostisch gemaakt: sidebar-tokens, business-type kleuren en
  zonsopgang-gradient verhuisd naar apps.
- Semantic token-layer toegevoegd (`--text-*`, `--surface-*`, `--border-*`).
- Classnames hernoemd naar leesbare vormen (`.bp` → `.btn-primary`, etc.).
- Componenten toegevoegd: `.modal`, `.dropdown`, `.tabs`, `.alert`, `.table`,
  `.tooltip`, `.avatar`, `.skeleton`.
- Dark-mode hook voorbereid via `[data-theme="dark"]` (nog niet ingevuld).
