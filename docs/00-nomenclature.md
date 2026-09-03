# Nomenclature

Symbols and abbreviations used throughout this documentation. Values specific to
the present design are collected in
[`04-engine-design.md`](04-engine-design.md).

## Roman symbols

| Symbol | Quantity | Units |
|---|---|---|
| `a` | Local speed of sound | m/s |
| `D_CJ` | Chapman-Jouguet detonation velocity | m/s |
| `D_w` | Observed wave velocity | m/s |
| `d_c` | Combustor inner diameter | mm |
| `E` | Total energy per unit mass | J/kg |
| `h*` | Critical detonation fill height | mm |
| `L_c` | Combustor axial length | mm |
| `M` | Mach number | – |
| `ṁ` | Mass flow rate | g/s |
| `N_w` | Wave multiplicity (number of co-rotating waves) | – |
| `p_c` | Mean chamber pressure | bar |
| `p_p` | Injection plenum pressure | bar |
| `T` | Static temperature | K |
| `t` | Time | s |
| `u` | Velocity vector | m/s |
| `Y_k` | Mass fraction of species *k* | – |

## Greek symbols

| Symbol | Quantity | Units |
|---|---|---|
| `Δ` | Annular channel width | mm |
| `ε` | Turbulent dissipation rate | m²/s³ |
| `γ` | Ratio of specific heats | – |
| `κ` | Turbulent kinetic energy | m²/s² |
| `λ` | Detonation cell size | mm |
| `μ` | Dynamic viscosity | Pa·s |
| `π_inj` | Injector pressure ratio, `p_p / p_c` | – |
| `ρ` | Density | kg/m³ |
| `τ` | Viscous stress tensor | Pa |
| `φ` | Equivalence ratio | – |
| `ω̇_k` | Net production rate of species *k* | kg/m³·s |

## Subscripts

| Subscript | Meaning |
|---|---|
| `c` | Combustor / chamber |
| `CJ` | Chapman-Jouguet state |
| `inj` | Injector |
| `k` | Species index |
| `p` | Plenum |
| `w` | Detonation wave |

## Abbreviations

| Term | Expansion |
|---|---|
| AMR | Adaptive mesh refinement |
| BC | Boundary condition |
| CFD | Computational fluid dynamics |
| CJ | Chapman-Jouguet |
| DDT | Deflagration-to-detonation transition |
| IC | Initial condition |
| ODWE | Oblique detonation wave engine |
| PDE | Pulse detonation engine |
| RANS | Reynolds-averaged Navier-Stokes |
| RDE | Rotating detonation engine |
| SAGE | Detailed-chemistry solver in CONVERGE |
| SLS | Selective laser sintering |
| STL | Stereolithography tessellation format |
| ZND | Zel'dovich-von Neumann-Döring detonation model |
