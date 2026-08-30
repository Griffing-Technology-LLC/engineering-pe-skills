---
name: mechanical-engineering
description: Mechanical engineering design and analysis aligned to the NCEES PE Mechanical exam — machine design, stress and fatigue, shafts, bearings, gears, fasteners and bolted joints, springs, thermodynamic cycles, heat transfer, fluid systems and pumps, and HVAC. Use when sizing a shaft or bearing, checking a bolted joint or weld, computing stress concentration or fatigue life, selecting a gear or belt drive, sizing a pump or duct, analysing a thermodynamic cycle or heat exchanger, doing a thermal or pressure-vessel check, or applying ASME codes.
license: MIT
metadata:
    author: Griffing Technology LLC
    discipline: Mechanical Engineering
    ncees_alignment: "PE Mechanical — three modules: HVAC and Refrigeration; Machine Design and Materials; Thermal and Fluid Systems"
    sponsoring_society: ASME (American Society of Mechanical Engineers)
    version: 0.1.0
---

# Mechanical Engineering

Machine design, thermal, and fluid-systems analysis aligned to the NCEES PE
Mechanical examination, with every method traceable to a cited authority.

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
> engineering judgment; it does not replace it, and it carries no professional
> liability.

Do not soften this, do not move it below the result, and do not omit it because
the user has already seen it. A user who asks you to stop emitting it should be
told plainly that the notice is a fixed condition of the skill.

## Examination standing

Aligned to **PE Mechanical** [REF-NCEES-003], which NCEES offers in three
modules — a candidate sits one:

| Module | Scope |
| --- | --- |
| **HVAC and Refrigeration** | Psychrometrics, loads, air and water distribution, refrigeration cycles |
| **Machine Design and Materials** | Stress, fatigue, machine elements, materials, joints |
| **Thermal and Fluid Systems** | Cycles, heat transfer, fluid mechanics, pumps and piping |

The exam is 80 questions across a 9-hour appointment; NCEES supplies the
electronic reference handbook and all specified design standards. Note that
because **no PE exam exists for aeronautical engineering**, this is also the
usual licensure route for engineers doing aircraft structural and propulsion
work — see `aeronautical-engineering` for that discipline's standing.

The principal standards-developing organisation is **ASME** [REF-SOC-004],
publisher of the Boiler & Pressure Vessel Code, ASME Y14.5 (GD&T), and the
ASME B-series dimensional standards.

## Non-negotiable practice rules

1. **Units are imperial-primary with metric in parentheses.** `lbf (N)` force,
   `lbm (kg)` mass, `psi (MPa)` stress, `Btu/hr (W)` heat rate. Never a bare
   "lb"; carry $g_c$ explicitly in US customary dynamics.
2. **Every allowable is cited.** Yield, ultimate, endurance limit, allowable
   stress — each comes from a material specification, a code table, or test data
   with a REF-ID. A remembered allowable is not an allowable.
3. **Name the failure mode.** Yield, ultimate, buckling, fatigue, creep, fretting,
   thread stripping, bearing, tear-out. A margin without a named failure mode is
   meaningless, and the governing mode is often not the obvious one.
4. **State the factor of safety and where it came from** — a code, a company
   standard, or an engineering judgment you are declaring.
5. **Anisotropic and additively manufactured materials are not isotropic
   metals.** Do not apply isotropic machine-design formulae to printed polymer
   without saying what that costs. See `references/materials-and-fatigue.md`.

## Method selection

| Problem | Read |
| --- | --- |
| Stress, stress concentration, fatigue, failure theories, allowables | `references/materials-and-fatigue.md` |
| Shafts, bearings, gears, springs, bolted joints, welds | `references/machine-elements.md` |
| Cycles, heat transfer, fluid systems, pumps, HVAC | `references/thermal-and-fluids.md` |

## Core workflow

1. **Define the load case.** Magnitude, direction, and whether it is static,
   fluctuating, or impact. Fatigue is governed by the *alternating* component and
   the mean stress, not the peak alone.
2. **Establish geometry and stress state.** Nominal stress, then the stress
   concentration factor $K_t$ at every discontinuity — fillets, holes, keyways,
   thread roots. For fatigue, apply the notch sensitivity to get $K_f$.
3. **Select the failure theory** appropriate to the material:
   * Ductile, static → distortion energy (von Mises) or maximum shear
   * Brittle, static → maximum normal stress or a modified Mohr theory
   * Fluctuating → a mean-stress criterion (Goodman, Gerber, Soderberg), stated
     by name
4. **Get the allowable** from a cited source, corrected for the real part —
   surface finish, size, loading type, temperature, reliability.
5. **Compute the margin** and name the failure mode it is against.
6. **Check the modes you did not compute.** Buckling on anything slender,
   deflection where fit matters, and the joint rather than the member — parts
   usually fail at their connections.

## Reporting a result

* **Result** in `imperial (metric)`, to justified significant figures
* **Load case** and whether static or fluctuating
* **Stress state** and the concentration factors applied
* **Failure theory** named
* **Allowable** with its source
* **Margin**, with its failure mode
* **Modes checked and found non-governing**, so the reader knows what was ruled
  out rather than overlooked
