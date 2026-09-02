---
name: trailofbits-redteam-skills
description: Red-team subset of trailofbits/skills installed — 16 skills namespaced at ~/.claude/skills/trailofbits + 6 commands + 1 agent; the 3 awesome-lists had no installable skills
metadata: 
  node_type: memory
  type: project
  originSessionId: b6a6212f-ddd1-4dbf-9fe3-e45eae75a302
  modified: 2026-08-26T05:05:15.206Z
---

On 2026-08-26 the user gave 4 repos and asked to pull only the RED-TEAM-relevant skills+commands:
- **hesreallyhim/awesome-claude-code**, **travisvn/awesome-claude-skills**, **BehiSecc/awesome-claude-skills**
  — all three are curated **link catalogs** (README/CSV only, 0 SKILL.md / 0 commands / 0 agents).
  Nothing installable in them. Notable red-team link they point to (NOT one of the 4 repos, so not
  installed): **jthack/ffuf_claude_skill** (ffuf web-fuzzing skill, Jason Haddix) — offered to fetch if
  wanted. Also referenced: anthropics/claude-code-security-review (defensive).
- **trailofbits/skills** (commit 65720f8) — the only one with real content: a plugin marketplace of 41
  plugins (83 SKILL.md, 86 agents, 8 commands), mostly DEFENSIVE audit/code-quality (Trail of Bits is
  an audit firm).

Installed the red-team / offensive / bug-hunting subset (16 skills) NAMESPACED at
**~/.claude/skills/trailofbits/** (verbatim, whole skill dirs incl. scripts like burp-search.sh /
scanner.sh; skills use `{baseDir}`-relative paths so they work standalone):
burpsuite-project-parser, firebase-apk-scanner, entry-point-analyzer, variant-analysis,
vulnerability-triage-brocards, codeql, sarif-parsing, semgrep (the 3 static-analysis skills),
semgrep-rule-creator, semgrep-rule-variant-creator, audit-context-building, constant-time-analysis,
supply-chain-risk-auditor, agentic-actions-auditor, dwarf-expert, yara-rule-authoring.

+ **6 commands** → ~/.claude/commands/ (burp-search, scan-apk, entry-points, semgrep-rule, audit,
ct-check) — no collision with the 18 existing commands.
+ **1 Claude subagent** → ~/.claude/agents/ (function-analyzer, from audit-context-building) — no
collision with the 52 pentest-ai agents.

**Caveat:** trailofbits ships as PLUGINS; a few commands (e.g. scan-apk) reference
`${CLAUDE_PLUGIN_ROOT}` which is only set when installed via `/plugin marketplace add trailofbits/skills`
+ `/plugin install <name>@trailofbits`. As bare user commands that var is unset, but each command's
skill IS installed (Claude can invoke the skill directly), and the commands carry documented fallbacks.
For fully-bundled behavior the user can run the `/plugin` route instead (interactive-only; Claude can't
invoke it).

EXCLUDED as non-red-team (defensive/dev/formal-verif): code-improver, modern-cpp/python, c/rust-review,
mutation-testing, property-based-testing, testing-handbook-skills, building-secure-contracts,
writing-lean-proofs, dimensional-analysis, spec-to-code-compliance, differential-review, sharp-edges,
second-opinion, goal-prompt, let-fate-decide, culture-index, devcontainer-setup, git-cleanup, gh-cli,
github-triage, open-sourcing, fp-check, claude-in-chrome-troubleshooting, trailmark, zeroize-audit.

Full repo preserved at **~/security-research/trailofbits-skills** (17M). The 3 awesome-lists were NOT
kept durably (catalogs, no content); re-clone if their link lists are wanted later.
