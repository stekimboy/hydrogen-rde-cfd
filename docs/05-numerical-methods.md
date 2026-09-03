# 5. Numerical Methods

This section states the equations solved and the numerical treatment applied.
Case-specific configuration, including boundaries, initialization, and output
settings, is in [`06-simulation-setup.md`](06-simulation-setup.md).

## Governing equations

The solver advances the compressible Navier-Stokes system augmented with species
transport and finite-rate chemistry. In conservative form:

**Mass**

```
∂ρ/∂t + ∇·(ρu) = 0
```

**Momentum**

```
∂(ρu)/∂t + ∇·(ρu⊗u) = −∇p + ∇·τ
```

**Energy**

```
∂(ρE)/∂t + ∇·(ρEu + pu) = ∇·(k∇T) + ∇·(τ·u) + Σ_k h_k ω̇_k
```

**Species, for each of the k species in the mechanism**

```
∂(ρY_k)/∂t + ∇·(ρY_k u) = ∇·(ρD_k ∇Y_k) + ω̇_k
```

The system is closed by the ideal gas equation of state and by
temperature-dependent thermodynamic and transport properties evaluated per
species from the mechanism data files.

Detonation is captured by this system without special treatment: the shock is a
solution of the compressible momentum equation, and the coupling that sustains
it comes from the `ω̇_k` source terms responding to the post-shock temperature
rise. Nothing in the formulation presumes a detonation will form, which is what
makes the result meaningful rather than assumed.

## Turbulence closure

The averaged equations are closed with a RANS k–ε model. The choice is a
concession to the cell budget rather than a claim about fidelity. A detonation
front is a sharp, largely inviscid structure whose propagation is governed by
shock dynamics and chemical induction rather than by turbulent transport, so the
closure has limited influence on wave speed and front position. It does affect
mixing in the fill region behind the wave, where a scale-resolving model would
be preferable and was not affordable. This is recorded as a limitation in
[`08-validation-and-limitations.md`](08-validation-and-limitations.md).

## Chemistry

Chemistry is integrated with SAGE, a detailed-chemistry solver that advances the
finite-rate kinetic system directly in each cell rather than interpolating a
tabulated flamelet library. This satisfies requirement R7 in
[`02-objectives-and-requirements.md`](02-objectives-and-requirements.md), and it
is a necessary choice for detonation: the induction delay behind the shock is a
kinetic quantity, and a model that presumes a flame structure cannot represent
it.

The mechanism is the LLNL archived hydrogen model, supplied as three files:

| File | Contents |
|---|---|
| `mech.dat` | Reaction set with rate coefficients |
| `therm.dat` | NASA polynomial thermodynamic data per species |
| `trans.dat` | Transport property coefficients per species |

Hydrogen oxidation is a comparatively small mechanism, which is part of why
hydrogen is tractable for detonation CFD at this budget. Import order matters:
species referenced in the case before the mechanism is loaded produce a fatal
error at setup, one of the failures catalogued in
[`09-lessons-learned.md`](09-lessons-learned.md).

## Discretization and meshing

CONVERGE generates a Cartesian cut-cell grid at runtime rather than requiring a
body-fitted mesh built in advance. The domain is filled with a structured base
grid, and cells intersecting the imported surface are cut to conform to it. The
practical consequence is that mesh quality is largely decoupled from geometry
complexity, which removes the usual meshing burden but makes the base grid size
the dominant cost parameter.

Adaptive mesh refinement is the mechanism by which the cell budget is met. A
uniform grid fine enough to resolve a detonation front would exceed the 500,000
cell cap by a wide margin across a domain that is nearly all smooth flow. AMR
instead refines on solution gradients, so cells are concentrated at the front
and released once it has passed. Because the front moves continuously around the
annulus, the refined region moves with it and the total count stays roughly
constant.

The trade is that refinement follows the solution rather than leading it, so the
achievable resolution at the front is bounded by how aggressively the criteria
are set against the budget that remains. Under-refinement smears the front and
depresses the wave speed, which is the first thing to suspect if a simulated
detonation runs slow.

## Numerical stability

Detonation cases are stiff in two independent senses. The chemical source terms
carry timescales orders of magnitude shorter than the flow timescales, and the
shock imposes a strong local CFL constraint. Both push the timestep down, and
together they set the multi-day wall-clock times reported in
[`03-methodology.md`](03-methodology.md).

Two practical consequences shaped the work. Ignition had to be forced rather
than left to arise, since a marginal thermal state can simply fail to transition
within the simulated window; the initialization approach is described in
[`06-simulation-setup.md`](06-simulation-setup.md). And output frequency had to
be budgeted explicitly, because a timestep small enough for stability will
generate far more frames than are useful or storable if writes are tied to it
naively.
