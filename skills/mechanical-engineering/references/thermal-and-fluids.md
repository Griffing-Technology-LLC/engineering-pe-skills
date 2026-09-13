# Thermodynamics, Heat Transfer, Fluids, and HVAC

Reference file for the `mechanical-engineering` skill.

## 1. Thermodynamic cycles

First law, closed system: $\Delta U = Q - W$. Steady-flow energy equation:

$$\dot{Q} - \dot{W} = \dot{m}\left[(h_2 - h_1)
  + \frac{V_2^{2} - V_1^{2}}{2} + g(z_2 - z_1)\right]$$

Carnot efficiency bounds every heat engine between two reservoirs:

$$\eta_{Carnot} = 1 - \frac{T_L}{T_H}$$

**Absolute temperature only** — Rankine or Kelvin. A cycle efficiency computed
with °F is simply wrong, and it is a routine error.

Common cycles and their governing parameter: Otto (compression ratio), Diesel
(compression and cutoff ratio), Brayton (pressure ratio), Rankine (boiler and
condenser pressures), vapour-compression refrigeration (evaporator and condenser
temperatures).

Refrigeration performance is a **COP**, not an efficiency, and it exceeds 1:

$$COP_R = \frac{Q_L}{W_{in}}, \qquad COP_{HP} = \frac{Q_H}{W_{in}} = COP_R + 1$$

## 2. Heat transfer

**Conduction**, plane wall: $\dot{Q} = kA\,\Delta T/L$, thermal resistance
$R = L/(kA)$.

**Convection:** $\dot{Q} = hA(T_s - T_\infty)$, resistance $R = 1/(hA)$.

**Radiation:** $\dot{Q} = \varepsilon\sigma A(T_s^{4} - T_{sur}^{4})$ —
**absolute temperature**, and it matters at high temperature or in vacuum, where
it often dominates.

Series resistances add. Composite walls, fouling, and contact resistance all
enter as additional terms — and **contact resistance between bolted or printed
interfaces is real and frequently dominant**, yet routinely omitted.

Heat exchangers by LMTD:

$$\dot{Q} = UA \cdot F \cdot \Delta T_{lm}, \qquad
  \Delta T_{lm} = \frac{\Delta T_1 - \Delta T_2}{\ln(\Delta T_1/\Delta T_2)}$$

Use effectiveness-NTU instead when outlet temperatures are unknown — it avoids
iteration.

**Fins** improve heat transfer only when $hA$ is the limiting resistance. Adding
fins to the high-$h$ side of an exchanger accomplishes very little.

## 3. Fluid mechanics

Continuity: $\dot{m} = \rho A V$. Bernoulli, along a streamline for steady
incompressible inviscid flow:

$$\frac{p}{\rho g} + \frac{V^{2}}{2g} + z = \text{constant}$$

**Bernoulli is inviscid.** Any real duct needs the head-loss term.

Darcy-Weisbach:

$$h_f = f\frac{L}{D}\frac{V^{2}}{2g}$$

with $f$ from the Moody chart or Colebrook. Laminar ($Re < 2300$):
$f = 64/Re$, independent of roughness. Turbulent: roughness matters,
increasingly
so at high $Re$.

Minor losses $h_m = K V^{2}/(2g)$ — in a compact system with many fittings,
"minor" losses often exceed the straight-pipe loss. Do not skip them on short
runs.

## 4. Pumps

System curve rises with flow; pump curve falls. The **operating point is their
intersection** — a pump does not deliver its rated flow, it delivers the flow
the
system allows.

$$\text{NPSH}_A = \frac{p_{atm} - p_v}{\rho g} + z - h_{f,suction}$$

**NPSH available must exceed NPSH required**, with margin, or the pump cavitates
— eroding the impeller and destroying performance. Cavitation is a suction-side
problem and cannot be fixed by throttling the discharge.

Affinity laws for a given impeller:

$$\frac{Q_2}{Q_1} = \frac{N_2}{N_1}, \qquad
  \frac{H_2}{H_1} = \left(\frac{N_2}{N_1}\right)^{2}, \qquad
  \frac{P_2}{P_1} = \left(\frac{N_2}{N_1}\right)^{3}$$

The cube law on power is why variable-speed drives save so much energy on
throttled systems.

## 5. HVAC and psychrometrics

Sensible load: $\dot{Q}_s = \dot{m} c_p \Delta T$. Latent load follows the
humidity ratio change, $\dot{Q}_l = \dot{m} h_{fg} \Delta W$. The **sensible
heat
ratio** $SHR = \dot{Q}_s/\dot{Q}_{total}$ sets the required coil condition, and
a
system sized on total load alone will fail to control humidity.

Work psychrometric problems on the chart, tracking dry-bulb, wet-bulb, humidity
ratio, enthalpy, and dew point. Mixing two air streams lands on the straight
line
between them, proportioned by mass flow.

Ventilation requirements come from the governing mechanical code and ASHRAE
standards for the jurisdiction. **Confirm the applicable standard and edition
before citing a rate** — do not quote one from memory.
