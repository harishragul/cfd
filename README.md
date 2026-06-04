# CFD from Scratch — Foundations to Turbulence

A self-contained, notebook-based course in Computational Fluid Dynamics. Every concept is built from first principles in Python — no black-box solvers, no pre-packaged CFD libraries. You write the physics, the numerics, and the code yourself.

The course runs from the very first equation (what *is* a finite difference?) all the way to turbulence models used in industrial CFD codes like OpenFOAM and Fluent.

---

## About this repo

I built this while learning CFD myself — these notebooks are the notes and exercises I wrote as I worked through each concept from scratch. I'm still actively learning and adding to it.

I'm sharing it publicly so other self-learners can follow the same path without having to piece together resources from a dozen different places.

The entire course was built with the help of a [Claude Code](https://claude.ai/code) AI agent acting as an interactive CFD tutor — asking me questions before explaining, making me implement each concept before moving on, and catching my mistakes along the way. The Socratic + Feynman approach it follows is baked into how each notebook is structured.

---

## Who this is for

- Engineers or scientists who want to understand what CFD solvers actually do inside
- Grad students preparing for research in fluid mechanics or numerical methods
- Anyone who has taken a fluids course but never implemented anything from scratch

**You need:** Python + NumPy comfort, basic calculus, some exposure to PDEs (the course builds intuition as it goes).

---

## What you will build

By the end of this course you will have implemented, from scratch:

| What | Key idea learned |
|------|-----------------|
| Finite difference schemes (1st–4th order) | Truncation error, order of accuracy |
| 1D linear advection (FTBS, FTCS, FTFS) | CFL condition, upwinding, numerical diffusion |
| 1D diffusion (explicit, implicit, Crank-Nicolson) | Stability vs accuracy, tridiagonal solvers |
| 1D Burgers' equation (inviscid + viscous) | Shock formation, characteristics, entropy condition |
| 2D scalar transport | Multi-dimensional upwinding, combined stability |
| Finite Volume Method | Flux balance, exact mass conservation |
| 2D Navier-Stokes solver | Pressure-velocity coupling, projection method |
| SIMPLE algorithm | Pressure correction, under-relaxation |
| Lid-driven cavity flow | Ghia et al. validation, iterative solvers |
| Flow over a cylinder | Drag, lift, vortex shedding |
| Boundary conditions | Dirichlet, Neumann, ghost cells |
| Turbulence: mixing-length model | RANS, Reynolds decomposition, Boussinesq hypothesis |
| Turbulence: k-ε and k-ω SST | Transport equations, blending functions, wall treatment |
| Mesh generation | Structured/unstructured/hybrid, y⁺ estimation, geometric clustering |

---

## Curriculum

### Module 1 — Foundations

| Notebook | Topic |
|----------|-------|
| [foundations/module1_05_finite_differences.ipynb](foundations/module1_05_finite_differences.ipynb) | Finite difference schemes, order of accuracy, convergence plots |
| [foundations/module1_06_1d_advection.ipynb](foundations/module1_06_1d_advection.ipynb) | 1D linear advection — FTBS, CFL, upwinding, periodic BCs |
| [foundations/module1_07_1d_diffusion.ipynb](foundations/module1_07_1d_diffusion.ipynb) | 1D diffusion — explicit FTCS, implicit BTCS, Crank-Nicolson |
| [foundations/module1_08_burgers_equation.ipynb](foundations/module1_08_burgers_equation.ipynb) | Burgers' equation — shock formation, viscous vs inviscid |
| [foundations/module1_08b_burgers_gaussian.ipynb](foundations/module1_08b_burgers_gaussian.ipynb) | Burgers' — Gaussian initial condition, adaptive time-stepping |
| [foundations/module1_schemes_comparison.ipynb](foundations/module1_schemes_comparison.ipynb) | All four scheme combinations side-by-side |

**Exercises written in `exercise/`:**
- [exercise/1d_advection.ipynb](exercise/1d_advection.ipynb)
- [exercise/1d_diffusion.ipynb](exercise/1d_diffusion.ipynb)
- [exercise/1d_diffusion_with_ghost_cells.ipynb](exercise/1d_diffusion_with_ghost_cells.ipynb)
- [exercise/1d_invicid_burgers_equation.ipynb](exercise/1d_invicid_burgers_equation.ipynb)
- [exercise/1d_viscous_burgers_equation.ipynb](exercise/1d_viscous_burgers_equation.ipynb)

---

### Module 2 — Core CFD Methods

| Notebook | Topic |
|----------|-------|
| [exercise/2d_scalar_transport.ipynb](exercise/2d_scalar_transport.ipynb) | 2D advection-diffusion, multi-dimensional stability |
| [exercise/fvm_1d_scalar.ipynb](exercise/fvm_1d_scalar.ipynb) | Finite Volume Method — flux balance, exact mass conservation |
| [exercise/lid_driven_cavity.ipynb](exercise/lid_driven_cavity.ipynb) | Full SIMPLE solver — Navier-Stokes, projection, Ghia validation |
| [exercise/cylinder_flow.ipynb](exercise/cylinder_flow.ipynb) | Flow over a cylinder — drag, lift, vortex shedding |
| [exercise/flow_over_vertical_plate.ipynb](exercise/flow_over_vertical_plate.ipynb) | Vertical plate flow |
| [Core CFD Methods/module2_16_boundary_conditions.ipynb](Core%20CFD%20Methods/module2_16_boundary_conditions.ipynb) | Dirichlet, Neumann, ghost cells — theory and implementation |

---

### Module 3 — Turbulence and Meshing

| Notebook | Topic |
|----------|-------|
| [Core CFD Methods/module3_17_turbulence_basics.ipynb](Core%20CFD%20Methods/module3_17_turbulence_basics.ipynb) | RANS, Reynolds decomposition, mixing-length, law of the wall |
| [Core CFD Methods/module3_18_turbulence_models.ipynb](Core%20CFD%20Methods/module3_18_turbulence_models.ipynb) | k-ε, k-ω SST, turbulent channel flow simulation |
| [exercise/mesh_design.ipynb](exercise/mesh_design.ipynb) | y⁺ estimation, geometric clustering, tanh stretching |

---

### Module 4 — Projects (coming)

Channel flow, heat exchanger, airfoil aerodynamics, turbulent jet.

---

## How to use this repo

**Recommended path:**

1. Read a reference notebook in `foundations/` or `Core CFD Methods/` — these explain the theory.
2. Open the matching exercise notebook in `exercise/` and implement it yourself.
3. The exercise notebooks have the structure and comments; the implementation cells are yours to fill.

**Learning order:**

```
Module 1 (foundations/) → Module 2 (exercise/ + Core CFD Methods/) → Module 3 (Core CFD Methods/)
```

You can also jump to any topic if you already know the prerequisites.

---

## Setup

```bash
git clone https://github.com/harishragul/cfd.git
cd cfd
pip install numpy matplotlib scipy jupyter
jupyter notebook
```

No additional CFD libraries needed. Every solver is written in plain NumPy.

---

## Key concepts covered

**Numerical methods:** finite differences, finite volumes, explicit/implicit time integration, upwinding, Crank-Nicolson, Jacobi/Gauss-Seidel/SOR iterative solvers, Poisson equation

**Fluid mechanics:** conservation laws, incompressible Navier-Stokes, pressure-velocity coupling, projection method, SIMPLE algorithm, boundary layer theory, Reynolds decomposition

**Turbulence modeling:** mixing-length model, k-ε model, k-ω SST (Menter 1994), law of the wall, y⁺, turbulent channel flow

**Meshing:** structured/unstructured/hybrid meshes, skewness, aspect ratio, non-orthogonality, geometric and tanh clustering, y⁺ estimation workflow

---

## Validation

The lid-driven cavity solver is validated against the benchmark results of:

> Ghia, U., Ghia, K. N., & Shin, C. T. (1982). High-Re solutions for incompressible flow using the Navier-Stokes equations and a multigrid method. *Journal of Computational Physics*, 48(3), 387–411.

---

## References

- Patankar, S. V. (1980). *Numerical Heat Transfer and Fluid Flow*. Hemisphere.
- Menter, F. R. (1994). Two-equation eddy-viscosity turbulence models for engineering applications. *AIAA Journal*, 32(8), 1598–1605.
- Barba, L. A., & Forsyth, G. F. (2018). CFD Python: the 12 steps to Navier-Stokes equations. *Journal of Open Source Education*, 2(16), 21.
- Ferziger, J. H., Perić, M., & Street, R. L. (2020). *Computational Methods for Fluid Dynamics* (4th ed.). Springer.

---

## License

MIT — use freely, attribution appreciated.
