# Computer Architecture and Systems Software

Reference file for the `computer-engineering` skill, covering NCEES knowledge
areas 2 (computer architecture: organisation and processor design, embedded
systems, system architecture, memory systems, system performance) and 3
(systems software: operating systems, RTOS, virtualisation, interrupts and
exceptions, firmware) [REF-NCEES-004]. Speed-up is attributed to Amdahl
(1967) [REF-PAPER-001] and fixed-priority schedulability to Liu and Layland
(1973) [REF-PAPER-002]; both full texts are paywall-blocked and the specific
results are marked `REQUIRES VERIFICATION` against the paper text
(`TODO.md` §0.9). Boot firmware is cited to the UEFI Specification
[REF-UEFI-001] and firmware resiliency to NIST SP 800-193 [REF-NIST-002].

## 1. Performance metrics

**Execution time is the only metric that cannot mislead.** For a program of
$N$ instructions on a processor at clock period $T_{clk}$ with average cycles
per instruction $CPI$:

$$t_{exec} = N \cdot CPI \cdot T_{clk}$$

$CPI$ is a weighted average over the instruction mix actually executed,
including stall cycles from cache misses, branch mispredictions, and
pipeline hazards — quote the mix and the stall assumptions with the number.
A "1.0 CPI" from a marketing sheet is a peak, not a workload value.

**Speed-up** from improving a fraction $f$ of the workload by a factor $k$:

$$S = \frac{1}{(1-f) + f/k}$$

with the limit $S \to 1/(1-f)$ as $k \to \infty$. This is the result
generally called Amdahl's law and attributed to Amdahl (1967)
[REF-PAPER-001]; the paper's text was not read here (`TODO.md` §0.9). Its
practical consequence stands regardless of attribution: **the unimproved
fraction bounds the gain**, so measure $f$ before buying $k$.

**Benchmarks** measure the benchmark. Report the benchmark name, version,
compiler flags, and the input set alongside any figure; a result without
them cannot be reproduced and should not drive a component decision.

**Power and energy:** dynamic switching power scales as
$P_{dyn} \propto C \cdot V^2 \cdot f$ with capacitance $C$, supply $V$, and
switching frequency $f$; static (leakage) power does not fall with $f$.
Energy per task, not power, is what a battery budget needs — a faster core
that sleeps sooner can cost less energy than a slow one that never idles.
State the duty cycle and the sleep-state current for any battery-life
estimate, with physical quantities imperial-primary where they arise
(enclosure volume in³ (cm³), board temperature °F (°C)).

## 2. Processor organisation

* **Datapath and control:** register file, ALU, and the control unit
  (hardwired or microprogrammed). Instruction-set architecture (ISA) is the
  contract; microarchitecture is one implementation of it.
* **Pipelining** raises throughput, not single-instruction latency. Hazards:
  *structural* (resource conflict), *data* (RAW/WAR/WAW dependences; RAW is
  the true dependence, the others are name conflicts removed by renaming),
  and *control* (branches). Forwarding, stalls, prediction, and speculation
  are the standard mitigations; each adds complexity that must be
  accounted for in the CPI.
* **Interrupt interface:** vectored versus polled, maskable versus
  non-maskable, priority and nesting, and the latency from assertion to the
  first instruction of the handler. **Interrupt latency is a worst-case
  figure** — it includes the longest critical section during which
  interrupts are disabled, not just the hardware entry time. Quote it at
  the worst corner (`SKILL.md` rule 4).
* **Special-purpose processors** (DSP, GPU, accelerators, security
  co-processors) shift the CPI/energy trade; treat their interface bandwidth
  and synchronisation cost as part of the workload, not as free.

## 3. Memory hierarchy

**Average memory access time** for a single cache level:

$$AMAT = t_{hit} + m \cdot t_{miss\ penalty}$$

where $m$ is the miss rate. Extend level by level for multi-level caches.
Miss classes — compulsory, capacity, conflict (and coherence in
multiprocessors) — point to different remedies (prefetch, larger cache,
higher associativity, protocol tuning respectively).

**Cache organisation** is stated by capacity, block (line) size,
associativity, write policy (write-through or write-back), and allocate
policy. A direct-mapped cache is 1-way associative; fully associative is
$N$-way for $N$ lines. Address decomposition is tag | index | offset with
the index width $\log_2(\text{sets})$ and offset width
$\log_2(\text{block bytes})$ — **check the arithmetic against the declared
prefix convention** (`SKILL.md` rule 3).

**Virtual memory:** page tables map virtual to physical pages; the TLB
caches translations. A TLB miss costs a page walk; a page fault costs a
disk or flash access and is orders of magnitude slower — a real-time task
must never take one, which is why RTOS designs lock or avoid paged memory.

**Storage:** RAID levels trade capacity, read/write performance, and fault
tolerance; state the level, the number of drives, and which single or
double failures it survives. NAS presents files over a network; SAN
presents blocks. Neither replaces a backup — a redundant array protects
against drive failure, not against deletion or corruption written to all
members.

**Memory devices for embedded work:** SRAM (fast, volatile, no refresh),
DRAM (dense, volatile, refresh required), flash (non-volatile; erase before
write, finite erase cycles, block-granular erase). State the flash
endurance and the wear-levelling scheme for anything logged to flash in
service — a write-every-second log without wear levelling has a
calculable, and usually short, life.

## 4. Embedded systems and interfacing

