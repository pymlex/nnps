# H01 — Attention residual on EAM for Al–Ni

Status: proposed  
Track: A

## Claim

A distance-aware attention residual on a frozen EAM backbone, trained on DFT $E$, $F$, $\Xi$ for Al–Ni, improves the joint experimental error in $\Delta H$ and $B$ and reduces softening on at least one defect probe relative to:

- pure EAM
- Mishin 2009
- MLP residual with the same data
- attention-only MLIP without EAM
- foundation fine-tune without classical backbone

## Method

$$
U = U_{\mathrm{EAM}} + \sum_i \varepsilon_\theta^{\mathrm{attn}}(\mathcal{N}_i)
$$

Conservative forces. Optional short-range empirical wall. Ablations mandatory.

## Data needs

DFT labels on strained cells, mixed supercells, one defect family. Active learning after first specialist. RTX 5090 for training.

## Metrics

Emergent $a$, $\Delta H$, $B$. Hold-out packing gaps. Softening probe versus DFT. NVE drift. Pareto of $\mathrm{MAE}(\Delta H)$ versus $\mathrm{MAE}(B)$.

## Decision

Waiting for supervisor-facing feedback: accept Track A, or switch to B/C.
