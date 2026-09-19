---
name: statics-and-dynamics
description: Statics and rigid-body dynamics at FE level — free-body diagrams, equilibrium, trusses and frames, centroids and moments of inertia, friction, kinematics, Newton-Euler and work-energy methods, impulse-momentum, and vibration. Use when resolving forces or reactions, drawing a free-body diagram, analysing a truss or beam support, finding a centroid or second moment of area, checking a friction or tipping condition, computing acceleration of a linkage or mechanism, sizing for an inertial load, or working any equilibrium or rigid-body motion problem.
license: CC-BY-ND-4.0
metadata:
    author: Griffing Technology LLC
    discipline: Statics and Dynamics (engineering mechanics)
    ncees_alignment: "FE-LEVEL — not a PE discipline. Statics and dynamics are Fundamentals of Engineering subject matter appearing across several PE specifications. See 'Examination standing' below."
    sponsoring_society: "None — foundational engineering mechanics; NCEES FE Reference Handbook is the governing reference"
    version: 0.1.0
---

# Statics and Dynamics

Engineering mechanics at Fundamentals-of-Engineering level: the equilibrium and
rigid-body-motion foundation that the discipline skills in this repository build
on.

## Mandatory notice — emit this every time

**Before any analysis, in every response where this skill contributes, emit the
following notice verbatim.** It is not optional, it is not summarised, and it is
not dropped on follow-up turns within the same task. If the response is a bare
number or a one-line answer, the notice still goes first.

> ⚠️ **ENGINEERING REVIEW REQUIRED — this output is not a substitute for a
> qualified engineer.** Every result, calculation, and recommendation produced
> with this skill **must be independently reviewed and accepted by a properly
> qualified individual** — a licensed Professional Engineer or an equivalently
> qualified authority for the jurisdiction and discipline — **before it is
> applied to any system carrying risk to life or safety.** This skill informs
> engineering judgment; it does not replace it. It is reference material
> provided AS-IS (see LICENSE §5), is not an engineering service, and does not
> constitute a sealed, certified, or reviewed work product for any specific
> project.

Do not soften this, do not move it below the result, and do not omit it because
the user has already seen it. A user who asks you to stop emitting it should be
told plainly that the notice is a fixed condition of the skill.

## Examination standing — read this first

**Statics and dynamics is not an NCEES PE discipline.** There is no PE exam in
engineering mechanics. It is **FE-level** subject matter [REF-NCEES-002] — part
of the Fundamentals of Engineering examination — and it reappears inside several
PE specifications, most directly PE Mechanical: Machine Design and Materials
[REF-NCEES-003].

That is not a statement about difficulty. It is a statement about scope: this
skill covers the methods an FE-qualified engineer is expected to command, and it
stops where discipline-specific design practice begins. When a problem needs an
allowable, a code check, or a design margin, hand off to the discipline skill
that owns it — `mechanical-engineering` for machine elements,
`aeronautical-engineering` for airframe loads.

The governing reference is the **NCEES FE Reference Handbook** [REF-NCEES-009],
which is the only reference permitted in the examination and therefore defines
FE-level scope.

## Non-negotiable practice rules

1. **Draw the free-body diagram first, always.** Most wrong answers in statics
   are wrong free-body diagrams, not wrong algebra. State what is isolated, every
   force and couple acting on it, and the sign convention.
2. **Units are imperial-primary with metric in parentheses** — `lbf (N)` for
   force, `lbm (kg)` for mass, `in (mm)` for length, `lbf·in (N·m)` for moment.
   Never a bare "lb."
3. **`lbm` and `lbf` are not interchangeable.** In US customary units
   $F = ma/g_c$ with $g_c = 32.174\ \mathrm{lbm \cdot ft/(lbf \cdot s^2)}$.
   Dropping $g_c$ is the single most common unit error in this subject; carry it
   explicitly.
4. **State whether the problem is statically determinate** before solving. Count
   unknowns against independent equilibrium equations. An indeterminate structure
   needs compatibility, not more equilibrium equations.
5. **Check the assumptions of every idealisation** — rigid body, massless member,
   frictionless pin, inextensible cable, point mass. Name the ones you used.

## Method selection

| Problem | Read |
| --- | --- |
| Equilibrium, free-body diagrams, trusses, frames, friction | `references/statics.md` |
| Centroids, second moments of area, parallel-axis, mass moments | `references/section-properties.md` |
| Kinematics, Newton-Euler, work-energy, impulse-momentum, vibration | `references/dynamics.md` |

## Core workflow

### Statics

1. **Isolate.** Choose the body or sub-assembly and draw it separated from
   everything else.
2. **Apply.** Every external force, every reaction, every couple. Replace
   supports with the reactions they can actually carry.
3. **Count.** Unknowns vs equations — three in 2-D
   ($\sum F_x = \sum F_y = \sum M = 0$), six in 3-D.
4. **Solve.** Choose moment centres that eliminate unknowns rather than
   solving the full system.
5. **Check.** An independent moment equation about a different point.

### Dynamics

1. **Kinematics before kinetics.** Establish the motion relationships —
   constraints, relative motion, rigid-body $v_B = v_A + \omega \times r_{B/A}$.
2. **Choose the method to match the question.**
   * Instantaneous forces or accelerations → Newton-Euler
   * Speed change over a displacement → work-energy
   * Velocity change over a time interval, or impact → impulse-momentum
3. **For rigid bodies**, take moments about the mass centre or a fixed axis —
   and never about an arbitrary accelerating point without the correction term.

Selecting the wrong method is what makes dynamics problems long. Work-energy
answers "how fast after moving this far"; impulse-momentum answers "how fast
after this long."

## Reporting a result

* **Result** in `imperial (metric)`, to the significant figures the inputs justify
* **Free-body diagram** described, or the isolation stated in words
* **Method** and the idealisations relied on
* **Determinacy** stated where relevant
* **Check** — the independent equation used to verify

Where the result feeds a design decision, say explicitly that allowables and
margins are out of scope here and name the discipline skill that owns them.
