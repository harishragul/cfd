# CFD Learning Progress

> Read automatically by the CFD Tutor agent at the start of every session.
> Last updated: 12 Jun 2026

---

## Student Profile

| Skill | Level | Notes |
|-------|-------|-------|
| Python + NumPy | 4/5 | Strong — writes clean vectorised code independently |
| PDEs (math) | 3/5 | Moderate — understands physical meaning, gaps in formal derivations |
| Finite Difference Method | 4/5 | Solid — order of accuracy, stability, truncation error |
| Finite Volume Method | 3/5 | Moderate — implemented full projection method and FVM scalar solver |
| Navier-Stokes | 3/5 | Moderate — implemented and Ghia-validated cavity solver |
| Turbulence | 2/5 | Conceptual: RANS, mixing-length, k-ε, k-ω SST; basic implementation |
| Meshing | 2/5 | Understands quality metrics, y+ estimation, geometric/tanh clustering |

**Teaching method:** Socratic + Feynman every session (student-requested, 24 May 2026)

---

## Notebooks

### Written by the STUDENT (exercise/)

| Notebook | Topic |
|----------|-------|
| exercise/1d_advection.ipynb | 1D linear advection — FTBS, CFL |
| exercise/1d_diffusion.ipynb | 1D diffusion — explicit/implicit |
| exercise/1d_diffusion_with_ghost_cells.ipynb | Ghost cell BCs |
| exercise/1d_invicid_burgers_equation.ipynb | Inviscid Burgers — shock formation |
| exercise/1d_viscous_burgers_equation.ipynb | Viscous Burgers — shock + diffusion |
| exercise/2d_scalar_transport.ipynb | 2D advection-diffusion |
| exercise/fvm_1d_scalar.ipynb | Finite Volume Method — flux balance |
| exercise/lid_driven_cavity.ipynb | Lid-driven cavity — full SIMPLE solver |
| exercise/cylinder_flow.ipynb | Flow over cylinder — drag/lift |
| exercise/flow_over_vertical_plate.ipynb | Vertical plate flow |
| exercise/mesh_design.ipynb | Mesh design — geometric clustering, y+ |
| exercise/higher_order_schemes.ipynb | TVD advection — minmod, van Leer, superbee, MC limiters |

### Created by the AI AGENT (reference / teaching material)

| Notebook | Topic | Folder |
|----------|-------|--------|
| module1_05_finite_differences.ipynb | FD schemes, order of accuracy | foundations/ |
| module1_06_1d_advection.ipynb | 1D advection theory + schemes | foundations/ |
| module1_07_1d_diffusion.ipynb | 1D diffusion — FTCS, BTCS, CN | foundations/ |
| module1_08_burgers_equation.ipynb | Burgers equation | foundations/ |
| module1_08b_burgers_gaussian.ipynb | Burgers — Gaussian IC | foundations/ |
| module1_schemes_comparison.ipynb | All schemes side-by-side | foundations/ |
| module2_16_boundary_conditions.ipynb | Dirichlet, Neumann, ghost cells | Core CFD Methods/ |
| module3_17_turbulence_basics.ipynb | RANS, mixing-length, law of wall | Core CFD Methods/ |
| module3_18_turbulence_models.ipynb | k-ε, k-ω SST, channel flow | Core CFD Methods/ |
| module3_19_mesh_generation.ipynb | Mesh types (superseded by curriculum) | Core CFD Methods/ |
| 03_mesh_generation.ipynb | Full mesh generation curriculum | curriculum/module_03_advanced/ |

---

## Curriculum Progress

### Module 1: Foundations — ✅ Complete (8.5/10)

| # | Topic | Status |
|---|-------|--------|
| 1.1 | What is CFD | ✅ Done |
| 1.2 | Python for CFD | ⏭ Skipped (strong Python) |
| 1.3 | Conservation Laws | ✅ Done |
| 1.4 | Continuity Equation | ⏳ Skipped for now |
| 1.5 | Finite Difference Method | ✅ Done |
| 1.6 | 1D Linear Advection | ✅ Done |
| 1.7 | 1D Diffusion Equation | ✅ Done |
| 1.8 | 1D Burgers' Equation | ✅ Done |
| — | Module 1 Test | ✅ 8.5/10 PASS (19 Apr 2026) |

