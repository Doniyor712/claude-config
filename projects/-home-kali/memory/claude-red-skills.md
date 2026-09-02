---
name: claude-red-skills
description: SnailSploit/Claude-Red offensive skills at ~/.claude/skills/claude-red — 26 native-frontmatter kept; 32 legacy checklist ones DELETED per user 2026-08-26
metadata: 
  node_type: memory
  type: project
  originSessionId: b6a6212f-ddd1-4dbf-9fe3-e45eae75a302
  modified: 2026-08-26T04:26:22.168Z
---

On 2026-08-26 installed github.com/SnailSploit/Claude-Red (commit aeb41ec, MIT) — a pure
**offensive-security skills** repo (no commands/agents/hooks). Used the repo's OWN `install.sh`:
`Skills/` → **~/.claude/skills/claude-red/** (namespaced subdir, preserves the category tree), so
NO directory collision with the flat arsenal in [[redteam-arsenal]]. 58 SKILL.md, byte-identical to
repo; only removed macOS `.DS_Store` junk from the install dir (durable clone keeps it verbatim).

Categories: active-directory, ai, auth (jwt/oauth), cloud, exploit-dev, fuzzing, infrastructure
(edr-evasion/initial-access/shellcode/redteam), iot, mobile, recon (osint), utility (reporting),
web (xss/sqli/ssrf/ssti/xxe/idor/rce/…), wireless (wifi/wpa2/wpa3/bluetooth/zigbee/z-wave/lorawan).

**Format caveat (repo's own state, left as-is per "save in original form"):** only **26 of 58** have
proper YAML frontmatter and will be auto-discovered by Claude Code as native skills. The other **32**
are legacy `## Metadata / - **Field**: value` checklist markdown (from SnailSploit/offensive-checklist)
with NO frontmatter → Claude Code will NOT surface them via the Skill tool, though they're preserved
and human-readable. The repo ships a `convert_skills.py` (author's build tool: legacy md → frontmatter,
name=folder) that would fix these, but it targets a lowercase `skills/` dir that doesn't match the
current `Skills/` layout. NOT run — would modify files and deviate from verbatim. Offered to the user
to add frontmatter to the 32 so they load; user instead chose to DELETE them (2026-08-26) — the
32 legacy skill dirs + the emptied `ai/` category were removed from the install. Only the 26
native-frontmatter skills remain active. The 32 still exist in the durable clone at
~/security-research/Claude-Red if ever needed.

One `name:` overlap: Claude-Red's `recon/offensive-osint` declares `name: offensive-osint`, same as a
Claude-BugHunter global skill — kept separate by the claude-red/ namespace but the name still collides
in the skill picker.

Full repo also preserved durably at **~/security-research/Claude-Red** (5.4M) alongside
~/security-research/Claude-BugHunter and ~/security-research/raptor.