* **GPIO, timers, PWM, ADC/DAC, and serial peripherals** (UART, SPI, I²C,
  CAN, USB, Ethernet) are the microcontroller's contract with the world;
  each has a datasheet-specified electrical and timing envelope. Signal
  conditioning between a sensor and an ADC input — level shifting,
  anti-alias filtering, protection — is an analog design task: hand off
  to `electronics-engineering` (planned) for the circuit, but **own the
  sampling rate, resolution, and settling-time requirement** here.
* **Bus selection** states the required data rate, node count, cable
  length `ft (m)`, noise environment, and whether determinism or
  arbitration is needed. Differential signalling (CAN, RS-485, LVDS,
  Ethernet) is the default over any distance beyond a board edge; see
  `digital-design-and-timing.md` §6.
* **Fault tolerance and recovery:** independent watchdog with a stated
  timeout and a stated safe action on expiry; brown-out detection with a
  stated threshold; a reset-cause register read at every boot so that a
  reset loop is logged rather than hidden. Name the failure mode each
  mechanism covers (`SKILL.md` rule 8).
* **Power provisioning:** every rail budgeted with margin — peak current
  (radio transmit, motor start, flash erase) not just average — and the
  brown-out threshold set above the minimum operating voltage of every
  device on the rail. No "TBD" (`SKILL.md` rule 9).

## 5. Operating systems and real-time scheduling

**General-purpose OS** schedulers optimise throughput and fairness; they
give no deadline guarantee. A **real-time operating system** provides
bounded scheduling latency, priority-based preemption, and deterministic
primitives; "real time" is a bound, not a speed (`SKILL.md` rule 5).

**Fixed-priority preemptive scheduling with rate-monotonic priority
assignment** (shorter period → higher priority): a set of $n$ independent
periodic tasks with periods $T_i$ and worst-case execution times $C_i$ is
schedulable if

$$U = \sum_{i=1}^{n} \frac{C_i}{T_i} \leq n\left(2^{1/n} - 1\right)$$

This utilisation bound decreases toward $\ln 2 \approx 0.693$ as $n$ grows.
It is a **sufficient** condition — a task set that exceeds the bound may
still be schedulable, and a response-time analysis (iterating each task's
worst-case response including all higher-priority interference) is the
exact test. The bound is the result generally attributed to Liu and Layland
(1973) [REF-PAPER-002]; the paper's text was not read here (`TODO.md`
§0.9). **Earliest-deadline-first** scheduling is schedulable for
independent periodic tasks up to $U \leq 1$ but degrades less gracefully
under overload.

**Assumptions to state with any schedulability claim:** independent tasks
(no shared resources) or the resource-sharing protocol used; deadlines
equal to periods or otherwise; context-switch and interrupt overhead
included in $C_i$ or accounted separately; single core. Priority inversion
through a shared resource can make a nominally schedulable set miss
deadlines — priority inheritance or ceiling protocols bound it; unbounded
inversion is a defect.

**Synchronisation:** mutexes, semaphores, and message queues; deadlock
requires mutual exclusion, hold-and-wait, no preemption, and circular wait
together — break any one by design (typically a global lock order). Handler
code that blocks is a defect in any interrupt context.

## 6. Interrupts and exceptions

Distinguish *interrupts* (asynchronous, from hardware), *exceptions*
(synchronous, from the executing instruction — faults, traps, aborts), and
*software interrupts / system calls*. For each handler state: its priority
and whether it can be preempted; its worst-case duration; what it must
never do (block, allocate, call non-reentrant code); and how it hands work
to task context (flag, queue, deferred procedure). The **longest
interrupts-disabled region anywhere in the system** bounds the latency of
the highest-priority interrupt — find it and quote it.

## 7. Virtualisation and containers

Hypervisors (type 1 bare-metal, type 2 hosted) virtualise hardware;
containers share a kernel and isolate at the process level. On
resource-constrained targets the cost is memory footprint, scheduling
jitter, and a larger trusted computing base. A mixed-criticality design
that co-hosts a safety function with a general-purpose workload must show
**temporal and spatial isolation** — bounded interference in CPU time and
in memory/bus bandwidth — not just logical separation.

## 8. Firmware and boot

* **UEFI** [REF-UEFI-001] defines the interface between platform firmware
  and the operating system loader on general-purpose platforms; the current
  specification version is listed on the UEFI Forum's specifications page.
  Legacy BIOS is the pre-UEFI interface. Most microcontroller-class targets
  use neither: they boot from a vendor ROM into a first-stage loader.
* **Firmware resiliency** per NIST SP 800-193 [REF-NIST-002] is organised
  around three principles — **protection** against unauthorised change,
  **detection** of unauthorised change, and **recovery** to a known-good
  state — applied to every mutable firmware component on the platform.
  Apply the same three questions to an embedded product's boot chain:
  what protects the bootloader, what detects a corrupted or unsigned image,
  and how the device recovers from a failed update.
* **Secure boot chain:** an immutable root of trust verifies the next stage
  before executing it; each stage verifies the next. State the trust anchor
  (ROM, fused key hash, hardware secure element), the signature algorithm,
  and the rollback-protection mechanism. The cryptographic details are a
  security-engineering task governed by NIST publications — see
  `networks-security-and-quality.md` §4 and `SKILL.md` rule 7.
* **Field update:** dual-bank or A/B images with a validated fallback;
  power loss at any byte of the write must leave a bootable device. Test
  it by pulling power during an update, not by inspection.
