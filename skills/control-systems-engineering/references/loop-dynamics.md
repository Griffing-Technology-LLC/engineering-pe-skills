# Loop Dynamics: Transfer Functions, Stability, Frequency Response

Reference file for the `control-systems-engineering` skill.

## 1. Plant models

Most industrial processes are adequately captured by **first-order plus dead
time (FOPDT)**:

$$G(s) = \frac{K_p e^{-\theta s}}{\tau s + 1}$$

Three parameters carry nearly all the design information:

* $K_p$ — process gain, Δoutput/Δinput **in stated units**
* $\tau$ — time constant, to 63.2% of the final change
* $\theta$ — dead time, before any response begins

Identify them from an open-loop step test: step the output in manual, record,
and fit. State how the model was obtained; a controller tuned against an
unidentified plant is a guess.

**Integrating processes** (level in a tank, position from velocity) have no
steady state and take $G(s) = K_p e^{-\theta s}/s$. Tuning rules for
self-regulating processes do not apply to them, and using them is a common cause
of slow cycling on level loops.

## 2. Why dead time is the binding constraint

The controllability ratio $\theta/\tau$ bounds achievable performance:

| $\theta/\tau$ | Consequence |
| --- | --- |
| < 0.2 | Easy; aggressive tuning viable |
| 0.2 – 1.0 | Moderate; standard PID with care |
| > 1.0 | Difficult; consider dead-time compensation or a better measurement location |

Dead time contributes phase lag without attenuation — it costs stability margin
and gives nothing back. **No amount of tuning removes dead time.** When
$\theta/\tau$ is large the honest answer is usually to move the sensor, not to
retune. Report this ratio in every loop analysis.

## 3. Closed-loop form

For a loop with controller $G_c$, plant $G_p$, and feedback $H$:

$$\frac{Y}{R} = \frac{G_c G_p}{1 + G_c G_p H}$$

The **characteristic equation** $1 + G_c G_p H = 0$ governs stability. Closed-loop
poles must lie in the left half of the s-plane.

Second-order standard form:

$$\frac{\omega_n^{2}}{s^{2} + 2\zeta\omega_n s + \omega_n^{2}}$$

with overshoot set by $\zeta$ alone, and settling time by $\zeta\omega_n$.

## 4. Stability margins

Determining stability is necessary but not sufficient — **report the margins**:

* **Gain margin** — factor by which loop gain may rise before instability,
  measured where phase crosses −180°. Typical target: 2 to 5 (6 to 14 dB).
* **Phase margin** — additional phase lag tolerable, measured where gain crosses
  0 dB. Typical target: 30° to 60°.

Phase margin correlates with damping: roughly $\zeta \approx PM/100$ for
moderate values. A loop with 15° phase margin is technically stable and
practically useless — it will ring on every disturbance and go unstable on any
process change.

Always name the frequency at which each margin occurs. A margin without its
frequency cannot be compared against the plant's expected variation.

## 5. Robustness is the real requirement

The plant you tuned against is not the plant you will run. Process gain varies
with throughput, valve characteristics are non-linear, and heat exchangers foul.

**Tune for the worst-case plant, not the nominal one.** Where process gain varies
with operating point, either tune at the highest-gain condition or apply gain
scheduling. A loop tuned tight at low throughput commonly goes unstable at high
throughput, and this is one of the most frequent causes of loops being left in
manual.