### Module 2: Core CFD Methods — ✅ Complete (10/12 = 83%)

| # | Topic | Status | Notebook |
|---|-------|--------|----------|
| 2.9 | 2D Scalar Transport | ✅ Done | exercise/2d_scalar_transport.ipynb |
| 2.10 | Finite Volume Method (FVM) | ✅ Done | exercise/fvm_1d_scalar.ipynb |
| 2.11 | Navier-Stokes Equations | ✅ Done | — |
| 2.12 | Pressure-Velocity Coupling | ✅ Done | — |
| 2.13 | SIMPLE Algorithm | ✅ Done | — |
| 2.14 | Lid-Driven Cavity Flow | ✅ Done | exercise/lid_driven_cavity.ipynb |
| 2.15 | Flow Over Objects | ✅ Done | exercise/cylinder_flow.ipynb |
| 2.16 | Boundary Conditions | ✅ Done | Core CFD Methods/module2_16_boundary_conditions.ipynb |
| — | Module 2 Test | ✅ 10/12 = 83% PASS |

### Module 3: Advanced Topics — 🔄 In Progress

| # | Topic | Status | Notebook |
|---|-------|--------|----------|
| 3.17 | Turbulence Basics | ✅ Done | Core CFD Methods/module3_17_turbulence_basics.ipynb |
| 3.18 | Turbulence Models | ✅ Done (17/20 = 85%) | Core CFD Methods/module3_18_turbulence_models.ipynb |
| 3.19 | Mesh Generation | ✅ Done | curriculum/module_03_advanced/03_mesh_generation.ipynb |
| 3.20 | Higher-Order Schemes | ✅ Done | curriculum/module_03_advanced/04_higher_order_schemes.ipynb, exercise/higher_order_schemes.ipynb |
| 3.21 | Multigrid Methods | ✅ Done (4.5/6 = 75%) | curriculum/module_03_advanced/05_multigrid_methods.ipynb |
| 3.22 | Unsteady Flows | ⏳ Pending | — |
| 3.23 | Compressible Flow | ⏳ Pending | — |
| 3.24 | Physics-Informed Neural Networks | ⏳ Pending | — |
| — | Module 3 Test | ⏳ Pending | — |

### Module 4: Projects — ⏳ Not Started

---

## Detailed Session Notes

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
- Forward difference: (f(x+h) − f(x)) / h → 1st order
- Backward difference: (f(x) − f(x−h)) / h → 1st order
- Central difference: (f(x+h) − f(x−h)) / 2h → 2nd order
- 2nd derivative: (f(x+h) − 2f(x) + f(x−h)) / h² → 2nd order (student thought 1st)
- Order confirmed by log-log convergence plot

### 1.6 — 1D Linear Advection
- Equation: ∂u/∂t + c ∂u/∂x = 0; exact solution: wave translates unchanged u(x,t) = u₀(x−ct)
- FTBS scheme: u_i^{n+1} = u_i^n − CFL·(u_i^n − u_{i-1}^n)
- CFL condition: CFL = c·dt/dx ≤ 1
- Upwinding: c>0 → backward space (looks left); c<0 → forward space (looks right); central → always unstable
- Numerical diffusion: 1st-order schemes smear solution; decreases with finer grid
- General upwind: max(c,0)·FTBS + min(c,0)·FTFS handles any sign of c

### 1.7 — 1D Diffusion Equation
- Diffusion: ∂u/∂t = α ∂²u/∂x²; curvature sign rule: negative curvature (peak) → u decreases
- Explicit FTCS: stability requires r = α·dt/dx² ≤ 0.5
- Implicit BTCS: tridiagonal system, unconditionally stable — any r
- Crank-Nicolson: average of explicit + implicit → 2nd order in time, unconditionally stable
- Decision rule: advection → explicit upwind; diffusion → implicit BTCS; N-S → IMEX

