# 10. Future Work

Ordered by dependency: each item is worth more once the ones above it are done.
The gaps these address are stated in
[`08-validation-and-limitations.md`](08-validation-and-limitations.md).

## 1. Wave speed against Chapman-Jouguet velocity

Extract `D_w` from monitor-point arrival times and compare against `D_CJ`
computed for the mixture and initial state. The velocity deficit `D_w / D_CJ` is
the standard health metric in the RDE literature, and it converts the present
qualitative result into a quantitative one. It is also the cheapest remaining
item, since it requires post-processing of data the existing runs already
produce rather than new solves.

This should come first because it calibrates everything after it. A large
deficit would indicate under-resolution and would change how the grid study
below is interpreted.

## 2. Grid-convergence study

Run the unwrapped domain at a sequence of base grid resolutions and track wave
speed and peak pressure against cell count. Without this there is no basis for
claiming the solution is resolution-independent, and under-refinement biases
detonation speed in a consistent direction rather than randomly.

This requires lifting the cell cap or accepting a smaller domain, so it depends
on compute access rather than on method.

## 3. Wave multiplicity against mass flow

Sweep injected mass flow and record the number of co-rotating waves that
establish. The two-to-four assumption used for bookkeeping in
[`04-engine-design.md`](04-engine-design.md) is an unverified input to the
sizing, and multiplicity is known to depend on mass flow and geometry in ways
that are not predictable in advance.

## 4. Three-dimensional annulus

Replace the unwrapped domain with a true annular chamber. This recovers
azimuthal curvature, wall interaction, and the possibility of mode switching,
none of which the two-dimensional reduction can represent. It is the largest
single increase in cost in this list and should not be attempted before the grid
study establishes what resolution is actually required.

## 5. Injector-resolved geometry

Resolve the individual injector orifices rather than treating the faceplate as a
distributed inlet. This is what makes the choked-injection assumption testable
in simulation instead of imposed, and it is a precondition for evaluating the
fluidic valve concepts.

## 6. Fluidic valve evaluation

Simulate the Tesla-type and original cavity-blockage valve concepts described in
[`04-engine-design.md`](04-engine-design.md) as standalone components, measuring
diodicity in isolation before integrating either into the faceplate. Both were
designed and neither was simulated.

## 7. Performance bookkeeping

Compute thrust and specific impulse from outlet momentum flux and compare
against the small-scale engines documented in
[`../references/`](../references/). This is the point at which the study becomes
comparable to published experimental work, and it depends on essentially
everything above it being in place.

## Hardware direction

A thrust-test stand using a linear rail and load cell was considered as a route
to experimental validation. Any such path depends on resolving the manufacturing
question implied by requirement R4 in
[`02-objectives-and-requirements.md`](02-objectives-and-requirements.md), and on
the safety infrastructure that hydrogen detonation testing requires. It is noted
as a direction rather than a plan.
