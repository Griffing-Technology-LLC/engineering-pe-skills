# REFERENCES

Authoritative reference catalog for the `engineering-pe-skills` repository.

Every specification, calculation method, and design rule asserted anywhere in
this
repository is traceable to an entry below.  Each entry carries a REF-ID, the
full
title of the source, a validated URL, the specific portion applied, and every
repository location that cites it.

## Verification status legend

| Status | Meaning |
| --- | --- |
| `VERIFIED` | URL returned HTTP 200 to an automated check on the date shown, and the cited content was read. |
| `VERIFIED (BLOCKED)` | Document is real and the URL is correct, but the host blocks automated retrieval (HTTP 403 anti-bot). Content verified from a secondary authoritative source; primary URL requires manual browser confirmation. |
| `REQUIRES VERIFICATION` | Cited from general knowledge, not yet confirmed against the issuing body. **Must not be relied upon** until upgraded. Tracked in `TODO.md` §0. |

All URLs checked 2026-08-29 unless noted otherwise.

---

## 1. Licensure and examination framework

### REF-NCEES-001 — NCEES PE Exam discipline catalog

* **Title:** *PE Exam* — National Council of Examiners for Engineering and
  Surveying
* **URL:** <https://ncees.org/exams/pe-exam/>
* **Status:** `VERIFIED`
* **Applied:** The authoritative list of 23 PE disciplines used to scope this
  repository and to assign each skill its `ncees_alignment` frontmatter field.
* **Cited in:** `README.md`, `AGENTS.md`, all `skills/*/SKILL.md` frontmatter.
* **Note:** NCEES discipline pages do **not** name sponsoring professional
  societies. Sponsorship claims in this repository are therefore cited to the
  society itself, never to NCEES. See §2.

### REF-NCEES-002 — NCEES FE Exam

* **Title:** *FE Exam* — National Council of Examiners for Engineering and
  Surveying
* **URL:** <https://ncees.org/engineering/fe/>
* **Status:** `VERIFIED`
* **Applied:** Establishes that statics and dynamics, and thermodynamics/heat
  transfer/fluid mechanics, are **FE-level** subject matter, not a PE
  discipline on their own. Governs the alignment of
  `skills/statics-and-dynamics/` and `skills/thermodynamics/`.
* **Cited in:** `skills/statics-and-dynamics/SKILL.md`,
  `skills/thermodynamics/SKILL.md`

### REF-NCEES-003 — PE Mechanical exam specification

* **Title:** *PE Mechanical* — NCEES
* **URL:** <https://ncees.org/exams/pe-exam/mechanical/>
* **Status:** `VERIFIED`
* **Applied:** Module structure (HVAC & Refrigeration; Machine Design &
  Materials;
  Thermal & Fluid Systems); 80 questions; 9-hour appointment.
* **Cited in:** `skills/mechanical-engineering/SKILL.md`

### REF-NCEES-004 — PE Electrical and Computer exam specification

* **Title:** *PE Electrical and Computer* — NCEES
* **URL:** <https://ncees.org/exams/pe-exam/electrical-and-computer/>
* **Status:** `VERIFIED`
* **Applied:** Module structure — Computer Engineering; **Electronics, Controls,
  and Communications**; Power. Power is 80 questions / 9 hours; the other two
  are 85 questions / 9.5 hours. Re-verified 2026-09-17: the landing page links
  the three module specification PDFs directly —
  * Computer Engineering (effective October 2025):
    <https://ncees.org/wp-content/uploads/2025/01/FINAL_PE-Electrical_Computer_Oct_2025.pdf>
    — **read in full 2026-09-17.** Defines eight knowledge areas with question
    ranges: 1 Data Representation (7–11); 2 Computer Architecture (12–18);
    3 Systems Software (9–14); 4 Application Development (8–12); 5 Digital
    Devices (8–12); 6 Digital Electronics (8–12); 7 Computer Networks and
    Cybersecurity (11–17); 8 Quality Processes (7–11). States the exam is
    closed book with an electronic reference and "uses both the International
    System of units (SI) and the US Customary System (USCS)."
  * Electronics, Controls, and Communications (effective April 2026):
    <https://ncees.org/wp-content/uploads/2025/10/PE-Electrical_ECC_April_2026.pdf>
    — link verified, not yet read (for `electronics-engineering`, TODO §2.7).
  * Power (effective October 2025):
    <https://ncees.org/wp-content/uploads/2025/04/PE-Electrical_Power_Oct_2025.pdf>
    — link verified, not yet read against `electrical-engineering` (TODO §0.5).
* **Cited in:** `skills/electrical-engineering/SKILL.md`,
  `skills/computer-engineering/SKILL.md`,
  `skills/electronics-engineering/SKILL.md`

### REF-NCEES-005 — PE Control Systems exam specification

* **Title:** *PE Control Systems* — NCEES
* **URL:** <https://ncees.org/exams/pe-exam/control-systems/>
* **Status:** `VERIFIED`
* **Applied:** 85 questions; 9.5-hour appointment; NCEES supplies the electronic
  reference handbook and all specified design standards.
* **Cited in:** `skills/control-systems-engineering/SKILL.md`

### REF-NCEES-006 — PE Chemical exam specification

* **Title:** *PE Chemical* — NCEES
* **URL:** <https://ncees.org/exams/pe-exam/chemical/>
* **Status:** `VERIFIED`
* **Applied:** 80 questions; 9-hour appointment.
* **Cited in:** `skills/chemical-engineering/SKILL.md`

