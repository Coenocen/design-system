# Coen Design System

Gedeeld design system voor alle apps van Coen (MijnCRM, Attentiecoach, Post Ads-tools, toekomstige projecten).

## Structuur

```
~/design-system/
├── v1/   # Legacy — gebruikt door MijnCRM
│   ├── tokens.css        # MijnCRM-specifieke tokens (sidebar, business-kleuren, gradient)
│   ├── base.css          # Reset + zonsopgang-achtergrond
│   ├── components.css    # Cryptische classnames (.bp, .ni, .bdg, ...)
│   ├── PRINCIPLES.md
│   └── styleguide.html
└── v2/   # Nieuw — app-agnostisch, aanbevolen voor alle nieuwe apps
    ├── tokens.css        # Primitieven + semantic layer + dark-mode hook
    ├── base.css          # Reset + typografie (geen app-achtergrond)
    ├── components.css    # Leesbare classnames (.btn-primary, .nav-item, ...)
    ├── PRINCIPLES.md
    ├── styleguide.html
    └── MIGRATION.md      # v1 → v2 classname/token-mapping
```

## Welke versie voor welke app?

| App | Versie | Status |
|-----|--------|--------|
| MijnCRM | v1 | Inline in `index.html`; migratie naar v2 ingepland |
| Attentiecoach (admin + web) | v2 | Gebruik v2 vanaf start |
| Post Ads-tools | v2 | |
| Toekomstige apps | v2 | Default |

## Snelstart — nieuwe app op v2

```bash
cd /pad/naar/app
mkdir -p styles
ln -s ~/design-system/v2/tokens.css     styles/tokens.css
ln -s ~/design-system/v2/base.css       styles/base.css
ln -s ~/design-system/v2/components.css styles/components.css
```

In HTML:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/icon?family=Material+Symbols+Rounded" rel="stylesheet">
<link rel="stylesheet" href="./styles/tokens.css">
<link rel="stylesheet" href="./styles/base.css">
<link rel="stylesheet" href="./styles/components.css">
```

Met symlink krijg je automatisch alle design-updates mee. Voor productie-apps kun je ook de bestanden kopiëren en de versie vastpinnen.

## Styleguides

Open in een browser:
- v2: `~/design-system/v2/styleguide.html`
- v1: `~/design-system/v1/styleguide.html`

## Principes

Zie `v2/PRINCIPLES.md` (of `v1/PRINCIPLES.md` voor de legacy-regels). Kernpunten:
- 8px radius standaard
- Work Sans als font
- Accent `#e33b2a` (rood-oranje)
- Nederlandse UI-copy
- Altijd tokens, geen hardcoded waarden
- In componenten: semantic tokens (`--text-primary`, `--surface`) boven primitieven (`--ink`, `--paper`)

## Contribueren

Nieuwe patronen worden eerst hier toegevoegd, daarna pas in de apps gebruikt. Nooit andersom. Bij wijziging: bump versie in `tokens.css`-header en documenteer breaking changes in `v2/PRINCIPLES.md`.
