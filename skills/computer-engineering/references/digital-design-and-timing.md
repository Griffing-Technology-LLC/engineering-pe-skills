# Digital Design, Timing, and Interfacing

Reference file for the `computer-engineering` skill, covering NCEES knowledge
areas 5 (digital devices: memory devices, standard modular devices, ASICs and
programmable devices, combinational and sequential circuits, synchronous and
asynchronous design, DFT, system design) and 6 (digital electronics:
solid-state devices, operating parameters, data conversion, circuit
implementation and signalling standards, timing design) [REF-NCEES-004].
Boundary scan is cited to IEEE 1149.1-2013 [REF-IEEE-004]. Transistor-level
device physics, analog signal conditioning, PCB signal integrity, and EMC
are the province of `electronics-engineering` (planned) — this file stops
at the logic-level and interface-level parameters a computer engineer must
own.

## 1. Combinational logic

* **Specification → truth table → minimised expression → implementation.**
  Minimisation (Boolean algebra, Karnaugh maps up to ~5 variables,
  algorithmic methods beyond) reduces gate count but can *introduce*
  hazards (§5); a redundant term is sometimes the correct design.
* **Standard modular devices:** multiplexers (select one of $2^n$ inputs
  with $n$ select lines), demultiplexers/decoders ($n$-to-$2^n$), encoders
  and priority encoders, adders (ripple-carry $O(n)$ delay; carry-lookahead
  trades area for $O(\log n)$), comparators, ALUs and FPUs. Report the
  worst-case propagation path, not the typical one.
* **Tri-state outputs** allow a shared bus; two enabled drivers on one net
  is a **bus contention** fault that can be destructive. Every tri-state
  bus needs a proven-exclusive enable scheme and a defined state when no
  driver is enabled (pull resistor or bus-keeper) — a floating CMOS input
  draws crossover current and reads as noise.

## 2. Sequential logic and finite-state machines

* **Latches** are level-sensitive; **flip-flops** are edge-triggered.
  Synchronous design uses edge-triggered flip-flops with a common clock;
  latches in a synchronous datapath are a source of timing ambiguity and
  should be justified explicitly.
* **FSM design:** state diagram → state table → state encoding (binary,
  Gray, one-hot — one-hot costs flip-flops, saves decode logic, and is the
  common FPGA choice) → next-state and output logic. **Moore** outputs
  depend on state only (glitch-free, one cycle later); **Mealy** outputs
  depend on state and input (faster, can glitch with the input).
* **Every FSM has a defined reset state and a defined response to every
  unused state encoding** — an undefined state reached by a single-event
  upset or a glitch must recover, not lock up. State what the recovery is.
* **Asynchronous sequential circuits** (no common clock) are analysed by
  flow tables and are subject to races and essential hazards; they are
  used deliberately only where a clock cannot be tolerated, and each
  instance needs its own race-free state assignment.

## 3. Synchronous timing

For a path from flip-flop A to flip-flop B through combinational logic of
delay $t_{logic}$, with clock period $T_{clk}$ and clock skew $t_{skew}$
(positive when B's clock arrives later than A's):

Setup (max-delay) constraint:

$$t_{cq,max} + t_{logic,max} + t_{setup} \leq T_{clk} + t_{skew} - t_{jitter}$$

Hold (min-delay) constraint:

$$t_{cq,min} + t_{logic,min} \geq t_{hold} + t_{skew}$$

$t_{cq}$ is clock-to-output delay. A setup violation is fixed by slowing the
clock or shortening the path; **a hold violation cannot be fixed by
changing the clock frequency** and must be fixed by adding delay or
reducing skew. Both constraints are checked at the worst-case
process/voltage/temperature corner for that constraint — fast corner for
hold, slow corner for setup — and the corner is reported with the result
(`SKILL.md` rule 4).

**Clock distribution:** skew is the static arrival-time difference; jitter
is the cycle-to-cycle variation. A clock tree or a PLL-generated clock has
datasheet-specified values for both — use them, do not assume zero.
**Gated clocks** save power and create skew and glitch risk; a glitch on a
clock net is a functional failure, so gating cells must be glitch-free by
construction.

## 4. Metastability and clock-domain crossing

A flip-flop whose input changes within its setup/hold window can enter a
metastable state and resolve to a valid level after an unbounded delay.
The mean time between failures of a single synchronising flip-flop is
modelled as

$$MTBF = \frac{e^{t_r / \tau}}{T_0 \cdot f_{clk} \cdot f_{data}}$$

where $t_r$ is the resolution time allowed after the capturing edge,
$\tau$ and $T_0$ are device-specific constants from the vendor's
characterisation, $f_{clk}$ is the receiving clock, and $f_{data}$ the rate
of asynchronous input transitions. **$\tau$ and $T_0$ come only from the
device vendor's metastability data** — never from a generic value. The
exponential dependence on $t_r$ is why a two-flip-flop synchroniser
(giving a full cycle of resolution time) is the standard minimum for a
single-bit crossing.

**Multi-bit crossings cannot be synchronised bit by bit** — the bits may
resolve on different cycles. Use a handshake, a Gray-coded pointer (only
one bit changes per increment), or an asynchronous FIFO with Gray-coded
read/write pointers. Every clock-domain crossing in a design is
enumerated and its scheme named; an unlisted crossing is a latent fault.

**Reset:** asynchronous assertion, synchronous de-assertion, per clock
domain, so that release does not itself cause metastability.

## 5. Hazards, races, and glitches

* **Static hazard:** an output that should stay constant momentarily
  changes because two paths to it have different delays. Removed in
  two-level logic by adding the redundant consensus term that covers the
  transition.
