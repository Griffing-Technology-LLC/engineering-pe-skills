# Analog and Digital Circuit Design, Data Conversion, and PCB Rules

Reference file for the `electronics-engineering` skill. Circuit-theory
content (op-amps, filters, logic timing, ADC/DAC theory) is standard
electronics-engineering theory, stated here without a per-equation citation,
matching the convention used elsewhere in this repository. PCB design-rule
content is cited to **IPC-2221** [REF-IPC-001] — no specific table value is
asserted here; confirm the current edition directly per `SKILL.md`'s caution.

## 1. Operational amplifier fundamentals

An ideal op-amp analysis assumes: infinite open-loop gain, infinite input
impedance, zero output impedance, and (in negative-feedback configurations)
that the two inputs are held at the same voltage ("virtual short"). Real
devices deviate from all four assumptions — **state which deviation matters
for the circuit under analysis** rather than defaulting silently to the
ideal case:

| Non-ideality | Where it matters |
| --- | --- |
| Finite gain-bandwidth product (GBW) | High closed-loop gain at high frequency — closed-loop bandwidth $\approx$ GBW / (1 + closed-loop gain) |
| Input bias/offset current | High-impedance sources, precision DC circuits |
| Input offset voltage | Precision DC circuits, especially at high closed-loop gain |
| Slew rate | Large-signal, high-frequency, or fast-edge outputs — check against required $dV/dt$ |
| Output current/voltage swing limits | Driving low-impedance loads or near-rail outputs |

Common configurations (inverting, non-inverting, differential, instrumentation
amplifier) each have standard gain equations set by the external feedback
network — **state the configuration explicitly** before quoting a gain
formula, since the inverting and non-inverting gain expressions differ by
whether the input signal path includes the input resistor to ground.

## 2. Passive and active filters

Classify a filter request along two independent axes before selecting a
topology:

1. **Response type** — lowpass, highpass, bandpass, bandstop/notch, allpass.
2. **Approximation** — Butterworth (maximally flat passband), Chebyshev
   (steeper rolloff, passband ripple), Bessel (maximally flat group delay,
   preserves pulse shape), elliptic/Cauer (steepest rolloff, ripple in both
   bands). **State which approximation governs and why** — a Bessel filter
   is the right choice when pulse/waveform shape matters more than rolloff
   steepness, and the wrong choice when steep out-of-band rejection is the
   requirement.

Passive (RLC) filters need no power supply and introduce no active-device
noise or bandwidth limit, but cannot provide gain and their performance
degrades with non-ideal (finite-Q) components, especially inductors. Active
(op-amp-based) filters avoid bulky inductors and can provide gain, but are
bounded by the active device's GBW and slew-rate limits (§1) — **check the
active device's bandwidth against the filter's cutoff frequency**, not just
against the nominal signal frequency.

## 3. Amplifier basics beyond the op-amp

For discrete transistor amplifier stages (BJT or FET), state the **bias
point** (DC operating point) before any small-signal gain analysis — small-
signal parameters ($g_m$, $r_\pi$, $r_o$, or FET transconductance) are
themselves functions of the bias point, so a gain result without a stated
bias point is incomplete. Distinguish clearly between:

* **Small-signal gain** — valid only for signal excursions small enough that
  the device's transfer characteristic is locally linear around the bias
  point.
* **Large-signal / power considerations** — clipping, slew-rate limiting, and
  class of operation (A, B, AB, C for power stages) all require large-signal
  analysis distinct from the small-signal model.

## 4. Digital logic families and interface compatibility

**Never assert digital interface compatibility from the fact that "both
sides are digital."** Check explicitly:

* **Supply/logic voltage** — e.g., 5 V TTL/CMOS, 3.3 V LVCMOS, 1.8 V, LVDS
  (differential, ~350 mV swing) are not interchangeable without level
  translation.
