# Discipline Prior: Metals / Metallurgy / Acta-class experimental materials

Use this playbook when **any** of the following is true:

- `target_name` matches a high-impact experimental materials venue
  (case-insensitive examples: `acta materialia`, `scripta materialia`,
  `materialia`, `acta mater`, names containing `metallurg`), **or**
- `special_requirements` mentions metals, metallurgy, alloy, or
  processing–structure–property (PSP), **or**
- the user draft / materials clearly describe experimental alloy processing,
  microstructure, and mechanical (or physical) properties.

This file is a **writing and research checklist**, not a substitute for official
author guidelines. **Never invent** page limits, highlight character caps, open
fees, or template versions — open `official_urls` and record facts in
`target_journal_research.md` / `research_dossier.md`.

Note: config field `materials_dir` means **user source-materials folder**, not
“materials science.” Do not reinterpret it.

## Must produce

1. `paper_rewriting_output/target_journal_research.md` via
   `references/target-journal-research.md` when `target_name` is set.
2. Venue-true exemplars in `exemplar_learning_dossier.md` (prefer papers from the
   named journal or the same editorial family).
3. `style_profile.md` calibrated with
   `references/journal-style-analysis.md` § “Hard experimental journals”.
4. Contribution typed as process / mechanism / structure–property / dataset —
   not forced into “new benchmark method” unless that is truly the paper.

## Processing–structure–property (PSP) spine

Write and review the paper as a chain:

```text
Composition / prior state
  → Processing path (thermo-mechanical, heat treatment, …)
    → Microstructure (phases, defects, length scales)
      → Properties (mechanical, thermal, functional, …)
        → Mechanism interpretation (bounded by evidence)
```

Every strong claim in Results/Discussion should land on at least one of:
processing condition, microstructural observation, property measurement.
`results_validation.md` rows should use result types such as
`microstructure`, `processing_effect`, `mechanical_property`,
`fracture_or_failure`, `mechanism`, `literature_comparison`.

## Experimental section — non-negotiable content (checklist)

Ensure Experimental / Materials and methods can answer:

- [ ] Alloy designation and **measured** composition (or clear statement of
      nominal + verification method).
- [ ] Processing / heat-treatment schedule (T–t path, atmosphere, cooling).
- [ ] Sample geometry and preparation for each characterization/test.
- [ ] Characterization tools with model/settings relevant to the claim
      (OM/SEM/EBSD/TEM/XRD/… as used).
- [ ] Property-test standards or explicit parameters (strain rate, temperature,
      environment).
- [ ] Replicates / statistics plan for quantitative figures.
- [ ] Enough detail that a skilled peer could attempt reproduction.

**Do not** merge Experimental into Results to satisfy a section-count budget.
If Experimental is thin, **add parameters**, do not delete the section.

## Figure–claim discipline

- Prefer multi-panel figures that separate condition series.
- Every contribution promise (C1…) needs ≥1 Results unit with a **Figure/Table**
  cell filled in `results_validation.md`.
- Captions state condition + what is shown; body text interprets without
  inventing unseen data.
- Missing image files or unreferenced floats are scientific risks — fix before
  calling the manuscript complete.

## Citation bank bias (materials)

When building `citation_support_bank.md`, prioritize channels and roles such as:

- foundational mechanism or constitutive papers,
- closest prior alloys / process routes,
- key characterization or test standards (as appropriate),
- recent Acta-class or field-leading experimental reports,
- honest negative or limit-setting literature.

Do **not** default to “SOTA dataset + ablation paper” lists unless the work is
computational materials / ML-for-materials with that structure.

## Discussion and claim boundary

- Separate **observation**, **correlation**, and **mechanism assertion**.
- Mechanism exclusivity requires evidence that rules out alternatives, or must
  be softened.
- State applicability window (alloy class, temperature, rate, length scale).
- List what was **not** measured (fatigue, corrosion, high-T, APT, …) under
  contribution claim boundary.

## Submission extras (Elsevier-family habits)

When building `submission_package/`:

- Highlights: usually 3–5 short bullets of **established results** (verify cap).
- Cover letter: journal fit from dossier + PSP contribution in plain English.
- Data availability / CRediT / conflict statements per official guide.
- Graphical abstract only if the venue requests it.

## Anti-patterns (reject in audit)

- ML Results spine (benchmark → ablation → FLOPs) on a pure experimental alloy
  paper.
- “SOTA” language without a defined comparison set.
- Mechanism story longer than the data support.
- Process meta-narrative (how the authors revised the draft) in the manuscript.
- Copying numbers, micrographs, or curves from exemplar papers
  (`deep-imitation` ban).

## Agent routing reminder

| Agent / stage | Extra duty under this prior |
|---|---|
| Scene Analyst | Venue requirements + Highlights / data policy from official pages |
| Exemplar Learner | Fill materials result-type rows, not only ablation/benchmark |
| SOTA Mapper | Gap as process window / mechanism / property trade-off, not only accuracy |
| Method reviewer | Use materials red flags in `agents/reviewer-method.md` |
| Writing stages | PSP chain in blueprints + rationale matrix Venue Norm column |
