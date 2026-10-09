# Problem statement: condensed Al–Ni

## Scientific object

Two-component condensed Al–Ni. Primary phases for reporting:

- fcc Al
- fcc Ni
- equiatomic NiAl

Hold-out packings of composition NiAl test transfer. Ni₃Al may appear in literature comparisons but is not required in every plot.

## Observables

$$
\Delta H = u - \sum_k x_k u_k^{\mathrm{pure}}
$$

$$
B = V\frac{\partial^2 u}{\partial V^2}\Big|_{V_0}
$$

plus equilibrium lattice parameter $a_0$ and energy gaps between competing NiAl packings.

Experimental anchors used for **evaluation**, not as separate loss terms in the legitimate track:

| phase | $a$ / Å | $\Delta H$ / eV atom$^{-1}$ | $B$ / GPa |
|---|---:|---:|---:|
| Al | 4.050 | 0 | 79.0 |
| Ni | 3.520 | 0 | 180.4 |
| NiAl | 2.887 | −0.610 | 166 |

## Baselines

1. Mishin 2009 tabulated EAM from NIST
2. Own Morse–Finnis–Sinclair EAM fitted with differential evolution
3. CHGNet as a universal neural model
4. Rose residual hybrid as a negative control

## Diploma question

Does a **hybrid** architecture

$$
U = U_{\mathrm{EAM}} + \sum_i \varepsilon_\theta(\mathcal{N}_i)
$$

with an attention-based residual $\varepsilon_\theta$, trained on DFT energies, forces and virials for Al–Ni, improve the Pareto front of formation thermodynamics versus elasticity and transfer to unseen packings relative to:

- pure EAM,
- Mishin,
- a pure equivariant MLIP of similar budget,
- a foundation model fine-tune without classical backbone?

## Acceptance criteria

- Experimental $a$, $\Delta H$, $B$ are emergent checks, not scalar loss terms
- Forces come from $-\nabla U$
- Hold-out packings keep the correct energy ordering
- At least one kinetic or defect probe where softening usually appears
- Ablation: attention residual versus MLP residual versus no residual, fixed data
