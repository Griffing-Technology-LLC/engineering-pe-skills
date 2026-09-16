# Arc-Flash Hazard Framework and Electrical Safety

Reference file for the `electrical-engineering` skill. The scope statement in
§1 is read directly from IEEE 1584-2018's own standards-page description
[REF-IEEE-001]. **This file deliberately does not reproduce IEEE 1584's
numeric model coefficients, lookup tables, or worked incident-energy values**
— they are copyrighted content of a paid standard and were not independently
verified against the primary text. Treat every number in an arc-flash study
as something to be computed from the current standard or an accepted study
tool, never recalled from memory or from this file.

## 1. What IEEE 1584-2018 actually covers — read the scope before applying it

**Verified scope, from the standard's own page:** three-phase AC systems,
**208 V to 15 kV** nominal. It **explicitly excludes** single-phase AC
systems, DC systems, and short-circuit studies themselves (short-circuit
current is an *input* to the arc-flash calculation, computed separately —
see `references/protection-and-fault-analysis.md`).

A related standard, **IEEE 1584.2-2025**, addresses arc-flash *data
collection* methodology for systems at 1000 V and below.

**Before attempting any arc-flash estimate, check the equipment against this
scope.** A single-phase panel, a DC bus, or a system above 15 kV falls
outside IEEE 1584-2018's validated model — state that explicitly rather than
extrapolating the method past its stated range.

## 2. The calculation framework, in outline

IEEE 1584's method, at the level this skill states it (without the
copyrighted coefficients themselves):

1. **Establish the bolted fault current** at the equipment bus — from a
   short-circuit study (`references/protection-and-fault-analysis.md`), at
   the system voltage and configuration.
2. **Determine the arcing current** — generally lower than the bolted fault
   current, from the standard's model as a function of bolted fault current,
   voltage, electrode configuration, and gap.
3. **Determine the protective device's clearing time** at the arcing-current
   level, from its actual time-current characteristic — not its nameplate
   rating.
4. **Compute incident energy** as a function of arcing current, clearing
   time, working distance, and equipment/enclosure configuration.
5. **Compute the arc-flash boundary** — the distance at which incident energy
   falls to the threshold associated with a second-degree burn.
6. **Select PPE** from the calculated incident energy against NFPA 70E's PPE
   category tables [REF-NFPA-002], not IEEE 1584 directly — 1584 computes the
   hazard, 70E governs the *work-practice and PPE* response to it.

**Step 3 is where coordination (§4 of `protection-and-fault-analysis.md`)
becomes an arc-flash safety issue, not just a reliability one** — a slower
clearing time directly increases incident energy. Improving coordination and
reducing arc-flash hazard are frequently the same engineering action.

## 3. Working distance and the bounding cube

Incident energy is evaluated at a stated **working distance** — the distance
between the potential arc source and the worker's face/chest, standardised
per equipment class (e.g., different typical distances for low-voltage
panelboards vs medium-voltage switchgear) rather than assumed generically.
State the actual working distance used; it strongly affects the result since
incident energy falls off with distance from the arc.

## 4. NFPA 70E — the work-practice side

NFPA 70E [REF-NFPA-002] requires, independent of the specific incident-energy
number:

* An electrical safety program with documented policies.
* An arc-flash and shock risk assessment for the equipment being worked.
* PPE selected for the assessed hazard, provided at no cost to the worker.
* Qualified-person requirements for anyone performing energized work.
* Lockout/tagout and other energy-control procedures as the **first**
  choice — de-energized work is always preferred over energized work
  performed with PPE; PPE is the last layer, not the primary control.

**This repository has not confirmed the currently-governing NFPA 70E edition
as of the query date** (bookseller listings show both a 2024 and a
forthcoming 2027 edition) — confirm directly against nfpa.org before citing a
specific edition year (`TODO.md` §0.8).

## 5. What this file will not do

* **Will not compute or state an incident-energy value, PPE category, or
  arc-flash boundary distance.** These require the copyrighted IEEE 1584
  coefficients and equipment-specific inputs (bus gap, enclosure type,
  electrode configuration) that this repository has not catalogued.
* **Will not assert a specific NEC or 70E article/section number** without
  the verification flagged in `TODO.md` §0.8.
* **Will hand off** any request for an actual arc-flash study to a current,
  licensed copy of IEEE 1584-2018 (and 1584.2-2025 where applicable) or an
  accepted arc-flash study tool, performed or reviewed by a qualified
  engineer — consistent with this skill's mandatory review notice.
