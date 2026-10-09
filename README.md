# NNPS

Neural network potentials for the condensed Al–Ni system. Diploma research lab: guides, hypotheses, experiment logs, and code.

## Layout

```text
docs/          theory, problem statement, method map, glossary, research tracks
hypotheses/    one file per hypothesis, status and decision
guides/        long-form educational notes in Russian
experiments/   run logs and metric tables
src/           code (to be added after track selection)
```

## Current baseline outside this repo

Classical Morse–Finnis–Sinclair EAM, Mishin 2009 tabulated EAM, CHGNet evaluation, and a Rose-residual hybrid live under a separate working folder. The Rose hybrid matches experimental $a$, $\Delta H$ and $B$ because the teacher already encodes them. It is documented here as a **negative control**, not as the diploma claim.

## License

GPL-3.0. Do not commit tokens, `.env`, or private keys.

## References

```bibtex
@misc{nnps2026,
  title  = {NNPS: neural network potentials for condensed Al--Ni},
  author = {pymlex},
  year   = {2026},
  url    = {https://github.com/pymlex/nnps},
  note   = {Diploma research repository}
}

@article{mishin2009,
  title   = {Development of an interatomic potential for the Ni-Al system},
  author  = {Pun, G. P. Purja and Mishin, Y.},
  journal = {Philosophical Magazine},
  year    = {2009}
}

@article{deng2023chgnet,
  title   = {CHGNet as a pretrained universal neural network potential for charge-informed atomistic modelling},
  author  = {Deng, Bowen and others},
  journal = {Nature Machine Intelligence},
  year    = {2023}
}

@article{batatia2022mace,
  title   = {MACE: Higher Order Equivariant Message Passing Neural Networks for Fast and Accurate Force Fields},
  author  = {Batatia, Ilyes and others},
  year    = {2022}
}

@article{tholke2022torchmdnet,
  title   = {TorchMD-NET: Equivariant Transformers for Neural Network based Molecular Potentials},
  author  = {Th{\"o}lke, Philipp and De Fabritiis, Gianni},
  booktitle = {ICLR},
  year    = {2022}
}

@article{qiu2024softening,
  title   = {Systematic softening in universal machine learning interatomic potentials},
  author  = {Qiu, Yue and others},
  journal = {npj Computational Materials},
  year    = {2024}
}

@article{rose1984,
  title   = {Universal features of the equation of state of metals},
  author  = {Rose, John H. and Smith, John R. and Guinea, Francisco and Ferrante, John},
  journal = {Physical Review B},
  volume  = {29},
  pages   = {2963},
  year    = {1984}
}
```

The project is under GPL-3.0 license.
