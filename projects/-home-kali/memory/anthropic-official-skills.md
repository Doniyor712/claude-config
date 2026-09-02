---
name: anthropic-official-skills
description: "anthropics/skills official example skills — 18 installed namespaced at ~/.claude/skills/anthropic-skills; claude-api skipped (built-in), full repo preserved"
metadata: 
  node_type: memory
  type: project
  originSessionId: b6a6212f-ddd1-4dbf-9fe3-e45eae75a302
  modified: 2026-08-26T04:57:08.776Z
---

On 2026-08-26 the user pointed at github.com/anthropics/skills (commit 3b3fad9, Anthropic's OFFICIAL
example-skills marketplace plugin — NOT red-team, unlike the other durable repos). 19 general-purpose
skills; README's native install is `/plugin marketplace add anthropics/skills` then
`/plugin install document-skills@anthropic-agent-skills` / `example-skills@…` (a `/plugin` command the
USER runs interactively — Claude can't invoke it). The skills are also "already available to paid plans
in Claude.ai."

Installed **18 of 19 NAMESPACED** at **~/.claude/skills/anthropic-skills/** (verbatim, .DS_Store
stripped), consistent with [[claude-red-skills]] / [[claude-osint-skills]] namespacing:
academy-guide, algorithmic-art, brand-guidelines, canvas-design, discernment-nudge, doc-coauthoring,
docx, frontend-design, internal-comms, mcp-builder, pdf, pptx, skill-creator, slack-gif-creator,
theme-factory, webapp-testing, web-artifacts-builder, xlsx.

**Skipped `claude-api`** — it name-collides with the Claude Code BUILT-IN `claude-api` skill (this repo
is that skill's upstream source; a user-scope copy would just duplicate the built-in `name:`). The
other 18 have no name collision with built-in harness skills (design/dataviz/artifact-*/code-review/
etc.) nor with the flat security-skills dir. claude-api still lives in the durable clone.

Note: namespacing only organizes directories — Claude Code keys skills by their `name:` frontmatter, so
these load by their canonical names (pdf, docx, skill-creator, …) regardless of the anthropic-skills/
parent. All 18 verified to have valid `name:`+`description` frontmatter.

`spec/agent-skills-spec.md` (the Agent Skills format spec) and `template/SKILL.md` are in the durable
clone only, not installed as skills. Full repo preserved at **~/security-research/anthropics-skills**
(16M) alongside Claude-BugHunter, raptor, Claude-Red, Claude-OSINT, pentest-ai-agents.
