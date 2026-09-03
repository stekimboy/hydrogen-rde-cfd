# Retrospective

Written at the close of the project. Technical conclusions are in
[`../docs/09-lessons-learned.md`](../docs/09-lessons-learned.md); this is an
assessment of how the work went against what was planned in
[`project-scope.md`](project-scope.md).

## Plan against outcome

The project was planned as a sequence: model an engine, configure the solver,
run it, analyze the results. That sequence turned out to describe perhaps a
quarter of the actual effort.

The first obstacle was not technical. Obtaining usable access to CONVERGE took
six weeks, a dead end through an institutional route requiring months of process
and on-site access, and finally a licensing call and a signed home-use
agreement. The path that worked was direct contact with the vendor on a second
approach. I would not describe it as reliably repeatable.

The second was the distribution of effort. I had assumed simulation work is
spent simulating. It is spent in case setup: boundary assignments, species
definitions, mesh limits, geometry repair. Errors there do not degrade results,
they prevent the run from starting, which makes them unmissable but slow to
localize. Most were resolved through official documentation and a considerable
amount of trial and error.

The third was that the physics imposed its own reductions. Pure oxygen gave way
to air, a three-dimensional annulus gave way to an unwrapped two-dimensional
domain, and a grid-convergence study was ruled out entirely by the cell cap.
Each was individually defensible and collectively they narrowed the achievable
claim considerably, which is set out honestly in
[`../docs/08-validation-and-limitations.md`](../docs/08-validation-and-limitations.md).

## What the work produced

A sustained rotating detonation reproduced in the reference case and confirmed
against three independent qualitative checks, and a complete case configuration
transferred onto original geometry. That closes the design loop the project set
out to close.

It does not produce a validated engine, and the documentation is written to make
that distinction rather than blur it. The single largest missed opportunity is
quantitative: wave speed was never extracted and compared against the
Chapman-Jouguet velocity, which is inexpensive relative to everything else that
was done and would have converted a qualitative result into a measured one. It
is first on the list in
[`../docs/10-future-work.md`](../docs/10-future-work.md) for that reason.

## What I would change

Two things, both scheduling rather than technique.

The vendor's official training material was found too late to use properly.
Months of trial and error would have compressed substantially had it been the
starting point rather than a late discovery.

Contact with researchers already running RDE work in CONVERGE came at the point
where there was no schedule left to exploit it. The guidance that did arrive,
particularly on periodic boundary conditions, resolved problems that
documentation had not, which suggests the return on seeking it earlier would
have been high.

More fundamentally, the cell cap was identified in the first month but its
consequences were absorbed late. It dictated two-dimensionality, precluded grid
convergence, and therefore bounded the strongest claim the project could support
before most of the work was done. Recognizing that earlier would have redirected
effort toward the quantitative measurements that were achievable rather than
toward fidelity that was not.

## Assessment

The methodological objective was met. Working through the full loop on a
production solver, under real licensing and compute constraints, produced a
concrete understanding of where the difficulty in this class of problem actually
sits, which is in case setup and in the gap between a result that looks correct
and one that has been shown to be correct.

The technical understanding transferred as intended. Choked injector orifices,
RANS closure and its limits, adaptive refinement as a budget mechanism, and the
distinction between verification and validation were all reached by needing them
rather than by reading about them.
