---
name: src-hunter-skill
description: MyuriKanao/src-hunter bug-bounty workflow skill installed verbatim (Chinese) at ~/.claude/skills/src-hunter — user waived translation for this one
metadata: 
  node_type: memory
  type: project
  originSessionId: b6a6212f-ddd1-4dbf-9fe3-e45eae75a302
  modified: 2026-08-26T05:10:03.913Z
---

On 2026-08-26 installed github.com/MyuriKanao/src-hunter-skill (commit 978b953, v1.2.1, MIT) — a single
rich SRC/众测/bug-bounty vuln-hunting **workflow skill** with a 50M `references/` corpus (3168 files):
5-phase methodology (intake→recon→enum→hunt→report) with mandatory checkpoints, 19 attack playbooks
(SQLi/XSS/RCE/SSRF/IDOR/CSRF/PathTraversal/FileUpload/SSTI/XXE/Race/HTTP-smuggling/OAuth/JWT/SAML/
GraphQL/Mobile/LLM/DoS), 305 payloads, 263 WAF/EDR bypass variants, 2887 real HackerOne High/Critical
disclosed cases, 88,636 WooYun case stats, Chinese OA/middleware fingerprint DB, banking/telecom
vertical playbooks. Installed at **~/.claude/skills/src-hunter/** (whole skill dir verbatim incl.
references + README the SKILL.md points to). No name collision.

**Translation waiver (IMPORTANT exception to the standing English-content rule in [[redteam-arsenal]]):**
this skill's SKILL.md and ~81 of its reference prose files (methodology + playbooks) are in Chinese. I
was about to translate the SKILL.md per the rule, but the user said *"agar ishlashiga xalaqit qilmasa
tarjima shart emas"* (if it doesn't hinder functionality, translation isn't needed). Chinese doesn't
hinder functionality — Claude reads it fine, and the description carries English trigger terms too (bug
bounty, hackerone, SQLi/XSS/RCE…) so it still fires on English queries. So installed FULLY VERBATIM, no
translation. **Rule refinement:** the English-content rule is functionality-driven — skip translation
when the non-English content still works as-is; only translate when it would otherwise break usability.

Full repo preserved at **~/security-research/src-hunter-skill** (64M) — 8th durable repo alongside
Claude-BugHunter, raptor, Claude-Red, Claude-OSINT, pentest-ai-agents, anthropics-skills,
trailofbits-skills.
