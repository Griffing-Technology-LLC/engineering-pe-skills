---
name: electronics-engineering
description: Electronics engineering aligned to the NCEES PE Electrical and Computer — Electronics, Controls, and Communications module — signal integrity and transmission-line analysis, EMC/EMI emissions and immunity, analog and digital circuit design, ADC/DAC and data-conversion basics, and board-level power regulation. Use when analyzing transmission-line reflections or termination, estimating crosstalk or an eye diagram, assessing EMC emissions/immunity or FCC Part 15 applicability, designing or reviewing an analog or digital circuit (amplifiers, filters, logic families), selecting an ADC/DAC, or sizing board-level power regulation. Not for power-system, protection, or arc-flash work — see `electrical-engineering` for that.
license: MIT
metadata:
    author: Griffing Technology LLC
    discipline: Electronics Engineering
    ncees_alignment: "PE Electrical and Computer — Electronics, Controls, and Communications module: 85 questions, 9.5-hour appointment [REF-NCEES-004]"
    sponsoring_society: IEEE (Institute of Electrical and Electronics Engineers)
    version: 0.1.0
---

# Electronics Engineering

Signal integrity, EMC, and board-level analog/digital circuit design aligned
to the Electronics, Controls, and Communications module of the NCEES PE
Electrical and Computer examination, with every method traceable to a cited
authority.

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

Aligned to the **Electronics, Controls, and Communications module** of PE
Electrical and Computer [REF-NCEES-004] — NCEES offers three modules under
this discipline (Computer Engineering; Electronics, Controls, and
Communications; Power); a candidate sits one. This module is 85 questions
across a 9.5-hour appointment; Power is 80 questions / 9 hours. This skill
covers signal integrity, EMC, and PCB-level analog/digital electronics —
per-unit power-system analysis, short-circuit/fault studies, overcurrent
protection coordination, and arc-flash hazard assessment belong to
`electrical-engineering` (Power module only).

**The detailed NCEES topic breakdown and its per-area question weighting were
not retrieved in this repository** — the exam specification PDF is hosted on
`ncees.org`, which this repository's research tooling could not reach
directly (network-policy block, not a content issue). Only the module name,
question count, and appointment length are asserted here, matching
REF-NCEES-004's existing verified scope. **Do not assert a specific topic
percentage weighting from this skill; confirm it against the current NCEES
specification document directly.** Tracked as `TODO.md` §0.9.

The principal SDO is **IEEE** [REF-SOC-005]. This skill cites **IEEE/ANSI
C63.4** (radiated/conducted emissions measurement methodology, 9 kHz–40 GHz)
[REF-IEEE-002] for the EMC emissions-testing framework, and **47 CFR Part 15**
[REF-FCC-001] for the US unlicensed-device emissions-limit and equipment-
authorization framework that governs most commercial electronic products.
Board-level PCB design guidance references **IPC-2221**, the generic printed-
board design standard [REF-IPC-001] — IPC is a separate SDO from IEEE; it is
cited because it is the accepted authority for PCB conductor spacing and
current-carrying-capacity design rules, and no equivalent IEEE standard covers
that scope.

## Non-negotiable practice rules

1. **Units are imperial-primary with metric in parentheses for physical
   quantities** — trace width and board dimensions in `mil/in (mm)` — but
   **electrical quantities themselves are SI: V, A, W, Ω, Hz, dB.** Do not
   invent an imperial unit for voltage, current, or impedance.
2. **State the frequency (or frequency range) before any signal-integrity or
   EMC result.** Characteristic impedance, propagation delay, skin effect,
   and emissions behavior are all frequency-dependent; a result without a
   stated frequency is incomplete.
3. **Name the transmission-line regime explicitly** — lumped (electrically
   short) versus distributed (electrically long) — before applying either a
   lumped-circuit approximation or transmission-line theory. Using the wrong
   regime for a given trace length and frequency is the single most common
   signal-integrity error.
4. **Termination and reflection analysis require the source and load
   impedances, not just the line impedance.** Report the reflection
   coefficient at both ends where relevant, not only at the load.
