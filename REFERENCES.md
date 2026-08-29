# REFERENCES

Authoritative reference catalog for the `engineering-pe-skills` repository.

Every specification, calculation method, and design rule asserted anywhere in this
repository is traceable to an entry below.  Each entry carries a REF-ID, the full
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

* **Title:** *PE Exam* — National Council of Examiners for Engineering and Surveying
* **URL:** <https://ncees.org/exams/pe-exam/>
* **Status:** `VERIFIED`
* **Applied:** The authoritative list of 23 PE disciplines used to scope this
  repository and to assign each skill its `ncees_alignment` frontmatter field.
* **Cited in:** `README.md`, `AGENTS.md`, all `skills/*/SKILL.md` frontmatter.
* **Note:** NCEES discipline pages do **not** name sponsoring professional
  societies. Sponsorship claims in this repository are therefore cited to the
  society itself, never to NCEES. See §2.

### REF-NCEES-002 — NCEES FE Exam

* **Title:** *FE Exam* — National Council of Examiners for Engineering and Surveying
* **URL:** <https://ncees.org/engineering/fe/>
* **Status:** `VERIFIED`
* **Applied:** Establishes that statics and dynamics are **FE-level** subject
  matter, not a PE discipline. Governs the alignment of
  `skills/statics-and-dynamics/`.
* **Cited in:** `skills/statics-and-dynamics/SKILL.md`

### REF-NCEES-003 — PE Mechanical exam specification

* **Title:** *PE Mechanical* — NCEES
* **URL:** <https://ncees.org/exams/pe-exam/mechanical/>
* **Status:** `VERIFIED`
* **Applied:** Module structure (HVAC & Refrigeration; Machine Design & Materials;
  Thermal & Fluid Systems); 80 questions; 9-hour appointment.
* **Cited in:** `skills/mechanical-engineering/SKILL.md`

### REF-NCEES-004 — PE Electrical and Computer exam specification

* **Title:** *PE Electrical and Computer* — NCEES
* **URL:** <https://ncees.org/exams/pe-exam/electrical-and-computer/>
* **Status:** `VERIFIED`
* **Applied:** Module structure — Computer Engineering; **Electronics, Controls,
  and Communications**; Power. Power is 80 questions / 9 hours; the other two are
  85 questions / 9.5 hours.
* **Cited in:** `skills/electrical-engineering/SKILL.md`,
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
* **Applied:** 85 questions; 9.5-hour appointment.
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
  Stated mission: "Advancing the art, science, and practice of naval architecture
  and marine engineering." Operates a member PE Review Course (PERC) and publishes
  T&R Bulletins and Reports.
* **Cited in:** `skills/naval-architecture-marine/SKILL.md`

### REF-SOC-003 — ISA (International Society of Automation)

* **Title:** *International Society of Automation*
* **URL:** <https://www.isa.org/>
* **Status:** `VERIFIED` (root domain); specific CSE-licensure page
  `REQUIRES VERIFICATION`
* **Applied:** Discipline society and SDO for control systems engineering;
  publisher of the ISA-5.1, ISA-84 / IEC 61511, ISA-88, ISA-95, and ISA/IEC 62443
  standards series.
* **Cited in:** `skills/control-systems-engineering/SKILL.md`
* **Open item:** The ISA page describing its role relative to the NCEES PE Control
  Systems exam returned HTTP 404 at the URL first tried. The specific sponsorship
  relationship is **not yet verified** and is not asserted anywhere in this
  repository. Tracked as TODO §0.1.

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
  `skills/electronics-engineering/SKILL.md`

### REF-SOC-006 — AIChE (American Institute of Chemical Engineers)

* **Title:** *American Institute of Chemical Engineers*
* **URL:** <https://www.aiche.org/>
* **Status:** `VERIFIED (BLOCKED)` — HTTP 403 to automated check
* **Applied:** Principal professional society for chemical engineering; parent of
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
* **Applied:** Operating rules and airworthiness expectations for civil sUAS under
  55 lbm (25 kg) in US airspace; §107.51 operating limitations.
* **Cited in:** `skills/aeronautical-engineering/SKILL.md`

### REF-FAA-002 — 14 CFR Part 23, Airworthiness Standards: Normal Category Airplanes

* **Title:** *Title 14 CFR Part 23 — Airworthiness Standards: Normal Category Airplanes*
* **URL:** <https://www.ecfr.gov/current/title-14/part-23>
* **Status:** `VERIFIED`
* **Applied:** Performance-based airworthiness structure; limit and ultimate load
  factor philosophy applied by analogy to unmanned airframes.
* **Cited in:** `skills/aeronautical-engineering/SKILL.md`,
  `skills/aeronautical-engineering/references/loads-and-factors.md`

### REF-FAA-003 — 14 CFR Part 21, Certification Procedures for Products and Articles

* **Title:** *Title 14 CFR Part 21 — Certification Procedures for Products and Articles*
* **URL:** <https://www.ecfr.gov/current/title-14/part-21>
* **Status:** `VERIFIED`
* **Applied:** Certification pathway definitions; distinguishes type-certificated
  from experimental and special-airworthiness pathways.
* **Cited in:** `skills/aeronautical-engineering/SKILL.md`

### REF-FAA-004 — FAA Advisory Circulars index

* **Title:** *Advisory Circulars* — Federal Aviation Administration
* **URL:** <https://www.faa.gov/regulations_policies/advisory_circulars>
* **Status:** `VERIFIED`
* **Applied:** Entry point for AC-series acceptable means of compliance. Individual
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
* **Cited in:** `skills/aeronautical-engineering/references/loads-and-factors.md`

### REF-NASA-002 — NASA-STD-5020, Threaded Fastening Systems

* **Title:** *NASA-STD-5020 — Requirements for Threaded Fastening Systems in
  Spaceflight Hardware*
* **URL:** <https://standards.nasa.gov/standard/nasa/nasa-std-5020>
* **Status:** `VERIFIED`
* **Applied:** Fastener preload, separation, and joint-margin methodology.
* **Cited in:** `skills/aeronautical-engineering/references/loads-and-factors.md`

### REF-NASA-003 — NASA Technical Reports Server

* **Title:** *NASA Technical Reports Server (NTRS)*
* **URL:** <https://ntrs.nasa.gov/>
* **Status:** `VERIFIED`
* **Applied:** Primary source for NACA/NASA airfoil and aerodynamic reports.
  Individual reports must be added with their own REF-ID and NTRS document number
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

---

## Removed / Superseded Citations

*None to date.*

---

## Adding a citation

1. Look the source up here by REF-ID first.
2. If absent, add it with a validated URL and the specific section applied.
3. If the section cannot be confirmed against the issuing body, mark it
   `REQUIRES VERIFICATION` and open a `TODO.md` §0.x item.
4. Never invent or guess a designation, section number, edition, or year.
