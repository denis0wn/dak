# Tryss — Try DAK: Deterministic AI Execution Demo

> **"Your AI agents. Mathematically verified."**

---

## What is Tryss?

**Tryss** is the zero-friction demo binary for **DAK (Deterministic AI Kernel)**. It proves — in under 30 seconds — that your AI agents can execute with:

| Capability | What It Means |
|------------|---------------|
| **Deterministic Replay** | Same input → same execution trace, every time, bit-for-bit |
| **Cryptographic Audit Trail** | Blake3 + Merkle trees = tamper-proof execution receipts |
| **Instant Snapshots** | Full state capture at any step for debugging/recovery |
| **Compliance-Ready** | SOC 2, HIPAA, PCI-DSS, EU AI Act artifacts generated automatically |

> **Tryss = "Try DAK"** — Download → Run → Verify → Believe

---

## Quick Start (30 Seconds)

```bash
# 1. Download (Linux x86_64)
curl -L -o tryss https://github.com/denis0wn/dak/releases/download/v0.2.0/tryss-linux-x86_64
chmod +x tryss

# 2. Run your first task
./tryss --brand run "Process refund for order #12345"

# 3. Verify deterministic replay
./tryss verify <task_id>

# 4. Capture snapshot for compliance
./tryss snapshot <task_id>
```

**Requirements:** Linux/macOS, Ollama running locally (for LLM), 2GB RAM

---

## Demo Scenarios

### 1. Financial Transaction Processing (FinTech)
```bash
./tryss run "Process wire transfer: $50,000 from Acme Corp to Global Inc, reference INV-2024-001, OFAC check required"
```
**Proves:** Audit trail for PCI-DSS/SOX, OFAC screening trace, immutable receipt

### 2. Healthcare Prior Authorization (HealthTech)
```bash
./tryss run "Submit prior auth for MRI lumbar spine, patient ID 88472, CPT 72148, ICD-10 M54.5, provider Dr. Smith"
```
**Proves:** HIPAA-compliant execution, PHI handling trace, payer rule verification

### 3. Legal Contract Review (LegalTech)
```bash
./tryss run "Review NDA for mutual confidentiality, 2-year term, CA jurisdiction, flag non-standard clauses"
```
**Proves:** EU AI Act compliance, clause-by-clause reasoning trace, version control

### 4. CI/CD Pipeline Repair (Platform Engineering)
```bash
./tryss run --compile-error cargo-check.log "Fix compilation errors in scheduler.rs"
```
**Proves:** Deterministic code fix, test verification replay, regression prevention

---

## What You'll See

### Terminal Output (Live)
```
╔═══════════════════════════════════════════════════════════════════╗
║        Try DAK — Deterministic AI Execution Demo                ║
║        Version 0.2.0  |  github.com/denis0wn/dak                ║
║        "Your AI agents. Mathematically verified."               ║
╚═══════════════════════════════════════════════════════════════════╝

✅ Task executed: task-a1b2c3d4
   Status: SUCCESS
   Steps: 7
   Events: 23
   Artifacts: 5
   Replay valid: ✅
   Elapsed: 3.42s
   Result: Refund processed successfully. Confirmation: REF-2024-10-20-001

🔍 Next: tryss verify task-a1b2c3d4  |  tryss snapshot task-a1b2c3d4
```

### Replay Verification
```
✅ Replay VALID: task-a1b2c3d4
   Bit-for-bit deterministic execution confirmed.
   Merkle root match: ✅
   Event chain integrity: ✅
   State graph isomorphism: ✅

📋 This task is audit-ready. Capture capsule for compliance:
   tryss snapshot task-a1b2c3d4
```

### Snapshot Capture
```
📸 Snapshot: task-a1b2c3d4
   Version: 1
   Schema: 2
   Created: 2024-10-20T15:30:45Z
   State hash: a1b2c3d4e5f6...
   Artifacts: 5
```

---

## Why Tryss Exists

### The Problem
| Pain Point | Industry Impact |
|------------|-----------------|
| **Non-deterministic agents** | 88% of LLM code fails in production |
| **No audit trail** | SOC 2 auditors reject "LLM did it" |
| **Flaky CI/CD** | 40% of agent pipelines fail randomly |
| **Vendor lock-in** | Can't migrate from LangChain/OpenAI |
| **Compliance gaps** | HIPAA, PCI-DSS, EU AI Act require proof |

### The Tryss Proof
Tryss demonstrates that **DAK solves all five**:

1. **Determinism** — Same prompt → identical execution trace (verified via `tryss verify`)
2. **Audit Trail** — Every event cryptographically chained (Blake3 + Merkle)
3. **Reliability** — Snapshots enable instant recovery, zero flakiness
4. **Portability** — Language-agnostic workers, on-prem/air-gapped ready
5. **Compliance** — SOC 2 control evidence, HIPAA audit logs, PCI-DSS receipts

---

## Architecture (What Makes It Work)

