# CFD Learning Progress

> This file tracks the student's progress through the CFD curriculum.
> It is read automatically by the CFD Tutor agent at the start of each session.

## Student Profile
- **Python + NumPy:** 4/5 (strong)
- **PDEs (math):** 3/5 (moderate)
- **FVM:** 2/5 (weak)
- **Navier-Stokes:** 1/5 (very weak)
- **Turbulence:** 0/5 (never studied)
- Existing notebooks (continuity_equation, lid_driven_cavity, flow_over_cylinder) were **code-agent generated**, NOT written by student

---

## Curriculum Progress

### Module 1: Foundations

| # | Topic | Status | Notebook |
|---|-------|--------|----------|
| 1.1 | What is CFD | ✅ Done | — |
| 1.2 | Python for CFD | ⏭ Skipped (strong) | — |
| 1.3 | Conservation Laws | ✅ Done | — |
| 1.4 | Continuity Equation | ⏳ Pending | — |
| 1.5 | Finite Difference Method | ✅ Done | foundations/module1_05_finite_differences.ipynb |
| 1.6 | 1D Linear Advection | ✅ Done | foundations/module1_06_1d_advection.ipynb |
| 1.7 | 1D Diffusion Equation | ⏳ Next up | — |
| 1.8 | 1D Burgers' Equation | ⏳ Pending | — |
| — | Module 1 Test | ⏳ Pending | — |

### Module 2: Core CFD Methods — ⏳ Not Started
- 2D Scalar Transport, FVM, Navier-Stokes, SIMPLE Algorithm, Lid-Driven Cavity, BCs

### Module 3: Advanced Topics — ⏳ Not Started
- Turbulence, higher-order schemes, multigrid, compressible flow, PINNs

### Module 4: Projects — ⏳ Not Started
- Channel flow, heat exchanger, airfoil, turbulent jet

---

## What Was Taught (Detailed)

### 1.1 — What is CFD
- Discretization: domain → grid → unknowns at each node
- 100×300 grid = 30,000 unknowns; 200×300 = 120,000 (not 60,000 — scales as N²)
- Cost vs accuracy tradeoff

### 1.3 — Conservation Laws
- Three laws: mass, momentum, energy
- Mass (continuity): ∂ρ/∂t + ∇·(ρu) = 0
- Momentum (Navier-Stokes): nonlinearity comes from **convection only** (not diffusion)
- Incompressible continuity: ∇·u = 0
- Reynolds number Re = inertial / viscous forces

### 1.5 — Finite Difference Method
- Forward difference: (f(x+h) − f(x)) / h → **1st order**
- Backward difference: (f(x) − f(x−h)) / h → **1st order**
- Central difference: (f(x+h) − f(x−h)) / 2h → **2nd order**
- 2nd derivative: (f(x+h) − 2f(x) + f(x−h)) / h² → **2nd order** (student thought 1st)
- Order confirmed by log-log convergence plot

### 1.6 — 1D Linear Advection
- Equation: ∂u/∂t + c ∂u/∂x = 0
- Exact solution: wave translates without changing shape — u(x, t) = u₀(x − ct)
- **FTBS scheme:** u_i^{n+1} = u_i^n − CFL·(u_i^n − u_{i-1}^n)
- **CFL condition:** CFL = c·dt/dx ≤ 1 (stability limit)
- **Upwinding principle:**
  - c > 0 (rightward): use Backward Space → looks left (upstream) ✓
  - c < 0 (leftward): use Forward Space → looks right (upstream) ✓
  - Central space: UNCONDITIONALLY UNSTABLE for pure advection
- **FTFS:** always unstable for c > 0 — exponentially growing oscillations
- **Forward Time = explicit:** compute future from present — simple, cheap, conditionally stable
- **Backward Time = implicit:** solve system of equations — unconditionally stable, expensive (Module 1.7)
- **Numerical diffusion:** 1st-order schemes artificially smear solution; decreases with finer grid
- **Periodic BC:** wave wraps around domain (x = 2.1 → appears at x = 0.1)
- **Diffusion vs Advection spatial stencil:** diffusion has no preferred direction → Central; advection has direction → Upwind

---

## Common Student Mistakes (for targeted review)

| Mistake | Correct Answer |
|---------|---------------|
| Doubling resolution → 2× unknowns | → 4× unknowns in 2D (scales as N²) |
| Said both convection AND diffusion cause nonlinearity | Only the **convection** term u·∇u is nonlinear |
| Said 2nd derivative FD is 1st order | It's **2nd order** accurate |
| Said "downstream" is where to look for upstream info | Look **upstream** — where the wave comes from |
| Pulse appearing left = going backward | Wave wrapped around periodic domain (Pac-Man) |
| Heat plate analogy — "backward space" = looking at left BC | Spatial stencil for diffusion is **central** (both sides); left BC is just a boundary value |

---

## Teaching Notes (for CFD Tutor agent)

- Student learns best: **physical analogy → equation → code**
- Socratic method works well — ask before explaining
- Student is comfortable with NumPy vectorized operations
- When confused, re-explain with a different analogy
- Student asks deep "why" questions — reward and engage them
- Next session: start with **Module 1.7 — 1D Diffusion Equation**
