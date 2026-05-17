# PaperSpine

PaperSpine is a motivation-driven Codex skill for academic papers and paper-like writing tasks. It is designed as a research-writing learning system rather than a prose polisher: it first studies the target venue or task genre, learns from strong exemplars, confirms the controlling motivation, builds section-level blueprints, and only then rewrites or integrates the manuscript.

In short: PaperSpine helps a manuscript grow around its central spine: motivation, evidence, section logic, and revision accountability.

## What It Does

- Confirms the paper's controlling motivation before substantive writing.
- Researches target journals, conferences, or paper-like task genres.
- Learns rhetorical structure from strong exemplar papers or reports.
- Builds traceable artifacts such as `confirmed_motivation.md`, `style_profile.md`, `section_blueprints.md`, `rewrite_matrix.md`, and `logic_transfer_audit.md`.
- Preserves version-specific requirements through `special_requirements.md`.
- Guards LaTeX projects against broken citations, labels, figures, and environments.
- Audits revisions for shallow editing and addition-heavy rewrites.

## Install

Clone or copy this folder into your Codex skills directory:

```text
$CODEX_HOME/skills/paper-spine
```

Then invoke it by asking Codex to use `paper-spine` for a manuscript, report, or paper-like writing task.

```text
Use $paper-spine to diagnose and rewrite my manuscript for a target journal.
```

## Typical Workflow

1. Create `source_map.md` to classify the draft, data, figures, references, and exemplar sources.
2. Carry forward `special_requirements.md` when making numbered versions such as V8, V9, or V10.
3. Confirm the motivation in `confirmed_motivation.md`, or create `motivation_options.md` for user selection.
4. Research the target venue or task genre.
5. Learn from exemplar papers or reports.
6. Build the motivation thread, evidence bank, section blueprints, and rewrite matrix.
7. Rewrite from the blueprint, not by appending sentences to old paragraphs.
8. Run revision, logic-transfer, and LaTeX integrity audits.

## Scripts

All scripts use only the Python standard library.

```bash
python scripts/style_metrics.py path/to/paper.tex --markdown
python scripts/revision_audit.py original.tex revised.tex --markdown
python scripts/latex_guard.py main.tex --bib references.bib --markdown
```

## Repository Hygiene

This repository should contain only the reusable skill. Do not commit user manuscripts, generated paper versions, local `paper_rewriting_output/` folders, compiled PDFs, or temporary one-off generation scripts.

## Privacy And Integrity

The skill is designed to keep user data separate from exemplar papers. Exemplar papers may teach structure and rhetorical moves, but their scientific results must not be copied into the user's manuscript. The skill also forbids fabricating data, citations, metrics, p-values, or experimental claims.
