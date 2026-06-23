# Coen Design System — Principes (v2)

Gedeeld, app-agnostisch design system voor alle projecten van Coen.
Versie 2.1 — Geist + Jugoo/GA4-stijl.

Deze principes zijn de **vaste design-afspraken** die overal worden toegepast.
Bron-van-waarheid: `tokens.css`, `base.css`, `components.css`.

---

## 1. Kernregels

### 1.1 Consistentie boven creativiteit
Nieuwe componenten sluiten aan bij bestaande. Nooit een nieuwe kleur, radius of
spacing-waarde introduceren tenzij er écht een goede reden is. Ontbreekt iets?
Voeg het toe aan `tokens.css` — niet ad-hoc in een app.

### 1.2 Altijd tokens gebruiken
Nooit hardcoded kleuren (`#e33b2a`), afmetingen (`8px`) of fonts in componenten.
Gebruik `var(--accent)`, `var(--radius)`, `var(--font)`, etc.

### 1.3 Semantic tokens > primitieven in componenten
- `var(--accent)` (semantic) i.p.v. `#1A73E8` (primitief)
- `var(--text-primary)` i.p.v. `#202124`
- Primitieven (`--grijs-100` etc.) zijn de bouwstenen, niet voor direct gebruik

---

## 2. Typografie

### 2.1 Font: Geist (Vercel)
**Alle applicaties gebruiken Geist** als hoofdfont (regular weight 400 default).

Loading via Google Fonts:
```html
<link href="https://fonts.googleapis.com/css2?family=Geist:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

```css
font-family: var(--font-family);
/* = 'Geist', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', sans-serif */
```

### 2.2 Font sizes (rem-based, 16px = 1rem)

| Token | Waarde | Pixel | Gebruik |
|-------|--------|-------|---------|
| `--fs-xs` | 0.7rem | 11.2px | Badges, pills, meta-info, labels |
| `--fs-sm` | 0.875rem | 14px | Body, knoppen, inputs (default) |
| `--fs-md` | 1rem | 16px | Sub-titels, belangrijke labels |

### 2.3 Headings (Material Design schaal)

| Tag | Size | Weight | Letter-spacing | Gebruik |
|-----|------|--------|----------------|---------|
| `h1` | 1.75rem (28px) | 500 | -0.02em | Page hero |
| `h2` | 1.375rem (22px) | 500 | -0.015em | Section header |
| `h3` | 1.125rem (18px) | 500 | -0.01em | Card / sub-section |
| `h4` | 1rem (16px) | 500 | -0.01em | Component title |
| `h5` | 0.875rem (14px) | 500 | -0.01em | Inline header |
| `h6` | 0.75rem (12px) | 500 | 0.08em uppercase | Overline / eyebrow |

### 2.4 Tekst-hiërarchie (GA4-stijl)

| Token | Color | Contrast op wit | Gebruik |
|-------|-------|-----------------|---------|
| `--text-primary` | `#202124` | 17.9:1 | Hoofdtekst, koppen |
| `--text-default` | `#3C4043` | 11.4:1 | Body |
| `--text-secondary` | `#5F6368` | 6.07:1 | Secundair, labels |
| `--text-tertiary` | `#80868B` | 3.65:1 | Meta-info, subtiel |
| `--text-disabled` | `#9AA0A6` | 2.66:1 | Disabled (alléén disabled) |

**WCAG 2.1 AA minimum**: body 4.5:1 — dus `--text-tertiary` mag NIET voor body.

---

## 3. Kleuren

### 3.1 Accent (primair)
- `--accent: #1A73E8` (Google blue)
- `--accent-hover: #1557B0`
- `--accent-light: #E8F0FE`
- Gebruik: primaire knoppen, links, active states, focus-rings

### 3.2 Aanvullende accent (PostAds warm)
- `--oranje: #E87C2A`
- Gebruik: badges voor unread/notifications, brand-touch op specifieke spots

### 3.3 Status-kleuren

| Token | Kleur | Light variant | Gebruik |
|-------|-------|---------------|---------|
| `--groen` | `#7CB77B` | `--groen-light: #e8f5e8` | Success, klaar |
| `--geel` | `#E8B84A` | `--geel-light: #fdf6e3` | Warning, pending |
| `--rood` | `#D4633A` | `--rood-light: #fde8e2` | Error, danger |