### 1.8 — 1D Burgers' Equation
- Burgers: ∂u/∂t + u·∂u/∂x = ν·∂²u/∂x²; nonlinearity: wave speed IS the solution
- Shock formation time: t_s = −1 / min(du₀/dx)
- Inviscid: shock forms at t_s; multi-valued solution requires entropy condition
- Viscous: shock thickness δ ∼ ν/U = 1/Re
- Two simultaneous stability conditions: CFL ≤ 1 (convection) AND r ≤ 0.5 (diffusion)
- Student independently caught np.roll periodic BC, dual stability conditions, adaptive dt

### Module 1 Test — 8.5/10 PASS (19 Apr 2026)
- Key gap: Q8 t_s = 0.98 (should be 1.0); missed rarefaction on left flank
- Q9: misdiagnosed diffusion formula as error; missed central diff instability + no BC update for endpoints

### 2.9 — 2D Scalar Transport
- Extended 1D upwind/diffusion to 2D: independent upwind per direction
- np.roll needs axis=1 (x) and axis=0 (y)
- Safe dt: safety / (u/dx + v/dy + 4α/dx²)
- Numerical diffusion ∝ u·Δx/2·(1−CFL): peak 0.618 → 0.756 when Nx doubled

### 2.10 — Finite Volume Method (FVM)
- FVM core: integrate PDE over CV → flux balance: dφ_P/dt = −(F_e − F_w)/Δx
- Conservation: F_e of cell P = F_w of cell P+1 → mass error = 0.00e+00 exactly
- Face reconstruction: upwind for convection (directional), central for diffusion (symmetric)

### 2.11 — Navier-Stokes Equations
- Missing term vs Burgers: pressure gradient −∇p
- v∂u/∂y: y-velocity carrying x-momentum across layers (connected to 2D scalar transport)
- Re→∞ ≠ turbulence: Euler equations are mathematical limit; viscosity still controls Kolmogorov scales
- Non-dimensionalization: u*=u/U, p*=p/ρU², t*=tU/L → NS in Re form

### 2.12 — Pressure-Velocity Coupling
- Pressure propagates at infinite speed (incompressible) → requires global Poisson solve
- Projection method: (1) Predictor u* ignoring p; (2) ∇²p = ρ/Δt · ∇·u*; (3) u^{n+1} = u* − Δt/ρ · ∇p
- Wall BC: Neumann ∂p/∂n = 0; one Dirichlet point needed to fix additive constant

### 2.13 — SIMPLE Algorithm
- SIMPLE = Semi-Implicit Method for Pressure-Linked Equations (Patankar & Spalding 1972)
- 500×500 grid = 750,000 unknowns; exact factorization O(N³) infeasible; SIMPLE O(N) per iteration
- Under-relaxation: α_p ≈ 0.3, α_u ≈ 0.7 — full α_p=1 overshoots because u* is approximate

### 2.14 — Lid-Driven Cavity Flow (✅ Complete — 8 May 2026)
- Setup: square cavity, top wall u=U_lid=1; all other walls no-slip
- Student built all 5 functions independently: BCs, predictor, divergence, Poisson (Jacobi), corrector
- Key bugs caught by student: p[0,0] pin conflicts with Neumann BCs → fixed to p[1,1]
- Converged at step 1428 (Re=100, 41×41 grid, tol=1e-4)
- Validated against Ghia et al. (1982): u-profile matches; v-profile shows ~15% undershoot on coarse grid
- Coarse grid + 1st-order upwind numerical diffusion is cause of v-profile discrepancy

### 2.15 — Flow Over Objects
- Cylinder flow: drag/lift computed; von Kármán vortex street at Re≥100
- Notebook: exercise/cylinder_flow.ipynb

### 2.16 — Boundary Conditions
- Dirichlet, Neumann, periodic, outflow (convective), ghost cells
- Notebook: Core CFD Methods/module2_16_boundary_conditions.ipynb

### Module 2 Test — 10/12 = 83% PASS

