# Research directions for the diploma

Ranked tracks. Primary track first. Each track is sized for ~60 pages with theory, related work, method, Al–Ni experiments, ablations and failure analysis.

## Field snapshot

Universal MLIPs are pretrained and ranked on crystal-stability discovery benchmarks. Specialist equivariant models dominate force accuracy when DFT data exist. Documented failure modes: PES softening, MD-breaking non-smoothness, short-range repulsion holes, and a Pareto tension between formation energies and elastic moduli. Attention already exists in TorchMD-Net-class models. Hybrid EAM+NN exists for Sn under pressure. The open niche for Al–Ni is a **specialist hybrid with attention residual**, trained on DFT forces and virials, evaluated on thermodynamics **and** elasticity **and** softening probes, against Mishin and a pure MLIP of matched budget.

---

## Track A — primary recommendation

### Attention residual on a frozen EAM backbone for Al–Ni

**Question.** Can a distance-aware attention residual $\varepsilon_\theta$, added to a classical EAM and trained on DFT $\{E,F,\Xi\}$, improve the joint error in $\Delta H$ and $B$ and reduce softening on defects relative to pure EAM, Mishin, MLP residual, and a pure attention MLIP without EAM?

**Architecture.**

$$
U = U_{\mathrm{EAM}} + \sum_i \varepsilon_\theta(\mathcal{N}_i)
$$

- $U_{\mathrm{EAM}}$ frozen Morse–FS or Mishin gauge-fixed baseline
- $\varepsilon_\theta$: equivariant Transformer block with distance-aware multi-head attention, gated to zero on pure-species environments if desired
- optional ZBL or hard short-range wall under both terms
- forces strictly $-\nabla U$

**What is new.** Not “attention exists”. The claim is the **interaction** of classical metallic inductive bias with attention residual on a binary alloy protocol where elasticity and formation heat are scored together, with hold-out packings and a softening probe. Closest prior art: EAM-R for Sn, TorchMD-Net for molecules, uMLIP fine-tunes without classical backbone.

**Data.** DFT energies, forces, virials on strained Al, Ni, NiAl cells, random alloy supercells, at least one defect class. Active learning after the first specialist. RTX 5090 is enough for the network. DFT is the bottleneck.

**Evaluation.** Emergent $a$, $\Delta H$, $B$ versus experiment. Gaps versus Mishin on hold-out packings. Vacancy or barrier versus DFT. Ablations: no residual, MLP residual, attention residual, attention-only MLIP, CHGNet or MACE fine-tune.

**Failure modes.** Residual fights EAM gauge. Attention introduces force spikes. Softening remains if high-energy DFT is missing. Experiment looks strong while DFT transfer fails.

**Why ~60 pages.** Symmetry and conservation theory, EAM review, attention residual derivation, DFT dataset construction, full ablation tables, MD stability, honest negative controls including the Rose hybrid.

**DFT required.** Yes.

---

## Track B — backup

### Softening-aware fine-tune of a foundation model on Al–Ni with curvature loss

**Question.** Does adding explicit curvature or barrier targets, plus replay against catastrophic forgetting, fix PES softening on Al–Ni better than vanilla fine-tuning?

**Method.** Start from CHGNet or MACE-MP-class checkpoint. Fine-tune with energy, forces, virial and a finite-difference or phonon/barrier term. Keep a replay buffer of general chemistries or use an EWC-style penalty.

**Novelty.** Softening papers show that a few high-energy points help. A full Al–Ni specialist study with elasticity + defect metrics and forgetting analysis is still thesis-sized and concrete.

**DFT required.** Yes, but fewer points than training from scratch.

---

## Track C — backup

### Multi-objective Pareto: formation enthalpy versus elasticity under one potential

**Question.** Where is the Pareto front of $\mathrm{MAE}(\Delta H)$ versus $\mathrm{MAE}(B)$ for EAM, hybrid residual, pure MACE-like specialist and foundation fine-tune on identical Al–Ni data?

**Method.** Fixed dataset. Sweep loss weights $(w_E,w_F,w_\Xi)$. Report fronts, not a single “winner” checkpoint. Optionally gradient-surgery style multi-task optimisation.

**Novelty.** Literature already hints that bulk modulus is harder than formation energy for graph models. A controlled binary-alloy Pareto with classical and neural models is a clear chapter-level contribution and supports Track A.

**DFT required.** Yes for the neural models. Classical EAM can sit on the same plot from existing fits.

---

## Track D — optional stretch

### Smoothness-constrained attention for metals

**Question.** Do temperature-controlled or otherwise smoothed attention kernels reduce bond-deformation artifacts and NVE drift on Al–Ni relative to vanilla multi-head attention at matched force RMSE?

**Method.** Implement BSCT-like bond scans and force-smoothness deviation as an in-the-loop metric. Compare attention variants inside Track A’s residual.

**Novelty.** Smoothness-guided architecture choice on a metallic alloy, not only on molecular testbeds.

**DFT required.** Same as Track A.

---

## Track E — reject as main claim

### Rose-curve residual or direct experimental scalar fitting

Already executed as a negative control. Matches experiment because the teacher encodes experiment. Keep in the thesis as a didactic failure mode.

---

## Suggested thesis spine if Track A is chosen

1. Interatomic potentials and alloy observables
2. Classical EAM for Al–Ni and Mishin reference
3. Neural and foundation MLIPs, attention, known blind spots
4. Hybrid attention residual method
5. DFT dataset and active learning
6. Results versus experiment, Mishin, pure MLIP, Rose negative control
7. Softening and smoothness probes
8. Limits and outlook

## Decision needed from you

Reply with `A`, `B`, `C`, or a mix such as `A+C`. Implementation starts after that choice, on the 5090 when available.
