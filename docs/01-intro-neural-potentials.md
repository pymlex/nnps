# Introduction to neural interatomic potentials

## Classical statement

In the Born–Oppenheimer picture the nuclei move on a potential energy surface

$$
U = U(\{R_i\},\{t_i\}),
$$

where $R_i$ are nuclear coordinates and $t_i$ are chemical types. Forces are

$$
F_i = -\nabla_i U.
$$

A useful potential must be **conservative** if forces come from $-\nabla U$, must respect permutation of identical atoms, and should respect Euclidean symmetries. For crystals one also needs a stable equation of state $E(a)$ with controlled curvature

$$
B = V\frac{\partial^2 u}{\partial V^2}\Big|_{V_0},
\qquad u = U/N.
$$

## Classical many-body forms

Embedded-atom method:

$$
U = \sum_i F_{t_i}(\bar\rho_i) + \frac12\sum_{i\neq j}\varphi_{t_i t_j}(r_{ij}),
\qquad
\bar\rho_i = \sum_{j\neq i}\rho_{t_j}(r_{ij}).
$$

Finnis–Sinclair takes $F=-\sqrt{\bar\rho}$. Binary Al–Ni needs pure functions for Al and Ni plus the cross pair $\varphi_{\mathrm{NiAl}}$. Gauge freedom means pair curves from different EAMs must not be overlaid as if they were unique observables.

## Neural potentials

A neural potential replaces hand-designed $F,\rho,\varphi$ by a learned map from local environments to atomic energies

$$
U = \sum_i \varepsilon_\theta(\mathcal{N}_i).
$$

Families in active use:

| family | idea | examples |
|---|---|---|
| descriptor + regression | fixed SOAP/ACS F + linear or GP | GAP |
| moment tensors | polynomial many-body basis | MTP |
| invariant message passing | scalar graph nets | SchNet, DeepMD-style |
| equivariant tensor nets | irreps / spherical features | NequIP, Allegro, MACE |
| attention / transformers | distance-aware multi-head attention | TorchMD-Net ET |
| foundation / universal | pretrained on large DFT corpora | CHGNet, MACE-MP, MatterSim, SevenNet, ORB, GRACE |

## What the field does now

1. **Foundation models.** Pretrain on Materials Project trajectories and larger corpora. Benchmark on Matbench Discovery for crystal stability. This ranks formation-energy hull logic, not alloy MD fidelity.
2. **Specialist fine-tunes.** Take a foundation checkpoint and adapt it to one chemistry with a small DFT set. Softening and catastrophic forgetting are the main failure modes.
3. **Active learning.** Iterate MD under the current potential, query DFT on uncertain or high-force frames, retrain.
4. **Hybrid physics + ML.** Keep ZBL or EAM at short range or as a baseline, train a residual for the rest. Used for robustness in long MD and for phase diagrams under pressure.
5. **Property multi-tasking.** Train on energy, forces and virial together. Elastic constants and phonons expose curvature errors that energy MAE hides.

## Blind spots that matter for a diploma

**PES softening.** Universal models underpredict energies and forces away from near-equilibrium training basins. Barriers, defects, surfaces and phonons become too soft. Reported for M3GNet, CHGNet and MACE-MP-style models.

**Elasticity versus formation enthalpy.** Graph models often fit $\Delta H$ more easily than bulk modulus. Second derivatives amplify representation and loss design choices.

**Smoothness artifacts.** Attention and hard neighbor cutoffs can inject kinks into $E(a)$ and $F(r)$. Standard E/F RMSE can look fine while MD diverges.

**Conservative versus non-conservative forces.** Some fast models predict forces directly. Energy conservation in long MD then fails.

**Long-range electrostatics.** Metals screen, oxides do not. Wrong inductive bias hurts transfer across chemistries.

**meV-level alloy thermodynamics.** Relative stabilities of competing Al–Ni packings sit near chemical accuracy. Foundation MAE of tens of meV/atom is not enough without specialist data.

## Attention is already used

Distance-aware equivariant transformers exist. Novelty is not “add attention”. Novelty is a **measurable gain** of an attention mechanism inside a fixed Al–Ni protocol against strong baselines, with an explanation of *which* physical residual it captures.