* **Dynamic hazard:** an output that should change once changes several
  times; arises in multi-level logic from static hazards on internal
  nodes.
* **Race:** two or more signals changing at nearly the same time such that
  the outcome depends on which wins. Critical if the final state differs.
* In a fully synchronous design, hazards on combinational outputs are
  harmless **provided** they settle before the next active clock edge and
  never drive a clock, an asynchronous set/reset, or an output that leaves
  the chip. Hazards on any of those three are functional failures.

## 6. Operating parameters and signalling

* **Logic levels:** $V_{IH}$, $V_{IL}$, $V_{OH}$, $V_{OL}$ from the datasheet
  at the operating supply; noise margin high is $V_{OH,min} - V_{IH,min}$
  and low is $V_{IL,max} - V_{OL,max}$. Mixed 3.3 V / 5 V / 1.8 V logic
  requires a level check on **every** cross-family net and a stated
  translation method; "5 V tolerant" is a datasheet attribute, not a
  family property.
* **Fan-out** is limited by DC input current at the far end **and** by the
  total load capacitance's effect on edge rate; the second limit usually
  binds in CMOS. Quote the driven capacitance and the resulting edge time.
* **Thermal:** junction temperature $T_J = T_A + P \cdot \theta_{JA}$,
  computed in °C because $\theta_{JA}$ is tabulated in °C/W, then reported
  °F (°C); $\theta_{JA}$ comes from the datasheet for the actual
  board/airflow condition — the datasheet value assumes a specific test
  board and can be badly optimistic in a sealed enclosure. Hand off
  enclosure and heat-sink design to `mechanical-engineering`.
* **Signalling standards:** single-ended CMOS/TTL levels for on-board,
  short nets; **LVDS** (low-voltage differential) for high-speed
  point-to-point links; **CAN** (differential, multi-drop, arbitrated,
  with dominant/recessive bus states and a bit-rate-versus-length
  trade-off set by propagation delay across the bus); **RS-485** for
  multi-drop half- or full-duplex serial; **Ethernet** [REF-IEEE-003] for
  networked links. Termination, common-mode range, and cable length
  `ft (m)` are stated for every differential link; the transceiver's
  datasheet and the bus standard govern, and neither is quoted from memory.
* **Current-mode logic** and other high-speed families trade static power
  for edge rate; their use is a signal-integrity decision handed off to
  `electronics-engineering`.

## 7. Data conversion

* **Sampling:** the sample rate must exceed twice the highest frequency
  *present at the ADC input* — not twice the signal of interest — or an
  anti-alias filter must remove the excess. State the filter's corner and
  order alongside the sample rate.
* **Resolution vs. accuracy:** an $n$-bit converter has a quantisation step
  of $V_{FS}/2^n$; its *accuracy* is set by offset, gain, INL/DNL,
  reference stability, and noise, and is typically several LSB worse than
  the resolution. Effective number of bits (ENOB) is the honest figure.
* **Settling and acquisition:** a multiplexed ADC needs its sample
  capacitor charged within the acquisition window through the source
  impedance — high-impedance sensors need a buffer or a longer window.
  This is an interface parameter the computer engineer owns; the buffer
  circuit is handed off.
* **DAC and actuators:** output update rate, glitch energy, and
  reconstruction filtering; PWM as a DAC substitute has a ripple/bandwidth
  trade set by the PWM frequency and the output filter.
* **Sensors and indicators** are specified by their electrical interface,
  update rate, latency, and resolution — the same four numbers the
  software will need — and physical ranges are quoted imperial-primary
  where the quantity is physical (pressure psi (kPa), temperature °F (°C)).

## 8. Programmable devices and memory

* **PLD/CPLD** (small, deterministic timing), **FPGA** (large, LUT-based,
  timing from place-and-route — **re-run timing analysis after every
  change**), **ASIC** (fixed after fabrication; NRE cost justified only at
  volume or for performance/power unreachable otherwise). **PLCs** are
  industrial controllers programmed in the standardised PLC languages
  (ladder, function block, structured text — the governing standard is not
  catalogued in `REFERENCES.md` and is not cited by number here); their
  scan-cycle time is the timing parameter that matters and is handed to
  `control-systems-engineering` for loop design.
* **Memory devices** as logic elements: ROM/LUT implements any
  combinational function of its address inputs; register files and FIFOs
  are the standard sequential building blocks. Dual-port and asynchronous
  FIFOs are the clock-domain-crossing primitives of §4.

## 9. Design for testability

* **Boundary scan / JTAG** per IEEE 1149.1 [REF-IEEE-004] defines a test
  access port and a boundary-scan register so that board-level
  interconnect can be tested through the chip's pins without physical
  probes. IEEE SA lists the 2013 edition's status as *Inactive-Reserved*
  as of 2026-09-17 — it remains the edition implemented in current
  silicon; confirm the status before citing it as "active."
* **Scan chains** convert internal flip-flops into a shift register in test
  mode, giving controllability and observability of internal state.
  **Built-in self-test (BIST)** generates patterns and compresses responses
  on-chip. Each costs area and adds constraints on the functional design
  (no uncontrolled asynchronous set/reset, no gated clocks without test
  bypass) that must be planned in, not retrofitted.
* **Fault models:** stuck-at is the baseline; delay and bridging faults
  need their own patterns. Report **fault coverage** as a percentage
  against a named fault model, never as "tested."
* **Production test** of an embedded product includes a boot-and-report
  self-test whose pass criteria are written down before the first unit is
  built; state the acceptance limits with the same rigor as the design
  limits.