### 3.17 — Turbulence Basics (✅ Complete)
- DNS cost: ~ Re³ in 3D — infeasible for Re > 10,000
- Reynolds decomposition: u = ū + u'; avg(u')=0 but avg(u'v') ≠ 0 (turbulent momentum transport)
- RANS: Reynolds stress term adds 6 unknowns → closure problem
- Boussinesq hypothesis: −ρ·avg(u'_i·u'_j) = 2μ_t·S_ij − (2/3)ρkδ_ij → reduces to 1 unknown (ν_t)
- ν_t is property of the FLOW (not fluid); varies 100–10,000× across domain
- Mixing-length: ν_t = (κy)²·|dū/dy|, κ=0.41; log-law: u⁺ = (1/κ)ln(y⁺) + 5.2 for y⁺>30
- Physical reason for viscous sublayer: wall kills v' → turbulence suppressed → only molecular viscosity
- Notebook: Core CFD Methods/module3_17_turbulence_basics.ipynb

### 3.18 — Turbulence Models (✅ Complete — 24 May 2026, 17/20 = 85%)
- Mixing-length limitation: memoryless — cannot track turbulent energy convected from upstream
- k-ε: k = turbulent KE, ε = dissipation rate; ν_t = C_μ·k²/ε; k/ε = turbulent time scale
- k-ε failure near walls: ε = u_τ³/(κy) → ∞ as y→0; no valid wall BC
- k-ω SST (Menter 1994): F1=1 near wall → k-ω; F1=0 free stream → k-ε
- SST stress limiter: ν_t = a1·k / max(a1·ω, Ω·F2) — prevents ν_t over-prediction at stagnation
- Spalart-Allmaras: 1-equation model; designed for attached BLs; used as DES base
- Turbulent channel: Van Driest damping ℓ_m = κy·(1−exp(−y⁺/26)); N=500 needed (first cell y⁺≈0.8)
- Re_tau scaling: u_tau = sqrt(|dPdx|·H/ρ) → 4× dPdx gives 2× Re_tau (square-root relationship)
- Minor quiz gaps: mixing-length failure reason (missed transport aspect), ε→∞ consequence (no valid BC)
- Notebook: Core CFD Methods/module3_18_turbulence_models.ipynb

### 3.20 — Higher-Order Schemes (✅ Complete — 9 Jun 2026)

- Godunov's theorem: no linear scheme can be both 2nd-order accurate AND TVD — limiter must be nonlinear
- Numerical diffusion (upwind): extra ∂²u/∂x² term smears features; vanishes at CFL=1
- Numerical dispersion (Lax-Wendroff): extra ∂³u/∂x³ term causes oscillations behind discontinuities
- Photo analogy: diffusion = Gaussian blur (soft edges); dispersion = over-sharpening halo artifact
- Total Variation: TV = sum of |u_{i+1} - u_i| — hiking trail elevation (total ups+downs, not net)
- TVD guarantee: scheme cannot create new extrema not in the initial condition
- Gradient ratio: r = (φ_P - φ_W)/(φ_E - φ_P) compares gradient behind vs ahead of cell P
  - r ≈ 1: smooth region (both gradients equal) → ψ = 1 → full 2nd-order correction
  - r < 0: local extremum (sign flip) → ψ = 0 → pure 1st-order upwind
  - r → 0: sudden steepening ahead → ψ → 0 → pure 1st-order upwind
- Limiter analogy: adaptive cruise control — brakes hard near sharp bends (r < 1), full speed on straight road (r ≈ 1)
- Limiters: minmod (safest), van Leer (smooth balance), superbee (sharpest), MC (general purpose)
- QUICK: 3rd-order, φ_e = (6/8)φ_P + (3/8)φ_E − (1/8)φ_W; not TVD; uses downstream cell
- MUSCL: FVM-native TVD — reconstruct slope Δ_P inside each cell, limited by minmod/van Leer/etc
- TVD vs MUSCL: same accuracy/TVD guarantee; TVD acts per-face (FD), MUSCL acts per-cell (FVM)
- Student Feynman gaps corrected: ψ=0 means sharp region (NOT smooth); r<0 and r→0 are distinct cases
- Exercise: implemented 4 TVD solvers on step IC; L2 errors: upwind 0.182 > minmod 0.137 > MC 0.129 > van Leer 0.132 > superbee 0.125
- Superbee wins on step function (sharpest); would lose on smooth Gaussian (over-compressive)
- Minmod chosen when safety > accuracy (near shocks in complex flows); superbee for preserving sharp fronts
- Bug caught by instructor: MC formula had min cap at 1 instead of 2 (affects r > 1 regime)
- Notebooks: curriculum/module_03_advanced/04_higher_order_schemes.ipynb + exercise/higher_order_schemes.ipynb

