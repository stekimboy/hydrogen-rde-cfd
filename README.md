# Rotating Detonation Engine: CFD Design and Simulation Study

Senior research project, October 2025 to March 2026, by Steven Kim.

Design, simulation, and analysis of a small-scale hydrogen-fueled rotating
detonation engine using CONVERGE CFD, Autodesk Fusion 360, and Tecplot.

Author: Steven Kim ([stekimboy](https://github.com/stekimboy) on GitHub,
Steven.B.Kim.30@dartmouth.edu).

![Tecplot velocity magnitude animation of the unwrapped RDE simulation](media/animations/tecplot-velocity-magnitude.gif)

*Velocity magnitude in the unwrapped RDE domain of the CONVERGE reference
case, rendered in Tecplot from the solver output. The same animation is in
[`media/videos/rde-simulation-animation.mp4`](media/videos/rde-simulation-animation.mp4)
as an MP4 export.*

---

## Summary

Conventional combustors burn propellant by deflagration, a subsonic flame front
consuming the mixture at roughly constant pressure. A rotating detonation engine
replaces that with a supersonic detonation wave travelling continuously around
an annular channel. Because detonation approximates constant-volume heat
addition, the cycle offers higher thermodynamic efficiency, simpler
turbomachinery, and a more compact engine.

This study carried an RDE design through the full early-phase loop: literature
review, analytical sizing against published operability criteria, parametric CAD
geometry, a reacting-flow CFD case with detailed hydrogen chemistry, and
post-processing to confirm a sustained detonation wave.

The result is a demonstrated methodology and a qualitatively correct rotating
detonation, not a validated engine. That distinction is maintained deliberately
throughout the documentation and is set out in full in
[`docs/08-validation-and-limitations.md`](docs/08-validation-and-limitations.md).

## Key results

A sustained rotating detonation was reproduced in the CONVERGE RDE reference
case after approximately four days of wall-clock time on four cores, and
confirmed against three independent checks: front structure, periodic
wrap-around without decay, and monitor-point pressure periodicity. The complete
case configuration was then transferred onto original Fusion 360 geometry,
which was re-flagged, re-meshed, passed CONVERGE Studio case validation, and
run, closing the design loop.

The only result figure in this repository is the reference-case animation
above (and its MP4 export in [`media/videos/`](media/videos/)). No field
render or trace from the custom-geometry run is included, so the figures show
the vendor reference case, not the original geometry.

Wave speed was not extracted and compared against Chapman-Jouguet velocity, and
no grid-convergence study was possible under the cell-count constraint. Both
gaps are documented, and closing them is the first priority in
[`docs/10-future-work.md`](docs/10-future-work.md).

| | |
|---|---|
| ![Fusion 360 RDE geometry](media/images/fusion360-rde-geometry-mesh-v1.png) | ![CONVERGE boundary flagging](media/images/converge-case-setup-boundary-flagging.jpg) |
| *Unwrapped RDE geometry in Fusion 360* | *Boundary flagging and validation in CONVERGE Studio* |

## Design point

| Parameter | Symbol | Value | Basis |
|---|---|---|---|
| Combustor inner diameter | `d_c` | 75 mm | Above minimum diameter bound; SLS manufacturability |
| Annulus channel width | `Δ` | 2 mm | Minimum-width criterion, with margin |
| Detonation fill height | `h*` | 4.7 mm | Bykovskii fill-height correlation |
| Mean chamber pressure | `p_c` | 5 bar | Design point; local peaks exceed 100 bar |
| Plenum pressure | `p_p` | 10 bar | Choked-injector condition |
| Injector pressure ratio | `π_inj` | 2.0 | `p_p / p_c` |
| Wave multiplicity | `N_w` | 2–4 | Literature-based assumption |
| Propellants | | H2 / air | Matches reference case chemistry |

Full derivation and the criteria behind each value are in
[`docs/04-engine-design.md`](docs/04-engine-design.md); symbols are defined in
[`docs/00-nomenclature.md`](docs/00-nomenclature.md).

## Limitations

The reference-case result is qualitative. Wave speed was not extracted and
compared against the Chapman-Jouguet velocity, so the velocity deficit is
unknown, and no thrust or specific-impulse figure is reported. The 500,000
cell cap ruled out a grid-convergence study, so the solution is not shown to be
grid-independent. The domain is a two-dimensional unwrapped annulus, which
excludes mode switching, wave and injector interaction, and curvature effects.
Ignition is forced by a 2000 K inert argon region, so nothing is claimed about
ignitability in hardware. Air was used in place of oxygen to match the
reference case, which makes the mass-flow estimate in the sizing not strictly
consistent with the CFD. The full argument is in
[`docs/08-validation-and-limitations.md`](docs/08-validation-and-limitations.md).

## Numerical model

| Aspect | Selection |
|---|---|
| Governing system | Compressible Navier-Stokes with species transport and finite-rate chemistry |
| Combustion | SAGE detailed chemistry, LLNL hydrogen mechanism |
| Turbulence | RANS k–ε |
| Mesh | Cartesian cut-cell, base grid plus adaptive mesh refinement, 500,000 cell cap |
| Domain | Two-dimensional unwrapped annulus, periodic in the azimuthal direction |
| Ignition | 2000 K inert argon initialization region |

Equations and discretization are in
[`docs/05-numerical-methods.md`](docs/05-numerical-methods.md); the case
configuration is in
[`docs/06-simulation-setup.md`](docs/06-simulation-setup.md).

## Reproducing this

The CONVERGE case files are not included. The reference case belongs to
Convergent Science and was supplied under an academic license, and the
custom-geometry case is a derivative of it. The Fusion 360 model and its STL
export are not included either; only a screenshot of the geometry is. What the
documentation does record, enough to rebuild the setup from scratch in CONVERGE
Studio, is:

| Item | Recorded value | Where |
|---|---|---|
| Domain | Two-dimensional unwrapped annulus; injection along the bottom faceplate, outflow at the top, periodic pair on the azimuthal cut faces, symmetry planes front and back | [`docs/06`](docs/06-simulation-setup.md) |
| Boundaries | 17 named boundaries: `inflow`, `nozzles`, two faceplate segments, `outflow`, two periodic pairs, and the 2D symmetry pairs, with triangle counts visible in the flagging screenshot | [`docs/06`](docs/06-simulation-setup.md) |
| Physics | Compressible transient flow, RANS k-epsilon, SAGE detailed chemistry with the LLNL hydrogen mechanism (mech, therm, trans files from the LLNL archive), H2/air | [`docs/05`](docs/05-numerical-methods.md), [`docs/06`](docs/06-simulation-setup.md) |
| Mesh | Cartesian cut-cell base grid with adaptive mesh refinement, total under the 500,000 cell cap. The base grid size and AMR criteria were not recorded | [`docs/05`](docs/05-numerical-methods.md) |
| Ignition | Inert argon initialization region at 2000 K with a pre-ignition buffer region | [`docs/06`](docs/06-simulation-setup.md) |
| Time step | Not recorded. The docs note only that chemistry stiffness and the shock CFL constraint set it | [`docs/05`](docs/05-numerical-methods.md) |
| Output | Field data at order 100 frames per simulated window; monitor points at a high rate, kept as a separate stream | [`docs/06`](docs/06-simulation-setup.md) |
| Hardware | Four-core desktop; approximately four days of wall-clock time for the reference case, under an hour for coarse duct flows | [`docs/03`](docs/03-methodology.md), [`docs/07`](docs/07-results.md) |
| Software versions | CONVERGE Studio 3.1 for the early cases and 5.1 for the final case. The solver version was not recorded separately | [`docs/06`](docs/06-simulation-setup.md), this README |
| Geometry | 75 mm inner diameter, 2 mm channel width, 4.7 mm fill height, 5 bar chamber, 10 bar plenum | [`docs/04`](docs/04-engine-design.md) |

The [`logbook/`](logbook/research-journal.md) and
[`docs/timeline.md`](docs/timeline.md) record the order in which the cases
were built, from a bent pipe through a two-dimensional combustion box to the
reference case and then the custom geometry.

## Documentation

| Document | Contents |
|---|---|
| [`00-nomenclature.md`](docs/00-nomenclature.md) | Symbols, subscripts, abbreviations |
| [`01-background.md`](docs/01-background.md) | Detonation physics, ZND structure, engine concepts, operability criteria |
| [`02-objectives-and-requirements.md`](docs/02-objectives-and-requirements.md) | Objectives, numbered requirements, scope boundaries |
| [`03-methodology.md`](docs/03-methodology.md) | Toolchain, software access, development sequence, simulation practice |
| [`04-engine-design.md`](docs/04-engine-design.md) | Sizing criteria, applied values, injection, geometry |
| [`05-numerical-methods.md`](docs/05-numerical-methods.md) | Governing equations, chemistry, meshing, stability |
| [`06-simulation-setup.md`](docs/06-simulation-setup.md) | Domain, boundaries, initialization, instrumentation, output |
| [`07-results.md`](docs/07-results.md) | Reference case, custom geometry, assessment against objectives |
| [`08-validation-and-limitations.md`](docs/08-validation-and-limitations.md) | Verification against validation, supported and unsupported claims |
| [`09-lessons-learned.md`](docs/09-lessons-learned.md) | Failure log, technical and process conclusions |
| [`10-future-work.md`](docs/10-future-work.md) | Prioritized continuation, ordered by dependency |
| [`timeline.md`](docs/timeline.md) | Project chronology |

## Repository layout

| Path | Contents |
|---|---|
| [`docs/`](docs/) | Technical documentation, as indexed above |
| [`report/`](report/) | Written report, project scope, retrospective |
| [`logbook/`](logbook/) | Dated working notes, October 2025 to February 2026 |
| [`references/`](references/) | Annotated bibliography and links to the primary source papers |
| [`media/`](media/) | Animations, video, and CAD/CFD figures |
| [`LICENSE`](LICENSE) | CC BY 4.0 for the authored content |

The final presentation deck is not included in this repository.

## Toolchain

| Tool | Role |
|---|---|
| CONVERGE CFD (Studio 3.1 to 5.1) | Case setup, meshing and AMR, reacting-flow solver |
| Autodesk Fusion 360 | Combustor and fluidic-valve CAD, STL export |
| Tecplot | Post-processing and animation |
| ParaView | Early-phase post-processing |
| LLNL hydrogen mechanism | Detailed H2 oxidation chemistry |

## Sources

Sizing criteria derive from Bykovskii's correlations and Wolanski's survey of
detonative propulsion. Design plausibility was checked against two experimental
small-scale engines: the USAF/AFIT engine documented by Dechert and the DLR
hydrogen RDE reported at ISTS 2023. Full citations and annotations are in
[`references/`](references/).

## Acknowledgments

My mentor, an aerosciences engineer at an aerospace firm, provided mentorship,
CFD guidance, and help with periodic boundary conditions and post-processing.
Convergent Science provided academic licensing and the RDE reference case.

## License

The text, images, animations, video and CAD screenshots authored by Steven Kim
in this repository are licensed under
[Creative Commons Attribution 4.0 International](LICENSE) (CC BY 4.0). The
CONVERGE, Tecplot, Fusion 360 and other logos and trademarks that appear in
screenshots, the CONVERGE reference case, the LLNL mechanism, and the papers
cited in [`references/`](references/) are third-party material and are not
covered.
