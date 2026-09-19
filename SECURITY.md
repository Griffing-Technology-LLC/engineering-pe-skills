# Security Policy

## Reporting a vulnerability or an engineering error

For this repository the dominant failure mode is not a software vulnerability
but a wrong equation, factor, or misattributed standard reaching fabrication.
Both are reported the same way.

Please report all vulnerabilities and engineering errors to
<info@griffing.tech>. Include:

* the skill name and its `metadata.version` from the `SKILL.md` frontmatter;
* the git commit hash you installed from, if known;
* the REF-ID, equation, or passage in question, and what you believe is wrong.

## Errata

Because the skills are licensed CC BY-ND 4.0, a corrected copy cannot be
republished by third parties; corrections flow only through this repository.

* Confirmed technical errors are corrected here, the affected skill's
  `metadata.version` is bumped, and the change is recorded in
  [`CHANGELOG.md`](CHANGELOG.md).
* Users who installed a skill independently (for example with
  `npx skills add`) should re-install on each tagged release to pick up
  corrections; an installed copy does not update itself.
