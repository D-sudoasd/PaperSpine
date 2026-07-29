# Scenario: Journal

Research journals as formal publication venues.

## Official Sources

Find and record:

- author guidelines,
- article types,
- word/page limits,
- abstract structure,
- figure/table rules,
- data availability policy,
- code/software availability policy,
- AI-use policy,
- LaTeX or Word template,
- cover letter expectations when relevant,
- Highlights / graphical abstract rules when the venue uses them.

When `target_name` is non-empty, also produce
`paper_rewriting_output/target_journal_research.md` from
`references/target-journal-research.md` (do not skip venue research).

## Example Learning

Use target-scene examples from the named journal when possible. Use field
examples from adjacent journals only as field logic, not venue logic.

Learn:

- how the Introduction narrows from field problem to specific gap,
- how Methods / Experimental justify design choices and enable reproduction,
- how Results order **primary evidence → comparison → mechanism/robustness →
  interpretation** (not a generic "metric dump"),
- how Discussion returns to the contribution, mechanism limits, and next work.

### Results ordering by paper type (pick the right default)

| Paper type | Prefer this Results order | Avoid as default spine |
|---|---|---|
| CS / ML methods | benchmark → ablation → generalization → efficiency | — |
| Experimental physical sciences (incl. **metals / materials**) | microstructure or process response → property response → mechanism / comparison to literature → limits | ablation / FLOPs / "SOTA leaderboard" as the main spine |
| Theory / modeling | model statement → validation vs data → parametric study → limits | claiming experiments you did not run |

If the user paper is experimental metals/materials (or `special_requirements`
mentions processing–structure–property / metallurgy / alloy), **do not** force
ML-style ablation subsections. Use process–structure–property (PSP) narrative.

## Hard experimental / materials journals (Acta-class habits)

Use when `target_name` matches high-impact experimental materials venues
(e.g. *Acta Materialia*, *Scripta Materialia*, *Materialia*) **or** when
`special_requirements` includes metals / metallurgy / PSP. Also read
`references/discipline-metals-acta.md`.

Typical expectations (always verify against official_urls):

- **Introduction:** short and gap-driven; end with clear contribution bullets
  that map to later figures.
- **Experimental / Materials and methods:** standalone section with enough
  composition, processing, characterization, and test parameters for
  reproduction. **Do not** merge this section into Results to "save sections."
- **Results:** figure-driven; every strong claim points at a figure or table.
- **Discussion:** mechanism and claim boundary — what the data do *not* prove.
- **Reproducibility:** heat-treatment windows, stoichiometry, sample count,
  equipment model, and statistics (n, error bars) when relevant.
- **Submission extras:** Highlights (often 3–5 short bullets), data availability,
  cover letter that states journal fit from `research_dossier.md`.

## Claim vs mechanism discipline

- Report what was measured before proposing a mechanism.
- Mechanism language must not outrun characterization resolution (e.g. do not
  claim atomic-scale cause from coarse SEM alone).
- Soften or cut claims listed under contribution `Claims to soften or avoid`.
