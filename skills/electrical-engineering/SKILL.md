---
name: electrical-engineering
description: Electrical power engineering aligned to the NCEES PE Electrical and Computer (Power) exam — per-unit and three-phase power system analysis, transformers, short-circuit and fault current calculation, overcurrent protection and coordination, grounding and bonding, and arc-flash hazard assessment. Use when computing per-unit or three-phase power quantities, sizing or checking a transformer, running a short-circuit or fault study, selecting or coordinating overcurrent protection, checking a grounding/bonding scheme, or estimating an arc-flash incident-energy or boundary requirement.
license: CC-BY-ND-4.0
metadata:
    author: Griffing Technology LLC
    discipline: Electrical Engineering (Power)
    ncees_alignment: "PE Electrical and Computer — Power module: 80 questions, 9-hour appointment [REF-NCEES-004]"
    sponsoring_society: IEEE (Institute of Electrical and Electronics Engineers)
    version: 0.1.0
    review_status: "UNREVIEWED DRAFT — pending licensed PE review (TODO.md §4.1)"
---

# Electrical Engineering (Power)

Power system analysis, protection, and arc-flash hazard assessment aligned to
the Power module of the NCEES PE Electrical and Computer examination, with
every method traceable to a cited authority.

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

## Examination standing

Aligned to the **Power module** of PE Electrical and Computer [REF-NCEES-004]
— NCEES offers three modules under this discipline (Computer Engineering;
Electronics, Controls, and Communications; Power); a candidate sits one. Power
is 80 questions across a 9-hour appointment; the other two modules are 85
questions / 9.5 hours. This skill covers Power only — signal integrity, EMC,
and PCB-level electronics belong to `electronics-engineering` (planned,
`TODO.md` §2.7); computer architecture, embedded systems, digital design,
networks, and cybersecurity belong to `computer-engineering`.

The principal SDO is **IEEE** [REF-SOC-005], publisher of the colour-book
series applied throughout this skill: IEEE 141 (Red Book, power distribution),
IEEE 242 (Buff Book, protection and coordination), IEEE 399 (Brown Book,
power system analysis), IEEE 493 (Gold Book, reliability), and
**IEEE 1584-2018** (arc-flash hazard calculations) [REF-IEEE-001], verified
directly in this repository. The colour books beyond 1584 are catalogued at
index level only under REF-SOC-005 — no specific colour-book section number
is asserted here without further verification.

**NFPA 70 (NEC)** [REF-NFPA-001] and **NFPA 70E** [REF-NFPA-002] govern
installation and workplace-safety requirements respectively. Both are
`VERIFIED (BLOCKED)` in this repository — existence and edition confirmed via
secondary sources, but nfpa.org's own text was not accessible for direct
section verification. **No NEC article or table number is asserted as fact in
this skill.** Where an article is relevant, it is named generically (e.g.
"NEC's overcurrent-protection article") with an explicit
`REQUIRES VERIFICATION` flag — confirm the current article/table number
against the actual 2026 NEC text before relying on it. See `TODO.md` §0.8.

## Non-negotiable practice rules

1. **Units are imperial-primary with metric in parentheses for physical
   quantities** — `ft (m)` conduit run, `in² (mm²)` conductor area — but
   **electrical quantities themselves are SI: V, A, W, VA, VAR, Ω, Hz.** Do
   not invent an imperial unit for voltage or current; state values in their
   native SI form.
2. **Declare the base** before any per-unit quantity is used — base MVA, base
   kV, and which side of a transformer the base refers to. A per-unit value
   without its base is not a number, it is a placeholder.
3. **State the fault type** before reporting a fault current — three-phase
   symmetrical, single-line-to-ground, line-to-line, and double-line-to-ground
   fault currents differ, often significantly, at the same location.
4. **Protection coordination is a system property, not a device property.**
   A correctly rated breaker or fuse can still fail to coordinate with its
   upstream and downstream devices — verify the time-current curve overlap,
   not just the individual device rating.
5. **Grounding and bonding are safety systems, not afterthoughts.** State
   which grounding scheme is assumed (solidly grounded, resistance grounded,
   ungrounded) — fault behaviour and required protection differ fundamentally
   between them.
6. **Never assert an arc-flash incident-energy number from memory.** IEEE
   1584's model coefficients are copyrighted, edition-specific, and equipment-
   configuration-dependent. This skill states the calculation *framework*
   [REF-IEEE-001] — bounding cube, working distance, arcing current and time
   — and explicitly hands off the actual coefficient lookup and numeric
   result to a current licensed copy of the standard or an accepted
   arc-flash study tool. Never fabricate a PPE category or incident-energy
   figure.
7. **Name the failure mode** for any protection or insulation margin, exactly
   as in `mechanical-engineering` — interrupting rating exceeded, let-through
   energy, insulation breakdown, selective-coordination failure.

## Method selection

| Problem | Read |
| --- | --- |
| Per-unit system, three-phase power, transformers, load flow basics | `references/power-systems-and-per-unit.md` |
| Short-circuit/fault current, overcurrent protection, coordination, grounding | `references/protection-and-fault-analysis.md` |
| Arc-flash hazard framework, NFPA 70E work-practice requirements | `references/arc-flash-and-safety.md` |

## Core workflow

1. **Build the one-line diagram** and establish system bases (MVA, kV) before
   any per-unit calculation.
2. **Convert every impedance to a common base** — generators, transformers,
   cables, and utility source impedance all need base conversion; a
   forgotten conversion is the most common per-unit error.
3. **Run the fault study for the fault type that governs** the device being
   sized — usually three-phase symmetrical for interrupting-rating checks,
   single-line-to-ground for ground-fault protection sizing.
4. **Size and coordinate protection** from the load outward: conductor
   ampacity and equipment ratings first, then overcurrent device selection,
   then time-current coordination against adjacent devices.
5. **Check grounding and bonding** against the assumed system grounding
   scheme, not a default assumption.
6. **Scope the arc-flash study** separately — state the equipment's bus
   voltage and configuration against IEEE 1584's stated scope [REF-IEEE-001]
   before attempting any incident-energy estimate, and hand off the numeric
   calculation as described in practice rule 6.

## Reporting a result

* **Result** — SI electrical units, with the base stated for any per-unit
  quantity
* **Fault type** stated explicitly for any fault-current result
* **Protection device** and its interrupting/let-through rating against the
  calculated fault current
* **Coordination** — confirmed or flagged as unchecked
* **Grounding scheme** assumed
* **Arc-flash scope check** against IEEE 1584's stated voltage/phase range,
  with the numeric incident-energy/PPE-category result explicitly deferred to
  the current standard or an accepted study tool per practice rule 6

Where a result feeds a code-compliance decision (conductor sizing, working
clearance, disconnect requirements), say explicitly that the specific NEC
article number is unconfirmed in this repository (`TODO.md` §0.8) and that
the current NEC and any local amendments must be consulted directly.
