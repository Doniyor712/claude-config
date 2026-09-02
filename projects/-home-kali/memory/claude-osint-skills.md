---
name: claude-osint-skills
description: elementalsouls/Claude-OSINT — 7 unique OSINT skills active at ~/.claude/skills/claude-osint; the 2 that collided with newer BugHunter versions were deleted from the namespace per user
metadata: 
  node_type: memory
  type: project
  originSessionId: b6a6212f-ddd1-4dbf-9fe3-e45eae75a302
  modified: 2026-08-26T04:35:52.015Z
---

On 2026-08-26 installed github.com/elementalsouls/Claude-OSINT (commit f4acf9e, same author as
[[redteam-arsenal]] Claude-BugHunter) — a dedicated external-recon/OSINT **skills** repo (no
commands/agents/hooks). 9 skills under `skills/`; the repo's `.claude/skills/run-claude-osint` is a
repo-build/test helper skill (project-scoped, references repo scripts) — kept in the durable clone
only, NOT installed globally.

**Installed NAMESPACED** at **~/.claude/skills/claude-osint/** (like [[claude-red-skills]]), NOT flat,
verbatim (only stripped macOS .DS_Store). Reason: 2 of the 9 share a `name:` with skills already
installed globally from Claude-BugHunter, and the GLOBAL ones are newer/richer — a flat
`cp -r skills/*` would have DOWNGRADED them:
- `offensive-osint`: global BugHunter = **v3.0.0** modular (399-line SKILL.md + 22 reference files);
  Claude-OSINT = v2.2 monolithic (4734-line SKILL.md, no references). Global is newer arch.
- `osint-methodology`: both **v2.3**, but global BugHunter = 1704 lines vs Claude-OSINT = 520 lines.

The `sync-skill-content.sh` step in the repo's docs is a no-op here — `docs/full-skills/` sources are
absent in this commit, so the shipped SKILL.md files ARE the full content. Install = plain copy.

7 genuinely NEW org-grade skills now active (no global collision): cloud-saas-exposure,
continuous-exposure-monitoring, email-domain-security, exposure-risk-quantification,
identity-provider-recon, org-attack-surface, osint-autopilot.

**Duplicate resolution (done 2026-08-26):** user chose to delete the 2 older claude-osint copies of
the name-colliders. Removed `claude-osint/offensive-osint` (v2.2) and `claude-osint/osint-methodology`
(520-line) from the install. The newer global BugHunter `offensive-osint` v3.0.0 (+22 refs) and
`osint-methodology` v2.3 (1704-line) remain and are now the sole copies. So claude-osint/ holds only
the 7 unique org-grade skills. Both deleted skills still exist in the durable clone if ever needed.

Full repo preserved durably at **~/security-research/Claude-OSINT** (3.8M), alongside
Claude-BugHunter, raptor, Claude-Red.
