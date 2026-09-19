---
name: thermodynamics
description: Thermodynamics, heat transfer, and fluid mechanics at FE level — properties of pure substances, first and second law, entropy, power and refrigeration cycles, conduction/convection/radiation heat transfer, fluid statics, continuity and the energy equation, dimensional analysis, and internal pipe flow. Use when computing cycle efficiency or COP, sizing a heat exchanger by LMTD or NTU, finding conductive or convective heat loss, applying Bernoulli's equation or the energy equation, computing head loss in a pipe, finding a Reynolds or Froude number, or working any FE-level thermal-fluid problem that feeds mechanical, chemical, aeronautical, naval architecture, or fire protection design.
license: CC-BY-ND-4.0
metadata:
    author: Griffing Technology LLC
    discipline: Thermodynamics, Heat Transfer, and Fluid Mechanics (engineering thermal-fluid sciences)
    ncees_alignment: "FE-LEVEL — not a PE discipline on its own. Thermodynamics, heat transfer, and fluid mechanics are Fundamentals of Engineering subject matter that reappears across multiple PE specifications. See 'Examination standing' below."
    sponsoring_society: "None — foundational thermal-fluid sciences; NCEES FE Reference Handbook is the governing reference"
    version: 0.2.0
    review_status: "UNREVIEWED DRAFT — pending licensed PE review (TODO.md §4.1)"
---

# Thermodynamics, Heat Transfer, and Fluid Mechanics

Thermal-fluid engineering science at Fundamentals-of-Engineering level: the
property, energy-balance, and transport foundation that multiple discipline
skills in this repository build on, the same role
[[statics-and-dynamics|`statics-and-dynamics`]] plays for rigid-body mechanics.

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

**Thermodynamics, heat transfer, and fluid mechanics are not a standalone
NCEES PE discipline.** They are **FE-level** subject matter [REF-NCEES-002],
part of the Fundamentals of Engineering examination, and they reappear inside
several PE specifications and several disciplines in this repository:

* **PE Mechanical** — Thermal and Fluid Systems module, and the HVAC and
  Refrigeration module [REF-NCEES-003]; see `mechanical-engineering`.
* **PE Chemical** [REF-NCEES-006] — process thermodynamics, heat and mass
  transfer (`chemical-engineering`, not yet published in this repository —
  TODO.md §2.5).
* **Naval architecture and marine engineering** — marine power plant cycles
  and heat rejection (`naval-architecture-marine`).
* **Aeronautical engineering** — propulsion thermodynamics (Brayton-cycle jet
  and turboshaft analysis; `aeronautical-engineering` currently covers
  propeller/EDF momentum theory, not thermodynamic cycle analysis — a handoff
  gap worth naming when a request needs both).
* **Fire protection engineering** — heat release rate and fire plume/heat
  transfer fundamentals (`fire-protection-engineering`, not yet published —
  TODO.md §2.9).

That is not a statement about difficulty. It is a statement about scope: this
skill covers the thermal-fluid methods an FE-qualified engineer is expected to
command, and it stops where discipline-specific design practice begins — an
allowable heat-exchanger fouling factor, a code-mandated ventilation rate, a
classed marine boiler rule, or a fire code heat-release table are all handed
off to the discipline skill that owns them.

The governing reference is the **NCEES FE Reference Handbook** [REF-NCEES-009],
the only reference permitted in the examination and therefore the definition of
FE-level scope here, exactly as for `statics-and-dynamics`.

## Non-negotiable practice rules

1. **Absolute temperature only for cycle efficiency, COP, and radiation.** A
   Carnot or Rankine efficiency computed in °F or °C, or a radiation heat rate
   computed in non-absolute units, is simply wrong — convert to Rankine or
   Kelvin before the calculation, not after.
