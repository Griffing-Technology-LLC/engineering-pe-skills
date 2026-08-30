# Machine Elements: Shafts, Bearings, Gears, Springs, Joints

Reference file for the `mechanical-engineering` skill.

## 1. Shafts

Shafts see combined bending and torsion, usually fluctuating. Bending stress
reverses every revolution even under a steady load — a rotating shaft under
constant transverse load is a fully reversed fatigue problem, which is the
central fact of shaft design.

For a solid circular shaft under static combined loading:

$$\tau_{\max} = \frac{16}{\pi d^{3}}\sqrt{M^{2} + T^{2}}$$

For fatigue, apply a named criterion (see `materials-and-fatigue.md`) to the
alternating bending and steady torsional components separately, with $K_f$ at
every shoulder, keyway, and groove.

**Check deflection as well as stress.** Shaft slope at bearings and deflection at
gears often govern before stress does — gear misalignment and bearing edge
loading start well below any stress limit. And check the **first critical speed**
against the operating range.

## 2. Rolling-element bearings

Bearing life is statistical, not deterministic:

$$L_{10} = \left(\frac{C}{P}\right)^{p}$$

in millions of revolutions, with $p = 3$ for ball bearings and $10/3$ for roller
bearings. $C$ is the basic dynamic load rating from the manufacturer, $P$ the
equivalent dynamic load combining radial and thrust components.

**$L_{10}$ means 90% survive** — one in ten is expected to fail by that life. It
is not a guaranteed life, and quoting it as one misrepresents the number.

The cube law is unforgiving: **doubling the load cuts ball-bearing life by a
factor of eight.**

## 3. Gears

Two independent checks, both required:

* **Bending strength** at the tooth root (Lewis / AGMA bending) — tooth breakage
* **Surface durability** (Hertzian contact) — pitting and spalling

Surface durability frequently governs in hardened steel gearing, and checking
only bending is a common omission.

Fundamentals:

$$\text{ratio} = \frac{N_2}{N_1}, \qquad m = \frac{d}{N}, \qquad P_d = \frac{N}{d}$$

Tangential tooth load from transmitted power:

$$W_t = \frac{2T}{d}$$

with separating radial load $W_r = W_t \tan\phi$ for a spur gear of pressure
angle $\phi$. That radial component loads the shaft and bearings, and it must
appear in the shaft analysis.

**Minimum tooth count** matters — too few teeth undercuts the root and destroys
bending capacity. Helical gears add an axial thrust component that the bearing
selection must carry.

## 4. Springs

Helical compression spring, shear stress with the Wahl curvature correction:

$$\tau = K_W \frac{8FD}{\pi d^{3}}, \qquad C = \frac{D}{d}$$

Deflection rate:

$$k = \frac{d^{4}G}{8D^{3}N_a}$$

The $d^4$ and $D^3$ dependencies mean small dimensional changes move the rate
sharply. **Check buckling** on long compression springs and **check solid-height
stress** — a spring that can be compressed solid must survive being compressed
solid, because eventually it will be.

## 5. Bolted joints

The most misunderstood machine element, and the most common failure site.

**A properly preloaded joint in tension does not see the full external load.**
Preload $F_i$ puts the bolt in tension and the members in compression; an
external load $P$ is shared by joint stiffness:

$$C = \frac{k_b}{k_b + k_m}$$

Bolt load: $F_b = C P + F_i$. Member load: $F_m = (1 - C)P - F_i$.

Since members are typically much stiffer than the bolt, $C$ is small — often
0.2 to 0.3 — so **most of an external tensile load unloads the members rather
than adding to the bolt**. This is why preload dramatically improves fatigue life:
the bolt's alternating stress is only $C\sigma_a$.

Two failure modes to check beyond bolt tension:

* **Separation** — when $P$ exceeds $F_i/(1-C)$, the joint gaps and the bolt then
  takes the entire load directly. Fatigue life collapses at that moment.
* **Slip** — for shear joints relying on friction, capacity is $\mu F_i n$, not
  bolt shear.

**Preload uncertainty is large** with torque control — the torque-tension
relationship is dominated by friction, and scatter of ±25% or more is normal.
Carry the uncertainty rather than assuming nominal preload.

**In polymer and printed parts, assume thread stripping governs** until shown
otherwise, and prefer threaded inserts or through-bolts with metal load paths.
Thread engagement length, not bolt strength, sets the capacity.

## 6. Welds

Size fillet welds on throat area, $t = 0.707 h$ for an equal-leg fillet.
Treat the weld group like a section: compute its centroid and second moment,
then combine direct and torsional shear vectorially at the worst point.

Welds are fatigue-critical at their toes. For any fluctuating load, the weld
detail category — not the base metal strength — governs.
