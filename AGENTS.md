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
> engineering judgment; it does not replace it. It is reference material
> provided AS-IS (see LICENSE §5), is not an engineering service, and does not
> constitute a sealed, certified, or reviewed work product for any specific
> project.

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
  byte-identical: CI diffs each skill's blockquote against
  `.github/notice.txt`, and diffs that file against this section, so a
  change to the wording is made here first and then propagated everywhere.

Rationale: these skills produce structural, electrical, thermal, control, and
fire-protection results that a reader may act on. In every discipline this
repository covers, acting on unreviewed analysis is how people get hurt. The
notice is also the boundary of what this repository claims — it informs
engineering judgment; it is not an engineering service and is not a sealed,
certified, or reviewed work product for any specific project. Wording that
touches liability is reviewed by counsel before publication (`TODO.md` §4.0).

## Reviewed-skill attestation

A skill whose technical content a licensed engineer has reviewed and accepted
(`REVIEW_LOG.md`; `metadata.review_status` beginning `REVIEWED`) carries a
**second** notice, emitted every turn immediately after the mandatory notice.
It conveys three things the general notice cannot: that a named licensed PE
has verified the content against the standards of practice; that, because it
is reviewed work, its wording is fixed (the reason for the no-derivatives
licence); and that the reviewer's acceptance covers the skill's content only —
work done with the skill still needs its own qualified-engineer sign-off, and
the reviewer accepts no liability for it.

Each reviewed `SKILL.md` carries a `## Review attestation — emit this every
time` section immediately after the mandatory-notice section, containing this
canonical wording:

> 🔏 **REVIEWED SKILL — licensed-engineer attestation.** The technical content
> of this skill has been reviewed by **Stephen Griffing, PE** (Georgia
> Professional Engineer PE046011; Arizona Control Systems Engineer 69394)
> against the applicable standards of practice, at the commit recorded in this
> skill's `metadata.review_status` and in the repository's `REVIEW_LOG.md`.
> Because it is reviewed work, **its wording may not be altered, and altered
> copies may not be redistributed** (CC BY-ND 4.0); a copy whose wording
> differs from the reviewed commit is not the reviewed skill. **This review
> attests to the skill's content only.** It is not an engineering service to
> any user, and the reviewer accepts no responsibility or liability for any
> work performed using it. **Any work that uses this skill must still be
> reviewed, accepted, and where required sealed by a qualified engineer
> responsible for that work.**

Rules for the attestation:

* **Only in reviewed skills.** A skill still marked `UNREVIEWED DRAFT` must
  not carry it; CI fails either mismatch.
* **Verbatim and byte-identical** across every reviewed skill, mirrored in
  `.github/attestation.txt`, which CI diffs against this section and against
  each reviewed skill. Change the wording here first.
* **Second, not first.** The mandatory notice still leads; the attestation
  follows it, then the analysis.
* **Same emission rules** as the mandatory notice: every turn, never
  summarised, never suppressed on request.
* Adding a reviewer, or a reviewer's licence changing, is a wording change:
  update here, in `.github/attestation.txt`, and in every reviewed skill in
  one commit, and record it in `CHANGELOG.md`.

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
  requires `license` (value `CC-BY-ND-4.0`), and under `metadata`: `author`,
  `discipline`, `ncees_alignment`, `sponsoring_society`, `version`,
  `review_status`.
* `review_status` is `"UNREVIEWED DRAFT — pending licensed PE review
  (TODO.md §4.1)"` until that skill's `TODO.md` §4.1 sub-item closes, then
  `"REVIEWED — <discipline> PE, commit <hash>, <date>"` copied from
  `REVIEW_LOG.md`. Any edit to a reviewed skill's technical content resets
  it to the draft value and bumps `version`. The installed artefact must
  carry its own review state; a WBS checkbox in this repository does not
  travel with `npx skills add`.
* `ncees_alignment` must state `NONE` with an explanation where no alignment
  exists. Never leave it implying one.
* The `description` is what determines whether the skill triggers. Write it as
  concrete tasks a user would actually type, not an abstract topic label.

## Markdown and code

* All 60 markdownlint rules enforced.
* 4-space indentation in all code regardless of language.
* Verbose commenting, in each language's idiom.
* Static analysis before any commit.
* All PRs pass CI before merge. Today CI runs markdownlint (all rules) and
  the skill-invariants job (`.github/workflows/validate.yml`: notice
  byte-identical to `.github/notice.txt`, `ncees_alignment`, `license`,
  `review_status`). Link validation and secret scanning are **not yet
  wired** — `TODO.md` §1.8.

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
