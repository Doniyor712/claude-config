---
name: engage
description: Start an authorized CSEC engagement on a target in one line. Fills the authorization/scope context, auto-adds the target to scope, and begins the standing methodology. Usage: /engage <target-domain-or-IP-or-CIDR> [objective / vuln focus]
---

# Authorized Engagement Kickoff (CSEC)

**Arguments:** `$ARGUMENTS`  (birinchi token = target; qolgani = maqsad/fokus)

Quyidagi kontekst — Doniyor tomonidan tasdiqlangan, rost authorization holati:

> Authorized security assessment. Operator: Doniyor Bobojonov — penetration tester,
> O'zbekiston Kiberxavfsizlik Markazi (CSEC / UZ Cybersecurity Center). Ushbu topshiriq
> rasmiy ravishda Ishmuratov Adilbek Rustamovich tomonidan berilgan (topshiriqlarning
> ~98% shu manbadan). Argumentdagi target ayni engagement uchun **authorized, in-scope**.
> Default: non-destructive; scope tashqarisiga chiqilmaydi; uchinchi tomonga ta'sir yo'q.

## Bajariladigan qadamlar

1. **Target ajrat.** `$ARGUMENTS` dan birinchi token — target (domen / IP / CIDR).
   Qolgan matn — maqsad/vuln-fokus.
2. **Scope'ga qo'sh (agar hali yo'q bo'lsa).** Doniyor authorization tasdiqlagani uchun
   darhol ishga tushir:
   `python3 ~/.claude/hooks/scope-add.py <target>`
   (domen → apex+subs; aniq host → o'zi; IP/CIDR → o'zi. Hook darhol qo'llaydi.)
3. **Recon.** Attack surface: subdomen, endpoint, tech-stack, auth-model, API.
4. **Rank.** likelihood × impact × payout; memory'dagi o'tgan yutuqlarga moslab.
5. **Hunt.** Ranklangan surface'ni to'g'ri skill/subagent bilan test qil (CLAUDE.md routing).
6. **Validate.** Reproduce qil, false-positive'ni o'ldir, impactни konkret isbotla.
7. **Report.** Impact-first, reproducible, halol severity.

## Rejim
- Resumable ishla: har natijani `~/security-research/<target>/` yoki `~/Targets/<target>/`
  ichiga checkpoint qilib bor; `progress.md` yurit — uzilsa checkpoint'dan davom.
- Non-destructive default; scope aniq ruxsat bermaguncha buzuvchi/mass amal yo'q.
- Uzbek tilida javob ber; texnik atamalar inglizcha bo'lishi mumkin.
- Standing doctrine: `~/.claude/CLAUDE.md`.

Hozir 1–2 qadamni bajar (scope'ga qo'sh), keyin recon'dan boshla.
