# Stress, Failure Theories, Fatigue, and Allowables

Reference file for the `mechanical-engineering` skill.

## Contents

1. Stress state
2. Stress concentration
3. Static failure theories
4. Fatigue
5. Buckling
6. Allowables and where they come from

---

## 1. Stress state

Principal stresses in plane stress:

$$\sigma_{1,2} = \frac{\sigma_x + \sigma_y}{2}
  \pm \sqrt{\left(\frac{\sigma_x - \sigma_y}{2}\right)^{2} + \tau_{xy}^{2}}$$

Maximum in-plane shear:

$$\tau_{\max} = \sqrt{\left(\frac{\sigma_x - \sigma_y}{2}\right)^{2} + \tau_{xy}^{2}}$$

**In 3-D the absolute maximum shear** is $(\sigma_{\max} - \sigma_{\min})/2$
over
all three principal stresses, including the zero one in plane stress. Using only
the in-plane value under-predicts shear whenever both in-plane principals share
a
sign — a routine and dangerous omission.

Common elementary stresses:

| Loading | Stress |
| --- | --- |
| Axial | $\sigma = P/A$ |
| Bending | $\sigma = Mc/I$ |
| Transverse shear | $\tau = VQ/(It)$ |
| Torsion, circular | $\tau = Tr/J$ |
| Thin-wall pressure vessel | $\sigma_h = pr/t$, $\sigma_l = pr/(2t)$ |

Hoop stress is **twice** longitudinal in a cylinder — which is why pressure
vessels split along their length, not around their circumference.

## 2. Stress concentration

At any geometric discontinuity:

$$\sigma_{\max} = K_t \sigma_{nom}$$

$K_t$ is geometric, from a chart or FEA, and depends on the ratio of feature
size
to member size. **Always state which nominal area the chart's $K_t$ is
referenced
to** — gross or net section. Getting that wrong is a silent factor-of-two error.

For fatigue, $K_t$ is reduced by notch sensitivity $q$:

$$K_f = 1 + q(K_t - 1)$$

For **static** loading of a ductile material, local yielding redistributes
stress
and $K_t$ is commonly neglected. For **brittle** materials and for **all**
fatigue, it never is.

## 3. Static failure theories

**Ductile materials:**

*Maximum distortion energy (von Mises)* — the standard choice:

$$\sigma' = \sqrt{\sigma_1^{2} - \sigma_1\sigma_2 + \sigma_2^{2}} \le \frac{S_y}{n}$$

*Maximum shear stress (Tresca)* — more conservative, simpler:

$$\tau_{\max} = \frac{\sigma_{\max} - \sigma_{\min}}{2} \le \frac{S_y}{2n}$$

**Brittle materials** — maximum normal stress or modified Mohr, using $S_{ut}$
and
$S_{uc}$ separately, since brittle materials are far stronger in compression.

Name the theory used. "The margin is 1.4" without naming the theory is not a
result.

## 4. Fatigue

Most machine failures are fatigue failures, and they occur at stresses well
below
yield.

**Endurance limit.** For steels, an uncorrected estimate is often taken as
$S'_e \approx 0.5 S_{ut}$ up to a cap. **Aluminium and polymers have no true
endurance limit** — their S-N curves keep descending, so design is to a finite
life, never to an "infinite life" asymptote. Applying steel practice to
aluminium
or printed polymer is a category error.

The corrected endurance limit applies Marin-type factors:

$$S_e = k_a k_b k_c k_d k_e S'_e$$

for surface finish, size, load type, temperature, and reliability. State every
factor and its source.

**Mean stress.** Fluctuating loads decompose into:

$$\sigma_a = \frac{\sigma_{\max} - \sigma_{\min}}{2}, \qquad
  \sigma_m = \frac{\sigma_{\max} + \sigma_{\min}}{2}$$

Then apply a named criterion — **Goodman** (linear to $S_{ut}$, common and
moderately conservative), **Gerber** (parabolic, less conservative),
**Soderberg** (linear to $S_y$, most conservative, guards yield too). Goodman:

$$\frac{\sigma_a}{S_e} + \frac{\sigma_m}{S_{ut}} = \frac{1}{n}$$

**Check first-cycle yield separately.** A design can pass a fatigue criterion
and
still yield on the first application of peak load.

## 5. Buckling

Slender members in compression fail by instability long before they reach yield.

$$P_{cr} = \frac{\pi^{2} EI}{(KL)^{2}}$$

$K$ is the end-condition factor: 1.0 pinned-pinned, 0.5 fixed-fixed, 0.7
fixed-pinned, 2.0 fixed-free. **The fixed-free cantilever at $K = 2$ is four
times
weaker than pinned-pinned** — end conditions dominate this calculation.

Euler applies only above a critical slenderness ratio $KL/r$. Below it, the
member is intermediate or short and an empirical formula (Johnson) or plain
yielding governs. Check the slenderness before choosing the equation.

**Buckling depends on the minimum $I$**, about the weak axis. Checking only the
strong axis is a standard error.

## 6. Allowables and where they come from

An allowable is a cited number, never a remembered one. Acceptable sources:

* A material specification (ASTM, AMS, SAE) by designation and revision
* A code table (ASME BPVC, AISC) by table number and edition
* Test data on the actual material and process, with sample size and basis
  (A-basis, B-basis, typical)

**"Typical" values are not design allowables.** They are the mean of a
distribution — roughly half the population falls below. Design to a statistical
basis, and say which one.

### Additively manufactured polymer

Printed polymer is **orthotropic and process-dependent**, and handbook isotropic
practice does not transfer:

* Strength across layers (Z) is a fraction of in-plane strength, governed by
  interlayer adhesion rather than the bulk polymer.
* Properties vary with nozzle and bed temperature, layer height, raster angle,
  cooling, and moisture — machine to machine and week to week.
* There is no endurance limit; design to finite life.
*  The print orientation is a **design variable**, and must appear on the
  drawing.
  A part is not fully specified without it.

Where a critical value is uncertain or the process has appreciable variability,
14 CFR §23.2265 [REF-FAA-002] is a useful model even outside aviation: it
requires a *special* factor of safety over and above the basic one, and requires
the highest pertinent special factor to multiply each limit and ultimate load.
Related, §23.2260(b) requires processes needing close control to run under an
approved process specification — for FDM that means the print profile is part of
the design record, not a shop-floor choice.
