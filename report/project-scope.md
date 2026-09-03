# Project Scope

The scope defined at the start of the project, retained as the reference record
of what the work set out to do. The objectives are carried forward, with the
constraints that shaped them, in
[`../docs/02-objectives-and-requirements.md`](../docs/02-objectives-and-requirements.md).

## Premise

Rotating detonation engines are studied almost entirely by national laboratories,
university research groups, and large aerospace firms. The concept is
demanding: detonation waves are fast, violent, and difficult to instrument, and
whether a given annulus will sustain one is not answerable from first principles.
It remains an open research area rather than a settled engineering practice.

The premise of this project was that the early-phase design loop for such an
engine, from literature-derived sizing through geometry to reacting CFD, is
reproducible independently given access to a production solver, and that
attempting it would expose the practical constraints that published results tend
to omit.

## Aim

To study rotating detonation engines in depth, covering the physics, the
mechanics, and the conditions required to sustain a propagating detonation wave,
and to apply that understanding to an original engine geometry evaluated in
computational fluid dynamics.

## Planned work

1. Reach working competence in CONVERGE CFD sufficient for an accurate reacting
   simulation.
2. Develop the engine geometry parametrically in Fusion 360.
3. Establish, from the research literature, the conditions that sustain a
   detonation wave.
4. Investigate valve configurations specific to rotating detonation engines,
   capable of delivering fuel against combustion back-pressure.
5. Build the ability to read and apply dense technical publications on RDE
   design and mathematical optimization.

## Planned deliverables

At minimum, a three-dimensional model of the engine geometry and a flow
simulation of that geometry under operating conditions, delivered as animations,
graphs, and supporting data.

## Background at the outset

Prior hands-on work with solid rocket motors and small engine repair. No prior
experience with production-grade CFD; closing that gap was treated as part of
the project rather than a prerequisite to it.

## Anticipated difficulty

The physics is coupled and stiff, the geometry criteria are empirical rather
than derived, and the software is specialized. The principal risk identified in
advance was the depth of the technical literature required to extract usable
design criteria.

In the event, the binding constraint proved to be neither the physics nor the
literature but software licensing and available compute, which is documented in
[`../docs/03-methodology.md`](../docs/03-methodology.md) and
[`../docs/09-lessons-learned.md`](../docs/09-lessons-learned.md).

## Conduct

All work original. Any confidentiality questions arising during the project to
be resolved within ethical and legal guidelines.

## Resources

No travel or material costs. Software licensing emerged as the real resource
constraint.
