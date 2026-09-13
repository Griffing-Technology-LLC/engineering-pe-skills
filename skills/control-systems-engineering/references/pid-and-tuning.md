# PID Forms, Tuning, and Loop Structures

Reference file for the `control-systems-engineering` skill.

## 1. Declare the PID form first

Vendors implement different algebra under the same name. **Gains are not
portable
between forms**, and moving a tuning set from one controller to another without
converting is a common and avoidable failure.

**Ideal / non-interacting:**

$$u(t) = K_c\left[e + \frac{1}{T_i}\int e\,\mathrm{d}t + T_d\frac{\mathrm{d}e}{\mathrm{d}t}\right]$$

**Parallel / independent:**

$$u(t) = K_p e + K_i\int e\,\mathrm{d}t + K_d\frac{\mathrm{d}e}{\mathrm{d}t}$$

**Series / interacting** — common in older analogue-derived DCS.

Also state whether integral is $T_i$ (minutes/repeat) or $K_i$ (repeats/minute)
—
they are reciprocals, and confusing them inverts the tuning.

## 2. What each term does

* **Proportional** — acts on present error. Alone, it leaves steady-state offset
  on any self-regulating process.
* **Integral** — eliminates offset by acting on accumulated error. It adds phase
  lag, so it always costs stability margin.
* **Derivative** — acts on rate of change, adding phase lead and damping. It
  amplifies measurement noise, and must be filtered.

**Derivative on measurement, not on error.** Otherwise a setpoint step produces
a
derivative kick — a large transient spike at the actuator. Most modern
controllers default to this; verify rather than assume.

**Do not use derivative on noisy or fast loops.** Flow and pressure loops are
normally PI. Temperature loops, being slow and smooth, are where derivative
earns
its place.

## 3. Tuning methods

**Ziegler-Nichols** — historically important, and aggressive. It targets roughly
quarter-amplitude decay, giving about 20–25% overshoot and thin margins. Treat
it
as a starting point, not a delivery.

**Lambda / IMC tuning** — specify a desired closed-loop time constant $\lambda$
and compute gains from the FOPDT model. Preferred for most process loops because
it makes the robustness/performance trade explicit: larger $\lambda$ is slower
and more robust. A common conservative choice is $\lambda \ge \theta$, or
$\lambda \approx \tau$ for a well-damped response.

**Cohen-Coon** — better than Z-N for dead-time-dominant processes, still fairly
aggressive.

Whatever the method, **verify the resulting margins** (see `loop-dynamics.md`)
rather than trusting the rule.

## 4. Structure beats tuning

Reach for structure before aggressive gains:

**Cascade** — an inner loop around a fast disturbance, outer loop on the primary
variable. The inner loop must be substantially faster than the outer, typically
by a factor of 3 to 5, or the two will interact. Cascade rejects inner-loop
disturbances far better than any single-loop tuning can.

**Feedforward** — measure the disturbance and act before the error appears.
Essential where dead time makes feedback inherently slow. Always **combine with
feedback**; feedforward alone has no error correction and drifts with model
mismatch.

**Ratio** — hold one flow proportional to another.

**Override / selector** — a constraint controller takes over when a limit is
approached. Requires anti-windup on the loop not currently selected, or it will
bump on transfer.

## 5. The non-linear reality

Textbook tuning assumes a linear plant and unlimited actuator. Neither holds.

**Integral windup.** When the actuator saturates, error persists and the
integral
term keeps accumulating, so the controller overshoots badly on recovery. Every
practical PID needs anti-windup — conditional integration or back-calculation.
This is not optional on any loop that can saturate, which is nearly all of them.

**Bumpless transfer** between manual and auto, and on setpoint changes.

**Valve reality** — deadband, stiction, hysteresis, and an inherent
characteristic that is rarely linear. Stiction produces a limit cycle that looks
like poor tuning but is not, and **retuning will not fix it.** A loop cycling
with a square-ish output and a sawtooth PV is stiction; the fix is mechanical.

**Sensor failure behaviour** — define what the loop does on loss of measurement.
Holding the last value, failing to manual, and driving to a safe output are
different choices with different consequences; make it deliberate.

## 6. Reporting a tuning result

State the controller form, the gains in that form's units, the plant model used,
the resulting gain and phase margins with frequencies, and the loop's behaviour
on saturation and sensor loss. A step response plot alone is not a deliverable.
