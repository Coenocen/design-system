# Design System — Coen van den Broek

Gedeeld design system voor alle apps van Coen (MijnCRM, Attentiecoach,
toekomstige projecten). Eén bron van waarheid voor kleuren, typografie,
spacing en componenten.

## Doel

Andere apps symlinken of kopiëren de CSS-bestanden uit dit project. Wijzigingen
hier werken (via symlinks) direct door in alle aangesloten apps.

## Bestanden

| Bestand | Inhoud |
|---------|--------|
| `tokens.css` | Alle CSS custom properties — kleuren, radius, spacing, fonts, glass-tokens |
| `base.css` | Reset + Work Sans typografie + zonsopgang-gradient achtergrond |
| `components.css` | Herbruikbare componenten: `.btn`, `.card`, `.fg`, `.pill`, `.sidebar`, `.main`, `.toast` |
| `styleguide.html` | Visuele referentie — open in browser om alles te zien |
| `PRINCIPLES.md` | Ontwerpregels en anti-patronen |

## Gebruiken in een app

```bash
cd ~/mijn-app
mkdir -p styles
ln -s ~/design-system/tokens.css     styles/tokens.css
ln -s ~/design-system/base.css       styles/base.css
ln -s ~/design-system/components.css styles/components.css
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

## Kernregels

1. **8px radius** overal (uitzonderingen: badges 4px, pills 999px, modals 12px)
2. **Work Sans** als enige font
3. **Glass-look** op kaarten (witte semi-transparante achtergrond + backdrop-blur)
4. **Accent `#e33b2a`** (rood-oranje) voor primaire actieknoppen/links
5. **Nederlandse UI-copy** — zakelijk maar menselijk, geen emoji
6. **Spacing schaal** — alleen 4/8/12/16/20/24 (`--sp-1` t/m `--sp-6`)

Zie `PRINCIPLES.md` voor het volledige overzicht inclusief anti-patronen.

## Workflow voor wijzigingen

1. **Nieuwe kleur/token nodig?** Voeg toe aan `tokens.css` met korte comment
2. **Nieuwe herbruikbare component?** Schrijf in `components.css`, demo in `styleguide.html`
3. **Bump changelog** onderaan `PRINCIPLES.md` bij breaking changes
4. **Visueel testen** — open `styleguide.html` om te checken dat bestaande componenten nog kloppen
5. **Commit** per logisch blok (tokens / componenten / docs afzonderlijk committen)

## Styleguide bekijken

```bash
open ~/design-system/styleguide.html
```

## Backlog / ideeën

- Modal-component (huidige `.modal` is inline per app)
- Dropdown-component met z-index management (bij `backdrop-filter` panels)
- Data-tabel met sorteerbare kolommen
- Dark mode tokens (parallel `:root[data-theme="dark"]`)
- Form-validation states (error / success borders)
- Loading spinner / skeleton loader
