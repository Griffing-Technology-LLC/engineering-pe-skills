# PROJECT INDEX

Active files in `engineering-pe-skills`. Archived files move to `ARCHIVE_INDEX.md`.

```text
engineering-pe-skills/
├── AGENTS.md                          Authoritative AI-agent instructions
├── CLAUDE.md                          Stub → AGENTS.md
├── LICENSE                            CC BY-ND 4.0, Griffing Technology LLC
├── PROJECT_INDEX.md                   This file
├── README.md                          Overview, discipline table, install
├── REFERENCES.md                      Citation catalog with verification status
├── REVIEW_LOG.md                      Per-skill licensed-PE review record (§4.1)
├── TODO.md                            Work Breakdown Structure
├── .markdownlint-cli2.jsonc           Lint config (MD013 tuned for tables/code)
├── .github/notice.txt                 Canonical review notice (CI diff target)
├── .github/workflows/validate.yml     CI: lint + skill-invariants (notice/licence/status)
└── skills/
    ├── aeronautical-engineering/
    │   ├── SKILL.md                   Licensure standing, practice rules
    │   └── references/
    │       ├── aerodynamics.md        Section, finite wing, drag, low-Re
    │       ├── loads-and-factors.md   Limit/ultimate, V-n, gust, MS, joints
    │       ├── propulsion.md          Momentum theory, prop, EDF, matching
    │       └── weight-and-balance.md  CG envelope, neutral point, static margin
    ├── computer-engineering/
    │   ├── SKILL.md                   PE Computer Eng. module standing, rules
    │   └── references/
    │       ├── architecture-and-systems-software.md   CPI, cache, RTOS, boot
    │       ├── data-representation-and-error-control.md  Numbers, 754, CRC/ECC
    │       ├── digital-design-and-timing.md   Logic, setup/hold, CDC, ADC, DFT
    │       └── networks-security-and-quality.md  TCP/IP, NIST, V&V
    ├── control-systems-engineering/
    │   ├── SKILL.md                   ISA role, practice rules, loop workflow
    │   └── references/
    │       ├── instrumentation-and-safety.md  Sensors, valves, P&ID, SIS/SIL
    │       ├── loop-dynamics.md       FOPDT, dead time, margins, robustness
    │       └── pid-and-tuning.md      PID forms, tuning, structures, windup
    ├── electrical-engineering/
    │   ├── SKILL.md                   PE Power module standing, IEEE/NFPA
    │   └── references/
    │       ├── arc-flash-and-safety.md         IEEE 1584 framework, 70E
    │       ├── power-systems-and-per-unit.md   Per-unit, 3-phase, xfmrs
    │       └── protection-and-fault-analysis.md  Faults, OCP, coordination
    ├── electronics-engineering/
    │   ├── SKILL.md                   PE Electronics/Controls/Comms standing
    │   └── references/
    │       ├── analog-and-digital-circuits.md  Op-amps, filters, logic,
    │       │                                    ADC/DAC, IPC-2221 PCB rules
    │       └── signal-integrity-and-emc.md     Transmission lines, Z0,
    │                                            crosstalk, EMC, FCC Part 15
    ├── mechanical-engineering/
    │   ├── SKILL.md                   Three PE modules, practice rules
    │   └── references/
    │       ├── machine-elements.md    Shafts, bearings, gears, springs, joints
    │       ├── materials-and-fatigue.md  Stress, failure theories, fatigue
    │       └── thermal-and-fluids.md  Cycles, heat transfer, fluids, HVAC
    ├── naval-architecture-marine/
    │   ├── SKILL.md                   PE standing, SNAME/PNA caveat, rules
    │   └── references/
    │       ├── hydrostatics-and-stability.md  KB/BM/GM, GZ, IMO IS Code, trim
    │       └── resistance-and-propulsion.md   Fr/Re scaling, ITTC-57, powering
    ├── statics-and-dynamics/
    │   ├── SKILL.md                   FE standing, g_c discipline, determinacy
    │   └── references/
    │       ├── dynamics.md            Kinematics, kinetics, energy, momentum
    │       ├── section-properties.md  Centroids, second moments, mass MOI
    │       └── statics.md             Equilibrium, trusses, frames, friction
    └── thermodynamics/
        ├── SKILL.md                   FE standing, cross-discipline handoffs
        └── references/
            ├── fluid-mechanics.md     Statics, continuity, energy eq, Re/Fr
            ├── heat-transfer.md       Conduction, convection, radiation, HX
            └── thermodynamics.md      Laws, entropy, cycles, psychrometrics
```

## Planned

Three further discipline skills under `skills/`, per `TODO.md` §2.5,
§2.9–2.10.
