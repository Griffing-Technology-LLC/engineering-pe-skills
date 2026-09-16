# Per-Unit System, Three-Phase Power, and Transformers

Reference file for the `electrical-engineering` skill. Standard power-systems
methods, governed generally by IEEE's colour-book series [REF-SOC-005] as the
discipline's SDO; formulas below are conventional forms and are not
individually cited beyond that governing framework, in keeping with this
repository's treatment of the FE-level `thermodynamics` and
`statics-and-dynamics` skills.

## 1. Why per-unit

Per-unit normalises every quantity to a chosen base, so that transformer
turns ratios disappear from the arithmetic and quantities of wildly different
magnitude (a 500 MVA generator and a 100 kVA load) become comparable numbers
near 1.0. **The base must be declared and carried through every step** — a
per-unit number without its base is not a result.

$$Z_{base} = \frac{kV_{base}^2}{MVA_{base}}, \qquad
  I_{base} = \frac{MVA_{base} \times 1000}{\sqrt{3}\,kV_{base}}\ \text{(three-phase)}$$

$$Z_{pu} = \frac{Z_{actual}}{Z_{base}}$$

**Changing base** for an impedance already in per-unit on a different base:

$$Z_{pu,new} = Z_{pu,old} \times \frac{MVA_{base,new}}{MVA_{base,old}} \times
  \left(\frac{kV_{base,old}}{kV_{base,new}}\right)^2$$

Apply this to **every** per-unit impedance pulled from a nameplate or a table
before combining it with anything else in the study — nameplate impedance is
almost never already on the study's chosen base.

## 2. Three-phase power quantities

For a balanced three-phase system:

$$S = \sqrt{3}\,V_{LL}\,I_L, \qquad P = \sqrt{3}\,V_{LL}\,I_L\cos\theta,
  \qquad Q = \sqrt{3}\,V_{LL}\,I_L\sin\theta$$

$S$ — apparent power (VA); $P$ — real power (W); $Q$ — reactive power (VAR);
$\theta$ — power factor angle; $V_{LL}$ — line-to-line voltage; $I_L$ — line
current. **State whether a quantity is per-phase or total three-phase** —
mixing the two is a routine and consequential error.

**Power triangle:** $S = \sqrt{P^2+Q^2}$, power factor $= P/S = \cos\theta$.
A **lagging** power factor (inductive load) draws reactive power from the
source; a **leading** power factor (capacitive) supplies it. Power-factor
correction adds capacitance to reduce the reactive component the source must
carry — size it from the actual $Q$ to be offset, not a rule of thumb.

## 3. Symmetrical components — when the system is not balanced

Any unbalanced three-phase condition (most fault types) resolves into three
balanced sequence networks — positive, negative, and zero:

$$V_a = V_0 + V_1 + V_2, \qquad V_b = V_0 + a^2 V_1 + a V_2,
  \qquad V_c = V_0 + a V_1 + a^2 V_2$$

$a = 1\angle120°$. Positive-sequence impedance is the normal balanced-system
impedance; negative-sequence is typically close to positive-sequence for
static equipment; **zero-sequence depends on the grounding and winding
connection** and is the sequence network that changes most between
equipment types — never assume it equals positive-sequence. See
`references/protection-and-fault-analysis.md` for how each sequence network
connects for each fault type.

## 4. Transformers

**Turns ratio and per-unit impedance:**

$$\frac{V_p}{V_s} = \frac{N_p}{N_s} = a_t$$

On its own rated base, a transformer's per-unit impedance is the same
referred to either winding — this is exactly why per-unit analysis eliminates
the turns ratio from multi-transformer system studies, provided every
impedance is correctly base-converted per §1.

**Winding connection sets the zero-sequence path.** A delta winding blocks
zero-sequence current from flowing through to the other side; a grounded-wye
winding provides a zero-sequence path to ground. This single fact governs
whether a transformer contributes to, or blocks, ground-fault current on
each side — state the winding connection (Dyn11, YNyn0, Dyn1, etc.)
explicitly before any ground-fault or zero-sequence calculation.

**Impedance voltage** (nameplate %Z) is the per-unit impedance directly, on
the transformer's own base — convert to the study base per §1 before use.

## 5. Load flow, at the level this skill covers

A full load-flow (Newton-Raphson or fast-decoupled) solution is a numerical
method beyond hand calculation and is **out of scope for this reference
file** — state that explicitly and hand off to a load-flow study tool for
anything beyond a simple radial-feeder voltage-drop check:

$$\Delta V \approx \frac{P\,R + Q\,X}{V}$$

(approximate voltage drop along a short feeder, real and reactive power flow
$P$, $Q$, resistance $R$ and reactance $X$ of the feeder, nominal voltage
$V$ — valid only for small angle differences and a radial, not meshed,
topology).
