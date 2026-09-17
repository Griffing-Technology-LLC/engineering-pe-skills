---
name: computer-engineering
description: Computer engineering aligned to the NCEES PE Electrical and Computer (Computer Engineering) exam — number and data representation, error detection and correction, processor and memory architecture, embedded systems and microcontroller interfacing, real-time scheduling and interrupts, firmware and boot, digital logic and timing analysis, ADC/DAC and signalling standards, computer networks, system cybersecurity, and software verification and validation. Use when choosing a number format or checking overflow, sizing a CRC or ECC scheme, estimating CPI/speed-up or cache performance, checking real-time schedulability or interrupt latency, designing or timing a synchronous digital circuit, resolving metastability or clock-domain crossing, selecting a bus or signalling standard (CAN, LVDS, Ethernet), specifying a secure boot or firmware-update chain, laying out a network or threat model for an embedded product, or building a V&V/test plan for safety-critical software.
license: MIT
metadata:
    author: Griffing Technology LLC
    discipline: Electrical and Computer Engineering (Computer Engineering)
    ncees_alignment: "PE Electrical and Computer — Computer Engineering module: 85 questions, 9.5-hour appointment [REF-NCEES-004]"
    sponsoring_society: IEEE (Institute of Electrical and Electronics Engineers)
    version: 0.1.0
---

# Computer Engineering

Computer architecture, embedded systems, digital design, networks, and
cybersecurity aligned to the Computer Engineering module of the NCEES PE
Electrical and Computer examination, with every method traceable to a cited
authority.

## Mandatory notice — emit this every time

**Before any analysis, in every response where this skill contributes, emit the
following notice verbatim.** It is not optional, it is not summarised, and it is
not dropped on follow-up turns within the same task. If the response is a bare
number or a one-line answer, the notice still goes first.

> ⚠️ **ENGINEERING REVIEW REQUIRED — this output is not a substitute for a
> qualified engineer.** Every result, calculation, and recommendation produced
> with this skill **must be independently reviewed and accepted by a properly
> qualified individual** — a licensed Professional Engineer or an equivalently
> qualified authority for the jurisdiction and discipline — **before it is
> applied to any system carrying risk to life or safety.** This skill informs
> engineering judgment; it does not replace it, and it carries no professional
> liability.

Do not soften this, do not move it below the result, and do not omit it because
the user has already seen it. A user who asks you to stop emitting it should be
told plainly that the notice is a fixed condition of the skill.

## Examination standing

Aligned to the **Computer Engineering module** of PE Electrical and Computer
[REF-NCEES-004] — NCEES offers three modules under this discipline (Computer
Engineering; Electronics, Controls, and Communications; Power); a candidate
sits one. Computer Engineering is 85 questions across a 9.5-hour appointment,
closed book with an electronic reference, and uses **both SI and US Customary
units**. The published exam specification (effective October 2025) was read
in full for this skill and defines eight knowledge areas, reproduced here
with their question ranges so the skill's scope is grounded in the spec, not
a summary page:

| # | Knowledge area | Questions |
| --- | --- | --- |
| 1 | Data representation | 7–11 |
| 2 | Computer architecture | 12–18 |
| 3 | Systems software | 9–14 |
| 4 | Application development | 8–12 |
| 5 | Digital devices | 8–12 |
| 6 | Digital electronics | 8–12 |
| 7 | Computer networks and cybersecurity | 11–17 |
| 8 | Quality processes | 7–11 |

The companion Power module is covered by `electrical-engineering`; the
Electronics, Controls, and Communications module belongs to
`electronics-engineering` (planned, `TODO.md` §2.7). Analog circuit design,
signal integrity at the PCB level, and EMC belong there, not here.

The principal SDO is **IEEE** [REF-SOC-005]. Standards verified directly for
this skill: **IEEE 754-2019** floating-point arithmetic [REF-IEEE-002],
**IEEE 802.3-2022** Ethernet [REF-IEEE-003], **IEEE 1149.1-2013** boundary
scan [REF-IEEE-004], and **IEEE 1012-2024** system/software/hardware V&V
[REF-IEEE-005]. Internet protocols are cited to the IETF RFC Editor
[REF-IETF-001..003]; security engineering to NIST [REF-NIST-001..005]; boot
firmware to the UEFI Forum [REF-UEFI-001]. Three foundational papers —
Amdahl (1967), Liu and Layland (1973), Hamming (1950) — are catalogued with
DOI-registry-verified metadata [REF-PAPER-001..003], but their full texts
are paywall-blocked: the well-known results attributed to them are marked
`REQUIRES VERIFICATION` against the paper text (`TODO.md` §0.9).

## Non-negotiable practice rules

1. **Physical quantities are imperial-primary with metric in parentheses** —
   cable run `ft (m)`, board temperature `°F (°C)`, enclosure dimensions
   `in (mm)`. **Electrical and information quantities are SI or their own
   native units: V, A, W, Hz, s, bit, byte.** Never invent an imperial unit
   for a data rate or a voltage. Airspeed and wind speed, where an embedded
   product reports them, are in **knots (kt)**.
