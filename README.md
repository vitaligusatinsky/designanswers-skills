# DesignAnswers Skills

[![skills.sh](https://skills.sh/b/vitaligusatinsky/designanswers-skills)](https://skills.sh/vitaligusatinsky/designanswers-skills)

Public agent skills from DesignAnswers.

## Skills

- **[Grounded Analysis](skills/grounded-analysis/)** — analysis you can trust, of sessions, ideas, plans, performance, and decisions.
- **[Grid Composition Design](skills/grid-composition-design/)** — typography-led grid design and audit.

## Sync Status

Last verified sync: 2026-05-28.

The published `grid-composition-design` skill matches the active Codex skill at
`~/.codex/skills/grid-composition-design`.

## Grounded Analysis

Produce analysis you can trust — of meetings and mentoring sessions, ideas, plans, performance, and decisions. Grounds every claim in the source before asserting it, separates observation from judgment, labels confidence, and runs each sharp or critical claim through an adversarial self-check before it ships. Built to stop the most common analysis failure: an insight-shaped claim, stated as fact, that the evidence doesn't actually support. Keeps critiques sharp *and* cited.

Attribution: created by Vitali Gusatinsky / DesignAnswers.

Install with the Skills CLI:

```bash
npx skills add https://github.com/vitaligusatinsky/designanswers-skills --skill grounded-analysis
```

The skill includes:

- `SKILL.md` for the core method (frame → ground → observe-before-evaluate → confidence-label → adversarial gate → deliver) and the five domain adapters
- `agents/openai.yaml` for Codex-facing metadata

## Grid Composition Design

Typography-led grid design and audit guidance for editorial pages, reports, dashboards, visual essays, and other compositions where hierarchy, proportion, grid contracts, responsive rhythm, asides, and visual modules matter.

Attribution: created by Vitali Gusatinsky / DesignAnswers from the DesignAnswers Composer responsive-grid experiments.

Install with the Skills CLI:

```bash
npx skills add https://github.com/vitaligusatinsky/designanswers-skills --skill grid-composition-design
```

The skill includes:

- `SKILL.md` for the core workflow
- `references/` for audit and example-gallery notes
- `assets/examples/` for visual precedents from the Composer experiments
- `agents/openai.yaml` for Codex-facing metadata

## Attribution

Created by Vitali Gusatinsky / DesignAnswers.

Please preserve attribution when copying, adapting, or redistributing the skill.
