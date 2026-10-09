# Research directions for the diploma

Primary track first. Each track is sized for about 60 pages. Rose residual fitting remains a negative control only.

Deepened after a dedicated research pass ([MLIP diploma novelty research](e9deecbe-cef9-4b5f-8c8c-8ee14cc0c715)). Paper years and numeric constants in that pass must be checked against primaries before the thesis text freezes.

## Field snapshot 2024–2026

Foundation MLIPs train on Materials Project, Alexandria, OMat24 and MPtrj families. Models in active use include MACE-MP, CHGNet, M3GNet, SevenNet, MatterSim, Orb, EquiformerV2, GRACE and related checkpoints. Matbench Discovery ranks hull stability, not meV alloy thermodynamics.

Documented blind spots:

- PES softening of forces, phonons and moduli after near-equilibrium pretraining
- Non-conservative force heads that break long MD
- Weak transfer of potential uncertainty onto phase boundaries and defect energies
- Elasticity versus formation-enthalpy tension inside limited functional classes
- Short-range repulsion holes fixed in practice by ZBL or EAM walls

Attention already exists in TorchMD-Net-class models. Hybrid EAM+NN already exists for Sn under pressure and in PINN-style parameterisation of analytic forms. Novelty must sit in what the hybrid **measures or proves**, not in the word hybrid.

---

## Track A — primary

### Target-oriented UQ hybrid for γ–γ′ and L1₂ planar defects

**Question.** What energy accuracy is necessary and sufficient to predict the γ–γ′ solvus and APB, SISF, CSF energies in Ni₃Al within a stated tolerance? Can that accuracy be reached with minimal DFT by acquiring configurations that maximise expected reduction of variance of the **target observable**, not of raw energy or force RMSE?

**Scale argument.** If coexistence satisfies $\Delta g(T^*)=0$, then

$$
\delta T^* \approx \frac{\delta\Delta h}{\Delta s}.
$$

With $\Delta s\sim 0.5\,k_B$ per atom one obtains roughly $20$ K per $1$ meV/atom. For a (111) planar defect in Ni₃Al, $1$ meV per interface atom is about $3$ mJ/m². Foundation MAE of several meV/atom is therefore not enough for the diploma observables.

**Architecture.**

$$
U(\mathbf R)
=
U_{\mathrm{EAM}}
+
\sum_i g(\gamma_i)\,
\mathbf w^\top \boldsymbol\varphi_\theta(\mathbf h_i).
$$

- $U_{\mathrm{EAM}}$ frozen Mishin or Morse–FS
- $\mathbf h_i$ from 2–3 layers of distance-aware attention with species-dependent biases and a cutoff placed so that $U$ stays smooth when neighbours enter the sphere
- Bayesian last layer $\mathbf w\sim\mathcal N(\boldsymbol\mu,\boldsymbol\Sigma)$ after features are trained
- extrapolation grade $\gamma_i$ with smooth gate $g(\gamma)$ that returns the model to pure EAM out of distribution
- forces strictly $-\nabla U$, including derivatives through the gate

**Target-oriented acquisition.** For an observable $Q$ with sensitivity $\mathbf g_Q=\partial Q/\partial\mathbf w$,

$$
\Delta\operatorname{Var}Q(x)
=
\frac{(\mathbf g_Q^\top\boldsymbol\Sigma\boldsymbol\psi)^2}{\sigma^2+\boldsymbol\psi^\top\boldsymbol\Sigma\boldsymbol\psi}.
$$

Candidates are chosen to reduce $\operatorname{Var}$ of solvus or defect energy, not only $\max\sigma_F$.

**What is new.** Foundation and specialist MLIPs optimise $E$/$F$ RMSE. Uncertainty-driven AL usually maximises force variance or D-optimality. Transfer of calibrated parameter uncertainty onto a metallic phase boundary and planar-defect energies, with an OOD gate back to EAM, is the claim. Closest neighbours: PINN for BOP parameters, FLARE/DP-GEN-style AL, EAM-R hybrids without target-oriented UQ.

