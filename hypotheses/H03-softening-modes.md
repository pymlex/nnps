# H03 — Modal PES softening and Hessian distillation

Status: proposed  
Track: C

## Claim

Softening of foundation MLIPs on Al–Ni is mode-dependent, not a single scalar. Distilling Hessian-vector products into an EAM-anchored residual corrects phonon and modulus errors with tens of reference Hessians.

## Method

Generalised eigenproblem between teacher and reference dynamical matrices. Hybrid residual trained with energy, force, stress and Hutchinson-style Hessian matching.

## Data needs

Experimental phonons for Ni, Al, NiAl, Ni₃Al. Optional 20–50 DFT Hessians.

## Decision

Backup framed around the softening literature.
