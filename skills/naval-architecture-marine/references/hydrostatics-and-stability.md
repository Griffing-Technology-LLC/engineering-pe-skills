# Hydrostatics and Intact Stability

Reference file for the `naval-architecture-marine` skill. Numeric criteria in
§3 are read verbatim from the IMO 2008 IS Code, 2020 Edition [REF-IMO-001].
Method framework (KB, BM, GZ) is standard naval-architecture practice
[REF-SNAME-001]; no specific PNA page is cited — see the caution against
REF-SNAME-001 in `REFERENCES.md`.

## 1. Buoyancy and displacement

Archimedes' principle: a floating body displaces a weight of fluid equal to its
own weight.

$$\Delta = \rho \, \nabla$$

$\Delta$ — displacement (mass, `t` or `lbm`); $\rho$ — water density
(salt water $\approx 1.025\ \mathrm{t/m^3}$, fresh $\approx 1.000\ \mathrm{t/m^3}$
— **the difference is not negligible for draft and stability**); $\nabla$ —
underwater volume.

**Tonnes per centimetre immersion (TPC):**

$$TPC = \frac{A_{wp}\,\rho}{100}$$

$A_{wp}$ — waterplane area. Use TPC for small draft-change estimates only; it
assumes a near-vertical, near-constant waterplane over the change.

**Fresh water allowance (FWA)** corrects the load-line draft for the density
change between salt and fresh water — apply it, do not assume salt-water
density universally.

## 2. Metacentric height and the righting arm

$KB$ is read from the hull form or hydrostatic curves.

$$BM = \frac{I_T}{\nabla}$$

$I_T$ — transverse second moment of the waterplane area about the centreline.
Then:

$$KM = KB + BM, \qquad GM = KM - KG$$

$GM$ — metacentric height, the small-angle stability lever arm about the
initial upright condition. **Valid only for small heel angles** (roughly
$< 10°$–$15°$) where $BM$ is effectively constant; beyond that, use the actual
GZ (cross) curves, not $GM\sin\varphi$.

**Righting arm (GZ):**

$$GZ = KN - KG\sin\varphi \quad \text{(from cross curves of stability, "KN curves")}$$

or, at small angles only:

$$GZ \approx GM \sin\varphi$$

**Free surface correction — never skip this.** A slack (partially full) tank
generates a free-surface moment $FSM$ that reduces the *effective* GM:

$$GM_{eff} = GM - \frac{FSM}{\Delta}$$

$FSM$ sums over every slack tank; a single large slack tank can eliminate most
of a vessel's stability margin. This applies "in all conditions of loading"
per the Code itself [REF-IMO-001 §2.1.2].

## 3. IMO 2008 IS Code, Part A — general intact stability criteria

Read verbatim from the 2020 Edition [REF-IMO-001], applicable to cargo and
passenger ships $\geq 24$ m in length (§1.1.1):

| § | Criterion |
| --- | --- |
| 2.2.1 | Area under GZ curve $\geq 0.055$ m·rad up to $\varphi = 30°$ |
| 2.2.1 | Area under GZ curve $\geq 0.090$ m·rad up to $\varphi = 40°$ (or $\varphi_f$ if less) |
| 2.2.1 | Area between $30°$ and $40°$ (or $30°$–$\varphi_f$) $\geq 0.030$ m·rad |
| 2.2.2 | $GZ \geq 0.20$ m at an angle of heel $\geq 30°$ |
| 2.2.3 | Max GZ occurs at heel $\geq 25°$ (or approved equivalent) |
| 2.2.4 | Initial metacentric height $GM_0 \geq 0.15$ m |

All criteria in this table apply **simultaneously** — none supersedes another.

### Severe wind and rolling ("weather") criterion — §2.3

Independent of the table above; evaluate it separately.

1. Steady wind heeling lever:
   $$l_{w1} = \frac{P\,A\,Z}{1000\,g\,\Delta}\ \text{(m)}, \qquad P = 504\ \mathrm{Pa}$$
   $A$ — projected lateral windage area above the waterline (m²); $Z$ —
   vertical distance from the centre of $A$ to the centre of underwater
   lateral area, or approximately half draft (m); $g = 9.81\ \mathrm{m/s^2}$.
2. Steady heel angle $\varphi_0$ from $l_{w1}$ against the GZ curve; must not
   exceed $16°$ or 80% of the deck-edge immersion angle, whichever is less.
3. Gust heeling lever: $l_{w2} = 1.5\,l_{w1}$.
4. Windward roll angle $\varphi_1$ (from Code Part B / an approved method), then
   **area $b \geq$ area $a$** per the Code's Figure 2.3.1-1, evaluated between
   $\varphi_0$ and $\varphi_2$ ($\varphi_2$ = down-flooding angle, $50°$, or the
   second GZ/wind-lever intercept $\varphi_c$ — whichever is least).
5. An alternative test method may substitute a measured wind speed of
   26 m/s full-scale, subject to Administration approval [REF-IMO-001 §2.3.3].

**This skill states the criteria; it does not perform the roll-angle
prediction of §2.3.1.2**, which draws on Part B methods not yet catalogued in
this repository. Flag that gap explicitly if a weather-criterion check is
requested in full.

## 4. Trim

Trim is the difference between forward and aft drafts. For a small trimming
moment about the centre of flotation (LCF):

$$t = \frac{Trimming\ Moment}{MCT1cm}$$

$MCT1cm$ — moment to change trim 1 cm, a hydrostatic-curve property. Report
trim by the bow or by the stern explicitly — the sign convention is a common
source of error.

## 5. Out of scope here

Longitudinal hull-girder strength, scantlings, classification-society
structural rules, damage stability (a separate IMO framework from intact
stability), and load-line freeboard tables are **not covered** by this
reference file. Name them explicitly as out of scope when a request reaches
into them.
