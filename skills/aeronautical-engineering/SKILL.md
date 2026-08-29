---
name: aeronautical-engineering
description: Aeronautical and aerospace engineering analysis with authoritative citations — airfoil and wing aerodynamics, lift/drag/moment build-up, propeller and EDF thrust, weight and balance, CG and static margin, V-n envelopes, and airframe load factors. Use when sizing a wing, computing lift or drag, analysing an airfoil or aerofoil section, checking CG or static margin, building a V-n diagram, sizing a propeller or ducted fan, doing a weight-and-balance or mass-properties roll-up, or evaluating a UAS or light aircraft airframe against FAA Part 23/107, NASA, or ASTM F38 standards.
license: MIT
metadata:
    author: Griffing Technology LLC
    discipline: Aeronautical Engineering
    ncees_alignment: "NONE — no NCEES PE discipline exists for aeronautical engineering. See 'Licensure standing' below."
    sponsoring_society: AIAA (American Institute of Aeronautics and Astronautics)
    version: 0.1.0
---

# Aeronautical Engineering

Hard-engineering analysis for aircraft and unmanned aircraft systems, with every
method traceable to a cited authority.

## Licensure standing — read this first

**There is no NCEES PE examination in aeronautical or aerospace engineering.**
The NCEES PE catalog contains 23 disciplines [REF-NCEES-001] and aeronautical is
not among them. Practitioners who require licensure in this field normally sit
the PE Mechanical exam — most often the *Thermal and Fluid Systems* or *Machine
Design and Materials* module [REF-NCEES-003] — or a state's Structural or
Electrical exam, depending on the work.

Do not describe this skill, or any output of it, as "NCEES-aligned" or
"PE-aligned." It is aligned instead to:

* **Regulatory authority** — FAA, under 14 CFR [REF-FAA-001, REF-FAA-002, REF-FAA-003]
* **Technical standards** — NASA technical standards [REF-NASA-001, REF-NASA-002]
  and ASTM Committee F38 for UAS [REF-ASTM-001]
* **Discipline society** — AIAA [REF-SOC-007]

State this standing whenever a user asks about licensure, stamping, or
certification of aeronautical work. A PE stamp on aeronautical analysis comes
from a licensee in an adjacent discipline accepting responsibility, not from an
aeronautical licence, because none exists.

## Non-negotiable practice rules

These bind every calculation this skill produces.

1. **Units are imperial-primary with metric in parentheses.** Mass in `lbm (kg)`,
   force in `lbf (N)`. Never write a bare "lb" where mass and force could be
   confused. Airspeed in **knots (kt)**, with m/s in parentheses where a
   calculation needs SI. Never mph or km/h for airspeed.
2. **Every number carries its source.** A figure is either computed here from
   stated inputs, or cited to a REF-ID in `REFERENCES.md`. There is no third
   category. Never present a remembered constant as a derived result.
3. **State the flow regime before choosing a method.** Reynolds number, Mach
   number, and whether the flow is attached. Thin-airfoil theory, lifting-line,
   and panel methods each have a validity envelope; naming it is part of the
   answer.
4. **Assumptions are labelled inline, not buried.** If a wire diameter, a
   mass, or an airfoil polar is assumed rather than measured, say so on
   every run — an assumption that stops being restated hardens into a fact
   by repetition.
5. **Never fabricate a polar, a coefficient, or a standard designation.** If
   $C_{l,\max}$ for a given section at a given Re is not known from a cited
   source, say it is not known and name what would establish it (XFOIL run, wind
   tunnel data, NTRS report [REF-NASA-003]).

## Method selection

Read the relevant reference file before working a problem in that area.

| Problem | Read |
| --- | --- |
| Load factors, V-n envelope, factors of safety, joint margins | `references/loads-and-factors.md` |
| Lift, drag, moment build-up; airfoil and finite-wing aerodynamics | `references/aerodynamics.md` |
| Weight & balance, CG, static margin, mass-properties roll-up | `references/weight-and-balance.md` |
| Propeller, ducted fan / EDF, and thrust-to-weight sizing | `references/propulsion.md` |

## Core workflow

### 1. Establish the aircraft class and governing rule

Determine, and state, which regulatory basis applies before any analysis:

* **Civil sUAS under 55 lbm (25 kg)** — 14 CFR Part 107 [REF-FAA-001]. Note that
  Part 107 governs *operations*; it imposes no structural certification basis, so
  structural criteria must be adopted deliberately (see step 3).
* **Normal-category airplane** — 14 CFR Part 23 [REF-FAA-002], performance-based
  since the 2017 restructure.
* **Certification pathway** — 14 CFR Part 21 [REF-FAA-003] distinguishes type
  certification from experimental and special airworthiness.

If the aircraft is an sUAS built for a specific operation rather than for
certification, say so plainly: the design is being held to a *self-adopted*
criteria set, and that set must be written down.

### 2. Define the flight envelope

Airspeeds — $V_S$, $V_A$, $V_C$, $V_D$ — in knots, with the load factor limits
$n_1$ and $n_2$. Build the V-n diagram before sizing any structure; it is the
input to every load case. Method in `references/loads-and-factors.md`.

### 3. Adopt and record the structural criteria

Limit load, ultimate load, and the factor of safety between them. For unmanned
airframes with no certification basis of their own, NASA-STD-5001
[REF-NASA-001] provides a defensible factor framework — **cite it with its scope
limitation stated**, since its own scope is spaceflight hardware, not aircraft.
Record the adopted factor and its justification in the project's own
requirements document; do not leave it implicit.

### 4. Aerodynamic build-up

Work in this order, stating the validity envelope at each step:

1. Section (2-D) characteristics — $c_l$, $c_d$, $c_m$ vs $\alpha$ at the
   design Re
2. Finite-wing correction — aspect ratio, taper, sweep; induced drag
3. Parasite drag build-up by component
4. Trim and control-surface effects

Details and equations: `references/aerodynamics.md`.

### 5. Mass properties and balance

Every component with a mass and a station. CG envelope across the fuel/payload
range, and static margin against the neutral point. Method in
`references/weight-and-balance.md`.

**A mass-properties roll-up with a "TBD" in it is not finished.** Estimate
with a stated basis and a stated uncertainty instead.

### 6. Propulsion match

Thrust required vs thrust available across the envelope; static and cruise
conditions treated separately. Method in `references/propulsion.md`.

## Reporting a result

Every analysis this skill produces ends with:

* **Result** — the number, in `imperial (metric)`, with the number of significant
  figures the inputs actually justify
* **Method** — the equation used and its validity envelope
* **Inputs** — each with its source or its "ASSUMED" label
* **Citations** — REF-IDs into `REFERENCES.md`
* **Margin** — where a limit exists, the margin against it, and whether it passes

Never report a margin without stating what it is a margin against.

## Adding a citation

Look the source up in `REFERENCES.md` by REF-ID. If it is not catalogued, add it
there with a validated URL and the specific section applied — then cite the
REF-ID here. If a section cannot be confirmed against the issuing body, mark it
`REQUIRES VERIFICATION` and open a `TODO.md` §0.x item. Never guess a standard
number, edition, or section.
