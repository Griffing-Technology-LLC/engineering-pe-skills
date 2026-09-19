# Engineering PE Skills

Agent Skills for licensed-discipline engineering practice, with authoritative
citations and explicit calculation methods.

Twelve skills covering the engineering disciplines needed for real hardware
design.
Each is aligned — where an alignment honestly exists — to an
[NCEES PE discipline](https://ncees.org/exams/pe-exam/), and each cites its
discipline's professional society and standards-developing organization.

## Qualified review is required

> ⚠️ **ENGINEERING REVIEW REQUIRED — output from these skills is not a substitute
> for a qualified engineer.** Every result, calculation, and recommendation
> produced with any skill in this repository **must be independently reviewed and
> accepted by a properly qualified individual** — a licensed Professional Engineer
> or an equivalently qualified authority for the jurisdiction and discipline —
> **before it is applied to any system carrying risk to life or safety.** These
> skills inform engineering judgment; they do not replace it. They are
> reference material provided AS-IS (see LICENSE §5), are not an engineering
> service, and do not constitute a sealed, certified, or reviewed work product
> for any specific project.

Every skill emits this notice at the start of every response it contributes to.
That behaviour is a fixed condition of the skills, not a configurable option.

## Design principles

* **No fabricated references.** Every standard, section, and figure is catalogued
  in [`REFERENCES.md`](REFERENCES.md) with a validated URL and a verification
  status. Anything unconfirmed is marked `REQUIRES VERIFICATION` and tracked in
  [`TODO.md`](TODO.md) §0 — it is never asserted as fact.
* **Imperial-primary units with metric in parentheses**, and `lbm`/`lbf`
  distinguished throughout. Airspeed in knots.
* **Methods carry their validity envelope.** A skill that gives you an equation
  also tells you where it stops being true.
* **Assumptions are labelled on every run**, so an assumed value never hardens
  into a fact by repetition.
* **Real builds.** These skills assume the output gets fabricated, not filed —
  which is exactly why the review notice above is mandatory and unconditional.

## Disciplines

| Skill | NCEES PE alignment | Society / SDO |
| --- | --- | --- |
| `aeronautical-engineering` | **None — no PE exam exists** | AIAA; FAA & NASA & ASTM F38 as authority |
| `mechanical-engineering` | Mechanical (HVAC&R; Machine Design & Materials; Thermal & Fluid Systems) | ASME |
| `statics-and-dynamics` | **FE-level**, not a PE discipline | — (foundational; NCEES FE) |
| `thermodynamics` | **FE-level**, not a PE discipline | — (foundational; NCEES FE) |
| `control-systems-engineering` | Control Systems | ISA |
| `chemical-engineering` | Chemical | AIChE / CCPS |
| `electrical-engineering` | Electrical and Computer: Power | IEEE |
| `electronics-engineering` | Electrical and Computer: Electronics, Controls, and Communications | IEEE |
| `computer-engineering` | Electrical and Computer: Computer Engineering | IEEE |
| `naval-architecture-marine` | Naval Architecture and Marine | SNAME |
| `fire-protection-engineering` | Fire Protection | SFPE / NFPA |
| `materials-and-additive-manufacturing` | Metallurgical and Materials (partial) | ASTM / ASM |

### Two honest exceptions

**Aeronautical engineering has no NCEES PE examination.** The PE catalog contains
23 disciplines and aeronautical is not among them. Engineers needing licensure in
this field typically sit PE Mechanical. This repository does not claim an
alignment that does not exist; the aeronautical skill is aligned to FAA
regulation, NASA technical standards, and ASTM F38 instead.

**Statics and dynamics, and thermodynamics/heat transfer/fluid mechanics, are
FE-level subject matter**, appearing in the Fundamentals of Engineering exam
and inside several PE specifications — not PE disciplines of their own. Both
are provided as foundational skills the others build on.

## Installation

```bash
npx skills add Griffing-Technology-LLC/engineering-pe-skills@aeronautical-engineering
```

Or clone into your skills directory:

```bash
git clone https://github.com/Griffing-Technology-LLC/engineering-pe-skills.git
```

## Status

Under active development. See [`TODO.md`](TODO.md) for the work breakdown
structure and current completion state.

| Skill | State |
| --- | --- |
| `aeronautical-engineering` | Draft — SKILL.md + 4 reference files |
| `mechanical-engineering` | Draft — SKILL.md + 3 reference files |
| `statics-and-dynamics` | Draft — SKILL.md + 3 reference files |
| `control-systems-engineering` | Draft — SKILL.md + 3 reference files |
| `naval-architecture-marine` | Draft — SKILL.md + 2 reference files |
| `thermodynamics` | Draft — SKILL.md + 3 reference files |
| `electrical-engineering` | Draft — SKILL.md + 3 reference files |
| `electronics-engineering` | Draft — SKILL.md + 2 reference files |
| `computer-engineering` | Draft — SKILL.md + 4 reference files |
| remaining three | Not started |

All nine drafts are pending licensed PE review (`TODO.md` §4.1) before
publication.

## Attribution

Authored by Griffing Technology LLC. Drafting assistance from **Claude Opus 5**
(Anthropic) under human direction and review; see `CLAUDE-MEMORY.md` for the
agent audit trail. All engineering content is reviewed by a licensed professional
engineer before release.

## Licence

Engineering PE Skills © 2026 Griffing Technology LLC, licensed
[CC BY-ND 4.0](LICENSE) — Creative Commons Attribution-NoDerivatives 4.0
International. Attribution: *"Engineering PE Skills, Griffing Technology LLC,
CC BY-ND 4.0,
<https://github.com/Griffing-Technology-LLC/engineering-pe-skills>"*.

### Why no-derivatives

Each skill's safety case rests on its reviewed, cited content. A modified
skill is no longer the reviewed artefact, but still emits the same
qualified-review notice — so it would carry this repository's name and
verification claims on content nobody here has checked. The licence therefore
permits use and unmodified redistribution but not sharing of modified versions.

### Licence scope — what CC BY-ND 4.0 does and does not do

* **You may** copy, redistribute, and install these skills unmodified, and
  adapt them for your own private use (LICENSE §2(a)(1)).
* **You may not** publicly distribute a modified version (LICENSE §2(a)(1)(b),
  §3(a)(1)). Send corrections upstream instead — see
  [`SECURITY.md`](SECURITY.md).
* **A locally modified copy is no longer the reviewed artefact.** It inherits
  none of this repository's citation-verification or engineer-review claims.
  If the mandatory notice is missing from a copy, treat its output as
  unreviewed.
* **Your own work is yours.** Analyses, calculations, reports, and designs
  you produce *using* these skills are not Licensed Material or Adapted
  Material under this licence; share them freely, subject to the
  qualified-review requirement above. Reproducing the review notice in such
  output is expressly permitted without further attribution.
* **The licence does not enforce the review requirement.** CC BY-ND governs
  copying; it neither substitutes for nor compels the qualified engineering
  review described above, which applies to any use, modified or not.
* **Not retroactive.** Revisions through commit `5300e0e` were published under
  the MIT License and that grant is not withdrawn for copies already obtained;
  CC BY-ND 4.0 applies from commit `a113589` (2026-09-19) onward.
