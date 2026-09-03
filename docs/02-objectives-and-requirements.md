# 2. Objectives and Requirements

The objectives below were fixed at the outset and are recorded in
[`../report/project-scope.md`](../report/project-scope.md). They are restated
here because they determine what the study set out to demonstrate, and
therefore how the results in [`07-results.md`](07-results.md) should be read.

## Primary objective

Complete the early-phase design loop for a small-scale hydrogen rotating
detonation engine, from literature-derived sizing through geometry definition to
a running reacting-flow CFD case, and establish whether the resulting
configuration sustains a rotating detonation in simulation.

## Supporting objectives

1. Reach working competence in a production CFD package to a standard
   sufficient for a reacting, compressible, transient case.
2. Develop the geometry in a parametric CAD environment and carry it into the
   solver without topology defects.
3. Establish, from the experimental literature, the geometric and injection
   conditions that govern whether a rotating detonation survives.
4. Evaluate injector configurations capable of delivering propellant against
   detonation back-pressure.
5. Build the ability to extract quantitative design criteria from primary
   research publications.

## Requirements

Requirements that constrained the design, separated by origin.

| ID | Requirement | Origin |
|---|---|---|
| R1 | The annulus shall satisfy the Bykovskii minimum fill-height criterion at the design pressure | Literature ([`references/`](../references/)) |
| R2 | The channel width shall exceed the minimum width criterion for the design mixture | Literature |
| R3 | The injector pressure ratio shall be sufficient to hold the orifices choked at mean chamber pressure | Literature |
| R4 | The combustor shall be manufacturable by metal SLS | Design intent |
| R5 | The computational domain shall not exceed 500,000 cells | License constraint |
| R6 | The case shall run to completion within days, not weeks, on four cores | Hardware constraint |
| R7 | Chemistry shall be resolved with a finite-rate mechanism rather than a tabulated model | Fidelity requirement |

## Consequences of the constraints

R5 and R6 are the binding constraints and they propagate through every later
decision. Together they rule out a three-dimensional annulus, which forces the
unwrapped two-dimensional reduction described in
[`04-engine-design.md`](04-engine-design.md), and they rule out a
grid-convergence study, which is the principal gap in the validation argument
set out in
[`08-validation-and-limitations.md`](08-validation-and-limitations.md).

R7 pulls in the opposite direction from R5 and R6, since detailed chemistry is
expensive. The resolution was adaptive mesh refinement: spend cells only where
gradients demand them, and accept a coarse base grid everywhere else.

## Out of scope

No hardware was built and no experimental validation was performed. Thrust and
specific impulse were not computed. The fluidic valve concepts in
[`04-engine-design.md`](04-engine-design.md) were designed but not simulated;
the modeled configuration uses plain choked orifices.
