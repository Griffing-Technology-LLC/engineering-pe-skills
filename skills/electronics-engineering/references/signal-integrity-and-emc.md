# Transmission Lines, Signal Integrity, and EMC

Reference file for the `electronics-engineering` skill. Signal-integrity
theory is standard electromagnetics/circuit-theory content and is stated here
without a per-equation citation, matching the convention used in
`electrical-engineering/references/protection-and-fault-analysis.md`. EMC
regulatory and test-method content is cited to **47 CFR Part 15**
[REF-FCC-001] and **IEEE/ANSI C63.4** [REF-IEEE-002] — no specific numeric
limit or table value from either is asserted here; confirm the current text
directly per `SKILL.md`'s caution.

## 1. Lumped vs. distributed regime

A trace behaves as a **lumped** (ordinary circuit-theory) element when its
physical length is short relative to the signal's electrical wavelength —
conventionally, when the one-way propagation delay along the trace is small
compared to the signal's rise/fall time (roughly, propagation delay less than
about one-sixth of the rise time is a common rule-of-thumb threshold; treat
this as a rough screening test, not a precise boundary). Otherwise the trace
is **distributed** and must be analyzed with transmission-line theory —
reflections, standing waves, and impedance discontinuities all require the
distributed treatment.

**Always state which regime applies before choosing a method.** Applying
lumped circuit theory to an electrically long trace, or full transmission-line
analysis to a genuinely short one, both produce wrong or needlessly
complicated results.

## 2. Characteristic impedance

For a lossless transmission line:

$$Z_0 = \sqrt{\frac{L'}{C'}}$$

where $L'$ and $C'$ are the per-unit-length inductance and capacitance of the
line geometry (microstrip, stripline, coplanar waveguide, twisted pair,
coaxial, etc.). $Z_0$ depends on the physical geometry and the surrounding
dielectric — a change in trace width, dielectric height, or dielectric
constant changes $Z_0$. **State the geometry assumed** (e.g., microstrip over
a solid reference plane) before quoting a $Z_0$ result; closed-form
approximations for common PCB geometries (microstrip, stripline) exist in
standard signal-integrity references and are geometry-specific — do not apply
a microstrip formula to a stripline geometry or vice versa.

## 3. Reflections and termination

At any impedance discontinuity, the reflection coefficient is:

$$\Gamma = \frac{Z_L - Z_0}{Z_L + Z_0}$$

applied separately at the **load** end (using the load impedance $Z_L$) and
at the **source** end (using the source impedance $Z_S$ in place of $Z_L$).
**Report both** where the source is not already matched to $Z_0$ — a
source-end reflection can re-reflect off the load and produce ringing that a
load-only analysis misses.

Common termination strategies, each trading off differently:

| Strategy | Placement | Trade-off |
| --- | --- | --- |
| Series (source) termination | At the driver, in series | Simple, low power; only fully effective for a single unbranched load (point-to-point) |
| Parallel (end/load) termination | At the receiver, to a reference rail | Effective for multi-drop topologies; draws continuous DC current |
| AC (RC) termination | At the receiver, through a capacitor | Limits steady-state power draw; adds a pole that must be checked against signal bandwidth |
| Differential termination | Across a differential pair, at the receiver | Matches the pair's differential impedance, not each leg's single-ended impedance individually |

**Never recommend a termination value without confirming which impedance it
is meant to match** — single-ended $Z_0$ and differential impedance $Z_{diff}$
are related but not interchangeable ($Z_{diff} \approx 2 Z_0$ only in the
weak-coupling limit; tightly coupled pairs deviate from this approximation
and need the coupled-line result).

## 4. Crosstalk and eye diagrams

**Crosstalk** between adjacent traces arises from mutual inductance and
mutual capacitance between them. Qualitatively:

* **Near-end crosstalk (NEXT)** appears at the aggressor's driving end of the
  victim line; **far-end crosstalk (FEXT)** appears at the far end.
