---
name: bug-hunter-skill
description: "codexstar69/bug-hunter defensive code-audit Node CLI installed verbatim at ~/.claude/skills/bug-hunter — needs node (absent), security-review sub-skill collides with built-in"
metadata: 
  node_type: memory
  type: project
  originSessionId: b6a6212f-ddd1-4dbf-9fe3-e45eae75a302
  modified: 2026-08-26T05:24:13.683Z
---

On 2026-08-26 installed github.com/codexstar69/bug-hunter (commit 3be6973, npm `@codexstar/bug-hunter`
v3.2.0) — a **DEFENSIVE code-security-review** Node.js CLI tool (NOT offensive/bug-bounty like the
others). Precision-first adversarial code audit: Hunter/Skeptic/Referee/Fixer multi-agent flow, STRIDE
threat modeling, PR review, fix-loops, evidence-bounded triage of YOUR OWN codebase. English.

Installed to **~/.claude/skills/bug-hunter/** (whole repo minus .git, verbatim, 38M — mostly
docs/images PNGs). Also preserved full repo at **~/security-research/bug-hunter** (75M, 10th durable
repo). Root SKILL.md + 10 nested sub-skills under skills/ (hunter, skeptic, referee, fixer, recon,
doc-lookup, security-review, commit-security-scan, threat-model-generation, vulnerability-validation).

**All three follow-ups DONE 2026-08-26 (user: "uchalasini ham qil, yengil ishlasin"):**
1. **Node installed** — no passwordless sudo (apt needs a password, not taken), so installed Node LTS
   **v24.19.0** user-scope from the official nodejs.org binary tarball (sha256-verified) to
   **~/.local/node**; added `export PATH="$HOME/.local/node/bin:$PATH"` to ~/.zshrc (line ~267, via
   Edit tool). node v24.19.0 + npm 11.17.0 + npx work. Then ran the tool's OWN installer
   `node ~/security-research/bug-hunter/bin/bug-hunter install --agent claude-code` → canonical
   managed-runtime install WITH `.bug-hunter-install-manifest.json`. `bug-hunter doctor --agent
   claude-code` = "runtime v3.2.0 current and complete, Ready to hunt bugs." (chub optional, Context7
   fallback ok.) The official managed runtime is already lean (no docs/images) — 1.5M.
2. **security-review collision fixed** — renamed the sub-skill's frontmatter `name: security-review`
   → **`name: bughunter-security-review`** so it no longer shadows the built-in security-review skill.
   Safe: bug-hunter's runtime loads it by PATH (`skills/security-review/SKILL.md`), never by skill-name,
   and the manifest tracks paths only (no content hash) so doctor stays green. NOTE: re-running the
   official installer reverts this rename (source has the original name) — re-apply after any reinstall.
3. **Trimmed** — from 38M to **1.5M**. The 36M was docs/images; the official managed-runtime install
   excludes them anyway.

The 10 nested sub-skills (hunter/skeptic/referee/fixer/recon/doc-lookup/commit-security-scan/
threat-model-generation/vulnerability-validation + the renamed security-review) are still discoverable
as top-level skills by design. Node LTS at ~/.local/node is now available for any other Node-based tool.
