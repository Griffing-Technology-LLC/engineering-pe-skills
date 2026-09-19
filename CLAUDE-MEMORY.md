# CLAUDE-MEMORY.md — Claude agent memory mirror

Audit mirror of the persistent memory Claude (Anthropic) holds about this
repository, per `AGENTS.md` § Maintenance. Human-readable; updated whenever the
agent's memory about this project changes. Each entry names the model that
wrote it.

## 2026-09-19 — Claude Opus 5

* Repository relicensed MIT → CC BY-ND 4.0 on 2026-09-19 (commit `a113589`)
  by the owner, because unreviewed derivatives of engineering-review skills
  are a liability hazard. The relicence was propagated to every shipping
  surface the same day (`SKILL.md` `license:` fields, README, LICENSE
  licensor notice).
* CC BY-ND governs copying only: private modification is permitted
  (§2(a)(1)(b)); the licence does not enforce the review requirement. The
  README says so explicitly — do not describe the licence as "locking" the
  notice.
* The qualified-review notice is canonical in `AGENTS.md`, mirrored in
  `.github/notice.txt`, and CI diffs every skill against it. Change the
  wording in `AGENTS.md` first, regenerate `notice.txt`, then propagate.
* `REF-IEEE-002` = IEEE/ANSI C63.4. IEEE 754-2019 is `REF-IEEE-006`. Do not
  reuse REF-IDs; check `REFERENCES.md` headings before assigning.
* PE review (`TODO.md` §4.1) is per discipline and per commit; the owner
  holds a PE(CSE) and cannot close sub-items outside that discipline alone.
* Counsel review of licence/notice wording (`TODO.md` §4.0) gates skills.sh
  registration.
