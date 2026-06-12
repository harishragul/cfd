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
|---|----------|-------|--------|-----------|
| 01 | [01_les_des_rsm.ipynb](01_les_des_rsm.ipynb) | LES, DES, RSM — beyond the Boussinesq hypothesis | ✅ Done | Module 3.17–3.18 (turbulence models) |
| 02 | `02_verification_validation.ipynb` | Verification & Validation — grid convergence, GCI, Richardson extrapolation | 📋 Planned | Any solver from Module 2 |
| 03 | `03_hpc_parallel_cfd.ipynb` | HPC for CFD — domain decomposition, MPI, GPU acceleration | 📋 Planned | Module 2.13 (SIMPLE) |
| 04 | `04_non_newtonian_flows.ipynb` | Non-Newtonian fluids — shear-thinning/thickening, viscoplastic models | 📋 Planned | Module 2.11 (Navier-Stokes) |
| 05 | `05_conjugate_heat_transfer.ipynb` | Conjugate heat transfer & natural convection — Boussinesq buoyancy, Rayleigh-Bénard | 📋 Planned | Module 2 (energy equation gap) |
| 06 | `06_multiphase_flows.ipynb` | Multiphase flows — VOF, Level-Set, Euler-Euler vs Euler-Lagrange | 📋 Planned | Module 2.14 (cavity), Module 3.19 (meshing) |
| 07 | `07_reduced_order_modeling.ipynb` | Reduced-Order Modeling — POD, DMD, fast surrogates | 📋 Planned | Module 3.24 (PINNs) |
| 08 | `08_immersed_boundary.ipynb` | Immersed Boundary Method — complex/moving geometry without body-fitted meshes | 📋 Planned | Module 3.19 (meshing) |
| 09 | `09_lattice_boltzmann.ipynb` | Lattice Boltzmann Method — mesoscale alternative to FVM/FDM | 📋 Planned | Module 2.10 (FVM) |
| 10 | `10_adjoint_optimization.ipynb` | Adjoint methods & shape optimization — sensitivity analysis for design | 📋 Planned | Module 2.11 + Module 4.03 (airfoil) |

---

## PhD / Research-Track Topics

The algorithms, solvers, and analysis techniques most commonly assumed knowledge for CFD-focused
PhD work — the stuff that shows up in qualifying exams, advisor discussions, and the "verification"
or "numerical method" section of nearly every methods paper.

| # | Notebook | Topic | Status | Builds on |
|---|----------|-------|--------|-----------|
| 11 | `11_piso_pimple.ipynb` | PISO & PIMPLE — pressure-velocity coupling for transient flows | 📋 Planned | Module 2.13 (SIMPLE), Module 3.06 (unsteady flows) |
| 12 | `12_krylov_solvers.ipynb` | Krylov subspace solvers & preconditioning — CG, GMRES, BiCGSTAB, ILU | 📋 Planned | Module 2.05 (SIMPLE), Module 3.21 (multigrid) |
| 13 | `13_code_verification_mms.ipynb` | Code verification — Method of Manufactured Solutions (MMS) | 📋 Planned | Extra 02 (V&V) |
| 14 | `14_spectral_high_order.ipynb` | Spectral & high-order methods — spectral/SEM/DG for DNS-quality accuracy | 📋 Planned | Module 3.20 (higher-order schemes) |
| 15 | `15_hydrodynamic_stability.ipynb` | Hydrodynamic stability & transition — Orr-Sommerfeld, linear stability, e^N method | 📋 Planned | Module 1 (1D solvers), Module 3.17 (turbulence basics) |
| 16 | `16_adaptive_mesh_refinement.ipynb` | Adaptive Mesh Refinement (AMR) — error estimators, dynamic refinement | 📋 Planned | Module 3.19 (meshing) |
| 17 | `17_overset_grids.ipynb` | Overset / Chimera grids — moving bodies & relative motion | 📋 Planned | Module 3.19 (meshing), Module 2.15 (cylinder flow) |
| 18 | `18_ml_turbulence_closures.ipynb` | Data-driven turbulence modeling — field inversion, ML-augmented closures | 📋 Planned | Module 3.18, Extra 07 (ROM) |

**Why these matter for PhD prep:**

- **PISO/PIMPLE (11)** — the algorithm behind OpenFOAM's `pimpleFoam`/`icoFoam`; assumed background
  if your research touches OpenFOAM at all.
- **Krylov solvers (12)** — every implicit CFD code calls CG/GMRES/BiCGSTAB under the hood;
  preconditioning is often the difference between a solver that scales and one that doesn't.
- **MMS (13)** — the standard rigorous code-verification technique cited in nearly every numerical
  methods paper's verification section; pairs directly with Extra 02.
- **Spectral/high-order (14)** — backbone of academic DNS/LES codes (Nek5000, Nektar++); high
  accuracy per degree of freedom.
- **Hydrodynamic stability (15)** — core toolkit for transition research: Orr-Sommerfeld,
  modal/non-modal stability, receptivity.
- **AMR (16)** and **Overset grids (17)** — standard techniques for resolving multi-scale features
  and moving geometries in research codes.
- **ML turbulence closures (18)** — one of the most active current research areas: field inversion,
  neural-network-augmented RANS/LES closures.

---

## Recommended order

Based on current skill profile (Python strong, PDEs moderate, turbulence/meshing weaker), suggested
sequence — though these are largely independent and can be taken in any order once the "builds on"
prerequisite is met:

1. **02 — V&V**: short, foundational, applies retroactively to every solver already built. Answers
   "how do I know my Module 2 results are actually correct?"
2. **04 — Non-Newtonian**: smallest conceptual jump from Navier-Stokes — just a different
   stress-strain closure.
3. **05 — Conjugate Heat Transfer**: extends the energy equation, sets up natural-convection
   intuition (buoyancy-driven flow).
4. **03 — HPC**: parallelization concepts using the existing SIMPLE/cavity solver as the example —
   no new physics, just a different execution model.
5. **07 — Reduced-Order Modeling**: natural follow-on to PINNs, useful for fast iteration on the
   Module 4 projects.
6. **06 — Multiphase**: big topic, builds on meshing + cavity-flow intuition.
7. **08 — Immersed Boundary**: directly targets the meshing weak spot via a different lens.
8. **09 — Lattice Boltzmann**: alternative numerical paradigm — best appreciated once FVM is solid.
9. **10 — Adjoint/Optimization**: most advanced, needs a confident grasp of the full NS solver and
   the airfoil project (Module 4.03).

**Research-track topics (11–18) slot in alongside these:**

- **11 — PISO/PIMPLE**: a natural near-term pick *right now* — it's the direct extension of SIMPLE
  (Module 2.13) to the unsteady flows you're currently studying (Module 3.06).
- **13 — MMS** pairs directly with step 1 (V&V) — do them back-to-back.
- **12 — Krylov solvers** pairs with step 4 (HPC) — both are about how the linear systems actually
  get solved/scaled.
- **14–18** are best tackled after their "builds on" prerequisites, similar to 06–10 — **15
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