### 3.4 Achtergronden
- `--app-bg: #F4F2F0` — pagina-achtergrond (warm cremé)
- `--wit: #FFFFFF` — kaarten, modals, list-rows, sidebar
- `--surface-alt: #F4F2F0` — alternerende rijen, list-headers

---

## 4. Borders & elevation

### 4.1 Standaard rand
**Altijd** `1px solid var(--divider-soft)` (`#E8EAED`).
Geen variaties — geen verschillende dikte, geen verschillende grijstinten.

```css
border: 1px solid var(--divider-soft);
```

### 4.2 Schaduwen
Default state: **GEEN schaduw**. Schaduw verschijnt op hover, modals, dropdowns.

| Token | Gebruik |
|-------|---------|
| `--shadow-sm` | Kaarten in hover |
| `--shadow` | Modals |
| `--shadow-lg` | Overlays, dropdowns |
| `--shadow-ga4` | Google-stijl micro-elevation |

### 4.3 Border-radius

| Token | Waarde | Gebruik |
|-------|--------|---------|
| `--radius-sm` | 4px | Knoppen, inputs, badges, kleine pills |
| `--radius` | 8px | Kaarten, panels, modals |
| `--radius-lg` | 12px | Grote modals (optioneel) |
| `50%` | n.v.t. | Avatars, ronde icoonknoppen |
| `999px` | n.v.t. | Status-pills (capsule-vorm) |

**Geen andere waarden** (2, 6, 9, 10px → ronden af naar 4 of 8).

---

## 5. Componenten

### 5.1 Knoppen

| Variant | Hoogte | Padding | Font | Radius |
|---------|--------|---------|------|--------|
| `.btn` (default) | 44px | 0 20px (sp-5) | 0.875rem (14px), 500 | 4px |
| `.btn-sm` | 40px | 0 16px (sp-4) | 0.85rem | 4px |
| `.btn-lg` | 48px | 0 24px (sp-6) | 0.95rem | 4px |
| Icon button | 32×32px | 0 | n.v.t. | 50% of 4px |

