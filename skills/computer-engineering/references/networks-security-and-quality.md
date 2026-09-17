# Networks, Cybersecurity, Software Design, and Quality Processes

Reference file for the `computer-engineering` skill, covering NCEES knowledge
areas 7 (computer networks and cybersecurity: network design and testing,
system cybersecurity), 4 (application development: software design, quality
assurance, software fundamentals, development tools, machine learning/AI),
and 8 (quality processes: requirements, test program development and
process reviews, validation and verification) [REF-NCEES-004]. Network
protocols are cited to the IETF RFC Editor [REF-IETF-001..003] and IEEE
802.3 [REF-IEEE-003]; security engineering to NIST [REF-NIST-001..005];
verification and validation to IEEE 1012-2024 [REF-IEEE-005].

## 1. Network layering

RFC 1122 [REF-IETF-002] §1.1.3 defines the Internet protocol suite in four
layers — **Application, Transport, Internet, Link** — and that model, not
the seven-layer teaching model, is the one the protocols are specified
against. Map any design to it:

| Layer (RFC 1122) | Governs | Cited source |
| --- | --- | --- |
| Link | Framing, MAC, physical medium | IEEE 802.3-2022 Ethernet [REF-IEEE-003] |
| Internet | Addressing, routing, fragmentation | RFC 791 IP [REF-IETF-001] |
| Transport | End-to-end delivery, ports | RFC 9293 TCP [REF-IETF-003]; UDP |
| Application | Protocol payloads | Per application |

**IP** [REF-IETF-001] provides connectionless, best-effort datagram
delivery with a header checksum covering the header only, a time-to-live
bound on datagram lifetime, and fragmentation when a datagram exceeds a
link's maximum transmission unit. Payload integrity is the transport or
application layer's responsibility.

**TCP** [REF-IETF-003] (RFC 9293 obsoletes RFC 793 and consolidates its
updates) provides reliable, ordered byte streams. Connection establishment
is the **three-way handshake** (RFC 9293 §3.5), whose stated principal
purpose is to prevent old duplicate connection initiations from causing
confusion; sequence numbers (§3.4) provide ordering and loss detection.
TCP's retransmission and congestion behaviour make its latency
**unbounded** — a control loop that needs a deadline does not run over
TCP without an explicit timeout design.

**Ethernet** [REF-IEEE-003] specifies "selected speeds of operation from
1 Mb/s to 400 Gb/s using a common media access control (MAC)
specification," with both half-duplex CSMA/CD and full-duplex operation.
Switched full-duplex Ethernet has no collisions, but store-and-forward
switching, queueing, and best-effort delivery still make plain Ethernet
non-deterministic; deterministic variants are separate specifications not
catalogued here and must be added to `REFERENCES.md` before being cited.

## 2. Network design and testing

State, for every link and network: **required throughput** (bit/s, with
the prefix convention — `SKILL.md` rule 3), **latency bound and jitter
tolerance**, **node count and topology**, **cable length** `ft (m)` and
medium, **availability target**, and **failure behaviour** (what a node
does when the network is absent). Throughput is then checked against the
raw rate *after* framing, protocol, and encoding overhead — a "100 Mb/s"
link carries materially less application payload.

**Addressing and segmentation:** subnet sizing from host count with growth
margin; VLAN or physical segmentation to separate safety, control, and
business traffic (the OT-security segmentation model is in §4).

**Testing:** functional (connectivity, addressing), performance
(throughput and latency under load, with the load generator and
measurement point named), robustness (link loss, duplicate addresses,
storm conditions), and security (§4). A network is not "tested" by
pinging it once.

## 3. Software design and fundamentals

* **Requirements first** (§6): a design is checked against written,
  numbered requirements; an unnumbered requirement cannot be traced to a
  test.
* **Structured design and state machines:** control-flow constructs
  (sequence, selection, iteration) and explicit state-transition diagrams
  for anything with modes. An embedded controller's mode logic is an FSM
  and gets the same treatment as a hardware FSM
  (`digital-design-and-timing.md` §2): defined reset state, defined
  handling of every event in every state, no undefined transitions.
* **Data structures and algorithms:** choose by the operation the system
  performs most and by **worst-case** complexity for anything on a
  deadline path — an average-case $O(1)$ hash table with an $O(n)$
  worst case is not real-time. Dynamic allocation in a real-time task
  is stated and justified or absent.
* **Handshaking and synchronisation** between tasks, cores, or devices
  follows the same rules as hardware clock-domain crossing: a named
  protocol (semaphore, message queue, lock-free ring with a single
  producer and consumer), with the ordering guarantees the hardware and
  compiler actually provide (memory barriers where needed), not assumed.
* **Fault tolerance and safety-critical software:** defensive checks on
  every external input; fail-safe defaults; watchdog service only from a
  point that proves the main loop is healthy, never from a timer
  interrupt. Name the failure mode each measure addresses (`SKILL.md`
  rule 8).
* **Model-based systems engineering** ties requirements, architecture,
  and behaviour models together so that changes propagate; its value is
  traceability, and it is only as good as the model's verification.