* Coupling increases with parallel-run length, decreases with separation
  distance, and is strongly affected by reference-plane continuity —
  crosstalk driven by a gap or split in the return path can dominate over
  simple trace-to-trace spacing effects.
* **State the aggressor/victim pairing and the parallel-run geometry**
  explicitly before making a crosstalk claim; a bare "these traces are too
  close" statement without geometry is not a finding.

An **eye diagram** is the standard tool for judging a digital link's overall
signal-integrity margin: overlaying many unit intervals of a data stream
reveals the combined effect of reflections, crosstalk, jitter, and
inter-symbol interference as eye closure (reduced voltage and/or timing
margin). **Report an eye-diagram-based result as margin against a stated mask
or budget** (voltage opening, timing opening, or both) — never as a bare
"eye looks fine" qualitative statement without the specific margin numbers
that were checked.

## 5. EMC — emissions and immunity, framework

**Electromagnetic compatibility (EMC)** has two complementary requirements:

* **Emissions** — the device must not radiate or conduct interference beyond
  a specified limit.
* **Immunity (susceptibility)** — the device must continue to function
  correctly when exposed to a specified level of external interference.

**IEEE/ANSI C63.4** [REF-IEEE-002] defines standardized measurement methods,
instrumentation, and test-site requirements for radiated and conducted
radio-noise emissions from low-voltage electrical and electronic equipment,
9 kHz to 40 GHz. It is a **test-method** standard — it specifies *how* to
measure, not the numeric limit a device must meet; the numeric limits
themselves are set by the applicable regulatory framework (in the US, FCC
Part 15 for unlicensed devices) [REF-FCC-001].

## 6. FCC Part 15 — US regulatory framework

**47 CFR Part 15** [REF-FCC-001] governs devices that may be operated in the
US without an individual license — it covers **intentional radiators**
(devices designed to emit RF energy, e.g., a wireless transmitter),
**unintentional radiators** (devices that use digital logic or RF-frequency
signals internally but are not intended to radiate, e.g., most digital
electronics), and **incidental radiators**. Devices are classified:

* **Class A** — intended for use in a commercial/industrial environment.
* **Class B** — intended for use in a residential environment; **Class B
  limits are more restrictive than Class A**, reflecting the closer typical
  proximity to other receivers.

**Never assert a specific numeric emissions limit (dBµV/m, dBµV, etc.) from
memory.** These are frequency-band- and class-specific, and are defined in
the current 47 CFR Part 15 text (primarily Subpart B for unintentional
radiators). State the applicable subpart and class, and defer the specific
limit table to the current regulation. Equipment authorization procedures
(certification vs. Supplier's Declaration of Conformity) are likewise
device-category-specific — do not assert which procedure applies to a given
device without confirming its classification against the current rule text.

## 7. Board-level grounding and shielding for EMC

At the board level, the dominant EMC design levers are:

* **A continuous, unbroken reference plane** under high-speed or RF traces —
  a split or gap in the return path forces return current to detour, which
  increases both radiated emissions and crosstalk (§4).
* **Decoupling capacitor placement and value selection** close to each IC
  power pin, sized to present low impedance across the frequency range of
  the switching currents involved — this is as much an EMC control as a
  power-integrity control.
* **Physical separation and orientation** of noisy (switching, RF) circuitry
  from sensitive (analog, low-level) circuitry, including connector and
  cable-exit placement relative to both.
* **Shielding**, where required, must maintain electrical continuity around
  the protected region — a shield with an unclosed seam or an ungrounded
  connector shell provides little benefit at the frequencies where shielding
  is usually needed.

These are qualitative design practices, not numeric standards; a specific
EMC pass/fail determination still requires either an accredited test per
IEEE/ANSI C63.4 or FCC Part 15's specified procedures, or a stated pre-
compliance estimate flagged explicitly as such.
