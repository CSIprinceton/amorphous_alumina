# Amorphous Alumina (Al$_2$O$_3$): Deep Potential Models, DFT Training Data, and Atomic Structures

This repository contains the machine-learned interatomic potentials, the *ab initio* (DFT) training datasets, and representative atomic structures supporting the study of amorphous aluminum oxide (Al$_2$O$_3$) from bulk to surface.

## Associated publication

Zheng Yu, Jiayan Xu, Abhirup Patra, Sharan Shetty, Detlef Hohl, Roberto Car,
*"From Bulk to Surface: Structure and Dynamics of Amorphous Alumina from Deep Potential
Molecular Dynamics,"* arXiv:2605.05361.
https://arxiv.org/abs/2605.05361

If you use these models, data, or structures, please cite the paper above.

## Overview

This work develops a Deep Potential (DP) model for Al$_2$O$_3$ that reproduces ab initio–quality energies and forces at length and time scales inaccessible to direct quantum-mechanical simulation, and applies it to the structure and dynamics of amorphous alumina in both bulk glass and melt-quenched free-surface configurations.

The released potential can be used directly for large-scale molecular dynamics of crystalline and amorphous alumina (bulk and surfaces) without further training, or as a starting point for fine-tuning to related systems. The atomic structures provide ready-to-run bulk and slab configurations for such simulations, and the DFT dataset can be reused to train or benchmark other interatomic potentials. The detailed methods describing how the training data were generated and how the structures were constructed are provided in the associated paper.

## Repository contents

### `models/`
Four trained Deep Potential models (`deepmd_m0.pb`–`deepmd_m3.pb`), frozen DeePMD-kit TensorFlow graphs (~21 MB each). The four models form a committee/ensemble used both for production molecular dynamics and for query-by-committee uncertainty estimation in active learning.

### `data/`
DFT training data in extended XYZ format, with per-configuration energies, atomic forces, stresses, and lattice vectors.

- `crystalline/` — bulk and surface configurations of crystalline alumina polymorphs (e.g. γ-Al$_2$O$_3$ and various surface terminations; cell sizes from Al$_16$O$_24$ up to Al$_192$O$_288$).
- `amorphous/` — actively-learned configurations of amorphous bulk and surface systems, with iteration-resolved structures (`iter.*.xyz`) from successive active-learning rounds (`r0`–`r3`).

### `structures/`
Representative atomic configurations in LAMMPS data format for downstream
simulation.

- `bulk/` — large amorphous bulk cells (up to 10,000 atoms).
- `surface/` — slab models at several sizes (`small_slow`, `medium`, `large`,
  up to ~90,000 atoms).

## File formats

- `*.pb` — frozen DeePMD-kit models, usable directly with LAMMPS (`pair_style deepmd`) or
  the DeePMD-kit Python/C++ API.
- `*.xyz` — extended XYZ; the comment line carries `Lattice`, `Properties`
  (`species:S:1:pos:R:3:forces:R:3`), `energy`, `stress`, and `pbc` fields.
- `*.dat` — LAMMPS data files (`units metal`, 2 atom types: Al and O).

## License

This repository is distributed under the GNU General Public License v3.0. See [LICENSE](LICENSE).

## Source repository

https://github.com/CSIprinceton/amorphous_alumina
