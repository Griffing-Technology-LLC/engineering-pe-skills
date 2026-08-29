# Weight, Balance, and Static Margin

Reference file for the `aeronautical-engineering` skill.

## 1. Mass properties roll-up

Every component gets a mass and a station. The rule from the project standard:
**no "TBD" values.** An estimate with a stated basis and uncertainty is
engineering; a TBD is a deferred failure.

Report mass in `lbm (kg)`. Longitudinal station $x$ is measured from a stated
datum — name the datum explicitly, since a CG figure without its datum is
unusable.

$$x_{cg} = \frac{\sum m_i x_i}{\sum m_i}$$

Same form for lateral and vertical CG. For a multi-rotor or tilt-nacelle
aircraft, lateral balance is a live constraint, not a formality.

**Moment of inertia** about the CG, needed for any dynamic or control analysis:

$$I = \sum \left( I_{cg,i} + m_i d_i^{2} \right)$$

the parallel-axis theorem. Neglecting the $I_{cg,i}$ term is acceptable only for
components small relative to their offset — state when that approximation is made.

## 2. CG envelope

CG is not a point; it is a range swept as payload and energy are consumed. Compute
the CG at every corner of the loading matrix:

* empty
* max payload, full battery/fuel
* max payload, depleted
* zero payload, full
* zero payload, depleted

The **forward** and **aft** extremes bound the envelope, and both must satisfy the
stability and control criteria. A design balanced only at one loading is not
balanced.

## 3. Neutral point and static margin

The neutral point $x_{np}$ is the CG location at which the aircraft is neutrally
stable in pitch. For a conventional wing-plus-tail configuration:

$$
\frac{x_{np}}{\bar{c}} = \frac{x_{ac}}{\bar{c}}
+ V_H \frac{a_t}{a_w}
\left(1 - \frac{\mathrm{d}\varepsilon}{\mathrm{d}\alpha}\right)
$$

with horizontal tail volume coefficient:

$$V_H = \frac{l_t S_t}{\bar{c} S_w}$$

where $l_t$ is the tail arm, $S_t$ tail area, $\bar{c}$ mean aerodynamic chord,
$a_t$ and $a_w$ the tail and wing lift-curve slopes, and
$\mathrm{d}\varepsilon/\mathrm{d}\alpha$ the downwash gradient.

**Static margin:**

$$SM = \frac{x_{np} - x_{cg}}{\bar{c}}$$

Positive static margin means statically stable in pitch. The margin must be
positive **across the whole CG envelope**, not merely at the nominal loading.

The downwash gradient is configuration-dependent and is a common place for
fabricated numbers to enter an analysis. Cite it or compute it; if estimated,
label it `ASSUMED` and carry the sensitivity.

## 4. Configurations where this formulation does not apply

The tail-volume formulation above assumes a conventional wing-plus-aft-tail
layout. It does **not** transfer unmodified to:

* tailless and flying-wing configurations
* canard configurations (the stability contributions reverse)
* tilt-rotor / tilt-nacelle aircraft, where the thrust line moves through the
  transition and the CG-relative thrust moment changes sign

For a tilting-propulsion aircraft, pitch balance must be evaluated **at each tilt
angle through the transition**, not only in cruise and hover. The critical
case is usually mid-transition, and it is routinely missed.
