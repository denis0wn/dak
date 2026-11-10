# DAK Objection Handling Guide

**For:** Sales conversations, demos, trial follow-ups  
**Format:** Objection → Root Cause → Response → Evidence/Proof Point

---

## Objection Categories

### 1. "We're already using LangChain / LangGraph / CrewAI"

**Root Cause:** Prospect thinks DAK replaces their framework  
**Response:** "DAK doesn't replace LangGraph — it runs underneath it. You keep your chains, agents, and prompts. DAK adds the deterministic execution layer: replay, audit trails, compliance artifacts. Migration is ~1 day to wrap existing chains in DAK workers."

**Proof Points:**
- LangGraph orchestrates, DAK guarantees
- LangSmith = observability, DAK = deterministic replay + crypto audit
- 100% backward compatible — your LangGraph code runs unchanged
- Demo: Show LangGraph chain → wrap in DAK worker → `dak replay --verify`

---

### 2. "We can build this ourselves"

**Root Cause:** Engineering team thinks it's "just logging + replay"  
**Response:** "It's 6-18 months of kernel engineering: event bus with causal ordering, instant snapshots with copy-on-write, Merkle tree receipts with Blake3, planner validation with compile/test/lint gates, provider abstraction layer, causal DAG scheduler, auto-recovery. DAK v0.2.0 is done, tested, benchmarked at 100% replay fidelity. Your team builds product, not AI runtime."

**Proof Points:**
- 6-18 months vs. days to integrate
- Opportunity cost: 3-5 engineers × $200K = $600K-1M + maintenance
- DAK Professional: $2,990/yr/seat = ROI in week 1
- Battle-tested: cryptographic receipts, instant snapshots, auto-recovery

---

### 3. "We don't have budget / too expensive"

**Root Cause:** Comparing to observability tools (LangSmith $30-50/mo/seat) not kernel infrastructure  
**Response:** "DAK isn't observability — it's deterministic execution infrastructure. Different category. LangSmith shows you what happened; DAK proves it happened identically every time. For regulated enterprises, that's the difference between passing SOC 2 and losing the deal. One lost enterprise deal = $100K-500K ARR. DAK Professional = $2,990/yr/seat."

**Proof Points:**
- Category of one: deterministic replay + crypto audit trail
- Compliance artifacts generated automatically (SOC 2, HIPAA, PCI-DSS)
- Enterprise: $14,990/yr (10 seats) = less than 1 senior engineer-month
- Custom/OEM available for platform embedding

---

### 4. "We're not regulated / don't need compliance"

**Root Cause:** Early-stage startup, pre-SOC 2  
**Response:** "Today you're not regulated. Tomorrow your first enterprise customer asks for SOC 2 Type II. The sales cycle extends 60-120 days while you scramble to build audit trails. DAK gives you compliance-ready infrastructure from day one. Also: deterministic replay = flaky CI/CD fixed, debugging 10x faster, model drift detected instantly. Value exists even pre-compliance."

**Proof Points:**
- Flaky CI/CD: same test passes 9 AM, fails 9:05 AM — DAK fixes this
- Debugging: time-travel replay vs. print statements
- Model drift: provider updates silently change behavior — DAK detects via replay
- Vendor lock-in: swap OpenAI → Anthropic → Local without code changes

---

### 5. "We need to evaluate / POC first"

**Root Cause:** Standard procurement process  
**Response:** "Perfect. Our trial is exactly that: 30 days / 1,000 executions, full binary, your platform, your use case. No credit card, no commitment. We'll send the binary today, you run your first task in 5 minutes. I'll check in on Day 7 and Day 21. If it's not a fit, no worries."

**Proof Points:**
- Trial: 30 days / 1,000 executions / full features
- Binary: Linux musl, macOS, Windows — single file, no dependencies
- Quick start: `chmod +x dak && ./dak doctor && ./dak run "your task"`
- Support: Direct access to Denis (founder) during trial

---

### 6. "We're using cloud AI (OpenAI/Anthropic) — vendor handles compliance"

**Root Cause:** Misunderstanding of shared responsibility model  
**Response:** "Cloud providers give you model outputs. They don't give you: per-decision audit trails, bit-for-bit replay, causal execution graphs, compliance artifacts mapped to SOC 2/HIPAA/PCI controls. You're responsible for *how* the output was generated and *what* happened in your system. DAK sits in your infrastructure, your control, your compliance boundary."

