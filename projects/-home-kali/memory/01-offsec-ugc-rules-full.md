# OffSec UGC — Full Rules & Submission Expectations (reference)

Compiled from the OffSec sources reviewed on 2026-09-02:
- Discord UGC Program Update (effective 2026-08-10)
- help.offsec.com "Grimoire Build Guide and UGC Submission Expectations" (changelog v6, 2026-08-03)
- offsec.com/community/ugc (payment tiers)
- The "How to read the wishlist" contributor reference

---

## 1. Program status — what is accepted right now (effective 2026-08-10)

**Standalone VM-based Offensive Labs are TEMPORARILY PAUSED.**
New concept submissions are accepted ONLY in these categories:
- **Chained-Host VM-based Offensive Labs** (multi-host attack chains)
- **Grimoire Labs** (blue-team investigative)
- **All VM-based Defensive Labs** (DFIR, malware analysis, IR)
- **CVE Labs — Defensive only**

All submissions in these categories MUST follow the **AI-Resistant (AI-R)** standard.

---

## 2. Payment tiers (offsec.com/community/ugc)

| Tier | Payment | Requirements |
|---|---|---|
| Basic | up to $300 | Working VM, unique build, accurate walkthrough, clear build script, CVEs ≤12 months old, MITRE alignment |
| Intermediate | up to $500 | + impeccable exploit chains, clear lessons, multi-step |
| Advanced | up to $1,500 | + grouped/chained VMs, realistic pentest scenarios |

- Wishlist match → priority review (within 3 days) + **25% rate uplift**.
- Grimoire: once accepted, paid on the next weekly payment cycle.
- OS allowed: Linux/UNIX, Windows 8.1+, or Server 2021+.
- Review: receipt confirmed within 24h, ~1 week target.

---

## 3. Wishlist rules ("How to read the wishlist")

- It is a **contributor reference, not a rulebook** — treat each casefile as a
  creative starting point; the exact shape of the lab is up to the author.
- **Adjustable:** question wording/order/count, point allocation (total stays
  reasonable for difficulty), difficulty ratings, scenario/characters/hostnames/
  IPs, artifact sets (swap/add/trim).
- **Claiming:** first come, first served; one accepted submission per item.
  Reviewer flags near-simultaneous later submissions as duplicates. No auto-lock.
- **Visibility:** most topics open to all; "Trusted creator only" rows reserved
  for Trusted Creators (20+ approved labs, or manually assigned).
- **Quality reminders:** consistent timestamps across logs/artifacts; neutral
  in-world filenames (no flag.txt/solution.pdf); enough realistic noise that the
  answer is *found* not handed over; verify proofs + walkthrough on a clean
  redeploy before submitting.

---

## 4. Grimoire Build Guide (help.offsec.com)

### What is a Grimoire
A blue-team investigative exercise teaching defensive skills through realistic
analysis of telemetry from a concrete attack/malware execution. Detective-style:
understand what happened, how, and what evidence proves it. Areas: threat
hunting, IR, endpoint/memory/network forensics, malware analysis, log analysis,
crypto/signal analysis. All Grimoires are educational and fictitious; realism is
valued and improves odds of acceptance.

### Core design principles
- **Evidence-driven** — conclusions from artifacts, not guesswork.
- **Narrative coherence** — one believable story.
- **Defensive mindset** — detection/investigation, not exploitation.
- **Realistic telemetry** — logs, memory, binaries, PCAPs like real environments.

