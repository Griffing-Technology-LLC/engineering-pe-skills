# Dynamics: Kinematics, Kinetics, Energy, Momentum, Vibration

Reference file for the `statics-and-dynamics` skill.

## Contents

1. Particle kinematics
2. Rigid-body kinematics
3. Newton-Euler kinetics
4. Work and energy
5. Impulse and momentum
6. Free vibration

---

## 1. Particle kinematics

$$v = \frac{\mathrm{d}s}{\mathrm{d}t}, \qquad a = \frac{\mathrm{d}v}{\mathrm{d}t}
  = v\frac{\mathrm{d}v}{\mathrm{d}s}$$

That third form eliminates time and is the one to reach for whenever the
question
relates speed to position.

**Constant acceleration only** — these do not generalise:

$$v = v_0 + at, \qquad s = s_0 + v_0 t + \tfrac{1}{2}at^{2}, \qquad
  v^{2} = v_0^{2} + 2a(s - s_0)$$

**Normal-tangential** components, for curvilinear motion:

$$a_t = \dot{v}, \qquad a_n = \frac{v^{2}}{\rho}$$

with $\rho$ the radius of curvature. $a_n$ always points toward the centre of
curvature and exists whenever the path bends, **even at constant speed**.

## 2. Rigid-body kinematics

For two points on the same rigid body:

$$\mathbf{v}_B = \mathbf{v}_A + \boldsymbol{\omega} \times \mathbf{r}_{B/A}$$

$$\mathbf{a}_B = \mathbf{a}_A + \boldsymbol{\alpha} \times \mathbf{r}_{B/A}
  + \boldsymbol{\omega} \times (\boldsymbol{\omega} \times \mathbf{r}_{B/A})$$

The last term is the centripetal contribution, magnitude $\omega^2 r$, directed
from B toward A. Omitting it is the standard error in linkage acceleration
analysis.

**Instantaneous centre of zero velocity** — for planar motion, locate the point
about which the body is momentarily rotating, then $v = \omega r$ from it for
every point. Often faster than the vector equation. It applies to **velocities
only**; accelerations about the IC are not simply $\alpha r$.

**Rolling without slipping:** $v_{centre} = \omega r$ and
$a_{centre} = \alpha r$, with the contact point having zero velocity but
non-zero acceleration.

## 3. Newton-Euler kinetics

For a rigid body in planar motion:

$$\sum \mathbf{F} = m\mathbf{a}_G, \qquad \sum M_G = I_G \alpha$$

Moments taken about the **mass centre** $G$. Moments about another point $P$
require the transfer term:

$$\sum M_P = I_G \alpha + m a_G d$$

Taking moments about an arbitrary accelerating point as though it were fixed is
the classic error here. Two points are safe: the mass centre, and a genuinely
fixed axis of rotation.

In US customary units:

$$
F = \frac{ma}{g_c}, \qquad
g_c = 32.174\ \frac{\mathrm{lbm \cdot ft}}{\mathrm{lbf \cdot s^{2}}}
$$

Carry $g_c$ explicitly. Every dropped-$g_c$ error is a factor-of-32 error, which
in a structural context is the difference between a part that works and a part
that is not there any more.

## 4. Work and energy

$$U_{1\to2} = \Delta T = \tfrac{1}{2}mv_2^{2} - \tfrac{1}{2}mv_1^{2}$$

For a rigid body, kinetic energy includes rotation:

$$T = \tfrac{1}{2}mv_G^{2} + \tfrac{1}{2}I_G\omega^{2}$$

Work of common forces:

* Constant force: $U = F d \cos\theta$
* Spring: $U = -\tfrac{1}{2}k(x_2^{2} - x_1^{2})$ — negative when stretching
* Gravity: $U = -mg\,\Delta h$ — path-independent
* Couple: $U = M\,\Delta\theta$
* **Friction: always negative**, $U = -\mu N d$, and it is not recoverable

**Use work-energy when the question relates speed to displacement.** It
sidesteps
acceleration entirely, which is why it is nearly always the shorter route for
"how fast at the bottom of the ramp."

Note that the normal force does no work when motion is perpendicular to it, and
that rolling friction on a non-slipping wheel does no work at the contact point
—
because that point is instantaneously stationary.

## 5. Impulse and momentum

$$\int \mathbf{F}\,\mathrm{d}t = m\mathbf{v}_2 - m\mathbf{v}_1$$

**Use it when the question relates velocity to a time interval, or involves
impact.** Momentum is conserved in any direction with no external impulse —
which
during a short impact includes directions where only finite forces act, since
their impulse is negligible against the impulsive contact force.

**Coefficient of restitution**, along the line of impact:

$$e = \frac{v'_{B} - v'_{A}}{v_{A} - v_{B}}$$

with $e = 1$ perfectly elastic (kinetic energy conserved) and $e = 0$ perfectly
plastic (bodies move together). For $0 < e < 1$, momentum is conserved but
**kinetic energy is not** — do not apply work-energy across an impact.

**Angular impulse-momentum:** $\int M_O\,\mathrm{d}t = \Delta H_O$, with
$H_O = I_O\omega$ for rotation about a fixed axis. Angular momentum is conserved
about a point when no external moment acts about it.

## 6. Free vibration

Undamped single-degree-of-freedom:

$$m\ddot{x} + kx = 0, \qquad \omega_n = \sqrt{\frac{k}{m}},
  \qquad f_n = \frac{\omega_n}{2\pi}$$

With viscous damping:

$$m\ddot{x} + c\dot{x} + kx = 0, \qquad \zeta = \frac{c}{2\sqrt{km}}$$

* $\zeta < 1$ — underdamped, oscillates with damped frequency
  $\omega_d = \omega_n\sqrt{1 - \zeta^{2}}$
* $\zeta = 1$ — critically damped, fastest non-oscillatory return
* $\zeta > 1$ — overdamped

**Springs in parallel add stiffness** ($k_{eq} = \sum k_i$); **in series they
add
compliance** ($1/k_{eq} = \sum 1/k_i$). Getting this backwards is common and
shifts $\omega_n$ the wrong way.

For resonance-avoidance work, the number that matters is the ratio of forcing
frequency to $\omega_n$. Report the natural frequency **and** the excitation it
is
being compared against — a natural frequency quoted alone answers nothing.