5. **EMC results are Class A (industrial) or Class B (residential/
   commercial), never unqualified.** Class B limits are more restrictive
   than Class A; state which class applies before comparing a measurement or
   estimate against a limit, and never assert a specific numeric limit value
   from memory — direct the user to the current FCC Part 15 and/or IEEE/ANSI
   C63.4 text for the governing table.
6. **Never assert a specific FCC Part 15 numeric emissions limit, or a
   specific IPC-2221 trace-width/current table value, from memory.** Both are
   edition- and condition-specific (frequency band, board copper weight,
   ambient temperature rise). This skill states the applicable *framework* —
   which subpart or table governs, and what inputs it needs — and hands off
   the numeric lookup to the current standard text.
7. **Digital logic family compatibility is a voltage-level and drive-strength
   problem, not just a "digital signal" problem.** State the logic family
   (e.g., TTL, CMOS, LVCMOS, LVDS) on both sides of an interface before
   asserting compatibility, and check $V_{OH}$/$V_{OL}$ against $V_{IH}$/
   $V_{IL}$ explicitly.
8. **Name the failure mode** for any margin reported, exactly as in
   `electrical-engineering` — insufficient noise margin, exceeded emissions
   limit, timing violation (setup/hold), ADC/DAC resolution or aliasing
   error, thermal derating exceeded.

## Method selection

| Problem | Read |
| --- | --- |
| Transmission lines, characteristic impedance, reflections, termination, crosstalk, eye diagrams | `references/signal-integrity-and-emc.md` §1–§4 |
| EMC/EMI emissions and immunity, grounding/shielding at board level, FCC Part 15 applicability | `references/signal-integrity-and-emc.md` §5–§7 |
| Analog circuits — op-amps, filters, amplifier basics | `references/analog-and-digital-circuits.md` §1–§3 |
| Digital logic families, timing, ADC/DAC, board-level power regulation | `references/analog-and-digital-circuits.md` §4–§7 |
| PCB design rules — conductor spacing, current-carrying capacity, stackup basics | `references/analog-and-digital-circuits.md` §8 |

## Core workflow

1. **State the frequency or frequency range** governing the problem before
   selecting a method — this decides whether transmission-line theory
   applies (practice rule 3).
2. **Classify the transmission-line regime** (electrically short vs. long)
   using the signal rise/fall time or frequency against the physical trace
   length.
3. **Run the signal-integrity check that governs** — characteristic
   impedance and termination for reflections, coupled-line analysis for
   crosstalk, or eye-diagram budget for a full link.
4. **Scope the EMC classification** (Class A vs. B) and the applicable
   regulatory framework (FCC Part 15 subpart, IEEE/ANSI C63.4 test method)
   before attempting any emissions estimate, and hand off the numeric limit
   lookup as described in practice rule 6.
5. **Design or review the circuit** — analog stage first (gain, bandwidth,
   noise), then digital interface compatibility (logic family, timing), then
   data conversion (ADC/DAC resolution, sample rate, aliasing).
6. **Check board-level power regulation and PCB design rules** — regulator
   selection and decoupling, then conductor sizing against IPC-2221's
   framework, deferring the specific table lookup per practice rule 6.

## Reporting a result

* **Result** — SI electrical units, with the frequency or frequency range
  stated explicitly
* **Transmission-line regime** — lumped or distributed, and why
* **Termination/reflection result**, with source and load impedance both
  stated
* **EMC class** (A or B) and the specific regulatory or test-method
  reference the numeric limit must be confirmed against — never a bare
  pass/fail without that reference
* **Logic family compatibility**, checked explicitly on both sides of any
  digital interface
* **PCB design-rule check** against IPC-2221's framework, with the specific
  table value explicitly deferred to the current standard per practice
  rule 6

Where a result feeds a regulatory compliance decision (FCC equipment
authorization, EMC class determination), say explicitly that the specific
numeric limit or authorization procedure must be confirmed against the
current 47 CFR Part 15 text and/or an accredited EMC test lab before it is
relied upon.