2. **Units are imperial-primary with metric in parentheses** —
   `Btu (kJ)` energy, `Btu/hr (W)` heat rate, `psia (kPa)` pressure,
   `lbm (kg)` mass, `lbf (N)` force. Never a bare "lb"; carry $g_c$ explicitly
   in US customary momentum and force balances, exactly as in
   `statics-and-dynamics`.
3. **State the system before writing any energy balance** — closed system
   ($\Delta U = Q - W$) or open/control-volume (steady-flow energy equation).
   Applying the closed-system form to a flow process is the single most common
   error in this subject.
4. **Efficiency and COP are not the same kind of number.** Heat-engine thermal
   efficiency $\eta \leq 1$. Refrigeration/heat-pump coefficient of performance
   routinely exceeds 1 — report it as $COP$, never mislabel it "efficiency."
5. **Name the flow regime before choosing a correlation.** Laminar vs turbulent
   (Reynolds number) for pipe friction; which non-dimensional group governs
   (Reynolds for viscous/inertial, Froude for gravity/inertial free-surface or
   wave phenomena — see `naval-architecture-marine` for the latter) before
   nondimensionalising or scaling any result.
6. **State every idealisation used** — incompressible, inviscid, steady,
   adiabatic, quasi-equilibrium, ideal gas. Bernoulli's equation in particular
   is inviscid and requires a head-loss term the moment a real duct is
   involved; do not apply it silently across a pump, valve, or long run of
   pipe.

## Method selection

| Problem | Read |
| --- | --- |
| Properties, first/second law, entropy, power and refrigeration cycles, psychrometrics | `references/thermodynamics.md` |
| Conduction, convection, radiation, heat exchangers | `references/heat-transfer.md` |
| Fluid statics, continuity, energy equation, dimensional analysis, pipe flow | `references/fluid-mechanics.md` |

## Core workflow

### Thermodynamics

1. **Define the system and process.** Closed or open; isothermal, isobaric,
   isochoric, adiabatic, or polytropic; ideal gas or real substance (steam
   tables, refrigerant tables).
2. **Write the governing energy balance** for that system — first law, in the
   form matching step 1.
3. **Bring in the second law where direction or limits matter** — entropy
   generation, Carnot bound, isentropic efficiency of a real device against its
   ideal counterpart.
4. **For a cycle**, identify the governing parameter (compression ratio,
   pressure ratio, boiler/condenser pressure) and compute each process before
   the overall efficiency or COP.

### Heat transfer

1. **Identify every mode present** — conduction, convection, radiation — and
   whether they act in series (thermal-resistance network) or in parallel.
2. **Build the resistance network** explicitly before computing a single
   overall $U$ or $\dot Q$; composite walls, contact resistance, and fouling
   all enter as additional terms.
3. **Choose LMTD or effectiveness-NTU** for a heat exchanger based on what is
   known — LMTD when both outlet temperatures are known, effectiveness-NTU
   when they are not (it avoids iteration).

### Fluid mechanics

1. **Establish the flow regime** — Reynolds number, laminar vs turbulent —
   before selecting a friction correlation.
2. **Write the energy equation with every term** — pressure, velocity,
   elevation, pump/turbine work, and head loss — then drop only the terms that
   are actually negligible, and say which ones and why.
3. **Separate major (pipe friction) and minor (fitting) losses**; in a compact
   system with many fittings, minor losses often dominate and must not be
   skipped on short runs.

## Reporting a result

* **Result** in `imperial (metric)`, to the significant figures the inputs
  justify
* **System and process** stated — closed/open, and the idealisations relied on
* **Governing equation** named, with the absolute-temperature check stated
  explicitly wherever a cycle, COP, or radiation term is involved
* **Flow regime or dimensionless group**, where relevant
* **Check** — an independent form of the energy balance, or an order-of-
  magnitude sanity check

Where the result feeds a design decision — an allowable fouling factor, a code
ventilation rate, a classed machinery rule, a fire heat-release value — say
explicitly that discipline-specific allowables are out of scope here and name
the discipline skill that owns them.
