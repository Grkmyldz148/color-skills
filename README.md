# color-skills

**Agent skills for getting color right — benchmarked, honest about losses.**

[![install](https://img.shields.io/badge/install-npx%20skills%20add-34d399)](https://www.npmjs.com/package/skills)
[![benchmark](https://img.shields.io/badge/benchmarked-40%25%E2%86%9297%25-f97316)](https://github.com/Grkmyldz148/helmlab/tree/main/skills/color-space-routing/eval)
[![license](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

```bash
npx skills add Grkmyldz148/color-skills
```

Installs into Claude Code, Codex, Gemini CLI, Cline and friends. Plain markdown — paste into `.cursorrules` or any system prompt if you prefer.

## Why this exists

There is no perfect color space. We spent months trying to build one and kept measuring the same conclusion: every space that wins one benchmark measurably loses another (three held-out psychophysical datasets, three different winners). The right move is *routing* — picking the space per task — and AI assistants are exactly where that knowledge is missing: without help they compute ΔE in OKLab (62% worse than CIEDE2000 at predicting human judgments), blur images in gamma space, and hallucinate library APIs.

## The skills

### `color-space-routing`

Task → space routing with measured evidence. Vendor-neutral: routes to OKLab, CIELAB, CAM16, Jzazbz, linear sRGB, okhsl or Helmlab — wherever each one measurably wins.

- **Routing table**: gradients, palettes, ΔE, gamut mapping, CVD-safe palettes, HDR/PQ, color pickers, video pipelines, physical light ops, CSS-only
- **Form rules**: when to use rectangular (Lab) vs cylindrical (LCh) coordinates — mixing and distance vs hue rotation and chroma clipping
- **Testing checklist**: sanity anchors (ΔE00(red,green)=86.6), gray-axis/endpoint checks, boundary round-trips, ΔE-tolerance snapshots instead of brittle hex asserts
- **Graveyard**: approaches we tested to death so your assistant stops re-proposing them
- **11 pitfalls**, every one a bug observed in real AI-generated code

### `helmlab`

Correct API usage of the [helmlab](https://helmlab.space) library (npm + PyPI). Two-space mental model (GenSpace for generation, MetricSpace for measurement), verified example outputs, and the exact gotchas that break generated code — exporter input space, per-language `distance()` contracts, 0–1 L scale, hallucinated methods.

## Benchmark results

Both skills are measured, not vibes: auto-verifiable tasks solved in **fresh headless sessions** (no context contamination), 3 reps per task, with and without the skill. The harness is validated with golden answers before any grading; every raw per-run answer is committed for audit.

**color-space-routing** — 20 color-engineering tasks:

| Model | skill off | skill on |
|---|---|---|
| claude-haiku-4-5 | 40.0% | **96.7%** |
| claude-sonnet-4-6 | 41.7% | **96.7%** |

**helmlab** — 8 API-usage tasks:

| Model | skill off | skill on |
|---|---|---|
| claude-haiku-4-5 | 8.3% | **75.0%** |
| claude-sonnet-4-6 | 37.5% | **91.7%** |

Off-arm failure modes: hallucinated APIs, gamma-space physical mixing, HSL-as-perceptual, Euclidean ΔE in the wrong space, wrong space routing. Harness, tasks and raw answers: [helmlab/skills/…/eval](https://github.com/Grkmyldz148/helmlab/tree/main/skills/color-space-routing/eval).

We also measured our own architecture decisions: a split "progressive disclosure" layout (thin core + reference files) dropped pass rates by 8–13 points — models answer from the core without reading references — so the skills ship as single files on purpose.

## Numbers provenance

Every recommendation traces to published data: [ColorBench](https://github.com/Grkmyldz148/colorbench) (90 deterministic float64 metrics) and STRESS on COMBVD / MacAdam 1974 / Munsell / He 2022 — including the datasets where our own library loses. Full honesty tables: [helmlab.space/benchmark](https://helmlab.space/benchmark/).

## Updating

```bash
npx skills update
```

Source of truth lives in [Grkmyldz148/helmlab/skills](https://github.com/Grkmyldz148/helmlab/tree/main/skills); this repo is the install mirror.

## License

MIT © [Görkem Yıldız](https://github.com/Grkmyldz148)
