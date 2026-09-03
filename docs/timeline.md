# Project Timeline

October 2025 to March 2026. Dated working notes are in
[`../logbook/research-journal.md`](../logbook/research-journal.md).

| Date | Milestone | Phase |
|---|---|---|
| Oct 12, 2025 | Obtained the Explore license. First installations, geometry imports, and tutorial attempts. | Setup |
| Oct 15–21 | Injection and backflow research: Tesla-valve literature, the Purdue RDE injector patent, a venturi-assist concept. Designed an original fluidic valve in Fusion 360. | Design research |
| Oct 23–24 | First flow cases, a 90° bent pipe then a simple duct. Resolved STL normal errors, the boundary and region distinction, species setup, and cell-cap errors. First successful run and visualization. | Tool learning |
| Oct 25–27 | Runtime tuning from 9 hours to under 1 hour. Established the two-dimensional reduction. Imported a three-port cylinder and began mechanism, thermodynamic, and transport data imports. | Tool learning |
| Nov 1–2 | First hydrogen and oxygen combustion case: LLNL mechanism, SAGE solver, AMR enabled, 2000 K argon initialization region. | Chemistry |
| Nov 3–4 | Compute reality check. One run projected roughly three months, another exhausted disk capacity. Analyzed partial-combustion output and configured cross-section views. | Chemistry |
| Nov 15 | Monitor points working, producing the first quantitative traces. Began pursuing an academic license through an institutional route. | Instrumentation |
| Nov 19 | RDE design research; converged toward a design in the 5 bar chamber-pressure class. | Design |
| Dec 1–7 | Analytical sizing against the Bykovskii and Wolanski bounds, the choked-injector criterion, and a two-to-four wave multiplicity assumption. Corrected the mass-flow error. Settled on 75 mm inner diameter, 2 mm channel, 4.7 mm fill height, 5 bar. | Design |
| Jan 29, 2026 | Licensing discussion covering license tiers; learned of the official RDE reference case. | Licensing |
| Feb 1–18 | Academic license granted following correspondence, calls, and a signed agreement. | Licensing |
| Feb 19 | Reference RDE case run to completion, approximately four days of wall-clock time. Tecplot animation confirmed a sustained rotating detonation. | Simulation |
| Feb 25 | Custom geometry: modified RDE modeled in Fusion 360, case setup transferred, periodic boundary conditions applied, simulation run. | Simulation |
| Mar 9 | Written report and summary presentation completed (the presentation is not included in this repository). | Reporting |

## Effort distribution

Total effort was approximately 70 to 90 hours. The largest single allocation was
case setup rather than geometry, analysis, or waiting on solvers, which is
discussed in [`09-lessons-learned.md`](09-lessons-learned.md).

Roughly six weeks of the schedule were spent obtaining software access. That
sequence runs from the first vendor contact on October 12 to the academic
license grant in mid-February, overlapping the technical work rather than
blocking it, but it determined which cases were runnable at each stage.
