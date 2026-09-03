# 3. Methodology

## Workflow

```
Fusion 360 (CAD)        CONVERGE Studio (case setup)      Tecplot / ParaView
   geometry  ── STL ──►  boundaries, mesh, chemistry ──►  solver ──►  post-processing
                          physics models, IC/BCs           (days)      fields, animations
```

| Stage | Tool | Output |
|---|---|---|
| Geometry | Autodesk Fusion 360 | Watertight STL of the fluid domain |
| Surface repair and flagging | CONVERGE Studio | Oriented, sealed surface with named boundaries |
| Meshing | CONVERGE (cut-cell Cartesian) | Base grid with AMR controls |
| Chemistry | SAGE detailed-chemistry solver | Finite-rate kinetics on the LLNL hydrogen mechanism |
| Turbulence | RANS k–ε | Closure for the averaged equations |
| Solution | CONVERGE solver | Time-resolved field and monitor-point data |
| Post-processing | Tecplot, ParaView | Field slices, iso-surfaces, animations |

## Software access

CFD capability was gated by licensing, and resolving it consumed a substantial
part of the schedule. The chronology is in [`timeline.md`](timeline.md).

An Explore license was obtained at no cost in October 2025. It caps the mesh at
500,000 cells, which forces two-dimensional or coarse domains but is sufficient
to learn the complete workflow. This cap became requirement R5 in
[`02-objectives-and-requirements.md`](02-objectives-and-requirements.md).

An academic license was pursued through an institutional route and abandoned,
since it required months of process and on-site access.

A home-use academic license was granted directly by the vendor in February 2026
following a licensing discussion and a signed agreement. This raised the
throughput ceiling and provided access to the official RDE reference case, which
became the validated starting point for the custom design.

## Development sequence

The workflow was built bottom-up so that every feature of the final case had
been exercised on a simpler problem first. This was deliberate: in a coupled
reacting case, a setup error and a physics error produce similar symptoms, and
the only economical way to tell them apart is to have eliminated the setup
mechanics beforehand.

| Step | Case | Capability established |
|---|---|---|
| 1 | 90° bent pipe, air | STL import, normal-orientation repair, boundary and region distinction, species definition |
| 2 | Straight duct and channel flows | Base-grid sizing, cell-count budgeting, run monitoring, first field renders |
| 3 | Three-port cylinder | Mechanism/thermodynamic/transport data import, combustion model activation, output management |
| 4 | Two-dimensional H2/O2 combustion box | LLNL mechanism with SAGE, AMR, thermal initialization region |
| 5 | CONVERGE RDE reference case | Periodic boundaries, unwrapped annulus, detonation post-processing |
| 6 | Custom RDE geometry | Transfer of the complete case setup to original CAD |

Each step introduced exactly one new class of difficulty. Step 4 is the first
case with chemistry, step 5 the first with periodic boundaries, step 6 the first
on geometry not supplied with a working configuration.

## Simulation practice

**Compute budget.** All runs executed on a four-core desktop. Run times ranged
from under an hour for coarse duct flows to approximately four days for the RDE
reference case. Disk capacity was an active constraint: one early run was
aborted after projecting 3.5 million output frames, and output write frequency
became a tuned parameter from that point forward. Cloud offload was evaluated
and rejected on cost.

**Resolution against cost.** Coarse uniform grids produced visibly blocky and
unreliable fields. The working compromise was a modest base grid with adaptive
refinement concentrated at gradients, principally the detonation front, holding
total cell count under the license cap. The reasoning is developed in
[`05-numerical-methods.md`](05-numerical-methods.md).

**Verification discipline.** Each case was checked against expected behavior
before advancing to the next complexity level, using pressure equalization
times, ignition behavior, and wave-speed sanity checks. Solver output was
treated as a prediction to be interrogated rather than as ground truth. What
this does and does not establish is set out in
[`08-validation-and-limitations.md`](08-validation-and-limitations.md).
