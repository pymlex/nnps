# Overview

Repository for a diploma on neural interatomic potentials for condensed Al–Ni.

## Goal

Build a **local** potential $U(\{R_i\},\{t_i\})$ that improves on classical EAM and on a published reference on properties that matter for alloys: formation thermodynamics, elasticity, transfer to other packings and defects. The claim must survive comparison with experiment and with Mishin 2009 without putting experimental $a$, $\Delta H$, $B$ as separate loss terms.

## What already exists

| model | role |
|---|---|
| Mishin 2009 EAM | literature reference |
| own Morse–FS EAM | classical baseline fitted to experiment |
| CHGNet | universal neural baseline |
| Rose residual hybrid | negative control: continuous EOS fit, not a scientific advance |

## What is forbidden as the main claim

- Fitting Rose or three experimental scalars with a neural residual and calling that novelty
- Claiming “attention on atoms” without a measurable gain on a fixed Al–Ni protocol
- Ranking only Matbench Discovery hull metrics while reporting alloy elasticity

## Decision flow

1. Pick one primary track in `docs/05-research-directions.md`
2. Open a file in `hypotheses/`
3. After 5090 access: DFT or active-learning data, then train
4. Freeze metrics before architecture changes
