# References

Sources underpinning the design criteria and methodology. The annotated
bibliography is in
[`annotated-bibliography.pdf`](annotated-bibliography.pdf). The two primary
experimental papers are not redistributed here; links to the publishers'
copies are given below.

Where these sources are applied: sizing criteria in
[`../docs/04-engine-design.md`](../docs/04-engine-design.md), detonation theory
in [`../docs/01-background.md`](../docs/01-background.md), and numerical
methodology in
[`../docs/05-numerical-methods.md`](../docs/05-numerical-methods.md).

## Primary sources

**Dechert, J. R. — *Development of a Small Scale Rotating Detonation Engine*, M.S. thesis, Air Force Institute of Technology, 2020**
[AFIT Scholar, etd/3212](https://scholar.afit.edu/etd/3212/) · [DTIC AD1102874](https://apps.dtic.mil/sti/trecms/pdf/AD1102874.pdf) (the DTIC link returned HTTP 403 when last checked; the AFIT Scholar copy is the reliable one)

Design, construction, and hot-fire testing of a small-scale RDE, with pressure,
thrust, and wave-stability measurements. The primary experimental evidence that
small-scale RDEs sustain rotating detonation, and the closest analogue to the
design class used here.

**Armbruster, W., Hermannsson, B. S., Börner, M., Martin, J., Hardi, J. — *Experimental Investigation of a Small-Scale Oxygen-Hydrogen Rotating Detonation Combustor*, 34th International Symposium on Space Technology and Science (ISTS), Kurume, 2023**
[elib.dlr.de/198217](https://elib.dlr.de/198217/) · [PDF](https://elib.dlr.de/198217/1/ISTS%20Exp%20Investig%202023-a-2-05.pdf)

Hydrogen-fueled small RDE test campaign examining the effect of pressure and
mass flow on wave stability. Informed the geometry-determination approach and
the choice of hydrogen as fuel.

## Supporting sources

**Wolanski, P. — *Detonative Propulsion*** · [bibliotekanauki.pl/articles/950134](https://bibliotekanauki.pl/articles/950134)

Survey of detonation propulsion history and concepts, covering PDE, ODWE, and
RDE configurations and the thermodynamic case for pressure-gain combustion.
Source of the empirical sizing relations used, together with Bykovskii's
correlations, in [`../docs/04-engine-design.md`](../docs/04-engine-design.md).

**Anderson, J. D. — *Computational Fluid Dynamics: The Basics with Applications***

Governing equations and discretization fundamentals underpinning the CFD
methodology.

**Truong, T. Q. & Nguyen, N.-T. — *Simulation and Optimization of Tesla Valves***

CFD optimization of check valves with no moving parts. Background for the
fluidic injector-protection concepts explored during the design phase.

## Additional resources

- [LLNL archived hydrogen reaction mechanism](https://combustion.llnl.gov/archived-mechanisms/hydrogen), providing the mech, therm, and trans data for the SAGE solver
- [Purdue Tesla-valve-inspired RDE injector patent announcement](https://www.purdue.edu/newsroom/2024/Q1/patented-purdue-design-inspired-by-tesla-valve-could-improve-performance-of-rotating-detonation-engines/)
- CONVERGE CFD official tutorials and user forums
