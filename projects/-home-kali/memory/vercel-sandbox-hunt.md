---
name: vercel-sandbox-hunt
description: "Active hunt on Vercel Sandbox Escape Challenge (HackerOne, $1M pool, ends 2026-09-01)"
metadata: 
  node_type: memory
  type: project
  originSessionId: 9b066252-f1a0-426a-a7d8-7915e46a7188
  modified: 2026-08-26T18:24:27.624Z
---

Hunting the **Vercel Sandbox Escape Challenge** — hackerone.com/vercel_sandbox (contact sandbox-escapes@vercel.com). Time-boxed: **2026-08-18 → 2026-09-01 23:59 UTC**, $1M pool, **max $50k/report**. Triage through 2026-10-01. Workspace: `~/security-research/vercel-sandbox-hunt` (@vercel/sandbox SDK installed, `phase-a-recon.mjs` harness written).

**Hard constraints:** LIVE PoC mandatory (static analysis = $0, N/A). "AI slop" (unverified/AI-generated claims, scanner output w/o working exploit) → N/A/Spam. Must test only accounts you own; cross-tenant = TWO of your own accounts, STOP at first confirmation. Cap 5 q/s, no volumetric DoS, no persistence. Report needs zip PoC + team_/prj_/sbx_ IDs.

**Architecture:** bare-metal EC2 hosts many sandboxes; 1 Firecracker microVM per sandbox (dedicated guest kernel). Host orchestrator launches Firecracker under a **jailer** (chroot+cgroup+netns). Inside microVM: init → runc/containerd container runs operator code (2 layers from host). **Security boundary = the Firecracker microVM**, NOT the container/namespaces.

**Control-plane REST API (in scope, IDOR target), all keyed by session/sandbox/snapshot IDs:**
`POST /v2/sandboxes`, `/v3/sandboxes`, `GET /v2/sandboxes/{name}`, `POST /v2/sandboxes/{src}/fork`, `/v2/sandboxes/sessions/{sessionId}` GET/DELETE, `.../cmd`, `.../cmd/{cmdId}/logs|kill`, `.../fs/read|write|mkdir`, `.../network-policy`, `.../snapshot`, `.../stop`, `.../extend-timeout`, `/v2/sandboxes/snapshots/{snapshotId}`, `/snapshots/tree`.

**OUT of scope / KNOWN duplicates — DO NOT report:** all container→guest-OS namespace escapes (core_pattern+/volumes/opt/vercel bind, 41 caps, /dev bind, seccomp ActAllow+vsock, mknod /dev/vda, modprobe/uevent_helper one-syscall); post-escape host surface (**vsock 2050** unauth RPC: resource/proxy-CA/cache-oracle/OCI read-write; containerd.sock/ipc.sock/APM world-accessible; sibling spawn; sandbox-init Ed25519 key); header injection (x-vercel-oidc-token, x-vercel-protection-bypass, x-vercel-proxy-signature) unless exfil via Vercel-side defect. DoS against own sandbox; third-party header reflection; documented firewall limitations (domain fronting, subnets.allow bypass, CIDR-only DNS); Firecracker CVE version-match w/o live weaponization; VCR/build-phase; SDK client bugs.

**Prioritized PAYABLE targets (no 0-day needed, most tractable first):**
1. **Control-plane API IDOR/authz** (2 own accounts) → cross-tenant read/modify = Critical $25-50k. Bread-and-butter API test.
2. **Firewall enforcement gaps** (1 account): silent fail-open, normalization (case/IDN/trailing-dot/wildcard-depth/port/unmasked-CIDR/precedence), lifecycle (policy not reapplied on resume/snapshot/restart, stale readback, unfiltered boot window) = Low-Med $1-10k.
3. **MMDS secret disclosure under deny-all/CIDR-deny** (Datadog/creds reachable) = High $10-25k.
4. Credential-brokering exfil via Vercel-side proxy defect (matcher/smuggling) = High.

**Status 2026-08-26:** setup done; blocked on user Vercel auth (HackerOne-alias account token) to run phase-a-recon live. Collaboration model: I write scripts/PoC, user's own authenticated account runs them; I analyze real output. See [[java-tron-bounty]] for the other active audit.