### 3.19 — Mesh Generation (✅ Complete — 2 Jun 2026)
- Structured: regular i-j indexing, cache-friendly, hard for complex geometry
- Unstructured: connectivity table, fits any geometry, slower random access
- Hybrid: structured prism layers near wall + unstructured bulk — industry standard
- Quality metrics: skewness (<0.85), aspect ratio (<5 bulk, <100 BL), non-orthogonality (<70°), expansion ratio (<1.2)
- y+ workflow: Re → Cf (empirical) → τ_w → u_τ → y1 = y⁺_target · ν / u_τ
- Flat plate: Cf = 0.027·Re^(−1/7); Pipe/channel: Cf = 0.079·Re^(−1/4) (Blasius)
- Hydraulic diameter: D_h = 4H for parallel plates (half-height H); L = D_h = 0.20 m for exercise
- Geometric clustering: dy_i = dy_0·r^i; tanh stretching: y_i = H·(1 − tanh(s(1−ξ))/tanh(s))
- Exercise result: 40 geometric cells (r=1.15) vs 500 uniform cells for same y⁺≈1 — 12.5× fewer
- Common mistake: said cells "reduce size" away from wall — corrected: cells GROW (coarser) away from wall
- Notebooks: curriculum/module_03_advanced/03_mesh_generation.ipynb + exercise/mesh_design.ipynb

### 3.21 — Multigrid Methods (✅ Complete — 12 Jun 2026, 4.5/6 = 75%)

- Amplification factor: G(k) = cos(k·π/N) — Jacobi/GS multiplies error mode k by G(k) each sweep
- High-freq (k≈N): G→0, killed in a few sweeps. Low-freq (k≈1): G≈1−π²/2N²≈1, survives thousands of sweeps
- "Line of people" analogy: a local spike averages out in ~5 rounds; a smooth end-to-end ramp takes ~N² rounds
- O(N²) stalling: iterations ~ 2N²/π² — refining the mesh 4× needs 16× more GS iterations (the Module 2.14 wall)
- "Step back" idea: the same smooth error, viewed on a coarser grid, looks more oscillatory relative to that grid's spacing → smaller G(k) → the same smoother kills it faster there
- Restriction (full-weighting): r_coarse_i = (1/4)·r_fine_{2i-1} + (1/2)·r_fine_{2i} + (1/4)·r_fine_{2i+1} — vs injection (every-other-point), which can silently drop a residual spike entirely
- Prolongation (linear interpolation): shared (even) points copy directly; new (odd) fine points = average of neighboring coarse values
- V-cycle: recursive — smooth, compute residual, restrict, recurse on coarser grid, prolongate the correction back, smooth again; bottoms out at a tiny grid (exact solve)
- Complexity: one V-cycle costs ~2N total (geometric series N + N/2 + N/4 + ...) = O(N); GS needs O(N²) iterations × O(N) per sweep = O(N³)
- Debugging episode: gauss_seidel/residual in the curriculum notebook had a sign error (solving u''=f instead of -u''=f). Symptom: rho_mg≈1 (flat, wrong plateau) and rho_gs>1 (error growing). Fixed both formulas (+f[i]·dx² instead of -f[i]·dx²) → confirmed working: rho_mg=0.930, rho_gs=0.99940, MG error drops suddenly vs GS gradual decrease
- Quiz gaps: (1) G(2) for N=32 calculation slip — correct value is cos(2π/32)=cos(π/16)≈0.981; (2) misconception that multigrid's smoother is "better/different" — corrected: the smoother (GS, same G(k) formula) is IDENTICAL at every grid level; the multi-level strategy itself (same smoother, different grid spacings) is the speedup
- Notebook: curriculum/module_03_advanced/05_multigrid_methods.ipynb (restructured this session — added analogies, full LaTeX formulas, Demo 1/2 fine-vs-coarse comparison, transfer operators, V-cycle implementation, convergence table)

