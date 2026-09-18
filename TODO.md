# TODO — Work Breakdown Structure

Formal WBS for `engineering-pe-skills`. All unresolved work lives here so it
survives across sessions.

**Legend:** `[ ]` open · `[x]` complete · `[~]` in progress · `[!]` blocked

---

## 0. Citation verification gate

Open citation debts. **No skill may be published while it depends on an item in
this section.** Each corresponds to a `REQUIRES VERIFICATION` entry in
`REFERENCES.md`.

* [x] **0.1** — **RESOLVED 2026-08-29.** ISA's role located at
  <https://www.isa.org/certification> and quoted verbatim in REF-SOC-003: ISA
  "supports the Control Systems Engineer (CSE) License" and "offers training
  courses and review materials." ISA does **not** claim to author or administer
  the NCEES exam, and the repository does not say it does.
* [ ] **0.2** — Verify individual ASTM F38 standard designations and years for UAS
  design and construction (F3298 and related). ASTM blocks automated retrieval;
  confirm by browser or through an institutional subscription.
  *(REF-ASTM-001; blocks `aeronautical-engineering` publication)*
* [x] **0.3** — **RESOLVED 2026-08-29.** Part 23 read in full from the eCFR API
  (title-14, issue date 2026-08-27). Findings, now in REF-FAA-002:
  * **§23.2230(b) states the 1.5 factor of safety explicitly** — it is current
    rule text. The earlier `REQUIRES VERIFICATION` mark was over-cautious and is
    withdrawn; the correction is recorded in `REFERENCES.md`.
  * The numeric manoeuvring load factors **+3.8 / −1.52 appear nowhere** in
    current Part 23 (zero occurrences of either number). §23.2200(b) is
    performance-based. The caution was correct for these.
  * §23.2265 *Special factors of safety* and §23.2260(b) captured — both apply
    directly to additively manufactured structure.
* [ ] **0.4** — Confirm AIAA and AIChE URLs by browser (both return HTTP 403 to
  automated checks; content unconfirmed). *(REF-SOC-006, REF-SOC-007)*
* [~] **0.5** — Obtain and catalogue the NCEES exam specification PDF for each
  discipline, to ground each skill's scope in the published exam spec rather than
  the summary web page. **Progress 2026-09-17:** the PE Electrical and Computer
  landing page links all three module specs (URLs now in REF-NCEES-004); the
  Computer Engineering spec was read in full and its eight knowledge areas
  are reproduced in `computer-engineering/SKILL.md`. Still open: read the
  Power spec against `electrical-engineering`, and obtain the specs for
  Mechanical, Control Systems, Naval Architecture, Chemical, and Fire
  Protection.
* [ ] **0.6** — Confirm the current NCEES FE Reference Handbook version and its
  published statics/dynamics section list. *(REF-NCEES-009;
  `statics-and-dynamics` cites the handbook generally, no section by number)*
* [ ] **0.7** — Confirm designations, editions, and years for the individual ISA
  standards (ISA-5.1, ISA-84/IEC 61511, ISA-88, ISA-95, ISA/IEC 62443) before any
  is cited by number. *(REF-ISA-001; `control-systems-engineering` currently
  cites the series only as an index entry, with in-file cautions)*