**Proof Points:**
- Shared responsibility: provider = model, you = execution governance
- DAK is provider-agnostic: swap providers without changing agents
- Air-gapped/on-prem: DAK runs fully offline, no cloud dependency
- Data never leaves your infrastructure

---

### 7. "We need to check with legal / security / compliance team"

**Root Cause:** Multi-stakeholder purchase  
**Response:** "Absolutely — and I'll make it easy for them. I'll send a one-pager mapping DAK receipts to SOC 2 criteria (CC6.1, CC7.2, CC8.1, PI.1), HIPAA 164.312(b), PCI-DSS v4.0. I can also join a call with your security team to walk through the threat model, cryptographic guarantees, and air-gapped deployment options."

**Proof Points:**
- One-pager: DAK receipts → SOC 2 criteria mapping
- Threat model documented in SECURITY.md
- Air-gapped deployment supported (Enterprise)
- Source code access under NDA (Professional+)

---

### 8. "What if DAK goes away / you get acquired?"

**Root Cause:** Vendor risk concern  
**Response:** "Valid concern. Three protections: (1) Enterprise tier includes source code license — you own the ability to maintain forever. (2) Binary is self-contained, no external dependencies, no phone-home — runs indefinitely. (3) Custom/OEM includes perpetual source license with escrow option. We're bootstrapped, profitable, customer-funded — no investor pressure to exit."

**Proof Points:**
- Professional: Source access under NDA
- Enterprise: Source included
- Custom/OEM: Perpetual source + escrow
- Bootstrapped, profitable, no VC pressure

---

### 9. "We're using Python/TypeScript — DAK is Rust?"

**Root Cause:** Language mismatch concern  
**Response:** "DAK workers are language-agnostic. Your agents stay in Python/TypeScript/Go/whatever. DAK communicates via stdio/HTTP/gRPC — any language that can spawn a process or make an HTTP call works. The kernel is Rust for performance and memory safety; your code stays in your language."

**Proof Points:**
- Language-agnostic worker protocol (stdio/HTTP/gRPC)
- Python SDK: `pip install dak-python` (planned v0.4)
- TypeScript SDK: `npm install @dak/sdk` (planned v0.4)
- Any compiler target works

---

### 10. "We need a UI / visual builder"

**Root Cause:** Non-technical stakeholders want no-code  
**Response:** "DAK is CLI/API-first for engineers who ship. No vendor lock-in to a visual builder. That said: v0.5 roadmap includes VS Code extension with inline replay, and we're exploring a web-based time-travel debugger. For now: engineers love the CLI, it's CI/CD native, and it works in any environment (local, CI, prod, air-gapped)."

**Proof Points:**
- CLI + API = CI/CD native, scriptable, automatable
- VS Code extension planned (v0.5)
- Time-travel debugger web UI planned (v0.5)
- No vendor lock-in to proprietary UI

---

## Quick Reference Card

| Objection | One-Liner Response |
|-----------|-------------------|
| "Using LangChain" | "LangGraph orchestrates. DAK guarantees. Run LangGraph *in* DAK." |
| "Build ourselves" | "6-18 months kernel engineering. DAK = days. ROI week 1." |
| "Too expensive" | "One lost deal = $100K+. DAK = $3K/seat. Different category." |
| "Not regulated" | "Flaky CI/CD fixed. Debugging 10x faster. Model drift detected." |
| "Need POC" | "30-day trial, 1K execs, binary today, 5-min start." |
| "Cloud handles it" | "Shared responsibility: provider = model, you = execution governance." |
| "Legal review" | "One-pager: DAK receipts → SOC 2/HIPAA/PCI criteria mapping." |
| "Vendor risk" | "Source license (Pro+), perpetual (Enterprise), escrow (OEM). Bootstrapped." |
| "Wrong language" | "Workers are language-agnostic. Your code stays in Python/TS/Go." |
| "Need UI" | "CLI/API = CI/CD native. VS Code extension + web debugger v0.5." |

---

## Escalation Paths

| Situation | Action |
|-----------|--------|
| Technical deep-dive needed | Book 30-min technical demo (Calendly) |
| Security team review | Join call, walk threat model + crypto guarantees |
| Legal/compliance review | Send SOC 2/HIPAA/PCI mapping one-pager |
| Procurement / pricing | Custom quote, flexible terms, crypto discount (5%) |
| Executive sponsor needed | Founder (Denis) joins call directly |

---

*Use this guide during calls, demos, and email follow-ups. Update based on real objections encountered.*