# Statics: Equilibrium, Trusses, Frames, and Friction

Reference file for the `statics-and-dynamics` skill. FE-level scope
[REF-NCEES-002].

## Contents

1. Equilibrium
2. Support reactions
3. Determinacy
4. Trusses
5. Frames and machines
6. Distributed loads
7. Friction

---

## 1. Equilibrium

A body is in equilibrium when the resultant force and resultant moment both
vanish. In two dimensions:

$$\sum F_x = 0, \qquad \sum F_y = 0, \qquad \sum M_O = 0$$

Three independent equations, so three unknowns are solvable. In three
dimensions there are six.

The moment of a force about a point:

$$\mathbf{M}_O = \mathbf{r} \times \mathbf{F}$$

$\mathbf{r}$ runs from the moment centre to *any* point on the line of action —
a force may be slid along its own line of action without changing its moment.

**A couple** is two equal, opposite, non-collinear forces. Its moment is the
same about every point, which is what makes it free to be moved anywhere on the
body.

## 2. Support reactions

Replace each support with the reactions it can physically carry. Getting this
table wrong is the most common source of wrong answers.

| Support | Reactions (2-D) | Unknowns |
| --- | --- | --- |
| Roller / rocker | Normal to surface | 1 |
| Pin / hinge | Two force components | 2 |
| Fixed / built-in | Two force components + couple | 3 |
| Cable | Tension along the cable, away from body | 1 |
| Smooth surface | Normal to the surface | 1 |
| Frictionless collar on shaft | Normal to shaft axis | 1 |

Two rules worth stating explicitly: a **cable can only pull**, and a
**two-force member carries load only along the line joining its two pins** —
recognising two-force members collapses most frame problems immediately.

## 3. Determinacy

Compare unknown reactions $r$ against independent equilibrium equations $e$:

* $r < e$ — unstable (a mechanism)
* $r = e$ — statically determinate; equilibrium alone solves it
* $r > e$ — statically **indeterminate** to degree $r - e$

An indeterminate structure cannot be solved by adding more equilibrium
equations. It needs compatibility of deformation, which is mechanics-of-materials
scope, not statics. **Say so rather than producing a number.**

## 4. Trusses

Idealisations, all of which must hold for the method to be valid:

* members are two-force members — straight, pin-jointed at their ends
* loads apply only at joints
* member weight is neglected or split to the end joints

Members are then in pure tension or compression, with no bending.

**Method of joints** — isolate one pin at a time, apply $\sum F_x = \sum F_y = 0$.
Two equations per joint, so start where at most two members are unknown.

**Method of sections** — cut through the members of interest, take the whole
sub-structure, and use $\sum M = 0$ about a point that eliminates the members you
do not want. Faster when only a few member forces are needed.

**Zero-force members**, worth spotting before any algebra:

* two non-collinear members at an unloaded joint — both are zero
* three members at an unloaded joint where two are collinear — the third is zero

Report member forces with sense: **T** for tension, **C** for compression.

## 5. Frames and machines

Frames contain at least one multi-force member, so members carry bending as well
as axial load and the method of joints does not apply.

Procedure: analyse the whole structure for external reactions first, then
dismember and analyse members individually. At every internal pin, the forces on
the two connected members are **equal and opposite** — this is where sign errors
enter, so draw both.

## 6. Distributed loads

A distributed load $w(x)$ is replaced for equilibrium purposes by a resultant:

$$R = \int w(x)\,\mathrm{d}x$$

acting through the centroid of the load diagram. For common cases:

* **Uniform** $w_0$ over length $L$ — $R = w_0 L$ at midspan
* **Triangular**, zero to $w_0$ over $L$ — $R = \tfrac{1}{2} w_0 L$ at $2L/3$ from
  the zero end

The equivalent resultant is valid for **external equilibrium only**. It must not
be used to compute internal shear and moment distributions within the loaded
region.

## 7. Friction

Coulomb dry friction. The distinction that matters:

**Impending motion** — friction is at its maximum:

$$F = \mu_s N$$

**Sliding** — friction is kinetic and opposes the velocity:

$$F = \mu_k N$$

**Static, not yet impending** — $F \le \mu_s N$, and $F$ is whatever equilibrium
requires. It is **not** $\mu_s N$. Assuming it is, when the body is not on the
verge of moving, is the standard error in this subject.

Procedure: assume a state, solve, then verify the assumption. If the required $F$
exceeds $\mu_s N$, the body moves and the assumption was wrong.

**Tipping vs sliding** — check both. A body tips when the resultant normal force
reaches the edge of the contact patch. Whichever occurs at the lower applied load
governs, and it is not always sliding.

**Angle of friction:** $\tan\phi_s = \mu_s$. Motion impends when the resultant of
$N$ and $F$ leans $\phi_s$ from the surface normal.

**Belt friction**, for a belt on a drum with wrap angle $\beta$ in radians:

$$\frac{T_{tight}}{T_{slack}} = e^{\mu\beta}$$