* [ ] **0.8** — Confirm specific NFPA 70 (NEC) article/table numbers by browser
  against the 2026 edition (nfpa.org blocked automated retrieval), and resolve
  which NFPA 70E edition is current as of the query date (2024 vs 2027
  editions both appear in bookseller listings). *(REF-NFPA-001, REF-NFPA-002;
  `electrical-engineering` currently cites NEC topics without article numbers
  and flags 70E's current edition as unconfirmed)*
* [ ] **0.9** — Read the full text of the three foundational papers catalogued
  as `VERIFIED (BLOCKED)` for `computer-engineering` and confirm that the
  results attributed to them appear as stated: Amdahl 1967 speed-up formula
  (REF-PAPER-001), Liu & Layland 1973 rate-monotonic bound
  $n(2^{1/n}-1)$ and EDF bound (REF-PAPER-002), Hamming 1950 minimum-distance
  and check-bit statements (REF-PAPER-003). ACM DL and IEEE Xplore block
  automated retrieval; use an institutional or personal subscription. Until
  closed, the skill presents the results as standard textbook material and
  names the papers without page or theorem numbers.

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
  * [x] 2.1.6 §0.3 resolved; `loads-and-factors.md` rewritten against verified
    §23.2200 / §23.2215 / §23.2230 / §23.2260 / §23.2265 text
  * [ ] 2.1.7 §0.2 (ASTM F38) still open — does not block the other skills
  * [ ] 2.1.8 Trigger evals
* [~] **2.2 Mechanical engineering** — PE Mechanical, three modules
  * [x] 2.2.1 `SKILL.md` — module table, practice rules, workflow
  * [x] 2.2.2 `references/materials-and-fatigue.md` — stress state, $K_t$/$K_f$,
    failure theories, fatigue, buckling, allowables, AM polymer
  * [x] 2.2.3 `references/machine-elements.md` — shafts, bearings, gears,
    springs, bolted joints, welds
  * [x] 2.2.4 `references/thermal-and-fluids.md` — cycles, heat transfer,
    fluids, pumps, HVAC
  * [ ] 2.2.5 Trigger evals
* [~] **2.3 Statics and dynamics** — FE-level [REF-NCEES-002]
  * [x] 2.3.1 `SKILL.md` — examination standing, $g_c$ discipline, determinacy
  * [x] 2.3.2 `references/statics.md` — equilibrium, reactions, trusses,
    frames, distributed loads, friction
  * [x] 2.3.3 `references/section-properties.md` — centroids, second moments,
    parallel-axis, mass moments
  * [x] 2.3.4 `references/dynamics.md` — kinematics, Newton-Euler, energy,
    momentum, vibration
  * [ ] 2.3.5 Trigger evals
* [~] **2.4 Control systems engineering** — ISA; §0.1 resolved
  * [x] 2.4.1 `SKILL.md` — ISA role quoted precisely, practice rules
  * [x] 2.4.2 `references/loop-dynamics.md` — FOPDT, dead time, margins,
    robustness
  * [x] 2.4.3 `references/pid-and-tuning.md` — PID forms, tuning methods,
    structures, windup and stiction
  * [x] 2.4.4 `references/instrumentation-and-safety.md` — measurement, final
    elements, P&ID, SIS/SIL, 62443
  * [ ] 2.4.5 Trigger evals
* [ ] **2.5 Chemical engineering** — AIChE / CCPS process safety
* [x] **2.6 Electrical engineering** — IEEE; power, protection, arc flash
  * [x] 2.6.1 `SKILL.md` — PE Electrical/Computer Power module standing,
    IEEE/NFPA citation caveats, practice rules
  * [x] 2.6.2 `references/power-systems-and-per-unit.md` — per-unit, base
    conversion, three-phase power, symmetrical components, transformers
  * [x] 2.6.3 `references/protection-and-fault-analysis.md` — fault types and
    sequence networks, symmetrical fault current, overcurrent sizing,
    coordination, grounding schemes
  * [x] 2.6.4 `references/arc-flash-and-safety.md` — IEEE 1584-2018
    calculation framework (verified scope, no fabricated coefficients),
    NFPA 70E work-practice requirements
  * [ ] 2.6.5 Trigger evals
* [ ] **2.7 Electronics engineering** — IEEE; signal integrity, EMC, PCB
  (PE Electrical and Computer — ECC module; spec PDF link now in
  REF-NCEES-004, not yet read)
* [x] **2.8 Naval architecture and marine** — SNAME; hydrostatics, stability,
  resistance
  * [x] 2.8.1 `SKILL.md` — PE Naval Architecture standing (no published module
    breakdown, re-verified 2026-09-16), SNAME/PNA citation caveat, practice
    rules
  * [x] 2.8.2 `references/hydrostatics-and-stability.md` — buoyancy, KB/BM/GM,
    GZ curve, IMO 2008 IS Code §2.2/§2.3 criteria (verified against primary
    text), trim
  * [x] 2.8.3 `references/resistance-and-propulsion.md` — Froude/Reynolds
    scaling, ITTC-57 correlation line, resistance decomposition, propulsion
    coefficients (verified against ITTC 7.5-02-02-01)
  * [ ] 2.8.4 Trigger evals
* [ ] **2.9 Fire protection engineering** — SFPE / NFPA
* [ ] **2.10 Materials and additive manufacturing** — polymer AM anisotropy, allowables
* [x] **2.11 Thermodynamics** — FE-level, cross-discipline (feeds mechanical,
  chemical, naval architecture, aeronautical, fire protection)
  * [x] 2.11.1 `SKILL.md` — FE examination standing, downstream discipline
    handoffs, practice rules ($g_c$, absolute-temperature discipline,
    efficiency-vs-COP)
  * [x] 2.11.2 `references/thermodynamics.md` — properties, first/second law,
    isentropic efficiency, power/refrigeration cycles, psychrometrics
  * [x] 2.11.3 `references/heat-transfer.md` — conduction, convection,
    radiation, fins, LMTD/effectiveness-NTU
  * [x] 2.11.4 `references/fluid-mechanics.md` — statics, continuity, energy
    equation, Reynolds/Froude, pipe flow
  * [ ] 2.11.5 Trigger evals
* [x] **2.12 Computer engineering** — IEEE; PE Electrical and Computer —
  Computer Engineering module (spec read in full 2026-09-17)
  * [x] 2.12.1 `SKILL.md` — module standing with the eight spec knowledge
    areas and question ranges, IEEE/IETF/NIST/UEFI citation basis, practice
    rules (representation, prefix convention, timing corner, bounded
    real-time, error-control blind spots, threat model, integrity level,
    no-TBD budgets)
  * [x] 2.12.2 `references/data-representation-and-error-control.md` —
    integer/fixed-point/endianness, IEEE 754-2019, character encoding and
    line codes, parity/checksum/CRC/Hamming/SECDED selection, compression
  * [x] 2.12.3 `references/architecture-and-systems-software.md` — CPI and
    speed-up, pipelining and hazards, AMAT and cache organisation, virtual
    memory, RAID/NAS/SAN, flash endurance, embedded interfacing and fault
    tolerance, RMS/EDF schedulability, interrupts, virtualisation, UEFI and
    SP 800-193 boot resiliency
  * [x] 2.12.4 `references/digital-design-and-timing.md` — combinational
    and sequential design, FSMs, setup/hold with skew and jitter,
    metastability MTBF and CDC, hazards, logic levels/fan-out/thermal,
    LVDS/CAN/RS-485/Ethernet signalling, ADC/DAC, PLD/FPGA/ASIC/PLC,
    IEEE 1149.1 boundary scan and DFT
  * [x] 2.12.5 `references/networks-security-and-quality.md` — RFC 1122
    layering, IP/TCP/Ethernet, network design and test, software design and
    fundamentals, NIST CSF 2.0 / SP 800-160 / SP 800-82 / SP 800-193 /
    FIPS 140-3 security practice, QA, IEEE 1012-2024 V&V
  * [ ] 2.12.6 §0.9 open (paper full texts) — does not block the skill's
    method content, which is presented as standard material
  * [ ] 2.12.7 Trigger evals

## 3. Cross-cutting

* [ ] **3.1** — Shared units/conversion convention documented once and referenced
  by every skill, rather than restated per skill
* [x] **3.2a** — Canonical qualified-review notice defined in `AGENTS.md` and
  implemented in `aeronautical-engineering`
* [~] **3.2b** — Propagate the byte-identical notice into every skill as it is
  authored, verified by CI. **8 of 12 done** (aeronautical, mechanical,
  statics-and-dynamics, control-systems, naval-architecture-marine,
  thermodynamics, electrical-engineering, computer-engineering).
  *(gates 4.2)*
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
