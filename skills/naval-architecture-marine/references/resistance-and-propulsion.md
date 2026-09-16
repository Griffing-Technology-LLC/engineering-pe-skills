# Resistance and Propulsion

Reference file for the `naval-architecture-marine` skill. The resistance
decomposition, ITTC-57 friction line, and Froude/Reynolds definitions in §1–2
are read verbatim from ITTC Recommended Procedure 7.5-02-02-01
[REF-ITTC-001]. Propulsion-coefficient framework in §3 is standard
naval-architecture practice [REF-SNAME-001] — no specific PNA page is cited;
see the caution against REF-SNAME-001 in `REFERENCES.md`.

**Scope note (from the source procedure itself):** this method set addresses
**conventional displacement vessels** only. Vessels with $Fr > 0.45$, or speeds
above $3.7\,\nabla^{1/6}$ (m/s), or planing/dynamically-supported craft, are
addressed by a different ITTC procedure (7.5-02-05-01, High Speed Marine
Vehicle Resistance Test) not catalogued in this repository — flag that gap
explicitly rather than applying this method outside its stated range.

## 1. Why two scaling laws, not one

A ship's total resistance has a viscous (frictional) component and a
wave-making component. Viscous drag scales with **Reynolds number**
$Re = VL/\nu$; wave pattern scales with **Froude number** $Fr = V/\sqrt{gL}$.

A geometrically-scaled model run at the ship's $Fr$ (correct wave pattern) runs
at a much lower $Re$ than the full-scale ship, so its *relative* frictional
resistance is too high. There is no model speed that matches both numbers at
once for a practical scale ratio — that mismatch is exactly why resistance is
extrapolated by **component**, not by a single overall coefficient.

$$Fr = \frac{V}{\sqrt{gL}}, \qquad Re = \frac{VL}{\nu}$$

$Fr_h = V/\sqrt{gh}$ is the depth Froude number, for shallow or restricted
water.

## 2. Resistance-coefficient decomposition

Non-dimensionalise on $\tfrac{1}{2}\rho S V^2$ ($S$ = wetted surface area):

$$C_T = \frac{R_T}{\tfrac{1}{2}\rho S V^2}$$

$$C_V = C_F(1+k), \qquad C_W = C_T - C_V = C_T - C_F(1+k)$$

$C_T$ — total resistance coefficient (measured, model test); $C_V$ — viscous
resistance coefficient; $C_W$ — wave-making resistance coefficient (assumed
to obey Froude similarity, and therefore transferable from model to ship at
matched $Fr$); $(1+k)$ — form factor, accounting for 3-D viscous effects a flat
plate does not have.

**1957 ITTC model-ship correlation line** — the frictional resistance
coefficient of an equivalent flat plate at the given Reynolds number:

$$C_F = \frac{0.075}{(\log_{10}Re - 2)^2} = (1 + 0.1194)\,\frac{0.067}{(\log_{10}Re-2)^2}$$

Extrapolation procedure, in outline:

1. Measure $C_{T,model}$ from a towing-tank test at the model's $Fr$-matched
   speed; determine $Re_{model}$ for that run.
2. Compute $C_{F,model}$ from the ITTC-57 line at $Re_{model}$; obtain the form
   factor $k$ (from a low-speed run or an empirical method) and $C_{V,model}$.
3. $C_{W,model} = C_{T,model} - C_{V,model}$. **Assume $C_W$ is scale-independent
   at matched $Fr$** — this is the Froude-similarity assumption at the core of
   the whole method.
4. Compute $C_{F,ship}$ from the ITTC-57 line at the ship's (much larger)
   $Re_{ship}$, at the same $Fr$-matched speed scaled to full size.
5. $C_{T,ship} = C_{F,ship}(1+k) + C_{W,model} + C_A$, where $C_A$ is a
   correlation allowance accounting for hull roughness and residual scale
   effects not captured by the form-factor method.
6. Add appendage resistance $C_{APP}$ and air/wind resistance $C_{AA}$ as
   needed for the actual ship condition.

## 3. Effective and delivered power

$$P_E = R_T \, V$$

$P_E$ — effective (towrope) power: the power to tow the bare hull at speed $V$
with no propulsion losses. This is **not** the power the engine must deliver.

**Propulsion factors** connect $P_E$ to shaft power:

$$\eta_H = \frac{1-t}{1-w}, \qquad \eta_D = \eta_H\,\eta_0\,\eta_R$$

* $w$ — wake fraction: the propeller works in water already moving with the
  hull's boundary layer and wave system, so its inflow speed is less than
  ship speed.
* $t$ — thrust deduction: the propeller's suction accelerates flow past the
  stern, adding resistance beyond the bare-hull figure.
* $\eta_H$ — hull efficiency, from $w$ and $t$ together — commonly $> 1$ for
  single-screw hulls, which is a real hydrodynamic interaction effect, not an
  error.
* $\eta_0$ — open-water propeller efficiency, from the propeller's own
  characteristic curves at its operating advance coefficient $J$.
* $\eta_R$ — relative rotative efficiency, correcting open-water efficiency for
  the actual (non-uniform) wake field behind the hull.
* $\eta_D$ — quasi-propulsive coefficient, the product of all three.

$$P_D = \frac{P_E}{\eta_D}$$

$P_D$ — delivered power at the propeller. Shaft power adds shafting losses;
brake (engine) power adds gearbox losses on top of that. **State which power
definition is being reported** — $P_E$, $P_D$, shaft, or brake — they are not
interchangeable and differ by tens of percent.

## 4. Sea and service margins

Trial-condition resistance is not service resistance. State explicitly what
margin was added for hull fouling, weather, and shallow-water effects, and
where that margin figure came from (a specific standard, class-society
guidance, or an engineering judgement being declared) — an unstated margin is
not a margin, it is a guess wearing a number.

## 5. Out of scope here

Cavitation inception, propeller strength/blade design, detailed self-propulsion
model-test correction methods beyond the outline in §2, and high-speed/planing
hull resistance (a different ITTC procedure, not catalogued here) are **not
covered**. Name them explicitly as out of scope when a request reaches into
them.
