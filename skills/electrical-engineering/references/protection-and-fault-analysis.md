# Short-Circuit Analysis, Overcurrent Protection, and Grounding

Reference file for the `electrical-engineering` skill. Standard
protection-engineering methods, governed generally by IEEE 242 (Buff Book)
and IEEE 399 (Brown Book) [REF-SOC-005] at index level — no specific
colour-book section number is asserted here. **NEC (NFPA 70) topics are named
generically, without article numbers**, per the caution in `SKILL.md` and
`REFERENCES.md` REF-NFPA-001; confirm current article/table numbers directly
before relying on them (`TODO.md` §0.8).

## 1. Fault types and which sequence networks they use

Build the positive-, negative-, and zero-sequence networks
(§3 of `power-systems-and-per-unit.md`) first, then connect them per fault
type:

| Fault | Sequence network connection | Notes |
| --- | --- | --- |
| Three-phase symmetrical | Positive-sequence only | Usually the **largest** fault current; governs interrupting-rating checks |
| Single-line-to-ground (SLG) | Positive, negative, zero — **series** | Needs a zero-sequence return path; magnitude strongly depends on grounding scheme |
| Line-to-line (LL) | Positive, negative — **parallel** | No zero-sequence involvement |
| Double-line-to-ground (DLG) | All three — combined | Less common as the governing case, but check it |

**State the fault type explicitly with every fault-current result** — this is
the single rule in `SKILL.md` that exists because it is the most common
omission.

## 2. Symmetrical fault current, per-unit method

$$I_{fault,pu} = \frac{1}{Z_{th,pu}}$$

$Z_{th,pu}$ — Thevenin impedance to the fault point, in the sequence-network
combination for the fault type, all on a common base. Convert back to actual
amperes using the base current at the fault-point voltage (§1 of
`power-systems-and-per-unit.md`).

**Asymmetry / DC offset:** the *first-cycle* fault current can substantially
exceed the steady-state symmetrical value due to the DC offset from the
X/R ratio at the fault point. Equipment interrupting and momentary/close-and-
latch ratings are tested against **specific** multiplying factors defined by
the applicable equipment standard for the device's X/R — **do not invent a
multiplier**; use the factor from the equipment's governing standard for the
calculated X/R, or flag that the study needs it.

## 3. Overcurrent protection sizing

A protective device must satisfy, simultaneously:

1. **Interrupting rating $\geq$ available fault current** at its location —
   the maximum, not the typical, fault current (usually the three-phase
   symmetrical value, first-cycle).
2. **Continuous rating** appropriate to the protected conductor's ampacity
   and the load — this is a code-table matter (conductor ampacity tables);
   confirm the specific table against the current NEC directly per
   `SKILL.md`'s caution — **no specific table number is asserted here.**
3. **Let-through energy** ($I^2t$) below the withstand rating of the
   downstream equipment and conductors it protects, for current-limiting
   devices.

## 4. Coordination

Two protective devices in series **coordinate** when the downstream (load-
side) device clears a fault before the upstream device operates, across the
full range of fault currents both could see. Verify this **graphically**, by
overlaying time-current characteristic (TCC) curves — a device passing its
individual rating check can still fail to coordinate with its neighbours.

**Selective coordination** requires margin at every current level the curves
overlap, not just at one operating point — check the full curve, not a
single fault-current value.

Instantaneous trip elements remove time delay at high current specifically to
protect equipment from short-duration high-energy events, at the direct cost
of coordination with anything downstream that also has an instantaneous
element in that current range — state this trade-off explicitly when
recommending an instantaneous setting.

## 5. Grounding and bonding

**State the system grounding scheme before any ground-fault analysis** —
it changes both the magnitude of ground-fault current and the correct
protection response:

| Scheme | Ground-fault current | Typical use |
| --- | --- | --- |
| Solidly grounded | High — behaves like a bolted fault | Utility distribution, most low-voltage systems |
| Low-resistance grounded | Limited to a defined, deliberately low value | Medium-voltage industrial, to limit damage while still tripping |
| High-resistance grounded | Very low, often below relay pickup for a single fault | Continuity-critical process systems — alarms rather than trips on the first fault |
| Ungrounded | Undefined/capacitive — a second fault becomes a phase-to-phase event | Legacy systems; generally discouraged in new design |

**Equipment grounding (safety bonding) is a separate concept from system
grounding** — equipment grounding conductors bond non-current-carrying metal
parts to provide a low-impedance fault-current return path for personnel
safety, and exist regardless of the system grounding scheme chosen. Confusing
the two is a common and dangerous error.

**Ground-fault protection sensitivity and pickup settings are a code and
equipment-specific matter** — this reference file states the grounding-scheme
framework only; the specific numeric settings and NEC ground-fault-protection
requirements need direct confirmation against the current code, per
`SKILL.md`'s caution.
