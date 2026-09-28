# Verified Design System v0.1

Applies to every Verified Solutions product UI: DiscoveryIQ, MusterOS, Aptora, KeepUp, NetGrova, CrownIQ, BuildOS.
Precedence: the work order's explicit instructions, then this file, then the agent's own judgment. If a screen needs something this file doesn't cover, stop and ask. Don't invent new tokens or components.

## 1. Setup (per repo)
- Copy `tokens.css` (section 6) into global CSS.
- Set `<html data-product="<product-key>">`. Keys: `discoveryiq`, `musteros`, `aptora`, `keepup`, `netgrova`, `crowniq`, `buildos`.
- Dark mode: `data-theme="dark"` on `<html>`.
- KeepUp mobile/field screens: add `data-mode="field"`.
- With Tailwind or shadcn/ui, map their theme variables to these tokens (`--primary` → `--accent`, `--destructive` → `--bad`, etc.). Never hardcode hex values in components.

## 2. Type
- Headings: IBM Plex Sans Condensed (600/700).
- UI and body text: IBM Plex Sans (400/500/600). Base 15px; field mode 17px.
- IDs, codes, hashes, SOC/CIP codes, UEI/CAGE, evidence labels: IBM Plex Mono.
- Numbers in tables: `font-variant-numeric: tabular-nums`, right-aligned.

## 3. Color rules
- `--accent` (product color) is only for: the primary button, active nav, focus ring, links and the product mark.
- Status always uses semantic tokens (`--ok`, `--warn`, `--bad`, `--info`) plus an icon plus a text label. Never color alone.
- All token pairs meet WCAG AA 4.5:1. Don't introduce new colors.

## 4. Evidence levels (shared across all products)
| Level | Meaning | MusterOS credential state |
|---|---|---|
| SYSTEM_VERIFIED | External system of record confirmed it | Verified |
| OWNER_CONFIRMED | A named, accountable person attested to it | Attested |
| REPORTED | Self-reported, not yet checked | Pending |
| DERIVED | Calculated from other evidence; inherits the weakest input | n/a |
| UNKNOWN | No evidence either way | Unverified |
| STALE | Evidence is past its freshness window | Expired |
| CONFLICTED | Sources disagree; a person must resolve it | Revoked / disputed |

Render these with the `EvidenceBadge` component only. Status pills (workflow state) and evidence badges (proof) are separate things and shouldn't be combined.

## 5. Core components (build once, reuse)
1. Button: primary, secondary, ghost, danger. One primary per screen. The label names the action.
2. Form field: label, input, hint. Error text says what went wrong and how to fix it.
3. StatusPill
4. StatTile
5. AppShell: side nav with an accent rail on the active item, plus a top bar with breadcrumb and the primary action.
6. Tabs
7. DataTable: mono uppercase headers, tabular numbers, horizontal scroll on small screens.
8. CredentialCard
9. AuditTimeline: append-only; each entry shows actor, time and chain hash.
10. Alert: warn, bad, info.
11. SyntheticDataBanner: **required** on any screen showing seeded or demo data. Can't be dismissed.
12. EmptyState: explains what fills the screen and offers one action.
13. ConfirmDialog: required for destructive actions; asks for a reason where it's audited.
14. Field mode: 48px targets, full-width critical buttons (KeepUp mobile).

Sizes: spacing scale 4, 8, 12, 16, 24, 32, 48. Radius 4px (badges), 6px (buttons and inputs), 10px (panels). Targets at least 40px (48px in field mode).

## 6. tokens.css
```css
@import url("https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Condensed:wght@500;600;700&family=IBM+Plex+Sans:wght@400;500;600&family=IBM+Plex+Mono:wght@400;500&display=swap");

:root {
  --font-display: "IBM Plex Sans Condensed", "Arial Narrow", sans-serif;
  --font-body: "IBM Plex Sans", system-ui, sans-serif;
  --font-mono: "IBM Plex Mono", ui-monospace, monospace;
  --navy: #0E2238;
  --bg: #F5F7F9; --surface: #FFFFFF; --surface-2: #EEF2F5;
  --border: #D9DFE6; --border-strong: #B8C2CD;
  --text: #16202B; --muted: #5A6776; --on-accent: #FFFFFF;
  --ok: #15803D; --ok-bg: #E7F5EC; --warn: #B45309; --warn-bg: #FDF1E1;
  --bad: #B91C1C; --bad-bg: #FBE9E9; --info: #1D4ED8; --info-bg: #E6EEFD;
  --p-discoveryiq: #4338CA; --p-musteros: #1D5FD1; --p-aptora: #0F766E;
  --p-keepup: #C2410C; --p-netgrova: #A16207; --p-crowniq: #BE185D; --p-buildos: #334155;
  --r-sm: 4px; --r-md: 6px; --r-lg: 10px; --target: 40px;
}
[data-theme="dark"] {
  color-scheme: dark;
  --bg: #0B131C; --surface: #121D29; --surface-2: #18263A;
  --border: #253444; --border-strong: #36485C;
  --text: #E6ECF2; --muted: #93A1B0; --on-accent: #0B131C;
  --ok: #4ADE80; --ok-bg: #0F2A1B; --warn: #FBBF24; --warn-bg: #2E2208;
  --bad: #F87171; --bad-bg: #321416; --info: #7AA7FF; --info-bg: #132544;
  --p-discoveryiq: #A5A6F8; --p-musteros: #7AAEFF; --p-aptora: #2DD4BF;
  --p-keepup: #FB923C; --p-netgrova: #E0B341; --p-crowniq: #F48BBF; --p-buildos: #A9B6C8;
}
[data-product="discoveryiq"] { --accent: var(--p-discoveryiq); }
[data-product="musteros"]    { --accent: var(--p-musteros); }
[data-product="aptora"]      { --accent: var(--p-aptora); }
[data-product="keepup"]      { --accent: var(--p-keepup); }
[data-product="netgrova"]    { --accent: var(--p-netgrova); }
[data-product="crowniq"]     { --accent: var(--p-crowniq); }
[data-product="buildos"]     { --accent: var(--p-buildos); }
[data-mode="field"] { font-size: 17px; --target: 48px; }
```

## 7. Never
Gradients, glassmorphism, emoji as icons, a new font per product, unlabeled synthetic data, status shown by color alone, or new components without ruling out an existing one.
