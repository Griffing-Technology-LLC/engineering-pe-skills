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
* [ ] **0.9** — Obtain and read the actual NCEES PE Electrical and Computer —
  Electronics, Controls, and Communications exam specification PDF
  (`ncees.org` was blocked by this repository's network-egress policy during
  authoring) to confirm the detailed topic breakdown and per-area question
  weighting. Only the module name, question count (85), and appointment
  length (9.5 hours) are currently asserted, per REF-NCEES-004's existing
  verified scope — no topic percentage is asserted.
  *(REF-NCEES-004; blocks a more detailed `electronics-engineering` §2.7
  topic map, does not block the skill's current scope)*
* [ ] **0.10** — Confirm REF-IEEE-002 (IEEE/ANSI C63.4), REF-FCC-001 (47 CFR
  Part 15), and REF-IPC-001 (IPC-2221) by direct browser access to
  `standards.ieee.org`, `ecfr.gov`, and `ipc.org` respectively — all three
  are currently `VERIFIED (BLOCKED)`, corroborated only via independent
  secondary listings because those domains were blocked by this
  repository's network-egress policy during authoring, not because the
  documents are unconfirmed to exist.
* [ ] **0.8** — Confirm specific NFPA 70 (NEC) article/table numbers by browser
  against the 2026 edition (nfpa.org blocked automated retrieval), and resolve
  which NFPA 70E edition is current as of the query date (2024 vs 2027
  editions both appear in bookseller listings). *(REF-NFPA-001, REF-NFPA-002;
  `electrical-engineering` currently cites NEC topics without article numbers
  and flags 70E's current edition as unconfirmed)*
* [ ] **0.11** — Read the full text of the three foundational papers catalogued
  as `VERIFIED (BLOCKED)` for `computer-engineering` and confirm that the
  results attributed to them appear as stated: Amdahl 1967 speed-up formula
  (REF-PAPER-001), Liu & Layland 1973 rate-monotonic bound
  $n(2^{1/n}-1)$ and EDF bound (REF-PAPER-002), Hamming 1950 minimum-distance
  and check-bit statements (REF-PAPER-003). ACM DL and IEEE Xplore block
  automated retrieval; use an institutional or personal subscription. Until
  closed, the skill presents the results as standard textbook material and
  names the papers without page or theorem numbers.

## 1. Repository infrastructure

* [x] **1.1** — Repository created under the MIT License; **relicensed to
  CC BY-ND 4.0 on 2026-09-19** (commit `a113589`). Revisions before that
  commit remain available under MIT and are not withdrawn.
* [x] **1.1a** — Propagate the relicence to every surface that names the
  licence: `LICENSE` licensor notice, `license:` frontmatter in all nine
  `SKILL.md`, `README.md`, `PROJECT_INDEX.md`. **Done 2026-09-19.**
* [x] **1.2** — `REFERENCES.md` citation catalog with verification-status legend
* [x] **1.3** — `AGENTS.md` authoritative agent instructions + `CLAUDE.md` stub
* [x] **1.4** — `README.md` with discipline table and honest alignment exceptions
* [x] **1.5** — `TODO.md` WBS
* [ ] **1.6** — `PROJECT_INDEX.md` maintained as files are added
* [ ] **1.7** — `CLAUDE-MEMORY.md` agent audit mirror
* [~] **1.8** — CI gates. **Done 2026-09-19:** markdownlint (all rules);
  skill-invariants job — notice byte-identical to `.github/notice.txt`
  (which is itself diffed against `AGENTS.md`), `ncees_alignment`,
  `license: CC-BY-ND-4.0`, `review_status` present. **Open:** link
  validation, secret scan.
* [ ] **1.9** — Skill trigger-description evals per `skill-creator` §"Optimize
  description", 20 queries per skill, before publication
* [ ] **1.9b** — Notice-emission evals: for each skill, multi-turn transcripts
  including a follow-up turn and an explicit "skip the disclaimer" request,
  asserting the notice text appears first in every response. Triggering
  (§1.9) and emission are different properties; CI checks only that the
  text is present in the file, not that an agent emits it.

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
* [x] **2.7 Electronics engineering** — IEEE; signal integrity, EMC, PCB
  * [x] 2.7.1 `SKILL.md` — PE Electrical/Computer Electronics, Controls, and
    Communications module standing (module name/question count/hours only;
    detailed topic weighting not asserted, §0.9), IEEE/FCC/IPC citation
    caveats, practice rules
  * [x] 2.7.2 `references/signal-integrity-and-emc.md` — transmission-line
    regime, characteristic impedance, reflections and termination,
    crosstalk and eye diagrams, EMC emissions/immunity framework
    (IEEE/ANSI C63.4), FCC Part 15 regulatory framework, board-level
    grounding/shielding
  * [x] 2.7.3 `references/analog-and-digital-circuits.md` — op-amp
    fundamentals, filters, discrete amplifier basics, digital logic family
    interface compatibility, ADC/DAC and aliasing, board-level power
    regulation, digital timing margins, IPC-2221 PCB design-rule framework
  * [ ] 2.7.4 Trigger evals
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
  * [ ] 2.12.6 §0.11 open (paper full texts) — does not block the skill's
    method content, which is presented as standard material
  * [ ] 2.12.7 Trigger evals

## 3. Cross-cutting

* [ ] **3.1** — Shared units/conversion convention documented once and referenced
  by every skill, rather than restated per skill
* [x] **3.2a** — Canonical qualified-review notice defined in `AGENTS.md` and
  implemented in `aeronautical-engineering`
* [~] **3.2b** — Propagate the byte-identical notice into every skill as it is
  authored, verified by CI. **9 of 9 authored skills done, 12 planned**
  (aeronautical, mechanical, statics-and-dynamics, control-systems,
  naval-architecture-marine, thermodynamics, electrical-engineering,
  electronics-engineering, computer-engineering — all nine copies confirmed
  byte-identical 2026-09-19). Remaining three land with §2.5, §2.9, §2.10.
  *(gates 4.2)*
* [ ] **3.2** — Consistent "report a result" block across all ten skills
* [ ] **3.3** — Cross-discipline handoff guidance (e.g. aeronautical → materials
  for allowables; control systems → electronics for actuator drive)
* [ ] **3.4** — Decide whether a `secure-controller-assurance` style gate applies
  to any skill producing safety-related control content

## 4. Publication

* [ ] **4.0** — Counsel review of the licence, licensor notice, and
  qualified-review notice wording before any skill is registered (§4.3).
  The 2026-09-19 reframe replaced "carries no professional liability" (a
  legal conclusion the licence does not establish — LICENSE §5 limits
  liability only between licensor and licensee, "to the extent possible")
  with a description of what the material *is*: AS-IS reference material,
  not an engineering service, not a sealed/certified/reviewed work product.
  Confirm that wording, and that a PE-owned LLC publishing engineer-reviewed
  reference material creates no practice-act exposure in its state.
* [ ] **4.1** — Licensed PE review of every skill's technical content,
  **per discipline and per commit**. One reviewer cannot close this for
  disciplines outside their licensure; the README demands of users a reviewer
  qualified "for the jurisdiction and discipline" and this gate must meet the
  same bar. Each sub-item closes only when `REVIEW_LOG.md` records the
  reviewer's GitHub username, licence discipline and state, and the reviewed
  commit hash, and the skill's `metadata.review_status` is updated. Any later
  edit to that skill's technical content reopens its sub-item.
  * [ ] 4.1.1 `aeronautical-engineering` — PE Mechanical or an equivalently
    qualified aerospace authority (no NCEES aeronautical PE exists; see
    README "Two honest exceptions")
  * [ ] 4.1.2 `mechanical-engineering` — PE Mechanical
  * [ ] 4.1.3 `statics-and-dynamics` — any PE whose exam specification
    includes statics/dynamics (FE-level content; Mechanical or Civil
    Structural preferred)
  * [ ] 4.1.4 `thermodynamics` — PE Mechanical (Thermal & Fluid Systems) or
    PE Chemical
  * [ ] 4.1.5 `control-systems-engineering` — PE Control Systems
  * [ ] 4.1.6 `chemical-engineering` — PE Chemical *(skill not yet
    authored, §2.5)*
  * [ ] 4.1.7 `electrical-engineering` — PE Electrical and Computer: Power
  * [ ] 4.1.8 `electronics-engineering` — PE Electrical and Computer:
    Electronics, Controls, and Communications
  * [ ] 4.1.9 `computer-engineering` — PE Electrical and Computer: Computer
    Engineering
  * [ ] 4.1.10 `naval-architecture-marine` — PE Naval Architecture and
    Marine
  * [ ] 4.1.11 `fire-protection-engineering` — PE Fire Protection *(skill
    not yet authored, §2.9)*
  * [ ] 4.1.12 `materials-and-additive-manufacturing` — PE Metallurgical and
    Materials *(skill not yet authored, §2.10)*
* [ ] **4.2** — Verify all §0 items closed
* [ ] **4.3** — Register on skills.sh; confirm install path resolves. The
  README install line uses the `owner/repo@skill` form; the skills CLI
  documents `--skill <name>` for `add` in at least some versions — confirm
  against the live CLI and correct the README. Gated on §4.0, §4.1, §4.2.
  "Publication" in §0 and §4 means this registration **and** removal of the
  `UNREVIEWED DRAFT` marker; public visibility of the repository is not
  publication.
* [ ] **4.4** — Announce with an explicit statement of what the skills do **not**
  do: they inform engineering judgment, they do not replace a licensed engineer
