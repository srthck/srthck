<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:020617,40:1E3A8A,100:2563EB&height=180&section=header&text=Sarthak%20Kadam&fontSize=52&fontAlignY=36&fontColor=F8FAFC&desc=Correctness-critical%20backend%20%C2%B7%20Fintech%20%C2%B7%20ML%20systems&descAlignY=58&descSize=15&animation=fadeIn" width="100%"/>

**B.Tech CSE @ MIT ADT University, Pune · 2028**

[LinkedIn](https://www.linkedin.com/in/sarthak-kadam-102134360) · [LeetCode](https://leetcode.com/u/sarthak6001/) · [Email](mailto:sarthakkadam.sk07@gmail.com)

</div>

---

```
         happy path                    where I work
    ─────────────────────   │   ───────────────────────────────
    it compiles             │   the same request arrives twice
    the test passes         │   the network dies mid-write
    the demo works          │   the model is confidently wrong
    the migration runs      │   the rollback has nowhere to go
```

I build systems where being *wrong* is more expensive than being *slow*: money that must balance to the paisa, decisions that must be reconstructable years later, deployments that must fail closed. One merged fix in XGBoost, one platform a real business runs on, two engines that refuse to turn uncertainty into confidence.

**Currently:** C++ and algorithms · gradient boosting internals · ML for credit and payment risk

---

## Open source

### XGBoost · numerical stability in the multiclass objective

**`C++`** **`CUDA`** · [Issue #12735](https://github.com/dmlc/xgboost/issues/12735) → [PR #12744 — merged](https://github.com/dmlc/xgboost/pull/12744) · shipped in master

Multiclass training produced **NaN gradients** when every class margin was strongly negative. Softmax is shift-invariant in theory. This implementation was not.

```cpp
// the bug: FLT_MIN is the smallest POSITIVE normalized float (~1.17e-38)
float wmax = std::numeric_limits<float>::min();
for (auto const& p : point) wmax = std::max(p, wmax);
// every margin negative  ->  wmax never updates  ->  stays ~0
// exp(x - 0) underflows across the row  ->  denominator 0  ->  NaN

// the fix: the most negative finite float
float wmax = std::numeric_limits<float>::lowest();
```

A one-line diff. Finding it was the work.

| | |
|---|---|
| **Found by** | Me — reproduction script, root-cause writeup, filed as an issue |
| **Confirmed** | Maintainer, same day |
| **Patched** | CPU (C++) and CUDA kernels |
| **Proved** | Regression test shifting all margins by −110, asserting gradient and pseudo-Hessian invariance — fails on unpatched code |
| **Verified** | 790 tests passed · 0 failed |
| **Disclosed** | ≤ 4.8e-6 margin drift over 100 boosting rounds |
| **Merged** | 6 days after the report |

<sub>CUDA not executed locally — no GPU build available. CI covered that path.</sub>

---

## Systems

### [TrackMarg](https://trackmarg.in) · transport & ledger platform <kbd>production</kbd>

`TypeScript` `React` `Node.js` `PostgreSQL` `Prisma`

Software a real transport and machinery business runs on. **10 customers, 15+ vehicles each, every working day.** The UI was the easy part.

```
   FIELD (offline, bad network)          SERVER (must never be wrong)
   ──────────────────────────           ─────────────────────────────
   trip submitted  ──┐
                     ├─ queued ──retry──►  idempotency key checked
   network dies    ──┘                     │
                                           ├─ ACID transaction
   SSE push  ◄──────────────────────────   ├─ exact decimal precision
   reconciled state                        ├─ concurrency control
                                           └─ append-only audit trail
```

A retried submission never double-posts. A contended row never interleaves. Every rupee that moves leaves a record of why. **258 PostgreSQL-backed integration tests** hold that line.

<details>
<summary><b>Why idempotency was the whole problem</b></summary>

<br>

A driver submits a trip. The request times out. He taps again. Without an idempotency key, that's two trips, two invoices, and a customer dispute three weeks later that nobody can reconstruct.

The server derives a deterministic key per submission. Same key, same body → the original response is replayed. Same key, different body → refused outright, because that is a client bug, not a retry. The ledger is append-only, so a correction is a new entry, never a mutation — which means the question *"why does this balance say this?"* always has an answer.

</details>

---

### [TrustMesh](https://github.com/srthck/trustmesh) · payment dispute decision engine

`Python` `SQLite` `Razorpay API` · [live demo](https://trustmesh-d9jj.onrender.com/) · Razorpay AI Buildathon 2026

> Payment systems tell you whether a transaction is **risky**. They don't tell you whether a dispute is **defensible**. Only one of those decides the chargeback.

```
CLAIM
  |  what must be proven?        weighted proof obligations
EVIDENCE
  |  is it admissible?           source registered, authority assigned
  |  is it independent?          4 photos of 1 delivery note = 1 source
  |  is it timely?               a fact that occurred after the
  |                              assessment cannot support it
PROOF STATE
  |  what is still missing?      unresolved mandatory obligations
  |  what should we get next?    ranked by decision impact AND deadline
  |  would it change anything?   real adjudicator, run on the hypothetical
POLICY GATE
  |
ACCEPT · REVIEW · CONTEST
```

Evidence authority is ranked `NETWORK 5 → SYSTEM_OF_RECORD 4 → THIRD_PARTY 3 → MERCHANT 2 → CUSTOMER 1 → MODEL_DERIVED 0`. A model may **propose** a candidate fact. It can never **admit** one — model output sits at authority rank zero regardless of its confidence, so it can corroborate but never carry an obligation alone.

Same inputs, same pinned policy versions, same verdict — years later, from a cold process. **1,062 tests pass with outbound sockets poisoned.**

<details>
<summary><b>What the benchmark does and does not prove</b></summary>

<br>

On a 44-case held-out set: **0 false contests, against 17** for a coverage-only baseline.

That number is weaker than it looks, and the repo says so. The benchmark is **synthetic and manually labelled**, and the labelling rule shares an author with the policy — so they agree partly by construction. This is construct validity (the implementation matches its stated intent), not production accuracy. The benchmark has also saturated, which means it has stopped discriminating. `docs/INDEPENDENT_EVALUATION_PROTOCOL.md` is how someone else could actually falsify it.

Reporting a metric without its limits is how you get a system nobody should trust.

</details>

---

### [PreFlight](https://github.com/srthck/preflight) · pre-deployment risk analyzer

`Python` `FastAPI` `Tree-sitter` `SQLGlot` `Next.js` · [live demo](https://preflight-delta-weld.vercel.app)

The migration succeeds. The build is green. Production still breaks.

```
ALTER TABLE users DROP COLUMN phone_number;
        |
        |  DB_READ
        v
   UserService ──HTTP_CALL──► ProfileAPI ──API_CONSUMES──► ProfileClient
        |
        v
   DO NOT DEPLOY        <- traced from source, not guessed
```

Parses source code (Tree-sitter), SQL migrations (SQLGlot) and OpenAPI contracts into an evidence graph, then traces multi-hop blast radius and rollback feasibility. Every finding links back to a file and line number, so the verdict is an argument you can audit rather than a score you have to trust.

Four verdicts, and the fourth matters most: `SAFE` · `CAUTION` · `DO NOT DEPLOY` · **`UNKNOWN`**. Missing evidence is reported as missing evidence. **UNKNOWN never silently becomes SAFE.**

Deterministic and hashed — identical input yields an identical decision hash, and the test suite asserts it. Uploaded repositories are treated as hostile: bounded extraction, no execution of uploaded code. **491 tests · `mypy --strict` · Playwright E2E.**

---

## The through line

| | Uncertainty about | Refuses to | Returns |
|---|---|---|---|
| **TrackMarg** | whether a request already happened | double-post on retry | the original response |
| **TrustMesh** | whether a dispute is provable | let a model authorize | ACCEPT · REVIEW · CONTEST |
| **PreFlight** | what a change reaches | call unknown "safe" | SAFE · CAUTION · DO NOT DEPLOY · UNKNOWN |

Same instinct every time: **make uncertainty explicit, make the decision explainable, fail closed.**

---

## Stack

| | |
|---|---|
| **Languages** | C++ · Python · TypeScript · SQL · Java |
| **Backend** | FastAPI · Node.js · Express · REST · PostgreSQL · SQLite · MongoDB · Prisma |
| **ML & data** | XGBoost · scikit-learn · pandas · NumPy |
| **Tooling** | Git · GitHub Actions · Docker · Linux · pytest · Playwright |
| **Practices** | ACID transactions · idempotency · concurrency control · audit trails · deterministic replay · static analysis |

<div align="center">
<br>

<img src="https://github-readme-stats.vercel.app/api?username=srthck&show_icons=true&include_all_commits=true&theme=transparent&hide_border=true&hide=issues&title_color=2563EB&text_color=475569&icon_color=2563EB" width="420"/>

</div>
