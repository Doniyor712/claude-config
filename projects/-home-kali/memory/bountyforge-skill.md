---
name: bountyforge-skill
description: "Gabson0x/bountyforge all-round bug-bounty skill installed verbatim at ~/.claude/skills/bountyforge (English, plain skill, official clone-into-skills-dir install)"
metadata: 
  node_type: memory
  type: project
  originSessionId: b6a6212f-ddd1-4dbf-9fe3-e45eae75a302
  modified: 2026-08-26T05:14:50.986Z
---

On 2026-08-26 installed github.com/Gabson0x/bountyforge (commit 7012850, English, MIT-ish) — a single
large all-round **bug-bounty skill**: 135KB SKILL.md orchestrator + 42 reference files
(references/attack-vectors, references/hacking-agents/* — recon/web-api/graphql/race/http-smuggling/
smart-contract/supply-chain/waf-bypass/etc. sub-agent prompt files, methodology, judging, reporting) +
23 Python tools (hunt.py, exploit_gen.py, fleet.py, ledger.py, kill_chain.py, opsec.py, …) + tests.
Covers smart-contract audits (EVM/Solidity, Move/Aptos, Solana, TRON), web/API, CI/CD attacks, LLM/AI,
supply-chain, and HackerOne/Bugcrowd/Intigriti/Immunefi report generation.

Install followed the README exactly: it says `git clone … ~/.claude/skills/bountyforge`, i.e. the whole
repo IS the skill dir. Copied verbatim to **~/.claude/skills/bountyforge/** (1.4M, minus .git). Plain
skill — no .claude-plugin, no install.sh, no requirements.txt. Name `bountyforge`, no collision.

The `references/hacking-agents/*.md` are the skill's own sub-agent prompt files (loaded on demand via
the SKILL.md orchestrator), NOT Claude Code `~/.claude/agents/` subagents — left inside the skill dir.
Note: README promotes a paid cloud service (bountyforge.xyz) and the SKILL.md prints a banner; that's
skill behavior, nothing installed for it.

Full repo preserved at **~/security-research/bountyforge** (1.9M) — 9th durable repo. Related to the
other bug-bounty workflow skills [[src-hunter-skill]] and Claude-BugHunter ([[redteam-arsenal]]).