* **$V_{OH}$/$V_{OL}$ (driver output high/low levels) against $V_{IH}$/
  $V_{IL}$ (receiver input high/low thresholds)** on the specific devices
  involved — a driver's guaranteed $V_{OH}$ must exceed the receiver's
  $V_{IH}$ with margin, and symmetrically for $V_{OL}$/$V_{IL}$.
* **Drive strength / fan-out** — a driver's guaranteed output current at its
  specified voltage must supply every load's input current (and any
  termination current, §5 of `signal-integrity-and-emc.md`) without the
  output voltage sagging below the required threshold.
* **Timing** — setup and hold time at the receiving device against the
  driving device's output timing and the interconnect's propagation delay;
  flag a setup/hold violation as a named failure mode, not a vague "timing
  might be tight."

## 5. Analog-to-digital and digital-to-analog conversion

Key parameters, always stated together (a resolution number alone is not a
complete ADC/DAC specification):

* **Resolution** ($N$ bits) — sets the ideal quantization step,
  $\text{LSB} = V_{FS} / 2^N$, where $V_{FS}$ is the full-scale range.
* **Sample rate** — must satisfy the Nyquist criterion, $f_s > 2 f_{max}$,
  for the highest frequency component of interest in the input signal;
  **state the anti-aliasing filter** that enforces this in practice, since
  no real signal is perfectly band-limited.
* **Effective number of bits (ENOB)** — the resolution actually achieved
  after accounting for noise and distortion, typically lower than the
  nominal $N$; do not conflate nominal resolution with achieved accuracy.
* **Reference voltage stability and accuracy** — the conversion is only as
  accurate as $V_{FS}$; a drifting or noisy reference degrades every
  conversion regardless of the converter's own linearity.

**Aliasing** occurs when the Nyquist criterion is violated — energy above
$f_s/2$ folds back into the baseband and is indistinguishable from a real
low-frequency signal after conversion. **Always state the anti-aliasing
provision** (or its explicit absence) when reporting a sampled-data result.

## 6. Board-level power regulation

At the board level, distinguish:

* **Linear regulation** — simple, low noise, but dissipates power
  proportional to $(V_{in} - V_{out}) \times I_{load}$; check the resulting
  thermal dissipation against the regulator's package rating and the board's
  thermal design, not just against its voltage/current datasheet limits.
* **Switching regulation** — higher efficiency across a wider input/output
  differential, but introduces switching-frequency ripple and harmonics that
  become an EMC concern (§5–§7 of `signal-integrity-and-emc.md`) and
  requires its own layout discipline (tight switch-node loop area, proper
  input/output capacitor placement).

**Decoupling** (local bypass capacitance at each IC) serves both power-
integrity (maintaining local supply voltage during fast current transients)
and EMC (§7 of `signal-integrity-and-emc.md`) purposes simultaneously —
report a decoupling recommendation against both concerns, not just one.

## 7. Digital timing margins

Report any timing-margin result as an explicit inequality against the
governing constraint, e.g., "setup time margin = (available time) −
(required setup time) = *n* ns, positive/negative" — never as a bare
"timing is fine" without the numbers that were checked. Include clock skew
and jitter explicitly where the interconnect or clock distribution network
introduces them; a margin computed against an ideal (jitter-free) clock
overstates the true margin.

## 8. PCB design rules — conductor spacing and current-carrying capacity

**IPC-2221** [REF-IPC-001] is the generic printed-board design standard
covering conductor spacing (for a given voltage, to avoid dielectric
breakdown or arcing) and conductor current-carrying capacity (trace width
vs. current, for a given copper weight and allowable temperature rise),
among other design areas (mechanical, thermal, environmental, reliability).

**Never assert a specific IPC-2221 trace-width, spacing, or current-capacity
table value from memory.** These depend on copper weight, ambient and
allowable temperature rise, internal-vs-external layer placement, and the
specific edition in force — confirm against the current standard text
directly. State the *inputs* the lookup needs (current, copper weight,
allowable temperature rise, internal/external layer) rather than guessing
the output.
