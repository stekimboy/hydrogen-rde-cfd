# 1. Background

## Deflagration and detonation

Nearly every propulsion system in service today, from rockets to turbofans to
piston engines, burns propellant by deflagration: a subsonic flame front that
propagates by thermal and species diffusion and consumes the mixture at roughly
constant pressure. Detonation is a fundamentally different combustion mode. A
shock wave coupled to a reaction zone propagates through the mixture at
supersonic speed, on the order of 2 km/s for hydrogen and air, consuming
propellant almost instantaneously and producing a large local pressure rise.

The distinction matters thermodynamically. A deflagrating combustor approximates
constant-pressure heat addition, and the ideal cycle built on it is the Brayton
cycle. A detonating combustor approximates constant-volume heat addition, whose
ideal analogue is the Humphrey cycle. For the same heat release, constant-volume
addition raises pressure across the combustor rather than losing it, so more of
the released energy is available as work. This is the pressure-gain combustion
argument, and it is the reason detonative propulsion has been pursued for
decades despite its practical difficulty. Wolanski's survey traces that history.

## Detonation structure

The one-dimensional model of a detonation is the ZND structure: a leading shock
compresses and heats the mixture to the von Neumann state, an induction zone
follows in which reaction has not yet begun in earnest, and a reaction zone
behind it releases heat and drives the shock forward. The self-sustaining
solution is the Chapman-Jouguet condition, in which the flow behind the reaction
zone is exactly sonic relative to the wave. The corresponding velocity `D_CJ` is
a property of the mixture and its initial state, and it is the natural reference
against which any observed wave speed `D_w` is compared.

Real detonations are not one-dimensional. The front is a cellular structure of
interacting transverse waves and triple points, and the characteristic size of
that structure is the detonation cell size `λ`. Because `λ` sets the length
scale over which a detonation can be confined and still survive, essentially
every geometric criterion for RDE design is expressed as a multiple of it. Cell
size falls with increasing pressure and rises with dilution, which is why an
oxygen-fed engine can be built smaller than an air-fed one at the same pressure.

## Detonation engine concepts

Three families of detonation engine have been studied in depth.

Pulse detonation engines fill a tube, detonate it, and purge it cyclically. The
configuration is mechanically simple, but thrust is intermittent, the valving
problem is severe, and each cycle must re-initiate the detonation.

Oblique detonation wave engines stabilize a standing detonation on a wedge. They
are useful only at hypersonic flight speeds, where the incoming flow already
supplies the required conditions.

Rotating detonation engines sustain one or more detonation waves travelling
continuously around an annular channel while fresh propellant is injected
axially behind each wave. Initiation happens once, thrust is quasi-steady, there
are no moving parts, and the engine operates from static conditions. This
combination is why the RDE has become the dominant research configuration, with
active programs at AFRL, NASA, DLR, and several universities.

## RDE operating principle

An RDE combustor is an annular gap between two cylinders. Propellant enters
axially through a faceplate of small orifices. After an ignition transient, a
detonation wave establishes itself in the azimuthal direction and travels around
the annulus at a large fraction of `D_CJ`, consuming the fresh mixture layer
that has accumulated since the previous wave passage. That layer is roughly
triangular in profile, thickest just ahead of the oncoming wave and thinnest
immediately behind the last one. Burned gas expands and exhausts axially,
producing thrust.

The engine is therefore a race between two processes: refill and wave arrival.
If the fresh layer has not reached sufficient height by the time the wave
returns, the wave is under-supplied and decays. Most of the operability
literature is a description of the conditions under which the race is won.

## Operability criteria

Four parameters govern wave survival. Bykovskii's correlations and the
small-scale test campaigns catalogued in [`../references/`](../references/) are
the primary sources; their application to this design is worked through in
[`04-engine-design.md`](04-engine-design.md).

**Fill height `h*`.** The fresh mixture layer must reach a critical height
before the wave arrives. Bykovskii expresses this as a multiple of the cell
size, conventionally on the order of `h* ≈ 12λ`. Below that height the wave
decays into a deflagration.

**Channel width `Δ`.** The annular gap must exceed a minimum width, likewise
tied to `λ`, for the cellular structure to fit. Too narrow a channel quenches
the detonation against the walls.

**Injector pressure ratio `π_inj`.** The plenum must stay well above mean
chamber pressure, conventionally by a factor of about two, so that the injectors
remain choked. Flow at the orifice throat reaches Mach 1, which fixes the mass
flux independently of downstream pressure and makes the injector behave as a
passive one-way valve against the back-pressure each passing detonation drives
into the manifold.

**Wave multiplicity `N_w`.** Depending on mass flow and geometry, one or several
waves may coexist, and an engine may switch modes during a run. Predicting the
count in advance remains an open research problem, so a range of two to four was
assumed for the mass-flow bookkeeping in this study.

## Rationale for a computational study

Detonation experiments are violent, expensive, and demanding to instrument.
Computational fluid dynamics solves the governing equations numerically, adding
species transport and finite-rate chemistry to the compressible Navier-Stokes
system, and is the standard first tool for RDE design studies in professional
research groups. The governing equations and the numerical treatment used here
are set out in [`05-numerical-methods.md`](05-numerical-methods.md). Anderson's
text and the CONVERGE documentation formed the methodological basis.

The scope this study set out to cover, and the constraints it worked under, are
stated in
[`02-objectives-and-requirements.md`](02-objectives-and-requirements.md).
