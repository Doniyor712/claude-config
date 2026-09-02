---
name: raptor-toolkit
description: "RAPTOR autonomous security-research framework preserved at ~/security-research/raptor (project-scoped Claude Code app, NOT a global plugin)"
metadata: 
  node_type: memory
  type: project
  originSessionId: b6a6212f-ddd1-4dbf-9fe3-e45eae75a302
  modified: 2026-08-26T04:21:50.896Z
---

On 2026-08-26 the user asked to grab github.com/gadievron/raptor.git "the same way" as
[[redteam-arsenal]] (Claude-BugHunter). But RAPTOR is a **fundamentally different** kind of tool,
so the install is different — and deliberately so.

**What RAPTOR is:** an autonomous security-research framework (static/binary analysis + LLM vuln
validation + exploit/patch generation) that **runs INSIDE its own repo via Claude Code**. Its README
is explicit: *"RAPTOR loads its configuration from the repo directory. If you run `claude` from any
other directory, you get plain Claude Code, not RAPTOR."* Launch via the `bin/raptor` launcher or
`claude` from the checkout.

**Why NOT copied into global ~/.claude** (unlike Claude-BugHunter):
- `.claude/settings.json` is 100% project-scoped — permissions are `Bash(libexec/raptor-* *)` and
  hooks call `$CLAUDE_PROJECT_DIR/libexec/raptor-session-init` / `raptor-lifecycle-hook` on
  SessionStart/Stop/SessionEnd/PostToolUseFailure. Merging into global settings would fire those
  hooks in EVERY project and fail everywhere `libexec/` is absent — breaks the user's whole harness.
- Its 37 commands + 18 agents + 13 own skills are coupled to `raptor.py` / `libexec/raptor-*` /
  `core/` — broken outside the repo. Copying them global = broken duplicates + a `validate` command
  collision with the Claude-BugHunter one.
- So "asl holidagidek saqlab ol" (save in original form) = preserve the repo where its `.claude/`
  actually works, NOT scatter it into global config.

**What was done:** full clone at **~/security-research/raptor** (commit 4e75ac9, ~168M) with the
**SecOpsAgentKit submodule initialized** (github.com/AgentSecOps/SecOpsAgentKit → `.claude/skills/
SecOpsAgentKit/`, 29 extra skills: appsec/offsec/devsecops/IR/threatmodel). Totals in-repo:
42 SKILL.md (13 raptor + 29 SecOps), 37 commands, 18 agents, 2 hooks, 75 libexec binaries.

**NOT done (needs user / explicit ask):**
- Add `~/security-research/raptor/bin` to PATH (README's launcher install) — persistent shell-rc
  change, same class the classifier blocked for [[redteam-arsenal]]'s hunt.sh line.
- `pip install -r requirements.txt`, semgrep, node deps — needed to actually RUN raptor, not to
  preserve it. User only asked to save it.

To use: `cd ~/security-research/raptor && ./bin/raptor` (after deps), or add bin/ to PATH.
