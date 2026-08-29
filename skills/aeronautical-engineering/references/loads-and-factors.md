# Loads, Factors of Safety, and the V-n Envelope

Reference file for the `aeronautical-engineering` skill. Read before working any
structural load, factor-of-safety, or flight-envelope problem.

## Contents

1. [Limit, ultimate, and the factor between them](#1-limit-ultimate-and-the-factor-between-them)
2. [The V-n manoeuvre envelope](#2-the-v-n-manoeuvre-envelope)
3. [Gust loads](#3-gust-loads)
4. [Adopting criteria when none are imposed](#4-adopting-criteria-when-none-are-imposed)
5. [Margin of safety reporting](#5-margin-of-safety-reporting)
6. [Threaded joints](#6-threaded-joints)

---

## 1. Limit, ultimate, and the factor between them

Three distinct quantities, routinely confused:

| Term | Definition |
| --- | --- |
| **Limit load** | The maximum load expected in service. Structure must carry it with no detrimental permanent deformation. |
| **Ultimate load** | Limit load × factor of safety. Structure must carry it without failure, though permanent deformation is acceptable. |
| **Factor of safety (FOS)** | The multiplier between them. |

$$P_{ult} = P_{limit} \times \mathrm{FOS}$$

The classical airframe FOS is **1.5**. This value is longstanding practice in
civil airworthiness codes, but the reader must confirm the governing paragraph
for the specific certification basis in play — the 2017 restructure of 14 CFR
Part 23 [REF-FAA-002] moved numerical criteria out of the rule and into consensus
standards, so a bare citation to "Part 23" no longer establishes a number.

> **`REQUIRES VERIFICATION`** — The specific paragraph formerly carrying the 1.5
> factor (pre-Amendment-64 §23.303) and the normal-category limit manoeuvring load
> factors (formerly §23.337, commonly cited as $n_1 = +3.8$, $n_2 = -1.52$) have
> **not** been verified against the current eCFR text for this repository. Do not
> assert these numbers as current regulatory requirements until confirmed. See
> `TODO.md` §0.3.

For spaceflight-derived practice, NASA-STD-5001 [REF-NASA-001] sets out a
structured factor framework distinguishing design, yield, and ultimate factors.
**Its scope is spaceflight hardware.** Applying it to an aircraft is an analogy,
and must be labelled as one every time it is used.

## 2. The V-n manoeuvre envelope

The V-n diagram bounds load factor $n$ against equivalent airspeed $V$. It is the
input to every structural load case; build it first.

Load factor is the ratio of lift to weight:

$$n = \frac{L}{W}$$

### Stall boundary

The aerodynamic limit — the aircraft cannot generate more lift than $C_{L,\max}$
allows:

$$n_{\max,aero}(V) = \frac{\tfrac{1}{2}\,\rho\,V^{2}\,S\,C_{L,\max}}{W}$$

where $\rho$ is air density, $S$ the reference wing area. This is a parabola in
$V$. Below the stall boundary the aircraft stalls before reaching the structural
limit; above it, structure governs.

### Corner speed

The manoeuvring speed $V_A$ is where the stall boundary meets the positive
structural limit $n_1$ — the lowest speed at which the limit load factor can be
reached, and therefore the highest speed at which full control deflection is
aerodynamically bounded:

$$V_A = V_S \sqrt{n_1}$$

with $V_S$ the 1-g stall speed. Both in knots.

### Envelope corners

Construct the closed envelope from:

* $V_S$ at $n = 1$
* the stall parabola out to $V_A$ at $n = n_1$
* the horizontal $n = n_1$ line out to $V_D$
* $V_D$ down to $n = 0$
* the negative-side limit $n_2$ back to the inverted stall boundary

$V_C$ (design cruise) and $V_D$ (design dive) must come from the governing
certification basis or be adopted explicitly per §4.

## 3. Gust loads

Gusts impose load factors independent of pilot input. The incremental load factor
from a sharp-edged gust of velocity $U_{de}$, with gust alleviation factor $K_g$:

$$\Delta n = \frac{K_g\,U_{de}\,V\,a\,\rho_0\,S}{2\,W}$$

where $a$ is the wing lift-curve slope $\mathrm{d}C_L/\mathrm{d}\alpha$ per radian
and $\rho_0$ sea-level density. Gust and manoeuvre envelopes are overlaid; the
governing case is whichever is outermost at each speed.

> **`REQUIRES VERIFICATION`** — Design gust velocities $U_{de}$ and the
> formulation of $K_g$ are specified by the certification basis. The values
> commonly quoted for normal-category aeroplanes are **not** verified here.
> See `TODO.md` §0.3.

## 4. Adopting criteria when none are imposed

An sUAS operated under Part 107 [REF-FAA-001] has **no imposed structural
certification basis** — Part 107 governs operations, not airworthiness. This is
the usual situation for a purpose-built unmanned airframe, and it is a trap: the
absence of an imposed criterion is not the absence of a criterion.

Adopt one deliberately and record it:

1. **State the mission envelope** — max airspeed, max manoeuvre load factor, gust
   environment, and the operating weight range.
2. **Adopt limit load factors** with a stated rationale. Deriving them from the
   mission ("the airframe shall sustain a 3.0 g pull-up at MTOW") is defensible;
   inheriting them silently from a certification basis that does not apply is not.
3. **Adopt an FOS** and justify it. Where the structure is polymer additive
   manufacture, the factor must account for anisotropy, layer adhesion, and
   process variability — these are not covered by metallic-structure practice.
4. **Write all of it into the project requirements document** before sizing
   anything, and cite it from the analysis.

## 5. Margin of safety reporting

$$\mathrm{MS} = \frac{\text{allowable}}{\text{applied} \times \mathrm{FOS}} - 1$$

A positive MS passes; MS = 0 is exactly critical. Report MS with:

* the **allowable** and its source (material spec, test, or cited data)
* the **applied** load and the load case it comes from
* the **FOS** applied
* the **failure mode** the margin is against

A margin quoted without its failure mode is meaningless — a part can have a large
tensile margin and fail in buckling at the same load.

## 6. Threaded joints

NASA-STD-5020 [REF-NASA-002] gives a defensible methodology for threaded
fastening systems: preload determination and uncertainty, separation margins,
and joint-slip margins. As with NASA-STD-5001, the scope is spaceflight hardware
and its use elsewhere is an analogy to be labelled.

Key discipline points regardless of source:

* Preload uncertainty is large for torque-controlled installation — carry it
  explicitly rather than assuming nominal preload.
* Check **separation** and **slip** as distinct failure modes from fastener
  tensile failure.
* Thread engagement length governs whether the failure is fastener tension or
  thread stripping; in polymer parts, assume thread stripping governs until shown
  otherwise.
