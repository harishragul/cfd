# Extra Modules — Roadmap

## What this folder is

`curriculum/extra_module/` holds **supplementary notebooks** for topics that matter in real-world CFD
but don't fit the core Module 1–4 path (foundations → core methods → turbulence/meshing → projects).
Core modules build one solver end-to-end; extra modules are shorter, focused deep-dives that plug
gaps the core path deliberately left out.

Same format as the rest of the curriculum: physical analogy → equation → working code demo →
predict-then-verify exercise.

---

## Status

| # | Notebook | Topic | Status | Builds on |
| --- | --- | --- | --- | --- |
| 01 | [01_les_des_rsm.ipynb](01_les_des_rsm.ipynb) | LES, DES, RSM — beyond the Boussinesq hypothesis | ✅ Done | Module 3.17–3.18 (turbulence models) |
| 02 | [02_numerical_solvers_toolbox.ipynb](02_numerical_solvers_toolbox.ipynb) | Numerical Solvers Toolbox — Thomas, LU, Jacobi, GS, SOR, Euler, RK2, RK4 | ✅ Done | Module 1.07, Module 2.13 |
| 03 | `03_verification_validation.ipynb` | Verification & Validation — grid convergence, GCI, Richardson extrapolation | 📋 Planned | Extra 02 (solvers toolbox) |
| 04 | `04_hpc_parallel_cfd.ipynb` | HPC for CFD — domain decomposition, MPI, GPU acceleration | 📋 Planned | Module 2.13 (SIMPLE) |
| 05 | `05_non_newtonian_flows.ipynb` | Non-Newtonian fluids — shear-thinning/thickening, viscoplastic models | 📋 Planned | Module 2.11 (Navier-Stokes) |
| 06 | `06_conjugate_heat_transfer.ipynb` | Conjugate heat transfer & natural convection — Boussinesq buoyancy, Rayleigh-Bénard | 📋 Planned | Module 2 (energy equation gap) |
| 07 | `07_multiphase_flows.ipynb` | Multiphase flows — VOF, Level-Set, Euler-Euler vs Euler-Lagrange | 📋 Planned | Module 2.14 (cavity), Module 3.19 (meshing) |
| 08 | `08_reduced_order_modeling.ipynb` | Reduced-Order Modeling — POD, DMD, fast surrogates | 📋 Planned | Module 3.24 (PINNs) |
| 09 | `09_immersed_boundary.ipynb` | Immersed Boundary Method — complex/moving geometry without body-fitted meshes | 📋 Planned | Module 3.19 (meshing) |
| 10 | `10_lattice_boltzmann.ipynb` | Lattice Boltzmann Method — mesoscale alternative to FVM/FDM | 📋 Planned | Module 2.10 (FVM) |
| 11 | `11_adjoint_optimization.ipynb` | Adjoint methods & shape optimization — sensitivity analysis for design | 📋 Planned | Module 2.11 + Module 4.03 (airfoil) |

---

## PhD / Research-Track Topics

The algorithms, solvers, and analysis techniques most commonly assumed knowledge for CFD-focused
PhD work — the stuff that shows up in qualifying exams, advisor discussions, and the "verification"
or "numerical method" section of nearly every methods paper.

| # | Notebook | Topic | Status | Builds on |
| --- | --- | --- | --- | --- |
| 12 | `12_piso_pimple.ipynb` | PISO & PIMPLE — pressure-velocity coupling for transient flows | 📋 Planned | Module 2.13 (SIMPLE), Module 3.06 (unsteady flows) |
| 13 | `13_krylov_solvers.ipynb` | Krylov subspace solvers & preconditioning — CG, GMRES, BiCGSTAB, ILU | 📋 Planned | Extra 02 (solvers toolbox), Module 3.21 (multigrid) |
| 14 | `14_code_verification_mms.ipynb` | Code verification — Method of Manufactured Solutions (MMS) | 📋 Planned | Extra 03 (V&V) |
| 15 | `15_spectral_high_order.ipynb` | Spectral & high-order methods — spectral/SEM/DG for DNS-quality accuracy | 📋 Planned | Module 3.20 (higher-order schemes) |
| 16 | `16_hydrodynamic_stability.ipynb` | Hydrodynamic stability & transition — Orr-Sommerfeld, linear stability, e^N method | 📋 Planned | Module 1 (1D solvers), Module 3.17 (turbulence basics) |
| 17 | `17_adaptive_mesh_refinement.ipynb` | Adaptive Mesh Refinement (AMR) — error estimators, dynamic refinement | 📋 Planned | Module 3.19 (meshing) |
| 18 | `18_overset_grids.ipynb` | Overset / Chimera grids — moving bodies & relative motion | 📋 Planned | Module 3.19 (meshing), Module 2.15 (cylinder flow) |
| 19 | `19_ml_turbulence_closures.ipynb` | Data-driven turbulence modeling — field inversion, ML-augmented closures | 📋 Planned | Module 3.18, Extra 08 (ROM) |

