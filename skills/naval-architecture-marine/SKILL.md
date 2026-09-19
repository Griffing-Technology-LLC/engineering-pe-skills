---
name: naval-architecture-marine
description: Naval architecture and marine engineering — ship hydrostatics, intact stability (GZ curve, metacentric height, IMO weather criterion), trim and freeboard, hull resistance and powering, and propeller/propulsion coefficients. Use when computing displacement or buoyancy, finding the metacentric height or righting arm, checking IMO intact stability criteria, analysing trim or list, estimating hull resistance from Froude or Reynolds number, applying the ITTC-57 friction line, or sizing propulsion power for a vessel.
license: CC-BY-ND-4.0
metadata:
    author: Griffing Technology LLC
    discipline: Naval Architecture and Marine Engineering
    ncees_alignment: "PE Naval Architecture and Marine Engineering — 85 questions, 9.5-hour appointment [REF-NCEES-008]. NCEES's exam landing page does not publish a named module breakdown the way PE Mechanical does; see 'Examination standing' below."
    sponsoring_society: SNAME (Society of Naval Architects and Marine Engineers)
    version: 0.1.0
---

# Naval Architecture and Marine Engineering

Ship hydrostatics, intact stability, and resistance/powering analysis aligned to
the NCEES PE Naval Architecture and Marine Engineering examination, with every
numeric criterion traceable to a cited authority.

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

Aligned to **PE Naval Architecture and Marine Engineering** [REF-NCEES-008] — 85
questions across a 9.5-hour appointment. Unlike PE Mechanical, the NCEES exam
landing page does not publish a named module breakdown; the full exam
specification PDF has not yet been obtained and catalogued for this repository
(`TODO.md` §0.5). Do not present a module structure for this exam as
NCEES-published fact.

The principal discipline society is **SNAME** [REF-SOC-002], whose stated
mission is "advancing the art, science, and practice of naval architecture and
marine engineering." SNAME operates a member PE Review Course and publishes
*Principles of Naval Architecture* (PNA) [REF-SNAME-001], the field's standard
reference text — cited here generally for method scope, not by specific page or
edition, per the caution recorded against REF-SNAME-001 in `REFERENCES.md`.

Two numeric method sets in this skill are verified against primary sources, not
against PNA:

* Intact stability criteria — the **IMO 2008 IS Code** [REF-IMO-001], read
  directly from the publisher's 2020 Edition text.
* Resistance-coefficient decomposition and the 1957 ITTC model-ship correlation
  line — **ITTC Recommended Procedure 7.5-02-02-01** [REF-ITTC-001], read
  directly.

## Non-negotiable practice rules

1. **Units are imperial-primary with metric in parentheses** — `ft (m)` length,
   `lbm (kg)` or long tons `(t)` for displacement, `lbf (N)` force,
   `kt (m/s)` speed. Marine practice runs metric internally (the IMO Code and
   ITTC procedures are both SI); convert explicitly and state the conversion
   rather than silently mixing systems.
2. **A stability or resistance result without its loading condition is
   meaningless.** State displacement, KG (or LCG/VCG), and trim for every GZ
   curve, GM, or resistance figure — these are not properties of the hull alone.
3. **Free surface effect is not optional.** Any slack tank reduces effective GM;
   apply the free-surface correction before comparing GM against a criterion
   [REF-IMO-001 §2.1.2].
4. **State which stability criterion governs** — the general righting-lever
   criteria (§2.2) and the weather criterion (§2.3) are both mandatory and
   independent; passing one does not imply passing the other.
5. **Model and full-scale resistance do not scale on the same law.** Froude
   scaling governs wave-making (geometrically similar models at matched
   $Fr$); Reynolds scaling governs viscous friction. A single model test cannot
   match both simultaneously — this is exactly why the ITTC-57 correlation line
   exists, to extrapolate frictional resistance separately from the
   Froude-scaled wave-making component [REF-ITTC-001].
6. **Name the failure mode** for any structural or freeboard check handed off
   elsewhere — this skill does not itself cover hull-girder longitudinal
   strength or scantlings; flag that as out of scope and refer to a classed
   structural analysis.

## Method selection

| Problem | Read |
| --- | --- |
| Buoyancy, displacement, GM, GZ curve, IMO stability criteria, trim, freeboard | `references/hydrostatics-and-stability.md` |
| Hull resistance, Froude/Reynolds scaling, ITTC-57 line, propulsion coefficients, powering | `references/resistance-and-propulsion.md` |

## Core workflow

### Hydrostatics and stability

1. **Fix the loading condition.** Displacement $\Delta$, LCG, VCG (KG), and any
   free-surface tanks. Nothing downstream means anything without this.
2. **Compute the hydrostatic properties** for that draft — KB, BM, $I_T/\nabla$
   — and the resulting GM.
3. **Build or read the GZ curve** (from hull GZ/KN cross-curves) across the
   heel range needed by the governing criterion.
4. **Check every applicable IMO general criterion independently**, then the
   weather criterion — do not stop at the first one satisfied.
5. **State margin against each criterion**, not just pass/fail.

### Resistance and powering

1. **Establish the speed range and length** to get $Fr$ and $Re$ — state which
   regime (displacement vs planing/high-speed) applies; this skill's method set
   is the conventional-displacement procedure [REF-ITTC-001].
2. **Decompose resistance**: frictional (ITTC-57 line, form-factor corrected)
   plus wave-making (from model test or a cited empirical series) plus
   appendage and air resistance.
3. **Convert to effective power** $P_E = R_T V$.
4. **Apply propulsion coefficients** — wake fraction, thrust deduction, hull
   efficiency, relative rotative efficiency, open-water propeller efficiency —
   to reach delivered and shaft power.
5. **State the margin** applied for sea state, hull fouling, and design service
   speed versus trial speed, and where that margin came from.

## Reporting a result

* **Result** in `metric (imperial)` — this discipline's primary sources are SI;
  invert the usual ordering and say so, rather than silently reporting only one
  system
* **Loading condition** — displacement, KG/VCG, trim, free-surface status
* **Criterion or method** applied, with its REF-ID
* **Margin**, not just pass/fail
* **Scaling law** used for any model-to-full-scale extrapolation, and its
  validity range
* Where the result feeds hull structure, propulsion machinery selection, or a
  classification-society submittal, say explicitly that those are out of scope
  here and name the discipline that owns them
