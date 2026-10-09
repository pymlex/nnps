# Negative controls

## Rose residual hybrid

Form:

$$
U = U_{\mathrm{EAM}} + \sum_i \varepsilon_\theta(\mathcal{N}_i)
$$

with $\varepsilon_\theta=0$ on pure Al and pure Ni, trained so that NiAl follows the Rose EOS whose parameters come from experiment.

Observed equilibrium for the hybrid:

| phase | $a$ / Å | $\Delta H$ / eV atom$^{-1}$ | $B$ / GPa |
|---|---:|---:|---:|
| Al | 4.0500 | 0 | 79.0 |
| Ni | 3.5200 | 0 | 180.4 |
| NiAl | 2.8868 | −0.6100 | 165.9 |

MAE versus experiment is near zero. This does **not** advance potentials. The teacher already contains $a_0$, depth and curvature. The network copies a simple analytic curve.

Keep this result in the thesis as proof that experimental tables can be matched without scientific novelty.

## Earlier Mishin-copy residual

Training a residual to match Mishin energies pointwise pulled NiAl lattice toward Mishin’s $2.832$ Å error and damaged $B$ through non-smooth $E(a)$. Lesson: teacher choice and curvature matter more than train RMSE alone.