* **Development tools:** version control for everything including build
  scripts and toolchain versions; static analysis run before review with
  findings dispositioned, not silenced; debuggers, trace, and emulators
  used with the understanding that a debugger halting the core changes
  timing — trace is the tool for timing faults.
* **Machine learning / AI components** are non-deterministic by
  construction from the verifier's point of view; they are bounded by
  conventional monitors and never given sole authority over a
  safety-related output without an explicit, reviewed argument.

## 4. System cybersecurity

**Threat model before mechanisms** (`SKILL.md` rule 7): assets, adversary
capability (network-adjacent, physical access, supply chain, insider),
attack surface, and the trust anchor. Then select and cite mechanisms.

**Governing NIST publications catalogued in this repository:**

| Source | Applies to |
| --- | --- |
| NIST CSF 2.0 [REF-NIST-004] | Organisational cybersecurity outcomes, organised in six Functions: **Govern, Identify, Protect, Detect, Respond, Recover** |
| NIST SP 800-160 Vol. 1 Rev. 1 [REF-NIST-003] | Systems security engineering — building trustworthiness into the system-engineering process |
| NIST SP 800-82 Rev. 3 [REF-NIST-001] | Operational technology security — systems that "interact with the physical environment"; topologies, threats, and countermeasures |
| NIST SP 800-193 [REF-NIST-002] | Platform firmware resiliency — protection, detection, recovery |
| FIPS 140-3 [REF-NIST-005] | Security requirements for cryptographic modules; four qualitative security levels |

**Practice points for embedded and control products:**

* **OT is not IT.** SP 800-82 [REF-NIST-001] exists because OT systems
  carry "performance, reliability, and safety requirements" that an IT
  control (patch now, reboot, block on anomaly) can violate. Availability
  and safety of the physical process rank above confidentiality; state the
  ranking for the system in hand.
* **Segmentation** between safety, control, and general networks, with
  explicit, minimal conduits; a flat network that reaches an actuator is
  a finding, not a topology.
* **Root of trust and secure boot** per SP 800-193's protect/detect/recover
  framing [REF-NIST-002]; hardware-anchored keys; signed and
  rollback-protected updates (`architecture-and-systems-software.md` §8).
* **Cryptography:** algorithm and key-length approvals are NIST's to
  state, not this skill's. Cite the current NIST publication for the
  algorithm in question — FIPS 140-3 [REF-NIST-005] governs module
  requirements; the algorithm-specific FIPS/SP documents must be added to
  `REFERENCES.md` before an algorithm is recommended by name. **Never
  design a cipher or protocol; never invent a key length.**
* **Authentication of every command path** into a device that can move
  something, including debug and maintenance interfaces; debug ports
  locked or authenticated in production.
* **Side channels** — timing, power, compressed length
  (`data-representation-and-error-control.md` §5) — are in scope when the
  adversary has physical or timing access.
* **Security operations:** logging that survives reset, a defined
  vulnerability-response process, and a software bill of materials so a
  disclosed component vulnerability can be traced to affected units.

## 5. Quality assurance

* **Reviews and inspections** with recorded findings and dispositions;
  a review that produces no record did not occur.
* **Testing** at unit, integration, and system level; **coverage** stated
  against a named criterion (statement, branch, condition/decision) and
  reported as a number. Coverage proves what was exercised, not what is
  correct.
* **Assertions** encode design assumptions in the code so that violation
  is detected at the earliest point; production builds state whether
  assertions remain active and what a failed assertion does.
* **Root-cause analysis** for every escaped defect: the causal chain to
  the process gap, and a change to the process, not just the code.
* **Safety and security** are reviewed as first-class quality attributes,
  with their own failure-mode and threat analyses feeding the test plan.

## 6. Requirements, verification, and validation

**IEEE 1012-2024** [REF-IEEE-005] defines V&V processes "used to determine
whether the development products of a given activity conform to the
requirements of that activity and whether the product satisfies its
intended use and user needs," specified "for different integrity levels,"
covering systems, software (including firmware and microcode), and
hardware. Apply it as follows:

1. **Assign the integrity level** from the consequence of failure, with
   the rationale written down (`SKILL.md` rule 8).
2. **Requirements** — numbered, testable, traceable to a source, with
   physical quantities imperial-primary with metric and every "shall"
   verifiable by a named method (test, analysis, inspection,
   demonstration).
3. **Verification** — the product conforms to its requirements at each
   stage ("built right"). **Validation** — the product satisfies its
   intended use ("built the right thing"). Both, with evidence, and the
   evidence retained.
4. **Test program** — a plan that states pass/fail criteria before
   execution; test cases traced to requirements; regression on every
   change; independence of the verifier proportionate to the integrity
   level.
5. **Process reviews** at defined milestones with entry and exit criteria;
   a milestone passed without its criteria met is recorded as a waiver
   with an owner, not as a pass.

Where a sector-specific standard governs (avionics, automotive, medical,
industrial functional safety), it is added to `REFERENCES.md` with a
validated URL before being cited — none is asserted here from memory.