Varianten:
- `.btn-primary` — accent-blauw, voor neutrale primaire acties (Opslaan, Versturen)
- `.btn-add` — groen (`--groen-action` #16a34a), **verplicht voor alle knoppen die iets nieuws aanmaken** (Nieuwe offerte, +Project, +Taak, etc.). Bevat altijd `<span class="mi">add</span>` en het icoon staat in een halftransparant wit rondje
- `.btn-secondary` — wit met accent-border (Annuleren, secundair)
- `.btn-danger` — rood, voor destructieve acties (Verwijderen)
- `.btn-ghost` — transparant, voor zwakke acties (Sluiten)

Regel: **groen = nieuw aanmaken, blauw = uitvoeren/opslaan**. Apps moeten dit onderscheid hanteren zodat gebruikers in één oogopslag zien wat een actie doet.

### 5.2 Inputs

| Eigenschap | Waarde |
|------------|--------|
| Hoogte | 44px |
| Padding | 0 12px (sp-3) |
| Font-size | 0.875rem (14px) |
| Border | 1px solid `--divider-soft` |
| Radius | 4px |
| Focus | border `--accent` + box-shadow 0 0 0 3px rgba(26,115,232,.15) |
| Placeholder color | `--text-tertiary` |

### 5.3 Tabs (cockpit-stijl)

- Container: `display:flex; border-bottom:2px solid var(--divider-soft)`
- Tab: padding `sp-3 sp-5`, font 0.9rem weight 500
- Active: color `--accent`, border-bottom-color `--accent`, weight 600
- Hover: color `--text-primary`, bg subtiele cremé tint

### 5.4 Cards

```css
.card {
  background: var(--wit);
  border: 1px solid var(--divider-soft);
  border-radius: var(--radius);
}
.card:hover { box-shadow: var(--shadow); }
.card-padded { padding: var(--sp-5); }
.card-header { padding: var(--sp-4) var(--sp-5); border-bottom: 1px solid var(--divider-soft); }
.card-body { padding: var(--sp-5); }
```

### 5.5 Modals

- Container: bg wit, `--shadow-lg`, `--radius`, max 90vh
- Header: padding `sp-4 sp-5`, border-bottom `--divider-soft`
- Body: padding `sp-5`
- Footer: padding `sp-3 sp-5`, border-top `--divider-soft`
- **Geen** backdrop-blur of glass-look

### 5.6 Sidebar (Jugoo CMS-stijl)

- Breedte: 240px
- Background: wit
- Nav items: full-width, padding `10px 20px`, `border-left: 3px solid transparent`

| Eigenschap | Inactief | Hover / Actief |
|------------|----------|----------------|
| Font-size | `0.9rem` (≈14.4px) | idem |
| Font-weight | 400 | 600 |
| Tekstkleur | `--sidebar-text` (`#212832`) | `--sidebar-text-active` (`#0061f2`) |
| Icon-kleur | `--sidebar-icon` (`#1f2933`) | `--sidebar-icon-active` (`#0061f2`) |
| Background | transparant | `--sidebar-active` (`#E8F0FE`) |
| Border-left | transparant | 3px `--sidebar-text-active` |

- Section labels: 10–11px, uppercase, letter-spacing 0.1em, top-border tussen secties
- De sidebar gebruikt **niet** `--accent` — Jugoo-blauw (`#0061f2`) is gereserveerd voor navigatie-context en blijft consistent over apps

### 5.7 Top-bar (page header)

- Sticky aan top, witte bg, 1px `--divider-soft` border-bottom
- Min-height: 60px
- Padding: 32px (sp-8) horizontaal, sp-3 (12px) verticaal
- Bevat: page title + subtitel + acties (rechts)

### 5.8 Iconen

- Material Symbols Rounded
- `wght: 200` (extra light — strakke, lichte lijnvoering)
- Default size: 18-20px voor inline, 24px voor headers
- Opacity 0.85 default, 1.0 op hover/active
- Embed: `<span class="mi">naam</span>` — `.mi` zet font + variation-settings

Canonieke iconenset (zie styleguide.html voor visuele preview):

| Categorie | Iconen |
|-----------|--------|
| Acties | `add`, `add_circle`, `edit`, `edit_square`, `delete`, `save`, `send`, `close`, `check`, `content_copy`, `undo`, `restart_alt`, `swap_horiz`, `autorenew` |
| Navigatie | `arrow_back`, `chevron_left`, `keyboard_arrow_down`, `expand_less`, `unfold_more`, `more_vert`, `open_in_new`, `logout` |
| Status | `check_circle`, `pending`, `schedule`, `info`, `lock`, `lock_open`, `visibility`, `stop`, `star` |
| Bedrijfsobjecten | `dashboard`, `person`, `person_add`, `person_off`, `group`, `work`, `description`, `receipt_long`, `payment`, `task_alt`, `checklist`, `label`, `folder`, `folder_open`, `beach_access`, `calendar_month`, `calendar_today`, `link`, `local_shipping`, `rocket_launch` |
| Communicatie | `mail`, `phone`, `chat`, `chat_bubble`, `forum`, `add_comment`, `notes`, `notifications` |
| Bestand &amp; media | `upload_file`, `upload`, `download`, `attach_file`, `print`, `add_a_photo`, `format_list_bulleted`, `format_list_numbered` |
| Systeem | `settings`, `palette`, `mood`, `repeat` |

Vuistregel: nieuwe iconen eerst toevoegen aan deze lijst (en in styleguide.html plaatsen) voor je ze in een app gebruikt — zo blijft de set consistent.

---

## 6. Spacing (4px-grid)

| Token | Waarde |
|-------|--------|
| `--sp-1` | 4px |
| `--sp-2` | 8px |
| `--sp-3` | 12px |
| `--sp-4` | 16px |
| `--sp-5` | 20px |
| `--sp-6` | 24px |
| `--sp-8` | 32px |
| `--sp-10` | 40px |
| `--sp-12` | 48px |

**Geen andere waarden** (5, 7, 11, 18 → afronden).

Standaard layout-spacing:
- Card padding intern: `sp-5` (20px)
- Lijst-rij padding: `sp-3 sp-4` (12px 16px)
- Tussen secties: `sp-6` of `sp-8`
- Form-row gap: `sp-4`
- Inline elementen (label + value): `sp-2`

---

## 7. Taal & toon (UI copy)

- Alle UI-tekst in het **Nederlands**. Toon: zakelijk maar menselijk.
- Labels: kort, imperatief ("Opslaan", "Verwijderen")
- Headers: Title Case ("Nieuw bedrijf"), inline: lowercase
- Pill-tekst: hoofdletter-eerste-letter ("Aangevraagd", niet "AANGEVRAAGD")
- Datum: `dd-mm-jjjj` of `12 juni 2026`
- Getallen met komma: `€1.295,00`, `1,5u`
- Leeg veld: `—` (em-dash), niet "0u" of leeg

Status-pill kleurkoppeling (consistent in alle apps):
- concept / aangevraagd → amber
- verzonden / in behandeling → blauw
- geaccepteerd / goedgekeurd / klaar → groen
- afgewezen / vervallen → rood
- gefactureerd / betaald → groen

---

## 8. Implementatie per app

### 8.1 Nieuwe app starten

1. Symlink (of copy) de 3 CSS files naar `<app>/styles/`:
   ```bash
   ln -s ~/design-system/v2/tokens.css     <app>/styles/tokens.css
   ln -s ~/design-system/v2/base.css       <app>/styles/base.css
   ln -s ~/design-system/v2/components.css <app>/styles/components.css
   ```

2. In HTML `<head>`:
   ```html
   <link href="https://fonts.googleapis.com/css2?family=Geist:wght@300;400;500;600;700&display=swap" rel="stylesheet">
   <link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Rounded:opsz,wght,FILL@20..48,100..700,0..1&display=swap" rel="stylesheet">
   <link rel="stylesheet" href="styles/tokens.css">
   <link rel="stylesheet" href="styles/base.css">
   <link rel="stylesheet" href="styles/components.css">
   ```

3. Bouw componenten met de tokens — geen hardcoded waarden.

### 8.2 Bestaande app migreren

Zie `MIGRATION.md` voor stappenplan (v1 → v2).

### 8.3 Wijzigingen aan design system

1. Wijzig **eerst** in `~/design-system/v2/`
2. Push naar GitHub
3. Op live server: `cd ~/design-system && git pull`
4. Apps gebruiken de bijgewerkte tokens automatisch bij volgende pageload

### 8.4 Niet doen

- ❌ Eigen tokens.css per app — gebruik shared
- ❌ Inline `style="font-size:13px"` — gebruik class met `var(--fs-sm)`
- ❌ Ad-hoc kleurkeuze — alle kleuren staan in tokens.css
- ❌ Mengsels van fonts — **Geist overal**
- ❌ Verschillende border-thickness — altijd 1px

---

## 9. Apps die dit systeem volgen

| App | Versie | Status |
|-----|--------|--------|
| MijnCRM (Jugoo CRM) | v2 | Migrated ✓ |
| Jugoo Dash | v2 | Native ✓ (referentie) |
| Lan2 | n.v.t. | Next.js — vereist npm-package aanpak |
| Attentiecoach | v2 | Planned |

---

## 10. Versiebeheer

- `v1/` — legacy MijnCRM tokens (glass-look, rood-oranje accent)
- `v2/` — huidige standaard (Jugoo/GA4-stijl, Geist, Google-blauw)
- Versie bumps: alleen breaking changes (kleurschema, font-family, etc.)
- Tussentijdse wijzigingen (waarde-tweaks) blijven binnen dezelfde versie

## Updates

- **2026-06-23** — `.card` is platgeslagen: alleen subtiele border, géén
  schaduw. Matcht de MijnCRM tabel-rij-stijl die Coen als standaard wil
  doortrekken naar alle apps. Hover geeft border-emphasis (border-color
  van --border-subtle → --border-strong), geen elevation. Apps die wél
  schaduw willen kunnen `.card-elevated` opt-in gebruiken (alleen voor
  modals, drop-overlays, échte hover-uit-de-laag situaties).
- **2026-06-23** — ~30 missende tokens toegevoegd aan `tokens.css`
  (--border-subtle/strong, --surface/-subtle/-sunken, --text-inverse,
  --h-btn-*, --radius-btn/card, --bg-/fg-success/warning/info/danger,
  --focus-ring, --lh-tight/normal, --glass-*). Hiermee zijn `.btn`,
  `.card`, `.alert`, `.badge`, `.pill` en `.surface-glass` zelfstandig
  bruikbaar.
