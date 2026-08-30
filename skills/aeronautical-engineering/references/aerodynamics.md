# Aerodynamics: Section, Finite Wing, and Drag Build-Up

Reference file for the `aeronautical-engineering` skill.

## Contents

1. Establish the regime first
2. Section (2-D) characteristics
3. Finite-wing correction
4. Drag build-up
5. Low-Reynolds-number practice

---

## 1. Establish the regime first

No method is valid everywhere. Before selecting one, compute and state:

**Reynolds number**, on the mean aerodynamic chord $c$:

$$\mathrm{Re} = \frac{\rho V c}{\mu} = \frac{V c}{\nu}$$

**Mach number**:

$$M = \frac{V}{a}, \qquad a = \sqrt{\gamma R T}$$

Then state the applicable method:

| Regime | Valid approach |
| --- | --- |
| $M < 0.3$ | Incompressible. Density constant. |
| $0.3 < M < 0.7$ | Prandtl–Glauert compressibility correction required |
| $M \to 1$ | Transonic; linearised corrections fail |
| $\mathrm{Re} < 5\times10^5$ | Low-Re. Laminar separation bubbles dominate; standard high-Re polars do **not** transfer |

Most small UAS operate at $\mathrm{Re} = 10^5$ to $5\times10^5$ — squarely in the
regime where textbook airfoil data taken at $\mathrm{Re} = 3\times10^6$ is
misleading. See §5.

## 2. Section (2-D) characteristics

Thin-airfoil theory gives the incompressible lift-curve slope:

$$a_0 = \frac{\mathrm{d}c_l}{\mathrm{d}\alpha} = 2\pi \ \text{per radian}$$

with zero-lift angle $\alpha_{L=0}$ set by camber. Then:

$$c_l = a_0(\alpha - \alpha_{L=0})$$

**Validity:** thin, attached, incompressible flow at small $\alpha$. It says
nothing about $c_{l,\max}$, and it cannot predict stall. $c_{l,\max}$ comes only
from cited experimental or computational data at the actual Re — never from
theory, and never from memory.

Compressibility correction (Prandtl–Glauert), valid to roughly $M = 0.7$:

$$c_{l,comp} = \frac{c_{l,inc}}{\sqrt{1 - M^{2}}}$$

## 3. Finite-wing correction

A finite wing sheds trailing vorticity, reducing effective incidence and
producing induced drag.

**Aspect ratio:**

$$AR = \frac{b^{2}}{S}$$

**Finite-wing lift-curve slope**, from lifting-line theory:

$$a = \frac{a_0}{1 + \dfrac{a_0}{\pi\,e_a\,AR}}$$

where $e_a$ is the span efficiency for lift-curve slope.

**Induced drag:**

$$C_{D_i} = \frac{C_L^{2}}{\pi\,e\,AR}$$

with Oswald efficiency $e$. For an ideal elliptical loading $e = 1$; real
straight-tapered wings run lower. **Do not assume a value for $e$** — either cite
a source for the planform in question or compute it, and label it if assumed.

**Validity:** lifting-line theory assumes high aspect ratio, unswept, attached
flow. It degrades for $AR \lesssim 4$, for significant sweep, and entirely at
stall.

## 4. Drag build-up

$$C_D = C_{D_0} + \frac{C_L^{2}}{\pi e AR}$$

$C_{D_0}$ is built up component by component — wing, fuselage, nacelles, landing
gear, antennas, and interference between them. Each component contributes:

$$C_{D_0,i} = \frac{C_{f,i}\, FF_i\, Q_i\, S_{wet,i}}{S_{ref}}$$

where $C_f$ is skin-friction coefficient, $FF$ form factor, $Q$ interference
factor, and $S_{wet}$ wetted area.

Flat-plate skin friction, turbulent:

$$C_f = \frac{0.455}{(\log_{10}\mathrm{Re})^{2.58}}$$

laminar:

$$C_f = \frac{1.328}{\sqrt{\mathrm{Re}}}$$

Each component's Re is based on **its own** reference length, not the wing chord.

Interference and form factors are empirical. Cite the source for each factor
used; if a factor is estimated, label it `ASSUMED` in the output.

## 5. Low-Reynolds-number practice

Below about $\mathrm{Re} = 5\times10^5$ the boundary layer separates laminar and
may or may not reattach. Consequences that routinely bite:

* **Published polars do not transfer.** A section characterised at
  $\mathrm{Re} = 3\times10^6$ can behave qualitatively differently at $2\times10^5$
  — lower $c_{l,\max}$, much higher $c_d$, and hysteresis in the stall.
* **$c_d$ can rise sharply** as Re falls, because of the separation bubble rather
  than skin friction.
* **Surface finish and trip location matter** more than at high Re. On an additively
  manufactured wing, layer lines are a de-facto trip strip whose effect is
  real and usually uncharacterised — say so rather than ignoring it.

Get section data from one of:

* **XFOIL / panel + integral boundary layer** at the actual Re — appropriate for
  attached and mildly separated flow; unreliable through stall
* **RANS CFD** with a transition-sensitive turbulence model — fully turbulent
  models will misrepresent the bubble
* **Cited experimental data** at matching Re — NTRS [REF-NASA-003] and the
  university low-Re airfoil databases

Whichever is used, name it in the output alongside the numbers it produced.
