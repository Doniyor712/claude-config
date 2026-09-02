---
name: redteam-arsenal
description: User installed the Claude-BugHunter red-team skill/command arsenal into ~/.claude
metadata: 
  node_type: memory
  type: project
  originSessionId: ca70e304-32fe-4c94-9a2d-1250f8a51bd9
  modified: 2026-08-25T16:58:23.651Z
---

On 2026-08-25 the user (Kali Linux box) had me install the **Claude-BugHunter** plugin
(github.com/elementalsouls/Claude-BugHunter, MIT, by Sachin Sharma) into `~/.claude`:

- **83 skills** → `~/.claude/skills/*/SKILL.md` (all `hunt-*` web/vuln-class + framework skills,
  recon/OSINT, reporting, validation; bug-bounty orchestrators)
- **15 commands** → `~/.claude/commands/*.md` (autopilot, hunt, recon, scope, triage, validate,
  report, chain, intel, surface, token-scan, pickup, remember, memory-gc, web3-audit)

Copied verbatim ("asliday nusxa"). The only edit: the Chinese "中文触发词" trigger tail in
`bug-bounty` and `bb-local-toolkit` SKILL.md descriptions was translated to an English
"Trigger words:" line, per the user's rule that non-English skill content is saved in English.

Also on 2026-08-25, installed a second skill from github.com/sanjarbiy/bugbountyrules:
- **bugbountyrules** → `~/.claude/skills/bugbountyrules/` (166 files, 2.2M) — a single
  behavioral-discipline "predator methodology" skill (42 rules, ~128KB SKILL.md) bundling a
  PortSwigger KB (145 files), reference shelf, waf-bypass-arsenal, writeup-library, vuln taxonomy,
  speed-commands. English skill; the only non-ASCII (Cyrillic homoglyphs in
  portswigger-kb/Web-LLM-attacks/AI-scanner-bypass) is intentional exploit payload, kept as-is.
Then installed a third source, github.com/mukul975/Anthropic-Cybersecurity-Skills (plugin
"cybersecurity-skills" v1.3.0):
- **818 skills** → `~/.claude/skills/` (descriptively named: analyzing-*, abusing-*, etc.),
  covering web security, pentest, DFIR, threat intel, cloud security, malware analysis. No commands
  or agents in this repo. All English (only non-Latin: the kanji tool-name 隼 in
  generating-forensic-timelines-with-hayabusa, explained in English — kept as-is). No name
  collisions with prior skills.

Skill total is now **902** (83 Claude-BugHunter hunt-* + bugbountyrules + 818 cybersecurity-skills),
commands 15. ~/.claude/skills is ~53M.

Source clone kept at scratchpad `Claude-BugHunter/`. The arsenal doc that pointed here
(`~/Downloads/Telegram Desktop/CLAUDE_SETUP_ARSENAL.md`) also listed 53 agents + 6 workflows,
but those live only in the doc author's private setup — NOT in this repo, so they were not installed.

User preference: skill files in English; **reply to the user in Uzbek**.
NOT done (would need explicit ask): settings.json changes like bypassPermissions / opus[1m] / effort max
that the arsenal doc recommends.

---
Update 2026-08-26: user re-pointed at the same repo (github.com/elementalsouls/Claude-BugHunter,
commit 1f9cdb6) and asked to study & preserve ALL skills, commands, AND **workflows** in original form.
Verified: all 83 skills + 15 commands still present in ~/.claude and byte-identical to a fresh clone
(only the 2 intentional English-trigger edits on bug-bounty / bb-local-toolkit differ — per English rule).

The missing piece was the **`hunt` engagement-scaffolder workflow** (the installer's 3rd artifact,
never installed on 2026-08-25). Now installed verbatim:
- `scripts/hunt.sh` → `~/.claude/scripts/hunt.sh` (chmod +x, byte-identical to repo).
  `hunt <target>` builds ~/Targets/<target>/ with CLAUDE.md, scope.md, submissions.txt, findings/,
  evidence/ (gitignored), notes.md — override parent via $HUNT_BASE.
- Full repo preserved durably at **~/security-research/Claude-BugHunter** (engine/ Python agent,
  cbh/ CLI, eval/ harness, docs/ — the workflow machinery the plugin installer leaves in the clone,
  NOT copied into ~/.claude by design).

PENDING (needs user): the one-line `source ~/.claude/scripts/hunt.sh` in ~/.zshrc was BLOCKED by the
auto-mode classifier (persistent shell-rc change). Until added, load per-session with
`source ~/.claude/scripts/hunt.sh` or the user adds that line to ~/.zshrc themselves.

---
Update 2026-08-26 (son yangilandi): keyingi manbalar ham qo'shilgach jami hisoblandi —
- **989 skill** (`find ~/.claude/skills -maxdepth 2 -name SKILL.md | wc -l`); top-level papka 998 ta
  (ba'zilari to'plam: anthropic-skills/=18, trailofbits/=16, claude-osint/=7, va h.k.).
- **24 command** (`~/.claude/commands/*.md`) — 2026-08-25 dagi 15 tadan 9 ta ko'paygan.
Eski "902 skills + 15 commands" raqami o'sha kungi holat edi; joriy aniq son yuqoridagi.