### Required components
1. **Difficulty** (from a defensive practitioner's perspective): Easy /
   Intermediate / Hard / Insane.
2. **Scenario description** — high-level context + clear investigative goal, no
   spoilers/leading.
3. **Artifact set** — memory dumps, executables/scripts (sanitized), logs (EDR,
   Windows Event, app), PCAPs, supporting files (configs, registry hives,
   timelines). Must be internally consistent (attacker IP in PCAP == IP in logs),
   clearly structured (filename gives no hint), realistically recorded (real
   attacks take time). **At least two distinct artifact types** unless strong
   justification.
4. **Questions** — guide logically, encourage hypothesis validation, escalate in
   difficulty, state the required answer format (e.g. filename vs full path).
   Not leading; not yes/no (use how/what/when/why). **At least 8 questions.**
5. **Points** — total tied to difficulty: **Easy 40 / Medium 60 / Hard 80 /
   Insane 100.** Harder questions worth more.
6. **Expected findings (internal)** — full investigative walkthrough for
   reviewers: key milestones, critical artifacts + how they support conclusions,
   common pitfalls/false leads. (Not shown to students.)

### Submission format (Grimoire)
README + walkthrough + questions-and-answers document + a **separate
password-protected zip** containing ONLY the artifacts. Zip password format:
**`WordWordWord123`** (three words, first letter capitalised, then three digits,
no spaces).

### Quality expectations
Solvable using only provided artifacts; no obscure/undocumented methods; reward
analysis over tool memorisation; reproducible + technically sound; teach at least
one clear defensive/investigative skill. Learning value > volume/complexity, but
files must have real-world complexity.

### Common pitfalls to avoid
- Missing artifacts needed to answer questions.
- Artifacts with minimal data. PCAP must include malicious + background/legit
  traffic; **PCAPs < 20 minutes or minimal Sysmon datasets will be rejected.**
- Artifacts contradicting the narrative.
- Overly vague questions with multiple valid interpretations.
- Offensive steps a learner couldn't realistically observe.
- Answers hidden behind unnecessary rabbit holes.
- **Do not use your own name/nickname/handle as usernames in the lab.**
- **AI-generated content will not be accepted** (repeat offenders greylisted/
  blacklisted).
- Plagiarized content rejected (incl. labs from OffSec/competitors).

### Success criteria
Learner can reconstruct the incident timeline, explain attacker behavior with
evidence, justify conclusions defensibly, and transfer skills to real defense.

---

## 5. AI Usage policy (critical)

**Permitted:**
- Generating/refining build scripts for an existing, independently-conceived concept.
- Populating test data (databases, user accounts, web page content).
- Brainstorming/ideation during initial concept sketching (with caution — AI
  ideation follows recognizable patterns that reduce originality/acceptance odds).

**Prohibited:**
- Generating the **walkthrough**.
- Generating **passwords/tokens/secrets** (AI values are predictable/identical
  across submissions — e.g. `v3ct0rDB_r0cks!2024`, `xyz-api-k3y-1390yZq`,
  `/tmp/rootbash`, `X-TOKEN: <value>`, `/usr/local/bin/PLACEHOLDER-helper`).
- Generating **artifacts** — must be produced from a fully built, functioning
  lab; the lab must demonstrably work before artifacts are collected. Prohibited:
  AI-fabricated/predicted artifact values; scripts generating placeholder/
  synthetic values instead of real lab output; hardcoding artifact values without
  running the exploit against a live instance; copying values from other
  submissions/write-ups.

**Enforcement (predominantly/entirely AI-generated with little author contribution):**
1st instance → formal warning + revise/resubmit. 2nd → 6-month suspension.
3rd → permanent ban.

---

## 6. Walkthrough standards

- **PDF format.** Screenshots must illustrate the essential exploitation path
  (proof it is built and works). Not every step needs a screenshot, but all
  critical steps must be visually documented.
- All steps described clearly and in sufficient detail.
- Tokens, exploit code, and payloads must NOT be truncated or omitted.
- Any file paths / system-specific values needed to craft an exploit must be
  shown explicitly, including the method used to obtain them.
- Command outputs included for each command.
- **Walkthroughs generated, drafted, or substantially written by AI are NOT
  permitted.** (Exceptions case-by-case.)

---

## 7. AI-Resistant (AI-R) standard — MANDATORY (v6, 2026-08-03)

All new UGC labs must be AI-Resistant. Attack vectors keep their intended
difficulty; the changes only increase processing complexity, session length, and
token cost for automated AI solvers. Humans barely notice.

### Primary techniques (numbers are guidelines, adapt to scenario)
- **Volume inflation** — overwhelm AI context windows:
  - Web apps: 50–80+ realistic pages (instead of 10)
  - Databases: thousands to hundreds of thousands of rows
  - Active Directory: ~200 groups / ~2,000 users
- **Realistic breadth** — believable alternative paths/services a human filters
  out by instinct, forcing AI to waste tokens on every path. Avoid obvious
  artificial noise or malicious rabbit holes.

### Advanced (optional)
- **Depth** — conceal a critical artifact deep in a large dataset (e.g. one valid
  credential inside a massive dump).
- **Chaining** — steps depend on artifacts discovered much earlier in a long
  session.

**Key rule:** if a concept is solid but simple, extend it with data padding. The
core vuln (e.g. SQLi) doesn't change — there is simply too much data for
imprecise automated AI queries to succeed economically.

### AI-R FAQ
- Mandatory for all future human-user UGC labs: **yes.**
- Harder for human students: **no** — primary vector + human difficulty identical.
- Must you test against an AI model before submitting: **no** (API cost) — just
  apply volume + breadth during construction.

---

## 8. Changelog (help.offsec.com article)

| Ver | Date | Summary |
|---|---|---|
| 0 | 2026-01-26 | Initial publish |
| 1 | 2026-02-17 | No own name/handle; no leading questions; points; difficulty |
| 2 | 2026-02-26 | Acceptance & Payment Timeline section |
| 3 | 2026-03-30 | Two distinct artifact types; AI-generated/plagiarized rejection |
| 4 | 2026-05-07 | AI Usage; Walkthroughs sections |
| 5 | 2026-05-27 | Updated number of questions required (≥8) |
| 6 | 2026-08-03 | Added AI-R requirements |

When submitting a support ticket, include your Discord name and ID.
