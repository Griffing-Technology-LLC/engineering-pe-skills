# Fluid Mechanics: Statics, Continuity, Energy Equation, Pipe Flow

Reference file for the `thermodynamics` skill. Standard FE-level treatment,
governed generally by the NCEES FE Reference Handbook [REF-NCEES-009]; formulas
below are conventional forms, not individually cited beyond that governing
framework. The Reynolds- and Froude-number scaling discussion in §4 hands off
directly to `naval-architecture-marine`'s resistance method, which applies
these same dimensionless groups to hull model testing under a primary-source
citation [REF-ITTC-001].

## 1. Fluid statics

$$p = p_0 + \rho g h$$

Hydrostatic pressure depends only on depth and fluid density, not on
container shape or orientation. **Manometers** apply this directly, summing
$\rho g h$ terms along the fluid path between reference points.

**Buoyancy** (Archimedes): a submerged or floating body experiences an upward
force equal to the weight of displaced fluid, acting through the centroid of
the displaced volume (the centre of buoyancy) — see
`naval-architecture-marine`'s hydrostatics reference for the full stability
treatment built on this principle.

## 2. Continuity

$$\dot m = \rho A V = \text{constant along a stream tube (steady flow)}$$

For incompressible flow, $\rho$ is constant and $AV = \text{constant}$ directly
— velocity increases where area decreases.

## 3. Energy equation

Bernoulli's equation, along a streamline, steady, incompressible, **inviscid**
flow:

$$\frac{p}{\rho g} + \frac{V^2}{2g} + z = \text{constant}$$

**Bernoulli is inviscid.** The moment a real duct, valve, fitting, pump, or
turbine enters the picture, extend it to the general energy equation with a
head-loss and machine-work term:

$$\frac{p_1}{\rho g} + \frac{V_1^2}{2g} + z_1 + h_{pump} = \frac{p_2}{\rho g} + \frac{V_2^2}{2g} + z_2 + h_{turbine} + h_L$$

Write every term first, then drop only the ones that are actually negligible
for the specific problem, and state which ones and why — silently dropping
elevation or velocity head because they are "usually small" is how errors
enter.

## 4. Dimensionless groups — name the one that governs

$$Re = \frac{\rho V L}{\mu} = \frac{VL}{\nu}, \qquad Fr = \frac{V}{\sqrt{gL}}$$

* **Reynolds number** governs the balance of inertial to viscous forces —
  laminar-vs-turbulent transition, pipe friction, boundary-layer behaviour.
* **Froude number** governs the balance of inertial to gravitational forces —
  free-surface and wave phenomena (open-channel flow, ship wave-making).
  `naval-architecture-marine` applies $Fr$ directly to hull resistance scaling,
  citing the ITTC-57 procedure [REF-ITTC-001].

**A single small-scale model generally cannot match both $Re$ and $Fr$
simultaneously** at a practical scale ratio — this is why model testing in
naval architecture extrapolates resistance by component (frictional vs
wave-making) rather than by one overall coefficient; see
`naval-architecture-marine/references/resistance-and-propulsion.md` for the
full method.

## 5. Internal pipe flow and head loss

Laminar flow ($Re < 2300$, circular pipe): $f = 64/Re$ — independent of
surface roughness. Turbulent flow: $f$ depends on both $Re$ and relative
roughness $\varepsilon/D$ — read from the Moody chart or compute from the
Colebrook equation; roughness matters increasingly at higher $Re$.

**Darcy-Weisbach major loss:**

$$h_f = f\,\frac{L}{D}\,\frac{V^2}{2g}$$

**Minor losses** (fittings, valves, entrances, exits):

$$h_m = K\,\frac{V^2}{2g}$$

In a compact system with many fittings — exactly the kind of tightly-packed
routing this repository's own avionics and cape designs involve, by analogy —
minor losses routinely exceed the straight-run friction loss. Do not omit them
on short runs on the assumption that "minor" means negligible.

## 6. Out of scope here

Compressible (high-Mach) flow, open-channel flow beyond the Froude-number
definition above, and turbomachinery selection (pump/fan curves, NPSH,
affinity laws) are **PE-level design topics**, covered in
`mechanical-engineering/references/thermal-and-fluids.md`, not here. Hand off
explicitly rather than restating that material at FE level.