**Why these matter for PhD prep:**

- **PISO/PIMPLE (12)** — the algorithm behind OpenFOAM's `pimpleFoam`/`icoFoam`; assumed background
  if your research touches OpenFOAM at all.
- **Krylov solvers (13)** — every implicit CFD code calls CG/GMRES/BiCGSTAB under the hood;
  preconditioning is often the difference between a solver that scales and one that doesn't.
- **MMS (14)** — the standard rigorous code-verification technique cited in nearly every numerical
  methods paper's verification section; pairs directly with Extra 02.
- **Spectral/high-order (15)** — backbone of academic DNS/LES codes (Nek5000, Nektar++); high
  accuracy per degree of freedom.
- **Hydrodynamic stability (16)** — core toolkit for transition research: Orr-Sommerfeld,
  modal/non-modal stability, receptivity.
- **AMR (17)** and **Overset grids (18)** — standard techniques for resolving multi-scale features
  and moving geometries in research codes.
- **ML turbulence closures (19)** — one of the most active current research areas: field inversion,
  neural-network-augmented RANS/LES closures.

---

## Recommended order

Based on current skill profile (Python strong, PDEs moderate, turbulence/meshing weaker), suggested
sequence — though these are largely independent and can be taken in any order once the "builds on"
prerequisite is met:

1. **✅ 02 — Solvers Toolbox**: done — Thomas, LU, Jacobi, GS, SOR, Euler, RK2/RK4 all in one place.
2. **03 — V&V**: next up — short, foundational, retroactively validates every solver already built.
3. **05 — Non-Newtonian**: smallest conceptual jump from Navier-Stokes — different stress closure.
4. **06 — Conjugate Heat Transfer**: extends energy equation, sets up buoyancy-driven flow intuition.
5. **04 — HPC**: parallelization using the existing SIMPLE/cavity solver — no new physics.
6. **08 — Reduced-Order Modeling**: natural follow-on to PINNs, fast surrogates for Module 4 projects.
7. **07 — Multiphase**: big topic, builds on meshing + cavity-flow intuition.
8. **09 — Immersed Boundary**: targets the meshing weak spot via a different lens.
9. **10 — Lattice Boltzmann**: alternative numerical paradigm — best once FVM is solid.
10. **11 — Adjoint/Optimization**: most advanced, needs confident grasp of NS solver + Module 4.03.

**Research-track topics (12–19) slot in alongside these:**

- **12 — PISO/PIMPLE**: natural near-term pick — direct extension of SIMPLE (Module 2.13) to
  unsteady flows (Module 3.06 currently open).
- **14 — MMS** pairs directly with step 2 (V&V) — do them back-to-back.
- **13 — Krylov solvers** pairs with step 5 (HPC) — both are about how linear systems scale.
- **15–19** are best tackled after their "builds on" prerequisites, similar to 07–11 — **16
  (hydrodynamic stability)** is the most self-contained and could be done early if transition/stability
  is of research interest.

---

## Further topics (not yet scheduled)

Bigger or more niche areas worth a notebook later if interest comes up:

- **Aeroacoustics** — Ffowcs Williams-Hawkings, broadband noise prediction
- **Fluid-Structure Interaction (FSI)** — coupling CFD with structural mechanics
- **Magnetohydrodynamics (MHD)** — plasma/astrophysical flows
- **SPH (Smoothed Particle Hydrodynamics)** — Lagrangian mesh-free method
- **Combustion / reacting flows** — species transport, chemical kinetics, flamelets
- **Uncertainty Quantification (UQ)** — Monte Carlo, polynomial chaos for CFD predictions

---

## Notes

- Update the status table as notebooks are completed.
- Each new extra-module notebook should follow the cell-ID and JSON conventions established in
  `01_les_des_rsm.ipynb` (nbformat 4.5, unexecuted code cells, `extraNN_*` cell IDs).
