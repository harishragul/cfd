# CFD Learning Progress

> This file tracks the student's progress through the CFD curriculum.
> It is read automatically by the CFD Tutor agent at the start of each session.

## Student Profile
- **Python + NumPy:** 4/5 (strong)
- **PDEs (math):** 3/5 (moderate)
- **FVM:** 3/5 (moderate — implemented full projection method)
- **Navier-Stokes:** 3/5 (moderate — implemented and validated cavity solver)
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

### Module 2: Core CFD Methods — ⏳ In Progress
| # | Topic | Status | Notebook |
|---|-------|--------|----------|
| 2.9 | 2D Scalar Transport | ✅ Done | exercise/2d_scalar_transport.ipynb |
| 2.10 | Finite Volume Method (FVM) | ✅ Done | exercise/fvm_1d_scalar.ipynb |
| 2.11 | Navier-Stokes Equations | ✅ Done | — |
| 2.12 | Pressure-Velocity Coupling | ✅ Done | — |
| 2.13 | SIMPLE Algorithm | ✅ Done | — |
| 2.14 | Lid-Driven Cavity Flow | ✅ Done | exercise/lid_driven_cavity.ipynb |
| 2.15 | Flow Over Objects | ✅ Done | exercise/cylinder_flow.ipynb |
| 2.16 | Boundary Conditions | 🔄 In Progress | — |
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
| Pinned pressure at corner p[0,0] | Conflicts with two Neumann BCs — pin at interior point p[1,1] instead |
| More grid points → "smoother" solution | Finer grid = sharper, more accurate features; coarse grid smears peaks |
| Upwind causes mass loss at sharp gradients | Upwind causes **numerical diffusion** — artificial viscosity proportional to Δx |

---

## Teaching Notes (for CFD Tutor agent)

- Student learns best: **physical analogy → equation → code**
- Socratic method works well — ask before explaining
- Student is comfortable with NumPy vectorized operations
- When confused, re-explain with a different analogy
- Student asks deep "why" questions — reward and engage them
- Module 1 Test: **8.5/10 PASS** (19 April 2026)
- Module 2.14: **Complete** (8 May 2026) — Ghia validated, all functions student-written
- Next session: **Module 2.15 — Flow Over Objects (cylinder flow, drag/lift, von Kármán vortex street)**
- Watch for: student tends to miss "what happens on the other side" (rarefaction, left flank) — ask explicitly
- Student writes clean code independently; encourage identifying bugs before running
- Combined 2D stability: CFL_x + CFL_y + 4r ≤ 1 (student hit instability at r=0.35, learned the hard way)
- FVM mass conservation = 0.00e+00 exactly — student verified and understood why
- Student asks good research questions (e.g. ML for α in SIMPLE) — encourage but redirect to finish implementation first

### 2.11 — Navier-Stokes Equations
- Q1: Student correctly identified Bernoulli / continuity as the hose-nozzle principle (p₁u₁ = p₂u₂)
- Q2: Student identified pressure gradient −∇p as the missing term vs Burgers'
- v∂u/∂y: student correctly connected to 2D scalar transport — y-velocity carrying x-momentum across layers
- Re→∞ ≠ turbulence: Euler equations (inviscid) are mathematical limit; viscosity still controls smallest scales in real turbulence (Kolmogorov microscales η ~ Re⁻³/⁴)
- Non-dimensionalization: u*=u/U, p*=p/ρU², t*=tU/L → NS in Re form
- Euler equations used in compressible aerodynamics where viscous effects are negligible away from boundary layers

### 2.12 — Pressure-Velocity Coupling
- Core problem: momentum evolves u,v but not p; continuity ∇·u=0 has no time derivative → must be satisfied instantly
- Pressure propagates at infinite speed (incompressible = sound speed → ∞) → requires global Poisson solve, not local stencil
- **Projection method:** (1) Predictor: u* from momentum ignoring p; (2) ∇²p = ρ/Δt · ∇·u*; (3) u^{n+1} = u* − Δt/ρ · ∇p
- Wall pressure BC: Neumann ∂p/∂n = 0 (from no-penetration u·n̂ = 0); outlet: Dirichlet p = p_ref
- Poisson equation needs exactly ONE Dirichlet point to fix the constant — solution unique only up to additive constant
- Student initially confused "nearby fluid moves" with local computation; corrected to global elliptic solve

