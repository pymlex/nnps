# Method landscape

## Classical

| method | notes for Al–Ni |
|---|---|
| EAM / Finnis–Sinclair | workhorse for metals |
| EAPOTc / potfit style | freeze pure metals, fit cross term |
| Mishin 2009 | published Ni–Al EAM reference |

## Specialist MLIPs

| method | core object |
|---|---|
| DeepMD | local embedding + deep net, force-heavy loss schedule |
| GAP / SOAP | Gaussian process on descriptors |
| MTP | moment tensor potentials |
| NequIP | E(3)-equivariant message passing |
| Allegro | local equivariant tensor products, scalable MD |
| MACE | higher-order equivariant messages |
| TorchMD-Net ET | distance-aware multi-head attention |

## Foundation / universal

CHGNet, M3GNet, MACE-MP family, MatterSim, SevenNet, ORB, GRACE and related checkpoints. Ranked on Matbench Discovery for stability classification. Softening off equilibrium is documented for several of them.

## Hybrid classical + neural

Documented patterns:

1. **Short-range empirical wall.** ZBL or similar repulsion under a learned body. Stops unphysical clustering in long MD.
2. **EAM baseline + positive residual.** Used for Sn phase sequence under pressure: EAM lower bound, neural correction constrained in sign.
3. **Residual on energies only.** Fragile for $B$ unless curvature or virial enters the loss.

## Losses that actually constrain physics

$$
\mathcal{L}
=
w_E\|E-\hat E\|^2
+
w_F\|F-\hat F\|^2
+
w_\Xi\|\Xi-\hat\Xi\|^2
+
\mathcal{R}_{\mathrm{smooth}}
$$

Virial $\Xi$ couples to stress and elasticity. Smoothness regularisers and bond-deformation probes catch attention kinks that RMSE misses.

## Evaluation protocol proposed for NNPS

1. Equilibrium $a$, $u$, $\Delta H$, $B$ for Al, Ni, NiAl
2. $E(a)$ scans and finite-difference modulus
3. Energy gaps for hold-out NiAl packings
4. Softening probe: vacancy, APB or migration barrier versus DFT or Mishin
5. Short NVE MD for energy drift if forces are derivatives
6. Ablations with frozen data split