---

## Common Mistakes

| Mistake | Correct Answer |
|---------|----------------|
| Doubling resolution → 2× unknowns | 4× unknowns in 2D (scales as N²) |
| Both convection AND diffusion cause nonlinearity | Only convection term u·∇u is nonlinear |
| 2nd derivative FD is 1st order | It is 2nd order accurate |
| "Downstream" is where to look for upstream info | Look upstream — where the wave comes from |
| Halving Δx → Δt halved to stay stable | Δt must shrink 4× (diffusion stability: r ∝ Δt/Δx²) |
| t_s for sin(x) → 0.98 | Exact: t_s = 1/|min(cos x)| = 1.0 |
| Curvature < 0 → u is "unstable" | Curvature < 0 = peak → u physically decreases |
| c < 0: left is upstream | c < 0 means wave moves left → upstream is right → use FTFS |
| Swapped diffusion numerator terms as "error" | u_{i+1}−2u_i+u_{i-1} = u_{i-1}−2u_i+u_{i+1} (same) |
| Central diff for convection is stable if fine enough | Central space for u·∂u/∂x: unconditionally unstable |
| Periodic BC: only interior updated | Must update ALL points including boundaries (np.roll) |
| Pin p[0,0] for pressure | Conflicts with Neumann BCs — pin at interior point p[1,1] |
| More grid points → "smoother" solution | Finer grid = sharper, more accurate; coarse smears peaks |
| Upwind causes mass loss at sharp gradients | Upwind causes numerical diffusion — artificial viscosity ∝ Δx |
| Mixing-length only limitation: local (no history) | Also: no transport — cannot carry k from upstream |
| ε near wall is finite, just needs fine grid | ε → ∞ as y→0 analytically — no valid boundary condition |
| Cells grow smaller away from wall | Cells GROW (coarser) away from wall — that is the point |
| G(2) for N=32 ≈ 0.99999 (calculation slip) | G(2) = cos(2π/32) = cos(π/16) ≈ 0.981 |
| Multigrid converges faster because its smoother is "better"/different | Smoother (GS, G(k)=cos(kπ/N)) is IDENTICAL at every level — the multi-level (coarse-grid) strategy is the actual speedup |

---

## Teaching Instructions (for CFD Tutor Agent)

- Teaching order: physical analogy → equation → code (every topic)
- Method: Socratic first (ask before explaining) + Feynman after (student explains back in plain words)
- Student learns best with physical analogies; rewards deep "why" questions — engage them
- Student writes clean code independently; encourage spotting bugs before running
- Watch for: student tends to miss "what happens on the other side" (rarefaction, left flanks)
- Combined 2D stability: CFL_x + CFL_y + 4r ≤ 1 (student hit instability at r=0.35)
- FVM mass conservation = 0.00e+00 exactly — student verified and understood why
- Student asks good research questions (ML for α in SIMPLE) — encourage but redirect to finish implementation first
- **Current session:** Module 3.21 — Multigrid Methods complete (4.5/6 = 75%). Next: ask student to choose — Module 3.22 (Unsteady Flows), or apply multigrid to the cavity solver's pressure-Poisson step
- Prior knowledge to connect to: 1st-order upwind numerical diffusion, central diff instability, FVM face interpolation, Ghia validation undershoot traced to 1st-order upwind
- **Open issue (not actively worked):** exercise/lid_driven_cavity_tvd_staggered.ipynb (staggered MAC grid, direct sparse Poisson solve) — u-velocity matches Ghia (1982), but v-velocity profile still doesn't match; student deferred this
