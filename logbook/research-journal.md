# Research Journal

Dated working notes from the project, October 2025 through February 2026.

---

## 10/12/2025 — Software access

Contacted Convergent Science about the free Explore license. Downloaded and
unlocked the software the same day, then trialed basic geometry imports,
investigated mesh errors, and attempted a first simulation. The tutorial series
I started from turned out to be outdated, and no run succeeded. Collected
background research on fluidic valve optimization, including a CFD study of
Tesla valves and the CONVERGE applications material.

## 10/15/2025 — Injection problem

Working on how to keep injecting fuel against the back-pressure of the
combustion chamber. One idea beyond fluidic valves: redirect part of the exhaust
into a manifold and use the resulting low-pressure, high-velocity gas to draw
fuel in through the venturi effect. Likely negligible or negative benefit once
the added complexity is accounted for. Found Purdue's patent announcement for a
Tesla-valve-derived RDE injector, which confirms the problem is a real one.

## 10/21/2025 — Original valve design

Designed a fluidic valve of my own in Fusion 360. Instead of using the residual
back-pressure of the flow to impede itself, which is the Tesla approach, reverse
flow runs into an enclosed cavity with a permanent blockage. If it behaves as
intended, diodicity should be high.

## 10/23/2025 — First attempts

Restarted learning the software step by step rather than jumping straight to
combustion. Modeled a simple 90° bent pipe in Fusion and imported it for plain
airflow. Fixed every issue flagged in case setup, but the run still failed,
probably on boundary or species assignment for air. Did successfully import the
STL and repair a surface-normal orientation error, which is clearly going to be
routine from here.

Second session: identified the actual mistake, which was the difference between
boundaries, meaning surfaces, and regions, meaning the fluid volumes themselves.
Fixed the mech.dat errors and defined air properly. New problem: the license
mesh cell cap is already binding on a trivial part. This will only get worse and
may force two-dimensional simulations.

## 10/24/2025 — First success

Solved the mesh problem through grid-control settings, reducing the base grid to
an estimated 2 to 3 million cells. The new lesson is computing power. Even a
bare pipe carrying plain air has been running for 4 to 5 hours. Next step is
learning to reduce a 3-D STL to a 2-D cross-section that combustion can be run
on, since staying at rock-bottom mesh sizes will only produce error.

## 10/25/2025 — Runtime tuning

The overnight run finished in 9 hours. Re-ran at 6. Learned ParaView to inspect
the outputs. The first run had written only 3 still frames, so I re-ran with
settings for roughly 100 frames over the simulated second. ParaView was very
slow until the file time-frames were compressed, after which rendering was fast.
From the visual data, pressure equalizes in 0.07 s, so the next run simulates
only 0 to 0.07 s at a higher output rate. Third run finished in under an hour.
Note for later: ParaView requires consecutive file names, so a script should
rename outputs automatically.

## 10/26/2025 — Two-dimensional reduction

Found a discussion thread on 2-D simulation in CONVERGE. The compute savings are
substantial. Open question is whether the reduction is valid for more than valve
studies, since the real engine is obviously not two-dimensional.

## 10/27/2025 — Toward combustion

Imported an STL for a very simple rocket geometry: a cylinder with three holes,
two for oxygen and hydrogen and one for exhaust. Now learning to import
mech.dat, therm.dat, and trans.dat, the chemical property data the simulation
needs, and to enable the combustion options in case setup.

## 11/1–2/2025 — First combustion case

Built a hydrogen and oxygen detonation case. Downloaded a hydrogen reaction
mechanism from the LLNL archive and loaded it with SAGE as the chemistry solver.
Could not work out initialization regions, and the events system is too involved
for this stage, so the workaround is to set the inner start region to inert
argon at 2000 K. Ignition is then effectively guaranteed when the oxygen and
hydrogen meet. Geometry is crude; the inlets are not even angled toward each
other. Mesh capped at 500,000 cells, with adaptive mesh refinement enabled for
the first time.

Later the same evening: canceled the run, which would have produced 3.5 million
output frames. Not enough disk, not viable. Restarted with fewer output files.

