# Centroids, Second Moments, and Mass Moments of Inertia

Reference file for the `statics-and-dynamics` skill.

## 1. Centroids

For a composite area built from parts of area $A_i$ with centroids $\bar{x}_i$:

$$\bar{x} = \frac{\sum A_i \bar{x}_i}{\sum A_i}, \qquad
  \bar{y} = \frac{\sum A_i \bar{y}_i}{\sum A_i}$$

Holes and cut-outs enter with **negative area**, which is usually easier than
decomposing around them.

By symmetry, a centroid lies on every axis of symmetry — use this before
integrating anything.

## 2. Second moment of area

Also called area moment of inertia. About a centroidal axis:

$$I_x = \int y^{2}\,\mathrm{d}A, \qquad I_y = \int x^{2}\,\mathrm{d}A$$

Common sections, about the **centroidal** axis:

| Section | $I$ about centroid |
| --- | --- |
| Rectangle $b \times h$ | $I = bh^{3}/12$ (about the axis parallel to $b$) |
| Solid circle, diameter $d$ | $I = \pi d^{4}/64$ |
| Hollow circle, $d_o$, $d_i$ | $I = \pi (d_o^{4} - d_i^{4})/64$ |
| Triangle, base $b$, height $h$ | $I = bh^{3}/36$ |

**Polar** second moment, for torsion of circular sections:

$$J = I_x + I_y = \frac{\pi d^{4}}{32} \ \text{(solid circle)}$$

## 3. Parallel-axis theorem

To shift a second moment from the centroidal axis to a parallel axis at distance
$d$:

$$I = I_{cg} + A d^{2}$$

Two conditions are routinely violated. The theorem transfers **from the
centroidal axis only** — you cannot hop between two arbitrary parallel axes in
one step, and must return to the centroid first. And $d$ is measured to the
*section's own* centroid, not to the composite's.

For a composite section:

$$I_{total} = \sum \left( I_{cg,i} + A_i d_i^{2} \right)$$

The $Ad^2$ term usually dominates for material far from the axis, which is the
whole reason I-beams and tubes are efficient. **A hollow tube of the same mass as
a solid rod is dramatically stiffer in bending** — this is the single most useful
consequence of the theorem for real design.

## 4. Radius of gyration

$$k = \sqrt{\frac{I}{A}}$$

The distance at which the whole area could be concentrated to give the same $I$.
It is what column-buckling slenderness ratios are built from.

## 5. Mass moment of inertia

The dynamics counterpart, with dimensions of mass × length²:

$$I = \int r^{2}\,\mathrm{d}m$$

Common bodies about the centroidal axis:

| Body | $I$ |
| --- | --- |
| Slender rod, length $L$, about centre, transverse | $mL^{2}/12$ |
| Slender rod about one end, transverse | $mL^{2}/3$ |
| Solid cylinder, radius $r$, about its own axis | $mr^{2}/2$ |
| Solid sphere, radius $r$ | $2mr^{2}/5$ |
| Thin hoop, radius $r$, about its axis | $mr^{2}$ |

Parallel-axis applies identically:

$$I = I_{cg} + m d^{2}$$

**Watch the units.** In US customary, mass must be in slugs — or lbm divided by
$g_c$ — before it enters a mass moment of inertia. Using lbm directly gives an
answer wrong by a factor of 32.174.
