---
name: offsec-ugc-rules
description: "OffSec UGC/Grimoire submission rules (Aug 2026) — categories, AI-R, AI limits, Grimoire format, payment; use when building a lab for Doniyor's OffSec UGC submissions"
metadata: 
  node_type: memory
  type: reference
  originSessionId: 1a3a3488-b852-42f5-884f-d9bc245b567b
  modified: 2026-08-29T17:55:20.282Z
---

OffSec UGC (User-Generated Content) submission rules for Doniyor (handle `doniyor_0712`). Apply these ONLY when the user says to use them for an OffSec lab build. Source: help.offsec.com Grimoire Build Guide (changelog v6, 2026-08-03) + Discord UGC update (effective 2026-08-10) + offsec.com/community/ugc.

**Accepted categories (standalone offensive VM labs PAUSED since 2026-08-10):**
- Chained-Host VM-based Offensive Labs (multi-host)
- Grimoire Labs (blue-team investigative)
- All VM-based Defensive Labs (forensics, malware analysis, IR)
- CVE Labs — Defensive only

**AI-R (AI-Resistant) — MANDATORY (v6):** inflate volume/breadth to break AI solvers, human difficulty unchanged. Web 50-80+ pages; DB thousands–100k+ rows; AD ~200 groups/~2000 users; add believable alt paths (not artificial rabbit holes). Optionally hide critical artifact deep in big dataset; chain steps across long session.

**AI usage limits (CRITICAL — violating = warning → 6mo suspension → permanent ban):**
- PROHIBITED: AI-generated walkthrough; AI-generated passwords/tokens/secrets (avoid AI-pattern values like `v3ct0rDB_r0cks!2024`, `xyz-api-k3y-...`, `/tmp/rootbash`); AI-generated artifacts (PCAP/logs/memory MUST come from a real running lab); predominantly AI-made submissions.
- ALLOWED: build scripts for an independently-conceived concept; populating test data (DB/users/page content); early ideation brainstorm.
- So: I help with concept, build scripts, test-data, structure, QA. USER must build the live lab, capture artifacts from it, choose secrets, and write the walkthrough themselves.

**Grimoire format:** README + walkthrough (PDF, human-written, screenshots of critical steps, no truncated payloads, command outputs shown) + Q&A doc + password-protected zip of artifacts only. Zip password format: `WordWordWord123` (3 capitalized words + 3 digits, no spaces). ≥8 questions, no leading/yes-no questions (how/what/when/why), escalate difficulty, specify answer format. ≥2 distinct artifact types. Points by difficulty: Easy 40 / Medium 60 / Hard 80 / Insane 100 (harder Qs worth more). PCAP >20 min with background noise; consistent timestamps across all logs; do NOT use own name/handle as in-lab usernames; neutral in-world filenames (no flag.txt/solution.pdf).

**Payment:** Basic ≤$300 / Intermediate ≤$500 / Advanced ≤$1,500 (grouped/chained VMs). Wishlist match = review ≤3 days + 25% uplift. Grimoire accepted = paid next weekly cycle. Trusted Creator = 20+ approved labs. OS: Linux/UNIX, Windows 8.1+, Server 2021+. First-come-first-served per wishlist item.

Related: [[java-tron-bounty]]