### 2.13 — SIMPLE Algorithm
- SIMPLE = Semi-Implicit Method for Pressure-Linked Equations (Patankar & Spalding 1972) — backbone of OpenFOAM, Fluent, Star-CCM+
- Steady-state target: drop ∂u/∂t → two coupled elliptic equations; outer iterations between momentum and pressure
- 500×500 grid = 750,000 unknowns; exact factorization O(N³) infeasible; SIMPLE iteration O(N) per step × 50–200 iter
- Under-relaxation α: p^{new} = p* + α_p·p'; typical α_p ≈ 0.3, α_u ≈ 0.7
- Student correctly identified: full α_p=1 overshoots because u* is approximate → oscillation → divergence
- Why no standalone notebook: projection + SIMPLE require Poisson solver + staggered grid + BCs + validation — all assembled in 2.14
- ML for α: active research; basic idea not novel but geometry-agnostic RL policy with theoretical guarantees → publishable (Computers & Fluids, JCP)

### 2.14 — Lid-Driven Cavity Flow (✅ Complete — 8 May 2026)
- Setup: square cavity, top wall u=U_lid=1 v=0; all other walls no-slip; no inlet/outlet
- Primary vortex forms (fluid spins inside); Re=100 → smooth laminar; Re=10000 → secondary corner vortices, potentially unsteady
- Collocated grid used (not staggered); checkerboard avoided by using consistent 2-cell central stencils for both divergence and pressure gradient
- Pressure Dirichlet: pin p=0 at ONE interior point p[1,1]; all walls are Neumann ∂p/∂n=0 — student correctly identified this as fixing constant ambiguity in pure-Neumann system
- Student built all 5 functions independently: apply_boundary_conditions, momentum_predictor, compute_divergence, pressure_poisson_connector (Jacobi), velocity_corrector
- Key bugs caught by student during code review: p[0,0] corner pin conflict with Neumann BCs → fixed to p[1,1]; rho missing from velocity correction formula
- Time loop order: BCs → predictor → Poisson (warm start from p_old) → correction → BCs → convergence check
- Converged at step 1428 (T≈7.9), Re=100, 41×41 grid, safety=0.8, tol=1e-4
- Validated against Ghia et al. (1982): u-profile (x=0.5) matches well; v-profile (y=0.5) shows ~15% undershoot of trough — attributed to coarse grid + first-order upwind numerical diffusion
- Iterative solvers: student learned Jacobi (vectorizable, slow), Gauss-Seidel (faster, hard to vectorize), SOR (10-50x faster, optimal ω≈1.8), CG (O(N) for SPD), multigrid (gold standard O(N))
- Student used max_iter=20000 (brute force); correct pedagogical answer was Option B (relax Poisson tol to 1e-2 for time-marching)
- Notebook: exercise/lid_driven_cavity.ipynb

### 2.9 — 2D Scalar Transport

- Extended 1D upwind/diffusion to 2D: independent upwind per direction
- np.roll needs axis=1 (x) and axis=0 (y) — student initially missed axis argument
- Safe dt: safety / (u/dx + v/dy + 4α/dx²) — general formula for any grid
- Numerical diffusion ∝ u·Δx/2·(1−CFL): peak 0.618 → 0.756 when Nx doubled
- Key bugs caught: variable collision (u=scalar vs u=velocity), roll without axis, missing /dx

### 2.10 — Finite Volume Method (FVM)
- FVM core: integrate PDE over CV → flux balance: dφ_P/dt = −(F_e − F_w)/Δx
- Conservation: F_e of cell P = F_w of cell P+1 — exact algebraic cancellation → mass error = 0.00e+00
- Face reconstruction: upwind for convection (directional), central for diffusion (symmetric/self-adjoint)
- Diffusion operator [1,−2,1] is symmetric — no preferred direction — central is correct
- Student correctly structured code with explicit F_east, F_west — clean FVM style
