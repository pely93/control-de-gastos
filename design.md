# Design — Control de Gastos

A locked design system for this app. Every page redesign reads this file before
emitting code. Do not regenerate per page — extend or amend this file when the
system needs to grow.

## Genre
modern-minimal (fintech B2B: directorio de infraestructura de gasto/afiliación
para agencias, pymes y profesionales — Stripe/Linear register, confianza
financiera, cero decoración gratuita)

## Macrostructure family
- Hub pages (`index.astro`): **Bento Grid**, asimétrico — un tile grande
  "disponible" + dos tiles apiladas más pequeñas "próximamente". Nunca 3
  columnas iguales.
- Landing / conversion pages (`agencias.astro`): **Workbench** — el panel de
  producto (límites de gasto por cliente) es el artefacto central, no una
  ilustración genérica. El quiz es la segunda mitad del workbench.
- Content pages (`legal/*.astro`): **Long Document** — sin cabecera de
  marketing, solo el enlace de vuelta + prosa continua.

## Theme — custom (anclado en la marca existente)
Vibe: "confianza financiera, precisión técnica, cero ruido" — teal + navy ya
establecidos en el proyecto, ahora expresados como paleta OKLCH completa en
vez de hex sueltos repetidos.

- `--color-paper`     oklch(100% 0 0)
- `--color-paper-2`   oklch(98% 0.006 185)
- `--color-paper-3`   oklch(96% 0.008 185)
- `--color-ink`       oklch(23.6% 0.060 256.6)
- `--color-ink-2`     oklch(46% 0.020 256)
- `--color-ink-3`     oklch(62% 0.015 256)
- `--color-rule`      oklch(90% 0.012 220)
- `--color-rule-2`    oklch(94% 0.008 200)
- `--color-accent`        oklch(63.2% 0.110 183.1)
- `--color-accent-strong` oklch(56.1% 0.098 183.0)
- `--color-accent-soft`   oklch(94% 0.020 183)
- `--color-accent-ink`    oklch(100% 0 0)
- `--color-focus`     oklch(63% 0.140 183)
- `--color-warn`      oklch(75% 0.150 70)
- `--color-dark-surface` oklch(23.6% 0.060 256.6)
- `--color-dark-ink`     oklch(94% 0.010 200)
- `--color-dark-ink-2`   oklch(72% 0.020 220)
- `--color-dark-rule`    oklch(34% 0.030 250)

Axes: paper-band = **light** · display-style = **grotesk-sans** · accent-hue =
**chromatic-other (teal)**.

## Typography
- Display: **Space Grotesk**, weight 600–700, style normal, tracking -0.02em
- Body: **Switzer** (Fontshare), weight 400–500
- Mono/outlier: **JetBrains Mono**, weight 500 — wordmark accent + tabular
  data (percentages, limits) ONLY. Two slots max.
- Type scale anchor: `--text-display: clamp(2.75rem, 5vw + 1rem, 4.75rem)`
- Ratio: 1.25 (major third)

## Spacing
4-point named scale, values in `tokens.css`. Pages use named tokens
(`var(--space-md)`), never raw values.

## Motion
- Easings: `--ease-out: cubic-bezier(0.16, 1, 0.3, 1)`, `--ease-in: cubic-bezier(0.7, 0, 0.84, 0)`, `--ease-in-out: cubic-bezier(0.65, 0, 0.35, 1)`
- Reveal pattern: none — the page is composed, per modern-minimal voice
- Microinteractions: CTA hover-lift (1.5px) + button press (scale 0.98) +
  quiz step crossfade. Three primitives max, respected site-wide.
- Reduced-motion fallback: opacity-only, ≤150ms

## Microinteractions stance
- Silent success (quiz result reveal has no "done!" toast)
- Hover delay 800ms / focus delay 0ms on any tooltip
- Focus rings appear instantly, never animated in

## CTA voice
- Primary CTA: filled teal, pill shape (`--radius-pill`), imperative verb
  ("Ver directorio", "Solicitar auditoría")
- Secondary CTA: outlined ink, same pill shape
- Never two primary CTAs competing in the same fold

