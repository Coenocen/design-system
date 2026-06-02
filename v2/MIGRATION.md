# Migratie v1 → v2

Gids om een bestaande app (MijnCRM) van design system v1 naar v2 over te zetten.

## Aanpak

1. Update de CSS-imports naar `~/design-system/v2/*`.
2. Voer find-and-replace uit op de classnames (zie tabel hieronder).
3. Vervang business-specifieke tokens door app-lokale definities.
4. Controleer dat body-achtergrond nu in de app staat (v2 base heeft geen gradient meer).
5. Test per schermgroep.

## Classname-mapping

| v1 | v2 | Opmerking |
|---|---|---|
| `.bp` | `.btn-primary` | |
| `.bg` | `.btn-secondary` | |
| `.bgr` | `.btn-ghost` | |
| `.btn-add` | `.btn-ghost` | Apart patroon samengevoegd |
| `.ib` | `.btn-icon` | |
| `.btn.sm` | `.btn-sm` | Modifier staat los |
| `.btn.md` | `.btn-md` | |
| `.btn.lg` | `.btn-lg` | |
| `.bdg` | `.badge` | |
| `.pill` | `.pill` | Ongewijzigd |
| `.pill-blue` | `.pill-info` | Semantisch hernoemd |
| `.pill-green` | `.pill-success` | |
| `.pill-amber` | `.pill-warning` | |
| `.pill-red` | `.pill-danger` | |
| `.pill-gray` | `.pill` | Default pill is grijs |
| `.fg` | `.field` | |
| `.fr` | `.field-row` | |
| `.ph` | `.page-header` | |
| `.nl` | `.nav-label` | |
| `.ni` | `.nav-item` | |
| `.ni.on` | `.nav-item.active` | Active-state hernoemd |
| `.glass` | `.surface-glass` | |
| `.card` | `.card` | Ongewijzigd |
| `.card-widget` | `.card` met `.card-body` padding | Gebruik de nieuwe card-structuur |
| `.toast` | `.toast` | Ongewijzigd |
| `.toast.success` | `.toast-success` | Modifier staat los |
| `.toast.error` | `.toast-danger` | Hernoemd |
| `.toast.info` | `.toast-info` | |

## Token-mapping

| v1 | v2 | Actie |
|---|---|---|
| `--ink` | `--text-primary` of `--ink` | Beide bestaan — gebruik semantic |
| `--ink2` | `--text-secondary` of `--ink-2` | |
| `--ink3` | `--text-muted` of `--ink-3` | |
| `--paper` | `--surface-subtle` of `--paper` | |
| `--paper2` | `--surface-sunken` of `--paper-2` | Hernoemd met koppelteken |
| `--line` | `--border-subtle` of `--line` | |
| `--accent`, `--accentd`, `--accentl`, `--accent100/300/500` | Ongewijzigd, behalve `--accentd` → `--accent-dark`, `--accentl` → `--accent-100` | |
| `--greenl`, `--amberl`, `--bluel`, `--dangerl` | `--green-100`, `--amber-100`, `--blue-100`, `--danger-100` | Koppelteken |
| `--c-dienst-*`, `--c-product-*`, `--c-inkoop-*` | **Weg uit design system** | Definieer lokaal in MijnCRM `:root` |
| `--grad-1..5` | **Weg uit design system** | Definieer lokaal; body-gradient is app-keuze |
| `--sidebar-bg/-border/-item-hover/-item-active`, `--radius-sidebar-item` | **Weg** | `.sidebar` in v2 gebruikt semantic tokens direct |
| `--sidebar-width` | Ongewijzigd | |
| `--font` | `--font` | Ongewijzigd |
| `--fs-xs/sm/md` | Ongewijzigd, plus `--fs-lg/xl/2xl` | |
| `--sp-1..6` | `--sp-1..8` | v2 heeft `--sp-7` (32px) en `--sp-8` (40px) erbij |
| `--radius`, `--radius-card/btn/input/badge/tag/pill/modal` | `--radius`, `--radius-md/lg/sm/pill` + aliassen | Aliassen voor oude namen bestaan nog |
| `--h-btn/-sm/-md/-lg`, `--h-input` | Ongewijzigd | |
| `--s1/s2/s3` | `--shadow-sm/md/lg` + `--shadow-xl` | Hernoemd |
| `--glass-bg/-blur/-border/-shadow` | Ongewijzigd | |
| `--badge-fs/px/py/fw`, `--tag-*`, `--pill-*` | Weg | Waarden zitten nu direct in de componentstijlen |

## App-specifieke tokens opnieuw definiëren

In MijnCRM `index.html` binnen een `<style>`-blok ná de v2-imports:

```css
:root {
  /* MijnCRM business-kleuren — niet in design system */
  --c-dienst-100:rgba(37,99,235,.05);
  --c-dienst-300:rgba(37,99,235,.2);
  --c-dienst-500:#2563eb;
  --c-dienst-600:#1d4ed8;
  --c-product-100:rgba(124,58,237,.05);
  --c-product-500:#7c3aed;
  --c-inkoop-100:rgba(5,150,105,.05);
  --c-inkoop-500:#059669;

  /* Zonsopgang-achtergrond — MijnCRM signature */
  --grad-1:#c87832;
  --grad-2:#d4896a;
  --grad-3:#e8b5a0;
  --grad-4:#8baed4;
  --grad-5:#7a4f2a;
}

@keyframes sunrise { /* ... uit v1/base.css kopiëren ... */ }

body {
  background: linear-gradient(
    160deg,
    var(--grad-1) 0%, var(--grad-2) 25%,
    var(--grad-3) 45%, var(--grad-4) 65%,
    var(--grad-5) 100%
  );
  background-attachment: fixed;
  animation: sunrise 3s ease-out forwards;
}
```

## Volgorde van werken

1. Voeg v2-imports toe (naast v1, nog niet vervangen).
2. Definieer de app-lokale tokens (business-kleuren + gradient).
3. Vervang één schermgroep tegelijk (begin met een rustig scherm zoals instellingen).
4. Zodra alle schermen over zijn: verwijder v1-imports.
5. Visuele regressie-check met de styleguide-screenshot of per pagina.
