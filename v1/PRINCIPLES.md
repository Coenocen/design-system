# Coen Design System — Principes

Gedeeld design system voor alle apps van Coen (MijnCRM, Attentiecoach, etc.).
Versie 1.0.

## Kernregels

### 1. Consistentie boven creativiteit
Nieuwe componenten sluiten aan bij bestaande. Nooit een nieuwe kleur of radius
introduceren tenzij er écht een goede reden is. Als je iets mist, voeg het toe
aan `tokens.css` — niet ad-hoc in een app.

### 2. Altijd CSS custom properties gebruiken
Nooit hardcoded kleuren (`#e33b2a`), afmetingen (`8px`) of fonts in componenten.
Gebruik altijd `var(--accent)`, `var(--radius)`, `var(--font)`.

Uitzondering: alpha-variaties van een bestaande kleur mogen hardcoded
(`rgba(37,99,235,.05)`) want die zijn niet los als token gedefinieerd.

### 3. 8px radius overal
Kaarten, knoppen, inputs, panels: allemaal `var(--radius)` = 8px.
Modals iets ronder (`--radius-modal` = 12px). Badges vierkanter (`--radius-badge` = 4px).
Pills volrond (`--radius-pill` = 999px).

### 4. Glass-look als signature
Kaarten en belangrijke panels krijgen de `.glass` class of gebruiken de tokens
`--glass-bg`, `--glass-blur`, `--glass-border`, `--glass-shadow`.
De achtergrond is een zonsopgang-gradient (`--grad-1` t/m `--grad-5`).

### 5. Nederlandse UI-copy
Alle labels, knoppen, foutmeldingen, toasts in het Nederlands.
Toon is zakelijk maar menselijk — geen "Oeps!" of overdreven enthousiasme.

### 6. Kleurgebruik
- **Accent (rood-oranje `#e33b2a`):** primaire actieknoppen, links, focus-state
- **Dienst (blauw):** services, verzend-acties, projecten
- **Product (paars):** producten
- **Inkoop (groen):** inkoop, positieve waarden, saldo
- **Groen:** success, uren, online-status
- **Amber:** waarschuwingen, planning
- **Rood:** errors, gevaarzone

### 7. Typografie
- Font: **Work Sans** (via Google Fonts)
- Fontsize base 16px, maar UI gebruikt `--fs-sm` (13px) voor de meeste tekst,
  `--fs-xs` (11.5px) voor labels en meta-info
- Gewichten: 400 (body), 500 (labels/buttons), 600 (headings/strong)

### 8. Spacing schaal
4, 8, 12, 16, 20, 24 (de `--sp-1` t/m `--sp-6` tokens).
Gebruik géén ad-hoc waarden zoals 10px, 14px, 18px.

### 9. Knoppen
- Default hoogte 32px (`--h-btn`)
- Kleinere varianten met `.sm` (26px), grotere met `.md` (34px) of `.lg` (40px)
- Primair = `.bp` (accent background)
- Secundair = `.bg` (witte achtergrond, grijze border)
- Ghost/add = `.bgr` of `.btn-add` (dashed border, transparant)
- Icon-only = `.ib`

### 10. Forms
- Label boven het veld, 11.5px grijs
- Inputs 36px hoog, 8px radius, focus-state = accent border
- Twee-kolom layout: wrap in `.fr`

## Anti-patronen

❌ Gebruik geen box-shadow op buttons — die komen alleen op kaarten
❌ Geen hover-animaties langer dan 200ms
❌ Geen emoji in UI-teksten (behalve waar expliciet gevraagd door gebruiker)
❌ Geen drop-downs zonder z-index management in panels met `backdrop-filter`
    (dat creëert een eigen stacking context — zie MijnCRM `toggleAssignDD` fix)
❌ Geen inline styles voor iets dat een token heeft

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
ln -s ~/design-system/tokens.css     styles/tokens.css
ln -s ~/design-system/base.css       styles/base.css
ln -s ~/design-system/components.css styles/components.css
```

Met symlink krijg je automatisch alle design-updates mee. Met kopiëren heb je
app-specifieke vrijheid maar moet je zelf bijhouden. Voor productie-apps: kopieer
en lock de versie. Voor snel schakelen tussen apps: symlink.

## Updates en versioning

Bij wijziging van `tokens.css`: bump de versie in de comment-header en documenteer
breaking changes hieronder:

### v1.0 (2026-04-23)
- Initiële versie, geëxtraheerd uit MijnCRM