## Per-page allowances
- Hub + landing pages MAY use Tier-A CSS-art enrichment (none currently
  shipped; typography + real product panel carry the page).
- Content (legal) pages: typography only, no enrichment.

## What pages MUST share
- The wordmark: **"Control de Gastos"** (isotype "CG") — this is now the
  single source of truth; drop "GI" and "GastoInteligente" wherever found.
- The accent teal, used ≤5% of any viewport (buttons, active states, focus).
- Space Grotesk + Switzer + JetBrains Mono.
- CTA voice (pill shape, radius, padding rhythm).
- Nav: **N5 Floating pill** — detached, blur backdrop, wordmark + 2 links +
  CTA, consistent on every page including landing pages (fixes the
  agencias.astro custom-header drift).
- Footer: **Ft1 Mast-headed** — wordmark + tagline, compact link row
  (Agencias · Privacidad · Cookies · Aviso legal · Afiliación), affiliate
  disclosure + copyright beneath in muted type. Same footer everywhere —
  legal links must stay reachable from every route (RGPD).

## What pages MAY differ on
- Macrostructure within the page-type family described above.
- Hero archetype: index.astro is a Bento hero; agencias.astro is a Workbench
  hero (H2 Split diptych knobs: ratio 7/5, right side = proof column).

## Exports

### tokens.css
```css
:root {
  --color-paper:        oklch(100% 0 0);
  --color-paper-2:       oklch(98% 0.006 185);
  --color-paper-3:       oklch(96% 0.008 185);
  --color-ink:           oklch(23.6% 0.060 256.6);
  --color-ink-2:         oklch(46% 0.020 256);
  --color-ink-3:         oklch(62% 0.015 256);
  --color-rule:          oklch(90% 0.012 220);
  --color-rule-2:        oklch(94% 0.008 200);
  --color-accent:        oklch(63.2% 0.110 183.1);
  --color-accent-strong: oklch(56.1% 0.098 183.0);
  --color-accent-soft:   oklch(94% 0.020 183);
  --color-accent-ink:    oklch(100% 0 0);
  --color-focus:         oklch(63% 0.140 183);
  --color-warn:          oklch(75% 0.150 70);
  --color-dark-surface:  oklch(23.6% 0.060 256.6);
  --color-dark-ink:      oklch(94% 0.010 200);
  --color-dark-ink-2:    oklch(72% 0.020 220);
  --color-dark-rule:     oklch(34% 0.030 250);

  --font-display: "Space Grotesk", ui-sans-serif, system-ui, sans-serif;
  --font-body:    "Switzer", ui-sans-serif, system-ui, sans-serif;
  --font-outlier: "JetBrains Mono", ui-monospace, monospace;

  --space-3xs: 0.25rem;  --space-2xs: 0.5rem;  --space-xs: 0.75rem;
  --space-sm:  1rem;     --space-md:  1.5rem;  --space-lg: 2rem;
  --space-xl:  3rem;     --space-2xl: 4.5rem;  --space-3xl: 7rem;

  --text-xs: 0.75rem;   --text-sm: 0.875rem;  --text-md: 1.0625rem;
  --text-lg: 1.25rem;   --text-xl: 1.5rem;    --text-2xl: 1.875rem;
  --text-3xl: 2.25rem;
  --text-display-s: clamp(2.25rem, 4vw + 1rem, 3.25rem);
  --text-display:   clamp(2.75rem, 5vw + 1rem, 4.75rem);

  --ease-out: cubic-bezier(0.16, 1, 0.3, 1);
  --ease-in: cubic-bezier(0.7, 0, 0.84, 0);
  --ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);
  --dur-short: 160ms; --dur-med: 240ms; --dur-long: 400ms;

  --radius-card: 14px; --radius-pill: 999px; --radius-input: 10px; --radius-chip: 8px;
}
```

(Tailwind v4 `@theme`, DTCG `tokens.json`, and shadcn CSS variables are not
needed for this project — it ships Tailwind v4 via `@theme` directly in
`src/styles/global.css`, which mirrors the block above.)