## 11/3/2025 — Compute reality

Checked the running simulation: 0.6% complete after a full day, a projected
three-month runtime. Terminated it and inspected the partial output in ParaView.
The gases appear to be in contact but there is no sign of combustion. Re-running
at only 1000 cells, about 3 hours, purely to see any combustion at all; accuracy
will be poor. Outsourcing compute would cost hundreds to thousands of dollars.
Also began inquiries about an institutional academic license.

## 11/4/2025 — First signs of ignition

The run stopped at roughly 60% on disk space, but produced enough to inspect.
Based on temperature it likely combusted momentarily and then died out. Pressure
is harder to read but looks consistent with that. Good enough to justify moving
to more complex geometry and a proper ignition setup instead of the 2000 K
start-temperature workaround. Configured cross-section views in ParaView. Next:
build an actual RDE geometry in Fusion and import it.

## 11/15/2025 — First useful graphs

Re-ran basic simulations to learn monitor points and useful graphing, and got
the first working monitor-point output today on a basic tube. Correspondence on
the academic license continues. Next: re-evaluate the fluidic valve, possibly
returning to my original design, and work through the relevant university
publications.

## Mid-November 2025 — Design direction

Working through the Bykovskii and Wolanski empirical formulas for the minimum
geometric bounds of an RDE and for what it takes to sustain the wave. Initial
mass-flow estimate for stoichiometric hydrogen and oxygen comes out to 0.7 g/s,
which is implausibly small for a chamber of this size and needs re-checking.
Current design point is 6 bar effective chamber pressure, with detonation peaks
above 100 bar but only briefly, against a 10 bar plenum. The 4 bar difference is
intentional, to physically drive fuel into the chamber. A Tesla valve would have
to be designed around that difference.

Tried running a detonation wave through a simple toroid, which failed to ignite,
probably because of my inexperience merging multiple boundaries. Separately, an
idea for a torus chamber with exhaust at the top end, giving a more constricted
detonation volume and possibly better reliability; the airflow math follows from
torus volume and wave transit time. Found the DLR paper, which takes a different
approach to geometry determination.

The institutional license route is out, as it requires months of process. The
Explore tier will have to suffice at low cell counts. Also salvaged a linear
rail from an old 3-D printer for a future thrust-test stand with a load cell.

## 12/1–7/2025 — Sizing

Leaning toward 5 bar rather than 6. Wave multiplicity is very hard to predict,
so assuming two to four waves for the mass calculations. Worked out what choking
an injector means: flow at the orifice reaches Mach 1, which makes reverse flow
naturally difficult and causes the injector to act as a one-way valve, with the
plenum at roughly twice chamber pressure.

Re-derived the numbers, and the earlier 0.7 g/s mass flow was indeed very wrong.
After reconsidering machinability for metal SLS, settled on a 75 mm inner
diameter chamber, 2 mm channel width, and 4.68 mm detonation height. The chamber
is physically extended beyond that height, but at 5 bar the detonation height is
what governs. Possible breakthrough while re-plugging values with assumed
constants, density around 6.25 and velocity around 500 from a modified Wolanski
equation, though this needs verification.

## 1/29/2026 — Licensing discussion

Call with Convergent Science covering the differences between academic,
commercial, and Explore licenses. Learned that an RDE reference case already
exists in CONVERGE. This is significant: it is two-dimensional rather than full
three-dimensional, so the cell count is low, and its case setup can be applied
to my own design. Also received pointers to university groups doing
CONVERGE-based RDE research.

## 2/1–18/2026 — License granted

Academic license obtained through support correspondence, calls, and a signed
agreement.

## 2/19/2026 — First RDE simulation

Ran the RDE reference case to completion, about four days of compute. Compared
the results and studied how the case setup handles the problems I had been
fighting. This is the template.

## 2/25/2026 — Custom geometry

Modeled my modified RDE, applied the reference case setup to it, and ran the
simulation, with periodic boundary conditions closing the unwrapped annulus.
