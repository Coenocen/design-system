# Design System — Coen van den Broek

Gedeeld design system voor alle apps van Coen (MijnCRM, Attentiecoach,
toekomstige projecten). Eén bron van waarheid voor kleuren, typografie,
spacing en componenten.

## Versies

- **v2** (`~/design-system/v2/`) — **default voor alle nieuwe apps**.
  App-agnostisch, semantic token-layer, leesbare classnames, voorbereid op
  dark mode. Uitgebreide componentset (modal, dropdown, tabs, alerts, table,
  tooltip, avatar, skeleton).
- **v1** (`~/design-system/v1/`) — legacy, gebruikt door MijnCRM. Bevat
  MijnCRM-specifieke tokens (sidebar-breedte, business-type kleuren,
  zonsopgang-gradient) en cryptische classnames (`.bp`, `.ni`, `.bdg`). Wordt
  later gemigreerd naar v2 — zie `v2/MIGRATION.md`.

## Bestanden (v2)

| Bestand | Inhoud |
|---------|--------|
| `v2/tokens.css` | Primitieven + semantic tokens (`--text-primary`, `--surface`, `--border-subtle`) + dark-mode hook |
| `v2/base.css` | Reset + Work Sans typografie + focus-ring. Géén app-achtergrond. |
| `v2/components.css` | `.card`, `.btn-*`, `.field*`, `.badge/pill/tag`, `.alert`, `.modal`, `.dropdown`, `.tabs`, `.table`, `.tooltip`, `.avatar`, `.skeleton`, `.toast`, `.sidebar`, `.nav-*` |
| `v2/styleguide.html` | Visuele referentie — open in browser |
| `v2/PRINCIPLES.md` | Ontwerpregels en anti-patronen |
| `v2/MIGRATION.md` | v1 → v2 classname/token mapping voor MijnCRM-migratie |
| `README.md` | Overzicht en snelstart |

## Gebruiken in een app (v2)

```bash
cd ~/mijn-app
mkdir -p styles
ln -s ~/design-system/v2/tokens.css     styles/tokens.css
ln -s ~/design-system/v2/base.css       styles/base.css
ln -s ~/design-system/v2/components.css styles/components.css
```

In de HTML `<head>`:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/icon?family=Material+Symbols+Rounded" rel="stylesheet">
<link rel="stylesheet" href="./styles/tokens.css">
<link rel="stylesheet" href="./styles/base.css">
<link rel="stylesheet" href="./styles/components.css">
```

## Kernregels (v2)

1. **8px radius** overal (uitzonderingen: badges/tags 4px, pills 999px, modals 12px)
2. **Work Sans** als enige font
3. **Accent `#e33b2a`** (rood-oranje) voor primaire actieknoppen/links
4. **Glass-look optioneel** — `.surface-glass` alleen waar de app-achtergrond dat rechtvaardigt
5. **Nederlandse UI-copy** — zakelijk maar menselijk, geen emoji
6. **Spacing schaal** — alleen 4/8/12/16/20/24/32/40 (`--sp-1` t/m `--sp-8`)
7. **Semantic tokens in componenten** — `--text-primary` boven `--ink`
8. **Leesbare classnames** — `.btn-primary`, niet `.bp`

Zie `v2/PRINCIPLES.md` voor het volledige overzicht inclusief anti-patronen.

## Workflow voor wijzigingen

1. **Nieuwe token nodig?** Voeg toe aan `v2/tokens.css` met korte comment
2. **Nieuwe component?** Schrijf in `v2/components.css`, demo in `v2/styleguide.html`
3. **Bump changelog** onderaan `v2/PRINCIPLES.md` bij breaking changes
4. **Visueel testen** — open `v2/styleguide.html` om bestaande componenten te checken
5. **Commit** per logisch blok (tokens / componenten / docs afzonderlijk)

v1 wordt niet meer uitgebreid. Fixes daar alleen voor MijnCRM-blokkerende bugs.

## Styleguide bekijken

```bash
open ~/design-system/v2/styleguide.html
```
