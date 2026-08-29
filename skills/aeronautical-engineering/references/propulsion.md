# Propulsion: Propellers, Ducted Fans, and Thrust Matching

Reference file for the `aeronautical-engineering` skill.

## 1. Momentum theory — the floor on power

Actuator-disc theory gives the ideal induced power for a rotor or fan of disc
area $A$ producing thrust $T$ in hover:

$$
v_h = \sqrt{\frac{T}{2\rho A}}, \qquad
P_{ideal} = T v_h = \frac{T^{3/2}}{\sqrt{2\rho A}}
$$

This is a **lower bound**. Real power is higher by the figure of merit:

$$FM = \frac{P_{ideal}}{P_{actual}}$$

Momentum theory tells you nothing about blade design and cannot predict stall or
profile power. Use it to bound the problem, never to size a final system.

**Disc loading** $T/A$ is the dominant driver of hover efficiency: power per unit
thrust scales as $\sqrt{T/A}$. A small-diameter fan is aerodynamically expensive
in hover — that is physics, not a design flaw to be optimised away.

## 2. Propeller coefficients

Non-dimensional, with $n$ in revolutions per second and $D$ diameter:

$$
C_T = \frac{T}{\rho n^{2} D^{4}}, \qquad
C_P = \frac{P}{\rho n^{3} D^{5}}, \qquad
J = \frac{V}{nD}
$$

Efficiency:

$$\eta = \frac{T V}{P} = \frac{C_T}{C_P} J$$

$C_T$ and $C_P$ are functions of $J$ and are **specific to a given propeller
geometry**. They must come from manufacturer data or test — never assumed. Static
thrust ($J = 0$) is a different operating point from cruise and cannot be
extrapolated from a cruise figure.

## 3. Ducted fans and EDFs

A duct changes the problem materially:

* The duct carries part of the thrust through the pressure it develops; total
  thrust is fan thrust **plus** duct thrust.
* A well-designed duct with a bellmouth inlet raises static thrust relative to an
  open rotor of the same disc area, by reducing tip losses and increasing the
  effective disc area at the exit.
* Duct performance is highly sensitive to **inlet lip geometry** and **tip
  clearance**. Tip clearance loss is severe and scales with clearance/diameter —
  on a small EDF this is a first-order effect.
* In forward flight the inlet develops its own drag and momentum drag; static
  thrust badly overstates installed cruise thrust.

Never quote a manufacturer's static thrust figure as installed thrust. State the
installation losses or state that they are uncharacterised.

## 4. Thrust matching

**Thrust required** in level flight equals drag:

$$T_{req} = D = \tfrac{1}{2}\rho V^{2} S C_D$$

with $C_D$ from the drag build-up in `aerodynamics.md`. Plot $T_{req}$ and
$T_{avail}$ against $V$ across the envelope; the intersections bound the speed
range and the gap gives climb capability:

$$\text{rate of climb} = \frac{(T_{avail} - T_{req})\,V}{W}$$

**Thrust-to-weight** for a hovering or VTOL aircraft must exceed 1.0 with margin
for control authority — the rotors must have thrust left over to generate control
moments while supporting the weight. State the assumed control margin; a design
sized to exactly $T/W = 1$ cannot manoeuvre.

## 5. Reporting

Thrust is a **force**: report in `lbf (N)`. Aircraft and component weights are
**masses**: report in `lbm (kg)`. Do not mix them, and do not write bare "lb".
