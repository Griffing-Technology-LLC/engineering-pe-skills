# Thermodynamics: Properties, Laws, Cycles, Psychrometrics

Reference file for the `thermodynamics` skill. Standard FE-level thermal
science, governed generally by the NCEES FE Reference Handbook [REF-NCEES-009]
as the examination's own sole permitted reference; formulas below are the
conventional forms found in any standard thermodynamics text and are not
individually cited beyond that governing framework, in keeping with this
repository's treatment of `statics-and-dynamics`.

## 1. Properties and state

A **pure substance** state is fixed by two independent intensive properties
(e.g. $T$ and $p$, outside the two-phase dome; $T$ or $p$ plus quality $x$
inside it). For an **ideal gas**:

$$pV = mRT, \qquad R = \frac{\bar{R}}{M}$$

Ideal-gas behaviour is an idealisation — valid away from the critical point and
away from saturation. Near saturation or at high pressure, use real-substance
tables (steam tables, refrigerant tables) instead.

## 2. First law

**Closed system:**

$$\Delta U = Q - W$$

**Open system, steady-flow energy equation** (per unit mass, or rate form):

$$\dot Q - \dot W = \dot m\left[(h_2-h_1) + \frac{V_2^2-V_1^2}{2} + g(z_2-z_1)\right]$$

Use enthalpy $h$, not internal energy $u$, for the open/flow form — the flow
work is already absorbed into $h = u + pv$. Applying the closed-system form to
a flow device (turbine, compressor, nozzle, throttle) is a routine and costly
error.

**Common device idealisations** (state which one is assumed):

| Device | Typical assumption |
| --- | --- |
| Turbine, compressor | Adiabatic; $\Delta KE, \Delta PE$ negligible |
| Nozzle, diffuser | Adiabatic, no work; KE change is the point |
| Throttle (valve) | Adiabatic, no work, no elevation change → $h_1 = h_2$ |
| Heat exchanger | No work; KE/PE negligible; energy balance between streams |

## 3. Second law, entropy, and cycle bounds

Entropy is generated, never destroyed, in any real (irreversible) process:

$$\Delta S_{gen} \geq 0$$

**Carnot efficiency** bounds every heat engine operating between two
reservoirs — an upper limit no real cycle reaches:

$$\eta_{Carnot} = 1 - \frac{T_L}{T_H}$$

**Absolute temperature only** — Rankine or Kelvin. This is the single most
common error in this subject; the practice rule in `SKILL.md` exists because
of it.

**Isentropic efficiency** compares a real device to its ideal (isentropic)
counterpart at the same inlet state and exit pressure:

$$\eta_{turbine} = \frac{w_{actual}}{w_{isentropic}}$$

$$\eta_{compressor} = \frac{w_{isentropic}}{w_{actual}}$$

Note the ratio inverts between turbine and compressor — a turbine's real work
output is less than ideal; a compressor's real work input is more than ideal.

## 4. Power and refrigeration cycles

Identify the governing parameter before computing overall performance:

| Cycle | Governing parameter | Application |
| --- | --- | --- |
| Otto | Compression ratio $r_v$ | Spark-ignition |
| Diesel | Compression ratio and cutoff ratio | Compression-ignition |
| Brayton | Pressure ratio $r_p$ | Gas turbine, jet propulsion |
| Rankine | Boiler and condenser pressure | Steam power |
| Vapour-compression refrigeration | Evaporator/condenser temperature | Refrigeration, heat pump |

**Refrigeration and heat-pump performance is a COP, not an efficiency, and it
exceeds 1:**

$$COP_R = \frac{Q_L}{W_{in}}, \qquad COP_{HP} = \frac{Q_H}{W_{in}} = COP_R + 1$$

For a Brayton-cycle propulsion application (turbojet, turboshaft), specific
thrust and propulsive/thermal/overall efficiency draw on momentum concepts —
hand off to `aeronautical-engineering`'s propulsion reference for the
thrust-side analysis; this file covers the thermodynamic cycle only.

## 5. Psychrometrics

Sensible heat: $\dot Q_s = \dot m\,c_p\,\Delta T$. Latent heat follows the
humidity-ratio change: $\dot Q_l = \dot m\,h_{fg}\,\Delta W$.

**Sensible heat ratio** $SHR = \dot Q_s/\dot Q_{total}$ sets the required
cooling-coil condition; a system sized on total load alone will not control
humidity correctly.

Work psychrometric problems on the chart: track dry-bulb, wet-bulb, humidity
ratio, enthalpy, and dew point together. Mixing two air streams lands on the
straight line between their state points, proportioned by mass flow.

**Ventilation and comfort criteria are a code/standard matter, not a
thermodynamics one** — confirm the applicable mechanical code and ASHRAE
standard edition before citing a rate; do not quote one from memory. That
citation belongs to the discipline skill applying it (e.g.
`mechanical-engineering` for HVAC design).