2. **State the radix, width, and signedness** of every number before any
   arithmetic on it. "0xFF" is 255, −1, or a bit pattern depending on the
   declaration; a result without its representation is not a result.
3. **Declare binary versus decimal prefixes.** Say whether "1 KB" means
   1000 or 1024 bytes and whether a "1 Gb/s" link is 10⁹ bit/s. Mixing them
   silently produces a ~7 % error at giga scale and a wrong memory-map
   boundary at any scale.
4. **A timing result names its clock and its worst-case corner.** Setup,
   hold, propagation, and interrupt-latency figures are meaningless without
   the clock period, the process/voltage/temperature corner assumed, and
   whether the number is typical or guaranteed-by-datasheet.
5. **Real-time means bounded, not fast.** A schedulability claim states the
   scheduling policy, every task's period and worst-case execution time, and
   which utilisation test was applied. Average-case throughput never proves
   a deadline.
6. **Every error-control scheme states what it cannot catch.** A CRC or
   parity choice is reported with its detection guarantee *and* its blind
   spots (undetected-error class); an ECC scheme with its correct/detect
   capability. "Has a checksum" is not a specification.
7. **Security is a stated threat model, not a feature list.** Before
   recommending secure boot, encryption, or authentication, state the assets,
   the adversary's assumed access (network, physical, supply chain), and the
   trust anchor. Do not assert a cryptographic strength, key length, or
   algorithm approval without citing the governing NIST publication
   [REF-NIST-005]; never invent one.
8. **Safety-critical software gets an integrity level and a V&V plan** per
   IEEE 1012 [REF-IEEE-005] — stated, not implied. Name the failure mode
   for any fault-tolerance or watchdog claim, exactly as in
   `mechanical-engineering`: silent data corruption, missed deadline,
   stuck interrupt, brown-out reset loop, unauthenticated update.
9. **No "TBD" for power, memory, or bandwidth budgets.** An estimate with a
   stated basis and uncertainty, or nothing — a microcontroller selection
   without a flash/RAM/current margin is a placeholder, not a design.

## Method selection

| Problem | Read |
| --- | --- |
| Number formats, IEEE 754, overflow, character encoding, parity/CRC/ECC, compression | `references/data-representation-and-error-control.md` |
| CPI, Amdahl speed-up, cache/memory hierarchy, RAID, embedded interfacing, RTOS scheduling, interrupts, firmware/boot | `references/architecture-and-systems-software.md` |
| Combinational/sequential logic, FSMs, setup/hold, metastability and CDC, hazards, fan-out, ADC/DAC, CAN/LVDS signalling, DFT and boundary scan | `references/digital-design-and-timing.md` |
| Network layering and design, TCP/IP, Ethernet, threat modelling, secure boot and firmware resiliency, software design, V&V and test planning | `references/networks-security-and-quality.md` |

## Core workflow

1. **Fix the representation first** — radix, width, signedness, endianness,
   and prefix convention for every quantity that will be stored or
   transmitted (rule 2, rule 3).
2. **Budget the platform** — CPU utilisation, flash, RAM, bus bandwidth,
   and current draw, each with margin and basis (rule 9). Selection of a
   processor or memory device follows the budget, never precedes it.
3. **Prove timing at the worst corner** — synchronous logic against setup
   and hold with clock skew and jitter included; software against
   worst-case execution time and interrupt latency (rule 4, rule 5).
4. **Choose error control from the fault model** — what errors the channel
   or memory actually produces (single bit, burst, erasure), then the code
   whose guarantee covers them (rule 6).
5. **Threat-model before securing** — assets, adversary, trust anchor; then
   select mechanisms and cite the governing NIST publication (rule 7).
6. **Plan V&V to the integrity level** — test coverage, assertions,
   reviews, and root-cause process proportionate to the consequence of
   failure (rule 8).

## Reporting a result

* **Result** with representation stated (radix/width/signedness or native
  unit), and physical quantities imperial-primary with metric
* **Corner and clock** for any timing figure; **policy, task set, and test**
  for any schedulability claim
* **Error-control guarantee and blind spot** for any code chosen
* **Budget margins** — CPU, memory, bandwidth, power — with basis
* **Threat model** assumed for any security recommendation, and the NIST or
  IEEE source for each mechanism
* **Integrity level and V&V scope** for any safety-related software
* **Handoffs** — analog front-end, signal integrity, and EMC to
  `electronics-engineering` (planned); loop tuning to
  `control-systems-engineering`; supply and protection to
  `electrical-engineering`

Where a result depends on a standard whose text was not read directly
(`VERIFIED (BLOCKED)` in `REFERENCES.md`) or on a paper result flagged under
`TODO.md` §0.9, say so explicitly rather than presenting it as confirmed.