**Protocol without DFT first.** Run the full AL loop against a frozen teacher MLIP. Compare target-oriented acquisition, max-$\gamma$ acquisition and random sampling on the curve “oracle calls versus $\operatorname{Var}Q$”. Replace the teacher by spin-polarised PBE DFT later.

**Evaluation versus experiment.** γ–γ′ boundary against CALPHAD and experiment, lattice misfit, planar-defect energy intervals from TEM literature, calibration of $\pm 2\sqrt{\operatorname{Var}Q}$ coverage.

**Evaluation versus Mishin.** Same observables plus decomposition into EAM contribution and residual. OOD rollback test: large $\gamma$ must recover EAM.

**Failure modes.** Underconfident Bayesian last layer. Force spikes if the gate is too sharp. Vibrational entropy comparable to configuration error. PBE systematics in Ni-rich $\Delta H$. Magnetic Ni in DFT.

**DFT.** Required for the final claim. About $10^3$–$3\cdot 10^3$ cells up to ~100 atoms is a working estimate. Pipeline debugging needs no DFT.

**Pages.** Theory of UQ transfer and acquisition, architecture, teacher AL, DFT AL, observables, calibration, limits.

---

## Track B — backup 1

### Pareto front of elasticity versus formation enthalpy across model classes

**Question.** Is the elasticity–thermochemistry compromise an intrinsic limitation of the EAM functional class in Al–Ni? What residual capacity collapses the front toward a single point?

**Analytic lever.** For cubic EAM the Cauchy pressure is tied to $F''$. For NiAl experiment gives $C_{12}-C_{44}$ of order $30$ GPa. Formation enthalpies depend on $F_s(\bar\rho_s)$ in mixed environments. That yields a constrained feasible set for simultaneous approximation inside pure EAM.

**Method.** Two loss families: elastic paths and $C_{ij}$; formation and defect energetics. Build Pareto fronts for EAM, pair residual, three-body residual, attention residual, full MLIP. Place foundation checkpoints as points in the same plane. Hypervolume versus capacity is the headline plot.

**What is new.** Not another scalar fit. An answer to **why** classical models sit where they sit, and how much neural capacity buys on a fixed Al–Ni protocol.

**DFT.** Optional. Experiment plus a teacher MLIP already support the front. A small DFT set strengthens it.

---

## Track C — backup 2

### Modal decomposition of PES softening and Hessian distillation into the hybrid

**Question.** Is softening a scalar factor, or does it depend on mode character, mixed Ni–Al motion and transversality? Can a few reference Hessians plus an EAM anchor correct it?

**Method.** Generalised eigenproblem between teacher and reference dynamical matrices. Distill Hessian-vector products into the hybrid residual. Compare phonon branches and $C_{ij}(T)$ against experiment and Mishin.

**What is new relative to scalar fine-tuning papers and Hessian distillation into generic MLIPs.** Modal structure of the error plus an EAM asymptotic wall.

**DFT.** Small: tens of DFPT or finite-displacement Hessians.

---

## Track D — chapter inside A

### Structural OOD: left-out packings and defects

Train on fcc, bcc, B2, L1₂ distortions. Test on D0₁₁, D5₁₃ and related packings, dislocation cores, γ–γ′ interfaces. Measure hull-distance sign errors and the gain from the OOD gate versus a pure MLIP of matched capacity.

---

## Track E — reject as main claim

Rose EOS residual or experimental $a$, $\Delta H$, $B$ as separate loss terms. Documented in `docs/06-negative-controls.md`.

---

## Optional later extensions

- Latent Ewald versus local cutoff for meV ordering hierarchy in Ni–Al. Likely a null or high-risk study.
- Conservative EAM+residual plus a measured non-conservative patch, scored on vacancy diffusion and melting coexistence.
- Multi-fidelity PBE / r2SCAN token after DFT of both levels exists.

## Recommendation

Take **A**, with **D** as a transfer chapter and a short conservative-force chapter. Keep **B** if DFT is late. Keep **C** if the softening literature becomes the supervisor’s preferred frame.

Reply with `A`, `B`, `C`, or `A+B` after feedback.