### REF-NCEES-007 — PE Fire Protection exam specification

* **Title:** *PE Fire Protection* — NCEES
* **URL:** <https://ncees.org/exams/pe-exam/fire-protection/>
* **Status:** `VERIFIED`
* **Applied:** 85 questions; 9.5-hour appointment.
* **Cited in:** `skills/fire-protection-engineering/SKILL.md`

### REF-NCEES-008 — PE Naval Architecture and Marine exam specification

* **Title:** *PE Naval Architecture and Marine Engineering* — NCEES
* **URL:** <https://ncees.org/exams/pe-exam/naval-architecture-and-marine/>
* **Status:** `VERIFIED`
* **Applied:** 85 questions; 9.5-hour appointment. Re-verified 2026-09-16: the
  exam landing page does **not** publish a named module breakdown (unlike PE
  Mechanical's three named modules) — the specification document itself was
  not retrieved. Do not assert a module structure for this exam. Open item:
  `TODO.md` §0.5.
* **Cited in:** `skills/naval-architecture-marine/SKILL.md`

---

## 2. Sponsoring and standards-developing professional societies

### REF-SOC-001 — SFPE (Society of Fire Protection Engineers)

* **Title:** *Society of Fire Protection Engineers*
* **URL:** <https://www.sfpe.org/>
* **Status:** `VERIFIED`
* **Applied:** Discipline society for fire protection engineering. Site states:
  "the Society of Fire Protection Engineers is the world's leading professional
  society for fire protection and fire safety engineering," operates a
  "Licensing & PE Exam" program, and publishes the *SFPE Handbook of Fire
  Protection Engineering*, 6th edition.
* **Cited in:** `skills/fire-protection-engineering/SKILL.md`

### REF-SOC-002 — SNAME (Society of Naval Architects and Marine Engineers)

* **Title:** *SNAME*
* **URL:** <https://www.sname.org/>
* **Status:** `VERIFIED`
* **Applied:** Discipline society for naval architecture and marine engineering.
  Stated mission: "Advancing the art, science, and practice of naval
  architecture
  and marine engineering." Operates a member PE Review Course (PERC) and
  publishes
  T&R Bulletins and Reports.
* **Cited in:** `skills/naval-architecture-marine/SKILL.md`

### REF-SOC-003 — ISA (International Society of Automation)

* **Title:** *International Society of Automation*
* **URL:** <https://www.isa.org/certification>
* **Status:** `VERIFIED`
* **Applied:** Discipline society and SDO for control systems engineering;
  publisher of the ISA-5.1, ISA-84 / IEC 61511, ISA-88, ISA-95, and ISA/IEC
  62443
  standards series.
* **Role, in ISA's own words:** "ISA supports the Control Systems Engineer (CSE)
  License, a specialized Professional Engineering (PE) license recognized in the
  United States for engineers working in automation and control. ISA offers
  training courses and review materials to help engineers prepare for state
  boards' exams held each October."
* **Scope of the claim:** ISA states it **supports** the CSE licence and
  supplies
  preparation material. It does **not** claim to author or administer the NCEES
  examination. Do not upgrade this wording to "sponsors" or "develops."
* **Cited in:** `skills/control-systems-engineering/SKILL.md`

### REF-SOC-004 — ASME (American Society of Mechanical Engineers)

* **Title:** *ASME*
* **URL:** <https://www.asme.org/>
* **Status:** `VERIFIED` (root domain)
* **Applied:** Principal SDO for mechanical engineering; publisher of the ASME
  Boiler & Pressure Vessel Code, ASME Y14.5 (GD&T), and ASME B-series
  dimensional standards.
* **Cited in:** `skills/mechanical-engineering/SKILL.md`

### REF-SOC-005 — IEEE (Institute of Electrical and Electronics Engineers)

* **Title:** *IEEE*
* **URL:** <https://www.ieee.org/>
* **Status:** `VERIFIED` (root domain, HTTP 202)
* **Applied:** Principal SDO for electrical, electronics, and computer
  engineering; publisher of the IEEE colour-book series (IEEE 141, 142, 242,
  399, 493, 1584) and IEEE 802.
* **Cited in:** `skills/electrical-engineering/SKILL.md`,
  `skills/computer-engineering/SKILL.md`,
  `skills/electronics-engineering/SKILL.md`

### REF-SOC-006 — AIChE (American Institute of Chemical Engineers)

* **Title:** *American Institute of Chemical Engineers*
* **URL:** <https://www.aiche.org/>
* **Status:** `VERIFIED (BLOCKED)` — HTTP 403 to automated check
* **Applied:** Principal professional society for chemical engineering; parent
  of
  the Center for Chemical Process Safety (CCPS).
* **Cited in:** `skills/chemical-engineering/SKILL.md`

### REF-SOC-007 — AIAA (American Institute of Aeronautics and Astronautics)

* **Title:** *American Institute of Aeronautics and Astronautics*
* **URL:** <https://www.aiaa.org/>
* **Status:** `VERIFIED (BLOCKED)` — HTTP 403 to automated check
* **Applied:** Principal professional society for aeronautical and astronautical
  engineering. **No NCEES PE discipline exists for aeronautical engineering**;
  AIAA is cited as the discipline society, not as an exam sponsor.
* **Cited in:** `skills/aeronautical-engineering/SKILL.md`

### REF-SOC-008 — NFPA (National Fire Protection Association)

* **Title:** *National Fire Protection Association*
* **URL:** <https://www.nfpa.org/>
* **Status:** `VERIFIED`
* **Applied:** SDO for the NFPA code set (NFPA 1, 13, 72, 101, 5000, and others)
  applied throughout fire protection engineering.
* **Cited in:** `skills/fire-protection-engineering/SKILL.md`

---

## 3. Aeronautical engineering — regulatory and technical sources

### REF-FAA-001 — 14 CFR Part 107, Small Unmanned Aircraft Systems

* **Title:** *Title 14 CFR Part 107 — Small Unmanned Aircraft Systems*
* **URL:** <https://www.ecfr.gov/current/title-14/part-107>
* **Status:** `VERIFIED`
* **Applied:** Operating rules and airworthiness expectations for civil sUAS
  under
  55 lbm (25 kg) in US airspace; §107.51 operating limitations.
* **Cited in:** `skills/aeronautical-engineering/SKILL.md`

### REF-FAA-002 — 14 CFR Part 23, Airworthiness Standards: Normal Category Airplanes

* **Title:** *Title 14 CFR Part 23 — Airworthiness Standards: Normal Category
  Airplanes*
* **URL:** <https://www.ecfr.gov/current/title-14/part-23>
* **Status:** `VERIFIED`
* **Applied:** Sections read in full from the eCFR API (title-14, issue date
  2026-08-27):
  * **§23.2200** *Structural design envelope* — para (b) requires "Design
    maneuvering load factors not less than those, which service history shows,
    may occur within the structural design envelope." **Performance-based: the
    rule states no numeric load factor.**
  * **§23.2215** *Flight load conditions* — gusts based on measured gust
    statistics; symmetric and asymmetric manoeuvres; asymmetric thrust.
  * **§23.2230** *Limit and ultimate loads* — para (b): "The ultimate loads,
    which are equal to the limit loads multiplied by a **1.5 factor of safety**
    unless otherwise specified elsewhere in this part."
  * **§23.2235** *Structural strength* — limit loads without detrimental
    permanent deformation; ultimate loads without failure.
  * **§23.2260** *Materials and processes* — para (b): fabrication requiring
    close control must be performed under an approved process specification.
  * **§23.2265** *Special factors of safety* — required where a critical design
    value is uncertain or the article is "subject to appreciable variability
    because of uncertainties in manufacturing processes or inspection methods."
* **Note:** The numeric manoeuvring load factors often quoted as +3.8 / −1.52
  appear **nowhere** in current Part 23 (zero occurrences of "3.8" or "1.52" in
  the retrieved text). They belong to the pre-2017 rule. Do not cite them to
  current Part 23.
* **Cited in:** `skills/aeronautical-engineering/SKILL.md`,
  `skills/aeronautical-engineering/references/loads-and-factors.md`

### REF-FAA-003 — 14 CFR Part 21, Certification Procedures for Products and Articles

* **Title:** *Title 14 CFR Part 21 — Certification Procedures for Products and
  Articles*
* **URL:** <https://www.ecfr.gov/current/title-14/part-21>
* **Status:** `VERIFIED`
* **Applied:** Certification pathway definitions; distinguishes
  type-certificated
  from experimental and special-airworthiness pathways.
* **Cited in:** `skills/aeronautical-engineering/SKILL.md`

### REF-FAA-004 — FAA Advisory Circulars index

* **Title:** *Advisory Circulars* — Federal Aviation Administration
* **URL:** <https://www.faa.gov/regulations_policies/advisory_circulars>
* **Status:** `VERIFIED`
* **Applied:** Entry point for AC-series acceptable means of compliance.
  Individual
  ACs must be added to this catalog with their own REF-ID before being cited.
* **Cited in:** `skills/aeronautical-engineering/SKILL.md`

### REF-NASA-001 — NASA-STD-5001, Structural Design and Test Factors of Safety

* **Title:** *NASA-STD-5001 — Structural Design and Test Factors of Safety for
  Spaceflight Hardware*
* **URL:** <https://standards.nasa.gov/standard/nasa/nasa-std-5001>
* **Status:** `VERIFIED`
* **Applied:** Factor-of-safety framework and the distinction between design,
  yield, and ultimate factors. Applied by analogy to airframe structure; the
  standard's own scope is spaceflight hardware and this limitation is stated
  wherever it is cited.
* **Cited in:**
  `skills/aeronautical-engineering/references/loads-and-factors.md`

### REF-NASA-002 — NASA-STD-5020, Threaded Fastening Systems

* **Title:** *NASA-STD-5020 — Requirements for Threaded Fastening Systems in
  Spaceflight Hardware*
* **URL:** <https://standards.nasa.gov/standard/nasa/nasa-std-5020>
* **Status:** `VERIFIED`
* **Applied:** Fastener preload, separation, and joint-margin methodology.
* **Cited in:**
  `skills/aeronautical-engineering/references/loads-and-factors.md`

### REF-NASA-003 — NASA Technical Reports Server

* **Title:** *NASA Technical Reports Server (NTRS)*
* **URL:** <https://ntrs.nasa.gov/>
* **Status:** `VERIFIED`
* **Applied:** Primary source for NACA/NASA airfoil and aerodynamic reports.
  Individual reports must be added with their own REF-ID and NTRS document
  number
  before being cited.
* **Cited in:** `skills/aeronautical-engineering/SKILL.md`

### REF-ASTM-001 — ASTM Committee F38 on Unmanned Aircraft Systems

* **Title:** *ASTM Committee F38 on Unmanned Aircraft Systems*
* **URL:** <https://www.astm.org/committee-f38>
* **Status:** `VERIFIED (BLOCKED)` — HTTP 403 to automated check
* **Applied:** Consensus standards for UAS design, construction, and operation
  (F3298 series and related). Individual ASTM standards must be added with their
  own REF-ID and confirmed designation/year before being cited.
* **Cited in:** `skills/aeronautical-engineering/SKILL.md`
* **Open item:** Individual F38 standard designations are **not yet verified**.
  Tracked as TODO §0.2.

### REF-NCEES-009 — NCEES FE Reference Handbook

* **Title:** *FE Reference Handbook* — NCEES
* **URL:** <https://ncees.org/engineering/fe/>
* **Status:** `VERIFIED` (landing page); specific handbook version
  `REQUIRES VERIFICATION`
* **Applied:** The sole reference permitted in the FE examination, and therefore
  the definition of FE-level scope for `skills/statics-and-dynamics` and
  `skills/thermodynamics`.
* **Cited in:** `skills/statics-and-dynamics/SKILL.md`,
  `skills/thermodynamics/SKILL.md`
* **Open item:** Confirm the current handbook version number and its published
  statics/dynamics and thermodynamics section lists. Tracked as TODO §0.6.

### REF-SNAME-001 — Principles of Naval Architecture (PNA)

* **Title:** *Principles of Naval Architecture* — Society of Naval Architects and
  Marine Engineers (SNAME)
* **URL:** <https://sname.org/principles-naval-architecture>
* **Status:** `VERIFIED` (publisher, series scope, and volume titles confirmed
  2026-09-16 by fetching the SNAME page directly)
* **Applied:** Governing textbook for naval architecture and marine engineering
  practice — cited generally as "PNA" for method scope (hydrostatics and
  stability, resistance and propulsion, strength, seakeeping, vibration,
  maneuverability). **No specific page, chapter, or edition number is cited from
  this source** — only the publisher, title, and coverage were confirmed, not the
  book's own text. Any numeric method or table attributed to PNA by
  chapter/section must be independently verified against the actual volume
  before being asserted; until then it is cited to a primary source instead
  (IMO, ITTC) where one exists.
* **Cited in:** `skills/naval-architecture-marine/SKILL.md`,
  `skills/naval-architecture-marine/references/hydrostatics-and-stability.md`,
  `skills/naval-architecture-marine/references/resistance-and-propulsion.md`

### REF-IMO-001 — International Code on Intact Stability, 2008 (2008 IS Code)

* **Title:** *International Code on Intact Stability, 2008 (2008 IS Code)*,
  2020 Edition — International Maritime Organization, adopted by IMO Resolution
  MSC.267(85)
* **URL:** <https://www.imo.org/en/OurWork/Safety/Pages/ShipDesignAndStability-default.aspx>
  (IMO entry point; the Code itself is a paid IMO/Witherbys publication, not a
  free full-text URL)
* **Status:** `VERIFIED` — chapter 1 and chapter 2 ("General criteria") text
  read directly from the publisher's publicly posted preview excerpt
  (2020 Edition) on 2026-09-16, not assumed from secondary sources.
* **Applied:** Part A mandatory general intact stability criteria, read verbatim
  from the 2020 Edition preview:
  * **§2.2.1** — area under the GZ curve $\geq 0.055$ m·rad to $\varphi=30°$,
    $\geq 0.09$ m·rad to $\varphi=40°$ (or the down-flooding angle
    $\varphi_f$ if less than 40°), and $\geq 0.03$ m·rad between 30° and 40°
    (or 30° and $\varphi_f$).
  * **§2.2.2** — $GZ \geq 0.2$ m at an angle of heel $\geq 30°$.
  * **§2.2.3** — maximum GZ shall occur at a heel angle $\geq 25°$ (or an
    Administration-approved equivalent).
  * **§2.2.4** — initial metacentric height $GM_0 \geq 0.15$ m.
  * **§2.3** — severe wind and rolling ("weather") criterion: steady wind
    heeling lever $l_{w1} = P\,A\,Z/(1000\,g\,\Delta)$ with $P = 504$ Pa;
    gust heeling lever $l_{w2} = 1.5\,l_{w1}$; steady heel angle
    $\varphi_0 \leq 16°$ or 80% of deck-edge immersion, whichever is less;
    area $b \geq$ area $a$ per Figure 2.3.1-1; alternative test wind speed
    26 m/s full-scale.
  * **§1.1.1** — applies to cargo and passenger ships $\geq 24$ m in length.
* **Cited in:**
  `skills/naval-architecture-marine/references/hydrostatics-and-stability.md`

### REF-ITTC-001 — ITTC Recommended Procedure 7.5-02-02-01, Resistance Test

* **Title:** *ITTC – Recommended Procedures and Guidelines, 7.5-02-02-01,
  "Resistance Test"*, Revision 04, effective 2017 — International Towing Tank
  Conference, Resistance Committee of the 28th ITTC
* **URL:** <https://www.ittc.info/media/8001/75-02-02-01.pdf>
* **Status:** `VERIFIED` — document read directly on 2026-09-16.
* **Applied:** §2.1 resistance-coefficient decomposition:
  $C_T = R_T / (\tfrac{1}{2}\rho S V^2)$, $C_V = C_F(1+k)$,
  $C_W = C_T - C_V$; the **1957 ITTC model-ship correlation line**
  $C_F = 0.075/(\log_{10}Re - 2)^2$; length Froude number $Fr = V/\sqrt{gL}$
  and depth Froude number $Fr_h = V/\sqrt{gh}$ (§2.1–2.2, verified formula
  set and variable definitions).
* **Cited in:**
  `skills/naval-architecture-marine/references/resistance-and-propulsion.md`

### REF-NFPA-001 — NFPA 70, National Electrical Code (NEC)

* **Title:** *NFPA 70, National Electrical Code (NEC)*, 2026 Edition —
  National Fire Protection Association
* **URL:** <https://www.nfpa.org/product/nfpa-70-national-electrical-code-nec/p0070code>
* **Status:** `VERIFIED (BLOCKED)` — the 2026 edition and its late-2025 release
  were confirmed via the ANSI webstore and ICC Safe listings (both accredited
  resellers) on 2026-09-16; nfpa.org itself returned only page chrome to
  automated fetch, matching the pattern already recorded for NFPA under
  REF-SOC-008.
* **Applied:** Governing US wiring and equipment code, cited generally as the
  authority for overcurrent protection, grounding and bonding, conductor
  ampacity, and working-space clearance topics discussed in
  `electrical-engineering`. **No specific NEC article or table number is
  cited from this source** — the full text was not accessible for direct
  verification. Any specific article/table number asserted in this
  repository must be confirmed against the actual 2026 NEC text before being
  relied upon; until then it is flagged `REQUIRES VERIFICATION` inline. See
  `TODO.md` §0.8.
* **Cited in:** `skills/electrical-engineering/SKILL.md`,
  `skills/electrical-engineering/references/protection-and-fault-analysis.md`

### REF-NFPA-002 — NFPA 70E, Standard for Electrical Safety in the Workplace

* **Title:** *NFPA 70E, Standard for Electrical Safety in the Workplace* —
  National Fire Protection Association
* **URL:** <https://www.nfpa.org/product/nfpa-70e-standard/p0070ecode>
* **Status:** `VERIFIED (BLOCKED)` — existence, scope, and the 3-year revision
  cycle confirmed via secondary bookseller listings on 2026-09-16; nfpa.org
  itself returned only page chrome. **Current governing edition as of this
  writing (2026-09-16) is ambiguous from available sources** — bookseller
  listings show both a 2024 edition and a forthcoming 2027 edition; do not
  assert a specific "current" edition number without confirming against
  nfpa.org directly. Tracked as `TODO.md` §0.8.
* **Applied:** Governs electrical safety work practices, arc-flash and shock
  risk assessment requirements, and PPE category selection — cited generally
  as the authority for the *work-practice* side of arc-flash hazard
  management, distinct from IEEE 1584's *calculation* method
  [REF-IEEE-001].
* **Cited in:**
  `skills/electrical-engineering/references/arc-flash-and-safety.md`

### REF-IEEE-001 — IEEE 1584-2018, Guide for Performing Arc-Flash Hazard Calculations

* **Title:** *IEEE 1584-2018 — IEEE Guide for Performing Arc-Flash Hazard
  Calculations*
* **URL:** <https://standards.ieee.org/standard/1584-2018.html>
* **Status:** `VERIFIED` — title, designation, and scope read directly from
  the IEEE Standards Association page on 2026-09-16.
* **Applied:** Defines the mathematical-model method for arc-flash incident
  energy and arc-flash boundary calculation. **Scope, as stated on the
  standard's own page: three-phase AC systems, 208 V to 15 kV nominal;
  explicitly excludes single-phase AC, DC systems, and short-circuit
  studies.** A related standard, IEEE 1584.2-2025, covers arc-flash data
  collection for systems at 1000 V and below. **The specific numeric model
  coefficients and lookup tables in IEEE 1584-2018 are not reproduced in this
  repository** — they are copyrighted content of a paid standard and were not
  independently verified; `skills/electrical-engineering` states the
  calculation *framework* only and directs the user to the current standard
  for coefficients.
* **Cited in:**
  `skills/electrical-engineering/references/arc-flash-and-safety.md`

### REF-ISA-001 — ISA standards portfolio

* **Title:** *Standards and Publications* — International Society of Automation
* **URL:** <https://www.isa.org/standards-and-publications>
* **Status:** `VERIFIED` (index page); individual standard designations
  `REQUIRES VERIFICATION`
* **Applied:** Entry point for the ISA-5.1 (instrumentation symbols), ISA-84 /
  IEC 61511 (safety instrumented systems), ISA-88 (batch control), ISA-95
  (enterprise-control integration), and ISA/IEC 62443 (industrial cybersecurity)
  series.
* **Cited in:** `skills/control-systems-engineering/SKILL.md`
* **Open item:** Each individual standard's designation, edition, and year must
  be
  confirmed before being cited by number. Tracked as TODO §0.7.

---

## 4. Computer engineering — standards, protocols, and foundational papers

All URLs in this section checked 2026-09-17.

### REF-IEEE-002 — IEEE 754-2019, Standard for Floating-Point Arithmetic

* **Title:** *IEEE 754-2019 — IEEE Standard for Floating-Point Arithmetic*
  (supersedes IEEE 754-2008)
* **URL:** <https://standards.ieee.org/ieee/754/6210/>
* **Status:** `VERIFIED` — designation, title, active status, approval
  (2019-06-13) and publication (2019-07-22) dates, and scope read directly
  from the IEEE SA page.
* **Applied:** Scope, quoted: "This standard specifies interchange and
  arithmetic formats and methods for binary and decimal floating-point
  arithmetic in computer programming environments. This standard specifies
  exception conditions and their default handling." Cited for the existence
  of binary and decimal formats, the exception classes, and the general
  structure of a binary interchange format. **The standard's body text
  (format tables, rounding rules) was not read** — the binary32/binary64
  field widths quoted in the skill are standard knowledge consistent with the
  format and are not attributed to a clause number.
* **Cited in:** `skills/computer-engineering/SKILL.md`,
  `skills/computer-engineering/references/data-representation-and-error-control.md`

### REF-IEEE-003 — IEEE 802.3-2022, Standard for Ethernet

* **Title:** *IEEE 802.3-2022 — IEEE Standard for Ethernet*
* **URL:** <https://standards.ieee.org/ieee/802.3/10422/>
* **Status:** `VERIFIED` — designation, title, active status, publication
  date (2022-07-29), and scope read directly from the IEEE SA page.
* **Applied:** Scope, quoted in part: "Ethernet local area network operation
  is specified for selected speeds of operation from 1 Mb/s to 400 Gb/s using
  a common media access control (MAC) specification ... The Carrier Sense
  Multiple Access with Collision Detection (CSMA/CD) MAC protocol specifies
  shared medium (half duplex) operation, as well as full duplex operation."
  Cited as the link-layer authority for Ethernet; no clause number asserted.
* **Cited in:** `skills/computer-engineering/SKILL.md`,
  `skills/computer-engineering/references/digital-design-and-timing.md`,
  `skills/computer-engineering/references/networks-security-and-quality.md`

### REF-IEEE-004 — IEEE 1149.1-2013, Test Access Port and Boundary-Scan Architecture

* **Title:** *IEEE 1149.1-2013 — IEEE Standard for Test Access Port and
  Boundary-Scan Architecture* (supersedes IEEE 1149.1-2001)
* **URL:** <https://standards.ieee.org/ieee/1149.1/4484/>
* **Status:** `VERIFIED` — designation, title, publication date (2013-05-13),
  and scope read directly from the IEEE SA page. **IEEE SA lists the
  standard's status as "Inactive-Reserved" (inactivated 2024-03-21)**, not
  "Active"; the 2001 edition's page (<https://standards.ieee.org/ieee/1149.1/1728/>)
  lists it as superseded by the 2013 edition. No later edition was found. The
  skill reports this status verbatim rather than calling the standard
  "current."
* **Applied:** Scope, quoted in part: defines "circuitry that may be built
  into an integrated circuit to assist in the test, maintenance and support of
  assembled printed circuit boards and the test of internal circuits," with a
  standard test interface and a boundary-scan register. Cited for the
  existence and purpose of boundary scan; no clause number asserted.
* **Cited in:** `skills/computer-engineering/SKILL.md`,
  `skills/computer-engineering/references/digital-design-and-timing.md`

### REF-IEEE-005 — IEEE 1012-2024, System, Software, and Hardware V&V

* **Title:** *IEEE 1012-2024 — IEEE Standard for System, Software, and
  Hardware Verification and Validation*
* **URL:** <https://standards.ieee.org/ieee/1012/7324/>
* **Status:** `VERIFIED` — designation, title, active status, publication
  date (2025-08-22), and scope read directly from the IEEE SA page.
* **Applied:** Scope, quoted in part: V&V processes "are used to determine
  whether the development products of a given activity conform to the
  requirements of that activity and whether the product satisfies its
  intended use and user needs. V&V life cycle process requirements are
  specified for different integrity levels. ... The term software also
  includes firmware and microcode." Cited for the integrity-level framing and
  the verification/validation distinction; no clause number asserted.
* **Cited in:** `skills/computer-engineering/SKILL.md`,
  `skills/computer-engineering/references/networks-security-and-quality.md`

### REF-IETF-001 — RFC 791, Internet Protocol

* **Title:** *RFC 791 — Internet Protocol* (DARPA Internet Program Protocol
  Specification, September 1981)
* **URL:** <https://www.rfc-editor.org/rfc/rfc791>
* **Status:** `VERIFIED` — full text retrieved from the RFC Editor
  2026-09-17.
* **Applied:** Header fields Time to Live ("an indication of an upper bound
  on the lifetime of an internet datagram") and Header Checksum ("a
  verification that the information used in processing internet datagram has
  been transmitted correctly" — header only); fragmentation when a datagram
  exceeds the local network's maximum packet size; network byte order.
* **Cited in:**
  `skills/computer-engineering/references/data-representation-and-error-control.md`,
  `skills/computer-engineering/references/networks-security-and-quality.md`

### REF-IETF-002 — RFC 1122, Requirements for Internet Hosts — Communication Layers

* **Title:** *RFC 1122 — Requirements for Internet Hosts — Communication
  Layers* (October 1989)
* **URL:** <https://www.rfc-editor.org/rfc/rfc1122>
* **Status:** `VERIFIED` — full text retrieved from the RFC Editor
  2026-09-17.
* **Applied:** §1.1.3 *Internet Protocol Suite* — the four-layer model:
  Application Layer, Transport Layer, Internet Layer, Link Layer.
* **Cited in:**
  `skills/computer-engineering/references/networks-security-and-quality.md`

### REF-IETF-003 — RFC 9293, Transmission Control Protocol (TCP)

* **Title:** *RFC 9293 — Transmission Control Protocol (TCP)* (August 2022;
  obsoletes RFC 793, 879, 2873, 6093, 6429, 6528, 6691)
* **URL:** <https://www.rfc-editor.org/rfc/rfc9293>
* **Status:** `VERIFIED` — full text retrieved from the RFC Editor
  2026-09-17; section numbers confirmed from the retrieved text.
* **Applied:** §3.4 *Sequence Numbers*; §3.5 *Establishing a Connection* —
  "The 'three-way handshake' is the procedure used to establish a
  connection" and "The principal reason for the three-way handshake is to
  prevent old duplicate connection initiations from causing confusion."
* **Cited in:**
  `skills/computer-engineering/references/networks-security-and-quality.md`

### REF-NIST-001 — NIST SP 800-82 Rev. 3, Guide to Operational Technology (OT) Security

* **Title:** *NIST Special Publication 800-82 Revision 3 — Guide to
  Operational Technology (OT) Security*, September 2023
* **URL:** <https://csrc.nist.gov/pubs/sp/800/82/r3/final> —
  DOI <https://doi.org/10.6028/NIST.SP.800-82r3>
* **Status:** `VERIFIED` — designation, title, date, final status, and
  abstract read directly from the NIST CSRC page.
* **Applied:** Abstract — guidance "on how to secure operational technology
  (OT) while addressing their unique performance, reliability, and safety
  requirements"; OT defined as programmable systems and devices that
  "interact with the physical environment"; the document "provides an
  overview of OT and typical system topologies, identifies common threats and
  vulnerabilities to these systems, and provides recommended security
  countermeasures." **Body sections were not read; no section number is
  asserted.**
* **Cited in:** `skills/computer-engineering/SKILL.md`,
  `skills/computer-engineering/references/networks-security-and-quality.md`

### REF-NIST-002 — NIST SP 800-193, Platform Firmware Resiliency Guidelines

* **Title:** *NIST Special Publication 800-193 — Platform Firmware Resiliency
  Guidelines*, May 2018
* **URL:** <https://csrc.nist.gov/pubs/sp/800/193/final> —
  DOI <https://doi.org/10.6028/NIST.SP.800-193>
* **Status:** `VERIFIED` — designation, title, date, final status, and
  abstract read directly from the NIST CSRC page.
* **Applied:** Abstract — "security mechanisms for protecting the platform
  against unauthorized changes, detecting unauthorized changes that occur,
  and recovering from attacks rapidly and securely" (the
  protect / detect / recover framing applied in the skill). **Body sections
  were not read; no section number is asserted.**
* **Cited in:** `skills/computer-engineering/SKILL.md`,
  `skills/computer-engineering/references/architecture-and-systems-software.md`,
  `skills/computer-engineering/references/networks-security-and-quality.md`

### REF-NIST-003 — NIST SP 800-160 Vol. 1 Rev. 1, Engineering Trustworthy Secure Systems

* **Title:** *NIST Special Publication 800-160 Volume 1 Revision 1 —
  Engineering Trustworthy Secure Systems*, November 2022
* **URL:** <https://csrc.nist.gov/pubs/sp/800/160/v1/r1/final> —
  DOI <https://doi.org/10.6028/NIST.SP.800-160v1r1>
* **Status:** `VERIFIED` — designation, title, date, final status, and
  abstract read directly from the NIST CSRC page.
* **Applied:** Abstract — "a basis for establishing principles, concepts,
  activities, and tasks for engineering trustworthy secure systems" applied
  "within systems engineering efforts." Cited as the systems-security-
  engineering authority; **no section number is asserted.**
* **Cited in:** `skills/computer-engineering/SKILL.md`,
  `skills/computer-engineering/references/networks-security-and-quality.md`

### REF-NIST-004 — NIST Cybersecurity Framework (CSF) 2.0

* **Title:** *The NIST Cybersecurity Framework (CSF) 2.0*, NIST CSWP 29,
  February 2024
* **URL:** <https://www.nist.gov/cyberframework> (programme page) —
  document DOI <https://doi.org/10.6028/NIST.CSWP.29>, PDF
  <https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.29.pdf>
* **Status:** `VERIFIED` — the CSWP 29 PDF was retrieved and its text read
  2026-09-17; the six Functions were confirmed from the document body, not
  the landing page (which does not enumerate them).
* **Applied:** The six CSF Core Functions, quoted with their one-line
  definitions from the document: GOVERN (GV), IDENTIFY (ID), PROTECT (PR),
  DETECT (DE), RESPOND (RS), RECOVER (RC).
* **Cited in:** `skills/computer-engineering/SKILL.md`,
  `skills/computer-engineering/references/networks-security-and-quality.md`

### REF-NIST-005 — FIPS 140-3, Security Requirements for Cryptographic Modules

* **Title:** *FIPS PUB 140-3 — Security Requirements for Cryptographic
  Modules*, March 22, 2019
* **URL:** <https://csrc.nist.gov/pubs/fips/140-3/final> —
  DOI <https://doi.org/10.6028/NIST.FIPS.140-3>
* **Status:** `VERIFIED` — designation, title, date, final status, and
  abstract read directly from the NIST CSRC page.
* **Applied:** Abstract — requirements for "cryptographic-based security
  systems to protect sensitive information in computer and telecommunication
  systems"; "four increasing, qualitative levels of security." Cited so the
  skill can defer cryptographic-module and algorithm-approval questions to
  NIST rather than assert them. **Algorithm-specific FIPS/SP documents are
  not catalogued and must be added before any algorithm is recommended by
  name.**
* **Cited in:** `skills/computer-engineering/SKILL.md`,
  `skills/computer-engineering/references/networks-security-and-quality.md`

### REF-UEFI-001 — UEFI Specification

* **Title:** *Unified Extensible Firmware Interface (UEFI) Specification*,
  Version 2.11 (released December 2024) — UEFI Forum
* **URL:** <https://uefi.org/specifications>
* **Status:** `VERIFIED` — the specifications index page was retrieved
  2026-09-17 and lists Version 2.11 (December 2024) as the latest UEFI
  Specification release, alongside 2.10 Errata A (August 2024). **The
  specification body was not read; no section number is asserted.**
* **Applied:** Existence and current version of the UEFI specification as
  the firmware–OS-loader interface standard on general-purpose platforms.
* **Cited in:** `skills/computer-engineering/SKILL.md`,
  `skills/computer-engineering/references/architecture-and-systems-software.md`

### REF-PAPER-001 — Amdahl (1967), single-processor validity / speed-up

* **Title:** G. M. Amdahl, "Validity of the single processor approach to
  achieving large scale computing capabilities," *Proceedings of the April
  18–20, 1967, Spring Joint Computer Conference (AFIPS '67 Spring)*, 1967.
* **URL:** <https://doi.org/10.1145/1465482.1465560>
* **Status:** `VERIFIED (BLOCKED)` — bibliographic metadata (title, author,
  venue, year) confirmed 2026-09-17 from the CrossRef DOI registry
  (`api.crossref.org`); the ACM Digital Library returns HTTP 403 to automated
  retrieval and the **full text was not read.**
* **Applied:** The speed-up bound generally called "Amdahl's law,"
  $S = 1/((1-f) + f/k)$. **The attribution of this specific formula to the
  paper's text is `REQUIRES VERIFICATION`** — the skill presents the formula
  as the standard result and names the paper, but does not cite a page.
  Tracked as `TODO.md` §0.9.
* **Cited in:** `skills/computer-engineering/SKILL.md`,
  `skills/computer-engineering/references/architecture-and-systems-software.md`

### REF-PAPER-002 — Liu and Layland (1973), hard-real-time scheduling

* **Title:** C. L. Liu and J. W. Layland, "Scheduling Algorithms for
  Multiprogramming in a Hard-Real-Time Environment," *Journal of the ACM*,
  vol. 20, no. 1, January 1973.
* **URL:** <https://doi.org/10.1145/321738.321743>
* **Status:** `VERIFIED (BLOCKED)` — bibliographic metadata confirmed
  2026-09-17 from the CrossRef DOI registry; ACM Digital Library returns
  HTTP 403 to automated retrieval and the **full text was not read.**
* **Applied:** The rate-monotonic utilisation bound
  $U \leq n(2^{1/n} - 1)$ and the earliest-deadline-first bound $U \leq 1$
  for independent periodic tasks. **Attribution of these specific theorems
  to the paper's text is `REQUIRES VERIFICATION`**; no theorem number is
  cited. Tracked as `TODO.md` §0.9.
* **Cited in:** `skills/computer-engineering/SKILL.md`,
  `skills/computer-engineering/references/architecture-and-systems-software.md`

### REF-PAPER-003 — Hamming (1950), error detecting and correcting codes

* **Title:** R. W. Hamming, "Error Detecting and Error Correcting Codes,"
  *Bell System Technical Journal*, vol. 29, no. 2, April 1950.
* **URL:** <https://doi.org/10.1002/j.1538-7305.1950.tb00463.x> (resolves to
  IEEE Xplore document 6772729)
* **Status:** `VERIFIED (BLOCKED)` — bibliographic metadata confirmed
  2026-09-17 from the CrossRef DOI registry; IEEE Xplore returns an anti-bot
  challenge (HTTP 202) to automated retrieval and the **full text was not
  read.**
* **Applied:** Origin of single-error-correcting systematic codes and the
  minimum-distance concept. **Attribution of the specific distance/
  correction statements ($d-1$ detect, $\lfloor(d-1)/2\rfloor$ correct;
  $2^r - r - 1$ data bits for $r$ check bits) to the paper's text is
  `REQUIRES VERIFICATION`**; the skill presents them as standard coding
  theory. Tracked as `TODO.md` §0.9.
* **Cited in:** `skills/computer-engineering/SKILL.md`,
  `skills/computer-engineering/references/data-representation-and-error-control.md`

---

## Removed / Superseded Citations

**Corrected 2026-08-29 — factor of safety in 14 CFR Part 23.** An earlier draft
of `references/loads-and-factors.md` marked the 1.5 airframe factor of safety
`REQUIRES VERIFICATION`, on the reasoning that the 2017 Part 23 restructure
moved
numeric criteria into consensus standards. Reading the current rule text from
the
eCFR API disproved that for the factor of safety specifically: **§23.2230(b)
states the 1.5 factor explicitly and it is current.** The caution was correct
for
the *manoeuvring load factors* (+3.8 / −1.52), which are genuinely absent from
the
current rule. Both are now cited accurately under REF-FAA-002.

---

## Adding a citation

1. Look the source up here by REF-ID first.
2. If absent, add it with a validated URL and the specific section applied.
3. If the section cannot be confirmed against the issuing body, mark it
   `REQUIRES VERIFICATION` and open a `TODO.md` §0.x item.
4. Never invent or guess a designation, section number, edition, or year.
