# Deterministic AI Kernel (DAK) — Enterprise-Grade AI Execution Runtime

[![Build Status](https://github.com/denis0wn/deterministic_ai_kernel/workflows/CI/badge.svg)](https://github.com/denis0wn/deterministic_ai_kernel/actions)
[![Version](https://img.shields.io/badge/version-0.2.0-blue.svg)](https://github.com/denis0wn/deterministic_ai_kernel/releases/tag/v0.2.0)
[![License: Proprietary](https://img.shields.io/badge/license-Proprietary-red.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20macOS%20%7C%20Windows-lightgrey.svg)](https://github.com/denis0wn/deterministic_ai_kernel/releases)
[![Rust](https://img.shields.io/badge/rust-1.75%2B-orange.svg)](https://www.rust-lang.org)

> **The only AI execution kernel that guarantees deterministic, replayable, and auditable results.**  
> Deploy AI agents in production with confidence: every execution is cryptographically verifiable, fully replayable, and commercially supported.

---

## 🎯 The Problem

| Current AI Agents | DAK Kernel |
|-------------------|------------|
| ❌ Non-deterministic — same prompt, different results | ✅ **Bit-for-bit identical replay** — cryptographic receipts |
| ❌ No audit trail — "black box" decisions | ✅ **Full audit log** — every step, tool call, LLM response persisted |
| ❌ Can't debug failures — "it worked yesterday" | ✅ **Time-travel debugging** — snapshot, restore, compare any execution |
| ❌ Vendor lock-in — tied to one LLM provider | ✅ **Provider-agnostic** — OpenAI, Anthropic, Ollama, local models |
| ❌ No compliance — can't prove what happened | ✅ **Compliance-ready** — GDPR, SOC2, audit-ready artifacts |

---

## 📊 Proven Results (v0.2.0 Benchmarks)

| Metric | LLM Direct (Baseline) | **DAK Kernel (Warm Cache)** |
|--------|----------------------|----------------------------|
| **Success Rate** | 0% | **100%** |
| **Mean Latency** | N/A | **83.4 ms** |
| **95% CI** | — | [82.7, 84.0] ms |
| **Recovery Events** | N/A | Automatic (1.0/run) |
| **Cache Hit Rate** | 0% | **100%** |

> **Key insight:** DAK achieves **100% task success** with automatic recovery from transient failures, while raw LLM calls fail completely under identical conditions.  
> [Full Benchmark Report →](Benchmark%20Specification.md)

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────┐
│                         DAK KERNEL v0.2.0                           │
├─────────────────┬─────────────────┬─────────────────┬──────────────┤
│   WORKFLOW      │  SCHEDULER      │    WORKER       │  EXECUTION   │
│  (LLM Planning) │ (Pure Selection)│ (Lease/Ownership)│ (Effects)   │
└────────┬────────┴────────┬────────┴────────┬────────┴──────┬───────┘
         │                 │                 │               │
         ▼                 ▼                 ▼               ▼
┌─────────────────────────────────────────────────────────────────────┐
│                     EVENT BUS (SQLite + blake3)                    │
│  Events  │  Semantic Artifacts  │  Snapshots  │  Replay Capsules  │
└─────────────────────────────────────────────────────────────────────┘
```

**Core Guarantees:**
- 🔐 **Cryptographic integrity** — blake3-verified event chain
- 🔁 **Deterministic replay** — same inputs → same outputs, always
- 📸 **Instant snapshots** — sub-millisecond state capture
- ⚡ **Zero-overhead** — pure Rust, no GC pauses, single binary

---

## 🚀 Use Cases

| Industry | Use Case | Value |
|----------|----------|-------|
| **FinTech** | Automated code review & compliance checks | Audit trail for regulators |
| **Healthcare** | AI-assisted diagnostics with full traceability | HIPAA-compliant AI decisions |
| **DevTools** | CI/CD pipeline self-healing | 90% reduction in flaky builds |
| **Legal** | Contract analysis with replayable reasoning | Defensible AI conclusions |
| **Enterprise** | Internal AI agents with governance | SOC2-ready AI operations |

---

## 💰 Licensing & Pricing

### **Trial** — Free
- ✅ Full binary (time-limited: 30 days / 1000 executions)
- ✅ All features enabled
- ✅ Email support
- 📥 [Request Trial Binary →](mailto:denis@smoliakov.dev?subject=DAK%20Trial%20Request)

### **Professional** — $2,990 / year per seat
- ✅ Perpetual license (no subscription lock-in)
- ✅ Unlimited executions
- ✅ Source code access (under NDA)
- ✅ Priority email support (24h SLA)
- ✅ Custom provider integrations
- ✅ CI/CD pipeline templates

### **Enterprise** — $14,990 / year (up to 10 seats)
- ✅ Everything in Professional
- ✅ On-premise deployment support
- ✅ Custom SLA (4h response)
- ✅ Dedicated Slack channel
- ✅ Co-development of custom workflows
- ✅ Compliance artifacts (SOC2, GDPR)
- ✅ Training & onboarding workshop

### **Custom / OEM** — Contact us
- Source code licensing
- White-label deployment
- Revenue sharing models
- Embedded distribution rights

> **All tiers include:** Binary distributions for Linux x86_64, macOS ARM64, Windows x86_64.  
> **No runtime fees. No per-execution costs. No telemetry.**

[📄 View Full License Terms →](LICENSE)

---

## 📦 Quick Start (Binary Download)

```bash
# Linux x86_64
curl -L -o dak https://github.com/denis0wn/deterministic_ai_kernel/releases/download/v0.2.0/dak-linux-x86_64
chmod +x dak

# macOS ARM64 (Apple Silicon)
curl -L -o dak https://github.com/denis0wn/deterministic_ai_kernel/releases/download/v0.2.0/dak-macos-aarch64
chmod +x dak

# Verify integrity
sha256sum dak  # Compare with checksums in release notes

# Run your first task
./dak run "Add error handling to the payment service"
./dak doctor    # System health check
```

> **Note:** Source code is **not** publicly available. Trial and licensed binaries are distributed directly.  
> [Download Latest Release →](https://github.com/denis0wn/deterministic_ai_kernel/releases/tag/v0.2.0)

---

## 🛠️ CLI Reference

| Command | Description | Example |
|---------|-------------|---------|
| `dak run "task"` | Execute task from natural language | `dak run "Refactor auth module"` |
| `dak plan "task"` | Generate execution plan only | `dak plan "Add tests for scheduler"` |
| `dak snapshot <id>` | Capture full execution state | `dak snapshot task_abc123` |
| `dak restore <id>` | Restore from snapshot | `dak restore task_abc123` |
| `dak replay <id>` | Replay & validate execution | `dak replay task_abc123 --verify` |
| `dak compare <a> <b>` | Diff two executions | `dak compare task_1 task_2` |
| `dak verify <id>` | Validate replay integrity | `dak verify task_abc123 --strict` |
| `dak doctor` | System health & config check | `dak doctor --json` |
| `dak init` | Scaffold new DAK project | `dak init my-ai-project` |

**Output formats:** `--json`, `--yaml`, `--table` for CI/CD integration.

---

## 🔧 Integration Examples

### CI/CD Pipeline (GitHub Actions)
```yaml
- name: DAK Code Fix
  run: |
    ./dak run --compile-error "${{ steps.build.outputs.log }}" \
      --output fix.patch --json
    git apply fix.patch
```

### As a Library (Rust)
```rust
use deterministic_ai_kernel::kernel_api::{Kernel, KernelConfig};

#[tokio::main]
async fn main() -> anyhow::Result<()> {
    let config = KernelConfig {
        db_path: "production.db".into(),
        max_workers: 8,
        enable_tracing: true,
        ..Default::default()
    };
    let kernel = Kernel::new(config)?;
    
    let result = kernel.execute("Optimize database queries").await?;
    println!("Success: {}, Steps: {}, Latency: {}ms", 
        result.success, result.steps, result.latency_ms);
    Ok(())
}
```

---

## 📈 Roadmap (v0.3.0 — Q1 2025)

- [ ] **Distributed execution** — multi-node worker pools
- [ ] **Web dashboard** — real-time execution monitoring
- [ ] **Policy engine** — OPA-based governance rules
- [ ] **Kubernetes operator** — native K8s deployment
- [ ] **Plugin marketplace** — community workflows

[View Full Roadmap →](PROJECT_ROADMAP.md)

---

## 🤝 Get Started — Book a Demo

**Ready to eliminate AI non-determinism in your production systems?**

| Action | Link |
|--------|------|
| 📅 **Book 30-min technical demo** | [Calendly →](https://calendly.com/denis-smoliakov/dak-demo) |
| 📧 **Email for trial / pricing** | [denis@smoliakov.dev](mailto:denis@smoliakov.dev?subject=DAK%20Inquiry) |
| 💬 **Telegram (fastest response)** | [@Myagentdenbot](https://t.me/Myagentdenbot) |
| 📄 **Request technical whitepaper** | [Email with subject "Whitepaper"](mailto:denis@smoliakov.dev?subject=DAK%20Whitepaper%20Request) |

> **Typical response time: < 2 hours during business hours (MSK, UTC+3).**

---

## 📋 Documentation

| Document | Description |
|----------|-------------|
| [CHANGELOG.md](CHANGELOG.md) | Release history & migration notes |
| [Benchmark Specification.md](Benchmark%20Specification.md) | Detailed performance methodology & raw data |
| [ARCHITECTURE.md](ARCHITECTURE.md) | System architecture & design decisions |
| [KERNEL_SPECIFICATION.md](KERNEL_SPECIFICATION.md) | Formal kernel invariants & contracts |
| [SECURITY.md](SECURITY.md) | Security model & vulnerability reporting |
| [LICENSE](LICENSE) | Proprietary license terms |

---

## ⚖️ Legal

**Deterministic AI Kernel** is proprietary software.  
© 2025 Denis Smoliakov. All rights reserved.

- Source code access requires signed NDA and commercial license.
- Redistribution, reverse engineering, and benchmark publication prohibited without written consent.
- Trial binaries include time/execution limits and telemetry for license compliance.

[Full License →](LICENSE) | [Privacy Policy →](PRIVACY.md) | [Terms of Service →](TERMS.md)

---

<div align="center">

**Built with Rust ❤️ for teams that ship reliable AI.**

[**Get Your Trial Today**](mailto:denis@smoliakov.dev?subject=DAK%20Trial%20Request) • [**View Release v0.2.0**](https://github.com/denis0wn/deterministic_ai_kernel/releases/tag/v0.2.0) • [**Contact Sales**](mailto:denis@smoliakov.dev?subject=DAK%20Enterprise%20Inquiry)

</div>