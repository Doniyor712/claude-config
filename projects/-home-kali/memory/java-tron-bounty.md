---
name: java-tron-bounty
description: Ongoing source-code audit of tronprotocol/java-tron for TRON DAO HackerOne bounty
metadata: 
  node_type: memory
  type: project
  originSessionId: 9b066252-f1a0-426a-a7d8-7915e46a7188
  modified: 2026-08-26T18:05:36.223Z
---

Auditing `tronprotocol/java-tron` (Java blockchain node, ~274k LOC, 1523 files) for the **TRON DAO HackerOne** program (hackerone.com/tron_dao, also bounty@tron.network). Repo cloned at `~/security-research/java-tron` (shallow).

**Scope:** only tronprotocol/java-tron code, all branches. Out-of-scope: tronscan.org, tron.network, tronlab.com websites.

**Reward tiers → modules:**
- $100k RCE (node takeover) → deserialization, protobuf/P2P parsing, TVM
- $50k private-key leakage → `crypto/` (36 files)
- $10k DoS via P2P → `framework/.../core/net` (81 files), `net/messagehandler/`
- $10k DoS via RPC-API → `framework/.../services/http` (220 files), `jsonrpc/`, gRPC `RpcApiService`
- $6k DoS via TRON protocol → tx/block validation, `consensus/` (19 files)
- $6k unauthorized account ops → `actuator/` (41 Actuators), permission checks

**Current focus (user chose):** P2P + RPC DoS ($10k tier).

Started 2026-08-26. Report findings responsibly via HackerOne; do not file public GitHub issues (per SECURITY.md).

**Dedup rule (user):** for every candidate, verify NOT a duplicate via (1) java-tron git history/blame, (2) GitHub issues/PRs + advisories, (3) Google + CVE/NVD. Duplicates hurt H1 signal/reputation. Full git history now available (unshallowed, 18831 commits, HEAD on develop 2026-08-06).

**Audited so far in P2P+RPC DoS — all HARDENED, no bug found:**
- P2P: TronMessageFactory (bounded by external `org.tron.p2p` frame size), ChainInventory/FetchInvData/Inventory handlers (size+rate+dedup+type checks). Team actively hardening: #6712 length-validation, #6731 inv rate-limit, #6851 unknown-inv-type reject, #6782 sig-length.
- RPC/HTTP/gRPC block endpoints: BLOCK_LIMIT_NUM=100. Pagination: *_COUNT_LIMIT_MAX=1000. AssetIssue paginated clamped.
- Constant contract / estimateEnergy: TVM OutOfTime time-bounded + retry-bounded; estimateEnergy off by default.
- JSON-RPC eth_getLogs/getFilterLogs: maxBlockRange (min(to,head)-from) + MAX_RESULT=10000 + SectionBloom index. sectionExecutor = fixed pool of 5 (shared) — noted, not clearly exploitable.
- All HTTP servlets extend RateLimiterServlet.
- JSON parser (JsonFormat): MAX_NESTING_DEPTH=20 (lowered from 100 in #6844), MAX_TOKEN_COUNT=100k; all recursive paths guarded.
- Shielded/zk scan endpoints: range <=1000 blocks; getMerkleTreeVoucherInfo bounded (synBlockNum<=1000, low-witness gap<=100).

**Assessment:** mature, actively-hardened, high-competition target; obvious P2P/RPC DoS closed. Next-best ROI: (a) audit newest merged PR diffs (lowest dedup risk), (b) pivot to actuator authz / $6k tier, (c) dynamic build+fuzz for real PoC.

**Newest-PR-diff audit (user-chosen direction) — all fixes SOUND, no residual bug:**
- #2fd5455c6 gRPC HTTP/2 stream limits: maxConcurrentCallsPerConnection 0→100 default; new GrpcNettyMaxConcurrentStreamsLimiter sets connection.remote().maxActiveStreams. gRPC is plaintext-only (no TLS path to miss). grpc bumped to 1.83.0 (rapid-reset handled by lib). Sound.
- #6845 JsonFormat parser refactor: converted per-field recursion→iteration (fixed a real many-fields StackOverflow); all object/array descent now enterRecursion-guarded (depth 20). Sound.
- #6820 bound/truncate signatures: getTransactionSignWeight + getTransactionApprovedList now reject sigCount>getTotalSignNum (default 5) BEFORE EC-recover, and truncate oversized sigs. Sound.
- Broadcast/push path: TransactionCapsule.validatePubSignature checks sigCount>getTotalSignNum (658) BEFORE validateSignature EC-recover (667). Sig-flood DoS closed.
- #6828 param validation (base58 len 34, addr/hash hex caps), #6867 hide stacktrace on overload, #6843 hide jetty internals in 413 — all careful hardening.

**Conclusion of pass 1:** No vulnerability found in P2P+RPC DoS surface incl. newest merged code. Team writes careful, well-tested security fixes; low probability of a bug in their fixes. Genuine result — mature targets commonly yield nothing on first static pass.
