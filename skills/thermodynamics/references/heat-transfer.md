# Heat Transfer: Conduction, Convection, Radiation, Exchangers

Reference file for the `thermodynamics` skill. Standard FE-level treatment,
governed generally by the NCEES FE Reference Handbook [REF-NCEES-009]; formulas
below are conventional forms, not individually cited beyond that governing
framework.

## 1. The three modes

**Conduction** (plane wall, steady state):

$$\dot Q = \frac{kA\,\Delta T}{L}, \qquad R_{cond} = \frac{L}{kA}$$

**Convection:**

$$\dot Q = hA(T_s - T_\infty), \qquad R_{conv} = \frac{1}{hA}$$

$h$ is a correlation result (free or forced convection, laminar or turbulent) —
state which correlation and which characteristic length were used; $h$ is not
a material property.

**Radiation:**

$$\dot Q = \varepsilon\sigma A(T_s^4 - T_{sur}^4)$$

**Absolute temperature only** — this expression is meaningless in °F or °C.
Radiation is often negligible at low $\Delta T$ near ambient but dominates at
high temperature or in vacuum; check the fourth-power terms before dismissing
it.

## 2. Resistance networks

Series resistances add directly: $R_{total} = \sum R_i$. Composite walls,
convection on each face, and **contact resistance at bolted or mated
interfaces** all enter as additional series terms. Contact resistance is real
and frequently the dominant term in an assembled joint, yet it is routinely
omitted — state explicitly whether it was included or assumed negligible, and
why.

Parallel paths (e.g. a wall with a stud and insulation side by side) combine as
parallel resistances or, more simply, as area-weighted heat rates through each
path — do not average the $R$-values directly when the areas differ.

## 3. Fins

A fin increases heat transfer only when convective resistance ($1/hA$) is the
limiting term in the network. Adding fins to the **high-$h$ side** of an
already convection-dominated-elsewhere system accomplishes very little — check
which side is actually limiting before proposing fins.

Fin effectiveness and efficiency are reported separately: effectiveness
compares the finned area's heat rate to the same bare area without the fin;
efficiency compares the actual fin heat rate to the rate if the entire fin were
at the base temperature.

## 4. Heat exchangers

**LMTD method**, when both inlet and outlet temperatures are known or assumed:

$$\dot Q = UA\,F\,\Delta T_{lm}$$

$$\Delta T_{lm} = \frac{\Delta T_1 - \Delta T_2}{\ln(\Delta T_1/\Delta T_2)}$$

$F$ is a correction factor for multi-pass/cross-flow arrangements (1.0 for true
counterflow or parallel flow); state which configuration and correct $F$
accordingly.

**Effectiveness-NTU method**, when an outlet temperature is unknown (avoids
iteration):

$$\varepsilon = \frac{\dot Q_{actual}}{\dot Q_{max}}$$

$$\dot Q_{max} = C_{min}(T_{h,in} - T_{c,in}), \qquad NTU = \frac{UA}{C_{min}}$$

$C_{min} = \min(\dot m_h c_{p,h},\ \dot m_c c_{p,c})$. Choose LMTD or
effectiveness-NTU based on **which temperatures are known**, not by habit — one
requires iteration the other case does not.

**Overall heat transfer coefficient** $U$ is a series combination of the two
convective film resistances, the wall conduction resistance, and any fouling
resistance on each side:

$$\frac{1}{UA} = \frac{1}{h_i A_i} + R_{fi} + R_{w} + R_{fo} + \frac{1}{h_o A_o}$$

$R_{fi}$, $R_{fo}$ — inside/outside fouling resistances; $R_w =
\ln(D_o/D_i)/(2\pi k L)$ — wall conduction resistance, cylindrical wall.

**A specific fouling-factor allowable is a design/code matter**, not a bare
thermodynamics fact — cite it from the governing code or manufacturer data in
the discipline skill applying it (e.g. `mechanical-engineering`), not asserted
generically here.

## 5. Combined modes and boundary conditions

Real problems commonly combine convection and radiation from the same surface
(e.g. a hot pipe in still air) — these act in **parallel**, not series, since
both draw from the same surface to the same or comparable ambient:

$$\dot Q_{total} = \dot Q_{conv} + \dot Q_{rad}$$

State surface emissivity $\varepsilon$ explicitly; it varies enormously with
surface finish and oxidation state and is not a fixed material constant the
way thermal conductivity approximately is.
