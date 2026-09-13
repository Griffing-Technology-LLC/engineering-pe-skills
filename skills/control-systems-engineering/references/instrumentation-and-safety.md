# Instrumentation, Final Elements, and Functional Safety

Reference file for the `control-systems-engineering` skill.

## 1. Measurement

The loop cannot outperform its measurement. Consider, and state:

* **Accuracy vs repeatability** — control needs repeatability; accounting needs
  accuracy. They are different specifications and are often confused.
* **Range and turndown** — accuracy quoted as a percentage of *span* becomes poor
  in absolute terms at the low end of a wide range.
* **Response time**, including sensor lag and any thermowell — a thermowell can
  add tens of seconds of lag to a temperature loop, which appears in the model as
  additional dead time and directly limits achievable performance.
* **Installation effects** — straight-run requirements for flow meters, impulse
  line filling for DP, and sensor location relative to the process.

Sensor location is a design decision with more leverage than tuning: moving a
measurement closer to the process action reduces dead time, and reducing dead
time is the only way to raise the performance ceiling.

## 2. Signal standards

4–20 mA remains dominant because **live zero distinguishes a real zero reading
from a broken wire** — a 0–20 mA signal cannot. HART overlays digital data on the
same pair; fieldbus and Ethernet-based protocols carry it fully digitally.

Declare engineering units vs percent of span explicitly at every interface. Span
and zero errors at controller boundaries cause more commissioning faults than
tuning does.

## 3. Final control elements

**Control valves.** Size for the *controllable* range, not the maximum flow.
An oversized valve operates nearly closed, where its gain is highest and most
non-linear, and the loop becomes untunable across the range.

* **Inherent characteristic** — linear, equal-percentage, quick-opening.
  Equal-percentage is common where valve pressure drop varies with flow, since
  the *installed* characteristic then approaches linear.
* **Fail position** — fail-open, fail-closed, or fail-in-place is a **process
  safety decision**, not a convenience. Determine it from what the process needs
  on loss of air or power, and document the reasoning.
* **Stiction and deadband** cause limit cycling that no tuning will remove.

**Variable-speed drives** are often a better final element than a throttling
valve, since pump power scales with the cube of speed.

## 4. P&IDs and documentation

ISA-5.1 [REF-ISA-001] defines instrumentation symbols and tag identification —
the letter conventions for measured variable and function, and the balloon
conventions for mounting and accessibility.

> Confirm the current ISA-5.1 designation and edition before citing it by number.
> See `TODO.md` §0.7.

A P&ID is the authoritative interface between process, control, and safety
disciplines. Loop numbering, tag consistency, and fail positions belong on it.

## 5. Safety instrumented systems

**The single most important architectural rule in this discipline: a safety
instrumented system is separate from the basic process control system.**

The BPCS controls the process. The SIS takes it to a safe state when the BPCS
and operator have failed. Deriving the safety function from the same sensor,
logic solver, or final element as the control function creates a common-cause
failure that defeats the protection layer entirely. ISA-84 / IEC 61511
[REF-ISA-001] governs the lifecycle.

**Safety Integrity Level (SIL)** expresses required risk reduction, determined by
hazard analysis — usually LOPA — not chosen by preference. Higher SIL demands
more capable architecture, better diagnostics, and more frequent proof testing.

Terms that must not be blurred:

* **PFD** — probability of failure on demand, for low-demand functions
* **Proof test interval** — directly drives PFD; a SIL claim without a stated
  test interval is incomplete
* **Safe failure fraction** and **hardware fault tolerance** — architectural
  constraints that a SIL claim must satisfy independently of PFD

**A SIL number quoted without its verification basis is not a SIL claim.** State
the architecture, the failure data source, the proof test interval, and the
calculated PFD.

## 6. Security

ISA/IEC 62443 [REF-ISA-001] governs industrial automation and control system
security. Treat it as a design input from the first architecture sketch, not a
network-layer addition afterwards.

The core concept is **zones and conduits** — group assets by required security
level, and control the communication paths between them. Note that safety and
security interact: a security control that can block a safety function is itself
a hazard, and must be assessed as one.

> Confirm current ISA/IEC 62443 part numbers and editions before citing them
> individually. See `TODO.md` §0.7.
