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
| 1.7 | 1D Diffusion Equation | ✅ Done | foundations/module1_07_1d_diffusion.ipynb |
| 1.8 | 1D Burgers' Equation | ✅ Done | foundations/module1_08_burgers_equation.ipynb, foundations/module1_08b_burgers_gaussian.ipynb |
| — | Module 1 Test | ✅ Done (8.5/10) | — |

### Module 2: Core CFD Methods — ⏳ Next Up
| # | Topic | Status | Notebook |
|---|-------|--------|----------|
| 2.9 | 2D Scalar Transport | ⏳ Next up | — |
| 2.10 | Finite Volume Method (FVM) | ⏳ Pending | — |
| 2.11 | Navier-Stokes Equations | ⏳ Pending | — |
| 2.12 | Pressure-Velocity Coupling | ⏳ Pending | — |
| 2.13 | SIMPLE Algorithm | ⏳ Pending | — |
| 2.14 | Lid-Driven Cavity Flow | ⏳ Pending | — |
| 2.15 | Flow Over Objects | ⏳ Pending | — |
| 2.16 | Boundary Conditions | ⏳ Pending | — |
| — | Module 2 Test | ⏳ Pending | — |

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
- **General upwind scheme:** max(c,0)·FTBS + min(c,0)·FTFS handles any sign of c automatically

### Module 1 Test — Results (8.5/10, Pass)
- ✅ Q1: Grid scaling (4× in 2D) — correct
- ✅ Q2: Nonlinearity from (u·∇)u — correct
- ✅ Q3: 2nd-order error halving (0.00075) — correct
- ✅ Q4: Max dt from CFL (0.025) — correct
- ✅ Q5: FTFS code is incorrect for c>0 — correct
- ✅ Q6: Max stable dt for explicit diffusion (0.25) — correct
- ✅ Q7: Implicit BTCS stable for any r — correct
- ⚠️ Q8: t_s = 0.98 (should be 1.0 exactly); missed rarefaction on left flank
- ❌ Q9: Misdiagnosed diffusion formula (correct) as error; missed: (1) central diff for convection is unstable, (2) no BC update for endpoints
- ✅ Q10: Both stability conditions + halving dx → halving dt — correct

### 1.8 — 1D Burgers' Equation
- Burgers equation: ∂u/∂t + u·∂u/∂x = ν·∂²u/∂x²
- Nonlinearity source: u·∂u/∂x — the wave speed **is** the solution itself
- Each point travels at its own speed → **characteristics** converge (right flank) or diverge (left flank)
- **Shock formation time:** t_s = −1 / min(du₀/dx)
  - For Gaussian: t_s = 1 / (A / (σ·√e)) ≈ σ√e / A
- **Inviscid:** ν=0 → shock forms at t_s; multi-valued solution beyond t_s → need entropy condition
- **Viscous:** shock forms but stays sharp with thickness δ ∼ ν/U = 1/Re
- **Adaptive time-stepping needed:** as shock steepens, u_max stays ~1 but local gradients grow; stable dt = min(CFL·dx/u_max, 0.4·dx²/ν)
- **Hopf-Cole transformation:** linearises Burgers to heat equation; exact solution via Bessel function series
- **Upwind required:** central differencing for u·∂u/∂x is unconditionally unstable
- **General upwind:** max(u,0)·(u−u_left)/dx + min(u,0)·(u_right−u)/dx handles any sign
- **Two stability conditions simultaneously:** CFL ≤ 1 (convection) AND r ≤ 0.5 (diffusion)
- Rarefaction: left flank of Gaussian/sine broadens (characteristics diverge)
- Connection to N-S: Burgers + pressure gradient = 1D incompressible momentum equation
- Module 1.8 quiz: 3/5 (first attempt); key gaps: shock time exact value, grid resolution at high Re
- Exercise notebooks written by student: exercise/1d_invicid_burgers_equation.ipynb, exercise/1d_viscous_burgers_equation.ipynb
- Student independently caught np.roll periodic BC, dual stability conditions, adaptive dt concept

### 1.7 — 1D Diffusion Equation
- Diffusion equation: ∂u/∂t = α ∂²u/∂x²
- Curvature sign rule: negative curvature (peak) → u decreases; positive curvature (valley) → u increases
- **Explicit FTCS:** u_i^{n+1} = u_i^n + r(u_{i+1}^n − 2u_i^n + u_{i-1}^n), stability requires r = α·dt/dx² ≤ 0.5
- **Implicit BTCS:** tridiagonal system A·u^{n+1} = u^n, unconditionally stable (any r)
- Halving Δx → must shrink Δt by 4× to stay stable (explicit only); not required for implicit
- Stability ≠ Accuracy: implicit with large r is stable but inaccurate; choose Δt based on physics to resolve
- **Crank-Nicolson** = average of explicit + implicit → 2nd order in time, unconditionally stable
- Decision rule: advection → explicit upwind; diffusion → implicit BTCS; N-S → IMEX (explicit convection, implicit viscous)
- Extra notebooks: foundations/module1_schemes_comparison.ipynb (all 4 scheme combinations side-by-side)

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
| Curvature < 0 → u is "unstable" | Curvature < 0 = peak → u physically **decreases** (no numerics involved) |
| Said left is upstream when c < 0 | c < 0 means wave moves left → upstream is **right** → use FTFS |
| Halving Δx → Δt halved to stay stable | Δt must shrink by **4×** (diffusion stability: r ∝ Δt/Δx²) |
| t_s for sin(x) → hardcoded 0.98 | Exact: t_s = −1/min(cos x) = −1/(−1) = **1.0** |
| Swapped diffusion numerator terms as "error" | u_{i+1} − 2u_i + u_{i-1} = u_{i-1} − 2u_i + u_{i+1} (commutative, identical) |
| Missed that central diff for convection is always unstable | Central space for u·∂u/∂x: unconditionally unstable — same as linear advection |
| Periodic BC: only interior updated, endpoints frozen | Must update ALL points including boundaries (use np.roll, not slicing) |

---

## Teaching Notes (for CFD Tutor agent)

- Student learns best: **physical analogy → equation → code**
- Socratic method works well — ask before explaining
- Student is comfortable with NumPy vectorized operations
- When confused, re-explain with a different analogy
- Student asks deep "why" questions — reward and engage them
- Module 1 Test: **8.5/10 PASS** (19 April 2026)
- Next session: begin **Module 2.9 — 2D Scalar Transport**
- Watch for: student tends to miss "what happens on the other side" (rarefaction, left flank) — ask explicitly
- Student writes clean code independently; encourage identifying bugs before running
