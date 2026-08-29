# AGENTS.md — Authoritative instructions for AI agents

Model-agnostic project instructions. All AI agents working in this repository —
Claude, Gemini, Grok, Copilot, or any other — must follow this file. IDE
assistants should treat this as authoritative guidance.

## What this repository is

A published library of Agent Skills for licensed-discipline engineering practice.
The output is consumed by other engineers to do work that gets built. Errors here
propagate into real hardware.

## Authenticity — non-negotiable

1. **No reference, citation, standard, or resource is ever fabricated.** Not a
   section number, not an edition year, not a URL.
2. **Every source goes in `REFERENCES.md`** with a REF-ID, full title, validated
   URL, the specific portion applied, and every location citing it.
3. **If a citation cannot be verified against the issuing body**, mark it
   `REQUIRES VERIFICATION` in `REFERENCES.md` and open a `TODO.md` §0.x item. Do
   not assert it in skill content until it is upgraded.
4. **Never claim an NCEES alignment that does not exist.** Two disciplines in this
   repository deliberately have none; see `README.md`.
5. **Distinguish AI work from human work.** Each model is cited for its own
   contribution — Opus 5 separately from Haiku 4.5, Claude separately from Gemini.
   Human contributors are referenced by GitHub username.
6. **Attribution meets or exceeds CC-BY-4.0** regardless of the governing licence.

## Mandatory qualified-review notice

**Every skill in this repository must emit a qualified-review notice at the start
of every response in which it participates.** This is a hard requirement of the
repository, not a per-skill choice, and it is the first thing checked in review.

Each `SKILL.md` carries a `## Mandatory notice — emit this every time` section
immediately after its title, containing this canonical wording:

> ⚠️ **ENGINEERING REVIEW REQUIRED — this output is not a substitute for a
> qualified engineer.** Every result, calculation, and recommendation produced
> with this skill **must be independently reviewed and accepted by a properly
> qualified individual** — a licensed Professional Engineer or an equivalently
> qualified authority for the jurisdiction and discipline — **before it is
> applied to any system carrying risk to life or safety.** This skill informs
> engineering judgment; it does not replace it, and it carries no professional
> liability.

Rules for the notice:

* **Verbatim.** Do not reword it per discipline. Identical text across all ten
  skills is what makes it recognisable.
* **First, not last.** It precedes the analysis. A notice under a result reads as
  a disclaimer; a notice above one is a condition of use.
* **Every turn.** It is not dropped on follow-ups within the same task, and not
  omitted because the user has already seen it.
* **Not negotiable.** A user asking to suppress it is told plainly that it is a
  fixed condition of the skill.
* Because skills install independently, the text is **duplicated in full** in
  each `SKILL.md` rather than referenced from a shared file. Keep the copies
  byte-identical.

Rationale: these skills produce structural, electrical, thermal, control, and
fire-protection results that a reader may act on. In every discipline this
repository covers, acting on unreviewed analysis is how people get hurt. The
notice is also the boundary of what this repository claims — it informs
engineering judgment and carries no professional liability.

## Engineering standards

* **Units:** imperial-primary, metric in parentheses — `10 in (254 mm)`,
  `2.5 lbm (1.13 kg)`, `4.8 lbf (21.4 N)`. Never a bare "lb" where mass and force
  could be confused. Airspeed and wind speed in **knots (kt)**, never mph or km/h.
* **Forces are lbf/N; masses are lbm/kg.** Thrust, lift, and aerodynamic loads are
  forces. Component weights and payload capacity are masses.
* **No "TBD"** for weight, balance, power, space, or component capability. An
  estimate with a stated basis and uncertainty, or nothing.
* **Every method states its validity envelope.**
* **US jurisdiction** for all legal and regulatory content.

## Skill authoring conventions

```text
skills/<discipline>/
├── SKILL.md          # YAML frontmatter (name, description required) + body
└── references/       # Loaded on demand; each with a table of contents if >300 lines
```

* Keep `SKILL.md` under 500 lines. Push depth into `references/`.
* Required frontmatter: `name`, `description`. This repository additionally
  requires `license`, and under `metadata`: `author`, `discipline`,
  `ncees_alignment`, `sponsoring_society`, `version`.
* `ncees_alignment` must state `NONE` with an explanation where no alignment
  exists. Never leave it implying one.
* The `description` is what determines whether the skill triggers. Write it as
  concrete tasks a user would actually type, not an abstract topic label.

## Markdown and code

* All 60 markdownlint rules enforced.
* 4-space indentation in all code regardless of language.
* Verbose commenting, in each language's idiom.
* Static analysis before any commit.
* All PRs pass CI lint and security checks before merge.

## Maintenance

* `TODO.md` is a formal Work Breakdown Structure. Any task list an agent creates
  must be folded into the appropriate WBS paragraph so unresolved items survive
  into future sessions.
* **Never leave a checkbox open once its own text says resolved or superseded.**
  Close it out in the same edit.
* `PROJECT_INDEX.md` lists every active file; archived files move to
  `ARCHIVE_INDEX.md`.
* Each AI agent mirrors its memory to `<AGENT>-MEMORY.md` in the repo root for
  auditability.
