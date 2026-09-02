---
name: agentic-bug-hunter
description: "Awarexone/Agentic-Bug-Hunter (a Claude-BugHunter derivative) — installed only its NEW 7 skills + 22 commands + 9 agents non-destructively; colliding items kept as BugHunter's"
metadata: 
  node_type: memory
  type: project
  originSessionId: b6a6212f-ddd1-4dbf-9fe3-e45eae75a302
  modified: 2026-08-26T05:39:29.063Z
---

On 2026-08-26 the user gave github.com/Awarexone/Agentic-Bug-Hunter (commit 0826b13) — a large
offensive bug-bounty framework: 16 skills, 37 commands, 9 agents + a Python engine (agent.py 85KB,
brain.py 121KB, engine.py, serve.py), install.sh/install_tools.sh, hooks/, mcp/, tools/, wordlists/,
web3/. Its root SKILL.md is named **`bug-bounty`** with a description nearly identical (incl. the
Chinese trigger tail) to Claude-BugHunter's — it's a **fork/superset of Claude-BugHunter**
([[redteam-arsenal]]). Its install.sh copies FLAT into ~/.claude (skills/commands/agents), which would
OVERWRITE Claude-BugHunter's same-named items — so did NOT run it.

Installed only the NON-colliding NEW parts (like the Claude-OSINT approach), all English (0 CJK), so no
translation:
- **7 new skills** → NAMESPACED **~/.claude/skills/agentic-bug-hunter/**: argus (6-scanner suite:
  CORS/CRLF/NoSQLi/JWT/OOB-interactsh/LLM-redteam), cicd-security, client-reverse, credential-attack,
  graphql-audit, mobile-pentest, web2-vuln-classes.
- **22 new commands** → ~/.claude/commands/ (now 46 total): arsenal, breach-check, bypass-403,
  cloud-recon, cors, crlf, domxss, jwt-scan, llm-redteam, nosqli, oob, osint-employees, param-discover,
  portscan, sast, scan-cves, scope-aggregate, screenshot, secrets-hunt, spray, takeover, wordlist-gen.
- **9 new agents** → ~/.claude/agents/ (now 63 total): autopilot, chain-builder, credential-hunter,
  recon-agent, recon-ranker, report-writer, token-auditor, validator, web3-auditor.

SKIPPED as colliding with Claude-BugHunter (kept BugHunter's versions):
- 8 skills: bug-bounty, bb-methodology, meme-coin-audit, report-writing, security-arsenal,
  triage-validation, web2-recon, web3-audit.
- 15 commands: autopilot, chain, hunt, intel, memory-gc, pickup, recon, remember, report, scope,
  surface, token-scan, triage, validate, web3-audit.
The skipped versions differ (this repo's bug-bounty SKILL.md is NOT byte-identical to BugHunter's, and
still carries the Chinese trigger tail). Offered to switch specific ones to this fork's version if wanted.

Its `.claude/settings.json` has a Stop hook (`python3 -m tools.memory_gc --rotate`, guarded + cwd-
relative) — install.sh does NOT copy it, so global settings untouched. Python engine + tools live only
in the durable clone at **~/security-research/Agentic-Bug-Hunter** (8.2M) — run from there with
requirements.txt if the autonomous engine is wanted (node not needed; it's Python).
