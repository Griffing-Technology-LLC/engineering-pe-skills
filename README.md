# Engineering PE Skills

Agent Skills for licensed-discipline engineering practice, with authoritative
citations and explicit calculation methods.

Ten skills covering the engineering disciplines needed for real hardware design.
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
> skills inform engineering judgment; they do not replace it, and they carry no
> professional liability.

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
| `control-systems-engineering` | Control Systems | ISA |
| `chemical-engineering` | Chemical | AIChE / CCPS |
| `electrical-engineering` | Electrical and Computer: Power | IEEE |
| `electronics-engineering` | Electrical and Computer: Electronics, Controls, and Communications | IEEE |
| `naval-architecture-marine` | Naval Architecture and Marine | SNAME |
| `fire-protection-engineering` | Fire Protection | SFPE / NFPA |
| `materials-and-additive-manufacturing` | Metallurgical and Materials (partial) | ASTM / ASM |

### Two honest exceptions

**Aeronautical engineering has no NCEES PE examination.** The PE catalog contains
23 disciplines and aeronautical is not among them. Engineers needing licensure in
this field typically sit PE Mechanical. This repository does not claim an
alignment that does not exist; the aeronautical skill is aligned to FAA
regulation, NASA technical standards, and ASTM F38 instead.

**Statics and dynamics is FE-level subject matter**, appearing in the Fundamentals
of Engineering exam and inside several PE specifications — not a PE discipline of
its own. It is provided as a foundational skill the others build on.

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
| remaining six | Not started |

All four drafts are pending licensed PE review (`TODO.md` §4.1) before
publication.

## Attribution

Authored by Griffing Technology LLC. Drafting assistance from **Claude Opus 5**
(Anthropic) under human direction and review; see `CLAUDE-MEMORY.md` for the
agent audit trail. All engineering content is reviewed by a licensed professional
engineer before release.

Licensed [MIT](LICENSE).
