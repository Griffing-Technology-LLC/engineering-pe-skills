# Changelog

All notable changes to the skills in this repository. Format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versions follow
[Semantic Versioning](https://semver.org/spec/v2.0.0.html) and are the
`metadata.version` carried in each `SKILL.md`. Entries are written for the
engineers and agents who install these skills, not for maintainers.

## [Unreleased]

### Added

* **Reviewed-skill attestation.** Skills a licensed engineer has reviewed now
  emit a second notice every turn, after the general one, in the reviewer's
  name: content verified against the standards of practice; wording fixed
  (CC BY-ND); reviewer's acceptance covers the skill's content only and
  carries no liability for work done with it; such work still needs its own
  qualified-engineer sign-off. First carried by `control-systems-engineering`.
  Canonical text in `AGENTS.md`, CI-enforced byte-identical.

## [0.2.0] — 2026-09-19

### Changed

* **Licence: MIT → CC BY-ND 4.0.** Skills may be used and redistributed
  unmodified; modified versions may not be shared. Revisions through commit
  `5300e0e` remain available under MIT. See `README.md` § Licence for what
  the licence does and does not do, including that analyses you produce with
  the skills are your own work.
* **Qualified-review notice reworded.** "…and it carries no professional
  liability" is replaced by a statement of what the material *is*: AS-IS
  reference material (LICENSE §5), not an engineering service, not a sealed,
  certified, or reviewed work product. All nine skills carry the new text
  byte-identically.
* **Review status is now in the installed file.** Every `SKILL.md` declares
  `metadata.review_status`; all nine are `UNREVIEWED DRAFT` pending licensed
  PE review (`TODO.md` §4.1, per discipline, recorded in `REVIEW_LOG.md`).
* README no longer states that PE review happens before release; it is a gate
  for 1.0. As of 2026-09-19 `control-systems-engineering` is the one skill
  whose technical content has been accepted by a licensed engineer (PE
  Control Systems; see `REVIEW_LOG.md`); its `review_status` is `REVIEWED`.

### Fixed

* `REF-IEEE-002` had been assigned to both IEEE/ANSI C63.4 and IEEE 754-2019.
  754 is now `REF-IEEE-006` (`computer-engineering`); no content changed.
* README status table omitted `electronics-engineering`.

### Security

* `SECURITY.md` now covers engineering-error reports and states how
  corrections reach independently installed copies (re-install on each
  tagged release; installed copies do not update themselves).

## [0.1.0] — 2026-09-17

### Added

* Initial drafts of nine skills: aeronautical-engineering,
  mechanical-engineering, statics-and-dynamics, thermodynamics,
  control-systems-engineering, electrical-engineering,
  electronics-engineering, computer-engineering, naval-architecture-marine.
  Licensed MIT at the time.

[Unreleased]: https://github.com/Griffing-Technology-LLC/engineering-pe-skills/compare/v0.2.0...HEAD
[0.2.0]: https://github.com/Griffing-Technology-LLC/engineering-pe-skills/compare/5300e0e...v0.2.0
[0.1.0]: https://github.com/Griffing-Technology-LLC/engineering-pe-skills/tree/5300e0e
