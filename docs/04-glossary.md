# Glossary

**Interatomic potential** $U(\{R_i\},\{t_i\})$ — map from nuclear positions and types to potential energy.

**PES** — potential energy surface, the same $U$ as a function of coordinates.

**Force** $F_i=-\nabla_i U$.

**Energy per atom** $u=U/N$.

**Cohesive energy** $E_{\mathrm{coh}}=-u$ relative to isolated atoms in the potential’s convention.

**Formation enthalpy**

$$
\Delta H = u - \sum_k x_k u_k^{\mathrm{pure}}.
$$

**Chemical potential** $\mu_k=\partial G/\partial N_k$ — thermodynamic derivative. Not the interatomic potential $U$.

**Equation of state $E(a)$** — energy along isotropic lattice scaling.

**Bulk modulus**

$$
B = V\frac{\partial^2 u}{\partial V^2}\Big|_{V_0}.
$$

**Rose universal binding curve** — analytic metallic EOS with parameters $a_0$, $E_{\mathrm{coh}}$, $B$. Useful teacher for continuous $E(a)$. Using it as the only teacher is not a scientific advance if those parameters are experimental.

**EAM** — embedded-atom method with embedding $F$, density $\rho$, pair $\varphi$.

**Finnis–Sinclair** — $F=-\sqrt{\bar\rho}$.

**Cross term $\varphi_{\mathrm{NiAl}}$** — unlike-pair interaction in a binary EAM.

**Mishin 2009** — published tabulated Ni–Al EAM from NIST.

**Cutoff** — distance beyond which interactions are zero.

**MLIP** — machine-learning interatomic potential.

**uMLIP / foundation model** — MLIP pretrained across many chemistries.

**Message passing** — recursive update of atom features from neighbours on a graph.

**Equivariance** — features transform consistently under rotations and translations.

**Attention** — learned weighted interaction among neighbours or tokens. In TorchMD-Net the weights depend on distance features.

**Atomic residual** $\varepsilon_\theta(\mathcal{N}_i)$ — learned correction added to a classical baseline.

**Hybrid potential** $U=U_{\mathrm{class}}+\sum_i\varepsilon_\theta(\mathcal{N}_i)$.

**PES softening** — systematic underestimation of curvature and high-energy features by models trained near equilibrium.

**Virial** — stress-related tensor entering elasticity-aware training.

**Hold-out packing** — structure of the same composition excluded from training.

**Emergent property** — quantity obtained by minimising a trained $U$, not inserted as a scalar loss term.

**Active learning** — iterative loop of simulation, uncertainty query, DFT labelling, retrain.

**Conservative model** — forces obtained as $-\nabla U$.
