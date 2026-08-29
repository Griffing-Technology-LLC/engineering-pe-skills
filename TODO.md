# TODO — Work Breakdown Structure

Formal WBS for `engineering-pe-skills`. All unresolved work lives here so it
survives across sessions.

**Legend:** `[ ]` open · `[x]` complete · `[~]` in progress · `[!]` blocked

---

## 0. Citation verification gate

Open citation debts. **No skill may be published while it depends on an item in
this section.** Each corresponds to a `REQUIRES VERIFICATION` entry in
`REFERENCES.md`.

* [ ] **0.1** — Verify ISA's documented role relative to the NCEES PE Control
  Systems exam. The first URL tried returned HTTP 404. Locate the current ISA page
  and record the exact wording, or record that ISA states no such role.
  *(REF-SOC-003; blocks `control-systems-engineering`)*
* [ ] **0.2** — Verify individual ASTM F38 standard designations and years for UAS
  design and construction (F3298 and related). ASTM blocks automated retrieval;
  confirm by browser or through an institutional subscription.
  *(REF-ASTM-001; blocks `aeronautical-engineering` publication)*
* [ ] **0.3** — Verify current 14 CFR Part 23 text for the factor-of-safety and
  limit-load-factor paragraphs. The 2017 restructure moved numerical criteria into
  consensus standards; the commonly quoted 1.5 FOS, n₁ = +3.8 / n₂ = −1.52,
  and the design gust velocities are **unverified**, and are currently
  marked as such in `references/loads-and-factors.md`.
  *(REF-FAA-002; blocks `aeronautical-engineering` publication)*
* [ ] **0.4** — Confirm AIAA and AIChE URLs by browser (both return HTTP 403 to
  automated checks; content unconfirmed). *(REF-SOC-006, REF-SOC-007)*
* [ ] **0.5** — Obtain and catalogue the NCEES exam specification PDF for each
  discipline, to ground each skill's scope in the published exam spec rather than
  the summary web page.

## 1. Repository infrastructure

* [x] **1.1** — Repository created, MIT licensed
* [x] **1.2** — `REFERENCES.md` citation catalog with verification-status legend
* [x] **1.3** — `AGENTS.md` authoritative agent instructions + `CLAUDE.md` stub
* [x] **1.4** — `README.md` with discipline table and honest alignment exceptions
* [x] **1.5** — `TODO.md` WBS
* [ ] **1.6** — `PROJECT_INDEX.md` maintained as files are added
* [ ] **1.7** — `CLAUDE-MEMORY.md` agent audit mirror
* [ ] **1.8** — CI: markdownlint (all 60 rules) + link validation + secret scan
  and a mandatory-notice presence check across every `SKILL.md`
* [ ] **1.9** — Skill trigger-description evals per `skill-creator` §"Optimize
  description", 20 queries per skill, before publication

## 2. Discipline skills

Each skill: `SKILL.md` (<500 lines) + `references/` + catalogued citations +
trigger evals.

* [~] **2.1 Aeronautical engineering** — *reference pattern for all others*
  * [x] 2.1.1 `SKILL.md` with licensure-standing statement and practice rules
  * [x] 2.1.2 `references/loads-and-factors.md` — limit/ultimate, V-n, gust,
    margin of safety, threaded joints
  * [x] 2.1.3 `references/aerodynamics.md` — section, finite wing, drag
    build-up, low-Re practice
  * [x] 2.1.4 `references/weight-and-balance.md` — CG envelope, neutral
    point, static margin
  * [x] 2.1.5 `references/propulsion.md` — momentum theory, propeller
    coefficients, EDF, thrust matching
  * [ ] 2.1.6 Resolve §0.2 and §0.3 citation debts
  * [ ] 2.1.7 Trigger evals
* [ ] **2.2 Mechanical engineering** — three NCEES modules as reference files
* [ ] **2.3 Statics and dynamics** — FE-level; grounded in NCEES FE Reference Handbook
* [ ] **2.4 Control systems engineering** — ISA; blocked on §0.1
* [ ] **2.5 Chemical engineering** — AIChE / CCPS process safety
* [ ] **2.6 Electrical engineering** — IEEE; power, protection, arc flash
* [ ] **2.7 Electronics engineering** — IEEE; signal integrity, EMC, PCB
* [ ] **2.8 Naval architecture and marine** — SNAME; hydrostatics, stability, resistance
* [ ] **2.9 Fire protection engineering** — SFPE / NFPA
* [ ] **2.10 Materials and additive manufacturing** — polymer AM anisotropy, allowables

## 3. Cross-cutting

* [ ] **3.1** — Shared units/conversion convention documented once and referenced
  by every skill, rather than restated per skill
* [x] **3.2a** — Canonical qualified-review notice defined in `AGENTS.md` and
  implemented in `aeronautical-engineering`
* [ ] **3.2b** — Propagate the byte-identical notice into the remaining nine
  skills as each is authored; verify with a CI check that every `SKILL.md`
  contains it *(gates 4.2)*
* [ ] **3.2** — Consistent "report a result" block across all ten skills
* [ ] **3.3** — Cross-discipline handoff guidance (e.g. aeronautical → materials
  for allowables; control systems → electronics for actuator drive)
* [ ] **3.4** — Decide whether a `secure-controller-assurance` style gate applies
  to any skill producing safety-related control content

## 4. Publication

* [ ] **4.1** — Licensed PE review of every skill's technical content
* [ ] **4.2** — Verify all §0 items closed
* [ ] **4.3** — Register on skills.sh; confirm install path resolves
* [ ] **4.4** — Announce with an explicit statement of what the skills do **not**
  do: they inform engineering judgment, they do not replace a licensed engineer
