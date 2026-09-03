# 8. Validation and Limitations

A simulation result is only as strong as the argument that it corresponds to
something real. This section states what that argument covers here and where it
stops.

## Verification and validation

The two terms are distinct and worth separating, since this study achieved one
and not the other.

**Verification** asks whether the equations are being solved correctly. It is
addressed here by the staged development sequence in
[`03-methodology.md`](03-methodology.md), in which each case exercised one new
capability against expected behavior before the next was attempted, and by the
qualitative checks in [`07-results.md`](07-results.md). It is not addressed by a
grid-convergence study, which is the standard instrument and which the cell cap
precluded.

**Validation** asks whether the correct equations are being solved for the
physical system, and is answered by comparison against experiment. No
experimental data was generated, and no quantitative comparison was made against
the published campaigns in [`../references/`](../references/). This study is
therefore unvalidated in the formal sense.

## What the results support

The reference case reproduces a sustained rotating detonation with the expected
front structure, periodic wrap-around, and monitor-point periodicity. That
supports three claims:

1. The case setup, chemistry, and boundary treatment are self-consistent and
   capable of producing the target phenomenon.
2. The unwrapped periodic reduction transmits a detonation without artificial
   decay, so the geometric idealization is not by itself destroying the physics.
3. The workflow transfers to independent geometry, since the same configuration
   was applied to CAD it was not built for.

## What the results do not support

**No quantitative performance claim.** Wave speed was not extracted and compared
against `D_CJ`, so the velocity deficit is unknown. Without it there is no
calibrated measure of how well-resolved the detonation is, and no basis for
thrust or specific-impulse figures. None are reported.

**No grid independence.** Under a 500,000 cell cap with AMR absorbing most of
the budget at the front, the solution cannot be shown to be insensitive to
resolution. Under-refinement smears a detonation front and depresses its speed,
so a result that looks qualitatively right may still be quantitatively wrong in
a consistent direction.

**No three-dimensional effects.** The unwrapped two-dimensional domain discards
wave and injector interaction, mode switching between wave counts, slapping
waves against the outer wall, and any azimuthal curvature effect. These are not
peripheral; mode switching in particular is a defining operational
characteristic of real RDEs and cannot appear in this domain by construction.

**No ignition claim.** Ignition is forced by a 2000 K inert region, which
establishes that the geometry sustains a detonation once one exists. Whether the
engine could be ignited in hardware is a separate question that this setup is
not constructed to answer.

**Oxidizer substitution.** Air replaced pure oxygen, an intentional
simplification matching the reference case chemistry and reducing stiffness. It
shifts the cell size, the detonation velocity, and the fill-height requirement
relative to the oxygen-fed bookkeeping used in the mass-flow estimate in
[`04-engine-design.md`](04-engine-design.md), so those two parts of the study
are not strictly consistent with one another.

**Turbulence closure.** RANS k–ε is a budget-driven choice. Its influence on
front propagation is limited, but it does not resolve the mixing in the fill
region that determines local equivalence ratio ahead of the wave.

## Sensitivity of the sizing

The design values in [`04-engine-design.md`](04-engine-design.md) inherit the
uncertainty of the correlations they come from. The fill height is the weakest
link: it derives from a cell size taken from correlation rather than
measurement, and the Bykovskii relation itself carries substantial experimental
scatter. The channel width was deliberately sized well above its minimum so that
an optimistic `h*` would not immediately invalidate the geometry, but that is
margin, not verification.

## Treatment of solver output

Throughout the project, solver output was treated as a prediction to be
interrogated rather than as ground truth. The animations in
[`../media/`](../media/) are evidence that the modeled configuration behaves as
an RDE should behave under the stated assumptions. They are not evidence that a
physical engine built to these dimensions would run.