```
┌─────────────────────────────────────────────────────────────────┐
│                        USER PROMPT                              │
└──────────────────────────┬──────────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                     PLANNER (LLM)                               │
│  Natural language → Structured DAG of typed steps               │
└──────────────────────────┬──────────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                   SCHEDULER (DAG)                               │
│  Dependency resolution → Topological execution order            │
└──────────────────────────┬──────────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                    WORKERS (Rust/WASM)                          │
│  • Code generation  • Compilation  • Testing  • Linting         │
│  • API calls  • Database ops  • File I/O  • Custom effects      │
└──────────────────────────┬──────────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                  EVENT BUS (SQLite + WAL)                       │
│  Every step, decision, artifact → Immutable event log           │
└──────────────────────────┬──────────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                  VERIFIER (Replay Engine)                       │
│  Deterministic re-execution → Merkle root comparison            │
└─────────────────────────────────────────────────────────────────┘
```

**Key Differentiator:** Unlike LangChain/LangGraph/AutoGen — DAK's verification is **mathematical**, not probabilistic.

---

## Compliance Artifacts (Auto-Generated)

| Framework | Artifact | Use Case |
|-----------|----------|----------|
| **SOC 2 Type II** | Control execution evidence | Security audits |
| **HIPAA** | PHI access audit trail | Healthcare agents |
| **PCI-DSS** | Transaction processing receipts | FinTech agents |
| **EU AI Act** | High-risk AI system logs | Regulated AI |
| **ISO 27001** | Change management records | Enterprise |
| **SOX** | Financial control execution | Public companies |

> Run `tryss snapshot <task_id>` → Get compliance-ready JSON capsule

---

## Compare: Tryss vs. Alternatives

| Feature | Tryss (DAK) | LangGraph | AutoGen | Custom Infrastructure |
|---------|-------------|-----------|---------|----------------------|
| **Deterministic replay** | ✅ Mathematical | ❌ | ❌ | 🔧 Build yourself |
| **Cryptographic audit** | ✅ Blake3+Merkle | ❌ | ❌ | 🔧 Build yourself |
| **Instant snapshots** | ✅ Sub-second | ❌ | ❌ | 🔧 Build yourself |
| **Auto recovery** | ✅ Built-in | ❌ | ❌ | 🔧 Build yourself |
| **Language-agnostic** | ✅ WASM workers | ❌ Python-only | ❌ Python-only | ✅ |
| **Air-gapped/on-prem** | ✅ Single binary | ❌ Cloud deps | ❌ Cloud deps | ✅ |
| **Compliance artifacts** | ✅ Auto-generated | ❌ Manual | ❌ Manual | 🔧 Build yourself |
| **CI/CD native** | ✅ GitHub Actions | ⚠️ Limited | ⚠️ Limited | ✅ |
| **Time to production** | **Minutes** | Weeks | Weeks | Months |

---

## Getting a Full Trial

**Tryss is the demo.** The full DAK kernel includes:

- ✅ Unlimited executions (Tryss: 1,000 trial limit)
- ✅ Source code access (Professional+)
- ✅ Custom effect development
- ✅ Enterprise SLA (4-hour response)
- ✅ White-label/OEM options
- ✅ Dedicated Slack support
- ✅ Compliance framework templates

### Trial Request (2 minutes)

| Method | Link |
|--------|------|
| **GitHub Issue** | [Open Trial Request](https://github.com/denis0wn/dak/issues/new?template=trial_request.yml) |
| **Email** | denis@smoliakov.dev |
| **Telegram** | [@Myagentdenbot](https://t.me/Myagentdenbot) — "DAK trial for [Company]" |
| **Calendly Demo** | [Book 30-min demo](https://calendly.com/denis-smoliakov/dak-demo) |

---

## Pricing (After Trial)

| Tier | Price | Seats | Best For |
|------|-------|-------|----------|
| **Trial** | Free | 1 | Evaluation (30 days, 1K execs) |
| **Professional** | $2,990/yr | 1 | AI startups, small teams |
| **Enterprise** | $14,990/yr | 10 | Regulated industries, platforms |
| **Custom/OEM** | Negotiated | ∞ | White-label, revenue share |

[View Full Pricing →](PRICING.md)

---

## Resources

| Resource | Link |
|----------|------|
| **Public Repo (Vitrine)** | https://github.com/denis0wn/dak |
| **Release v0.2.0 (Binaries)** | https://github.com/denis0wn/dak/releases/tag/v0.2.0 |
| **Full Documentation** | https://github.com/denis0wn/dak#readme |
| **Trial Request Form** | https://github.com/denis0wn/dak/issues/new?template=trial_request.yml |
| **Blog: Why AI Agents Fail SOC 2** | https://github.com/denis0wn/dak/discussions/1 |
| **Competitive Comparison** | [DAK_Competitive_Comparison.md](../DAK_Competitive_Comparison.md) |

---

## Contact

| Channel | Details |
|---------|---------|
| **Email** | denis@smoliakov.dev |
| **Telegram** | @Myagentdenbot (instant replies) |
| **Demo Booking** | https://calendly.com/denis-smoliakov/dak-demo |
| **GitHub** | https://github.com/denis0wn/dak |

---

*Tryss v0.2.0 — Part of DAK (Deterministic AI Kernel) — Proprietary License — © 2025 Denis Smoliakov*