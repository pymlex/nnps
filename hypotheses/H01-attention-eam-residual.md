# H01 — Target-oriented attention residual on EAM

Status: proposed  
Track: A

## Claim

A distance-aware attention residual on a frozen EAM backbone, with a Bayesian last layer and an OOD gate back to EAM, trained by target-oriented active learning on DFT $E$, $F$, $\Xi$, predicts the γ–γ′ solvus and L1₂ planar-defect energies with calibrated uncertainty using fewer DFT labels than force-uncertainty AL, and beats Mishin, pure EAM, MLP residual and attention-only MLIP on the joint diploma protocol.

## Architecture

$$
U = U_{\mathrm{EAM}} + \sum_i g(\gamma_i)\,\mathbf w^\top\boldsymbol\varphi_\theta(\mathbf h_i)
$$

Conservative forces. Smooth cutoff in attention. Gate returns to EAM out of distribution.

## Data needs

Teacher-MLIP AL loop first. Then spin-polarised PBE on strained cells, mixed supercells, planar-defect cells. RTX 5090 for the network. DFT is the bottleneck.

## Metrics

- $\operatorname{Var}$ of solvus temperature and APB/SISF/CSF versus number of oracle calls
- emergent $a$, $\Delta H$, $B$ for Al, Ni, NiAl, Ni₃Al
- coverage of experiment by $\pm 2\sqrt{\operatorname{Var}Q}$
- OOD rollback to EAM
- ablations: no residual, MLP residual, attention residual, no gate, no Bayesian layer

## Decision

Waiting for feedback.
