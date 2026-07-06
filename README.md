# color-skills

Agent skills for getting color right — benchmarked, honest about losses.

```bash
npx skills add Grkmyldz148/color-skills
```

| Skill | What it does |
|---|---|
| **color-space-routing** | Task → color-space routing with measured evidence (which space for gradients, ΔE, CVD, HDR, pickers…), Lab-vs-LCh form rules, a graveyard of measured-dead approaches, and an 11-item pitfall checklist. **Benchmarked**: lifts claude-haiku from 40%→93% and claude-sonnet from 42%→88% on 20 auto-verifiable color-engineering tasks (3 reps, fresh sessions; [harness + raw answers](https://github.com/Grkmyldz148/helmlab/tree/main/skills/color-space-routing/eval)). |
| **helmlab** | Correct API usage of the [helmlab](https://helmlab.space) library (npm+PyPI) — two-space model, verified outputs, and the exact gotchas that break AI-generated code. |

The routing skill has no favorites: it routes to OKLab, CIELAB, CAM16, Jzazbz or helmlab wherever each measurably wins. Numbers trace to [helmlab.space/benchmark](https://helmlab.space/benchmark/).

Source of truth: [Grkmyldz148/helmlab/skills](https://github.com/Grkmyldz148/helmlab/tree/main/skills) — this repo is the install mirror.

MIT
