# DAK Public Roadmap

**Last Updated:** October 2026  
**Repository:** https://github.com/denis0wn/dak  
**Private Development:** https://github.com/denis0wn/deterministic_ai_kernel

---

## Vision

Build the **deterministic execution layer** that makes AI agents production-legal for regulated enterprises.

> "DAK is not an agent framework. It's the deterministic execution kernel that makes agent frameworks production-legal."

---

## Release History

| Version | Date | Highlights |
|---------|------|------------|
| **v0.2.0** | Oct 2026 | First public release: Linux/macOS/Windows binaries, Tryss demo, cryptographic replay, instant snapshots, trial program |
| **v0.1.x** | Internal | Private development, core kernel, planner/scheduler/executor, event store, receipt generator |

---

## Near Term (Q4 2026 — Q1 2027)

### v0.3.0 — "Compliance Hardening" (Target: Nov 2026)

- [ ] **SOC 2 Evidence Pack** — Native `dak compliance-report --framework soc2` output
- [ ] **HIPAA Audit Controls** — Per-PHI-access receipts, 6-year retention config
- [ ] **PCI-DSS v4.0** — 12-month log retention, 3-month immediate access, tamper-evident flags
- [ ] **EU AI Act Technical Docs** — Auto-generated Annex IV documentation from receipts
- [ ] **ISO 42001 Mapping** — Clause 8.4/8.5/9.1 evidence generation

### v0.4.0 — "Enterprise Integration" (Target: Dec 2026)

- [ ] **LangGraph Native Wrapper** — `pip install dak-langgraph`, drop-in replacement
- [ ] **CrewAI Integration** — `dak-crewai` package, worker abstraction
- [ ] **REST API Gateway** — `/execute`, `/replay`, `/snapshot`, `/compliance` endpoints
- [ ] **Kubernetes Operator** — `DAKCluster` CRD for orchestrated deployments
- [ ] **Prometheus Metrics** — `/metrics` endpoint with execution latency, replay success rate

### v0.5.0 — "Developer Experience" (Target: Jan 2027)

- [ ] **VS Code Extension** — Inline replay, snapshot viewer, trace timeline
- [ ] **CLI Improvements** — `dak init`, `dak doctor --fix`, `dak migrate`
- [ ] **Time-Travel Debugger UI** — Web-based step-through replay
- [ ] **Configuration Schema** — JSON Schema + `dak config validate`
- [ ] **Plugin Architecture** — Custom validators, custom providers, custom sinks

---

## Medium Term (Q2 — Q3 2027)

### v1.0.0 — "Production GA" (Target: Q2 2027)

- [ ] **Windows Native** — Full parity (currently cross-compiled)
- [ ] **ARM64 Linux** — Graviton, Oracle Cloud, Raspberry Pi support
- [ ] **FIPS 140-2 Mode** — For US Federal / Defense customers
- [ ] **Multi-Tenancy** — Organization/workspace isolation in single binary
- [ ] **RBAC** — Role-based access control for team deployments
- [ ] **SLA-Backed Enterprise** — 99.9% uptime, 4-hour response, dedicated Slack

### Platform Integrations

- [ ] **Snowflake Connector** — Direct audit log ingestion
- [ ] **Datadog/Splunk/Elastic** — Native log forwarding
- [ ] **Vanta/Drata/Thoropass** — Compliance automation partnerships
- [ ] **GitHub Actions / GitLab CI / CircleCI** — Native pipeline steps
- [ ] **Terraform Provider** — `dak_binary`, `dak_license` resources

---

## Long Term (2027+)

### v2.0 — "Distributed Determinism"

- [ ] **Cluster Mode** — Multi-node execution with consensus replay
- [ ] **Cross-Region Replication** — Geo-distributed snapshot sync
- [ ] **WASM Workers** — Browser/edge execution with deterministic replay
- [ ] **Policy-as-Code** — OPA/Rego integration for execution guardrails

### Research Areas

- [ ] **Zero-Knowledge Replay** — Prove execution correctness without revealing inputs
- [ ] **Hardware Attestation** — TPM/SGX/SEV integration for hardware-rooted trust
- [ ] **Formal Verification** — Coq/Lean proofs for kernel correctness properties

---

## Commercial Milestones

| Milestone | Target | Status |
|-----------|--------|--------|
| First Trial Request | Oct 2026 | 🎯 In progress |
| First Paid License (Professional) | Nov 2026 | 🎯 Target |
| First Enterprise License | Dec 2026 | 📅 Planned |
| 5th Paid License | Q1 2027 | 📅 Planned |
| $10K MRR | Q1 2027 | 📅 Planned |
| $100K MRR | Q3 2027 | 📅 Planned |
| Series A / Strategic Round | 2027 | 💭 Exploring |

---

## Feedback & Influence

This roadmap is shaped by:

1. **Trial User Feedback** — Direct from `dak trial` users
2. **Enterprise Conversations** — Requirements from POC/POV engagements
3. **Regulatory Changes** — SOC 2, HIPAA, EU AI Act, PCI-DSS updates
4. **Competitive Landscape** — LangGraph, CrewAI, observability platforms

**Want to influence the roadmap?**
- Request a trial → https://github.com/denis0wn/dak/issues/new?template=trial_request.yml
- Book a demo → https://calendly.com/denis-smoliakov/dak-demo
- Email → denis@smoliakov.dev
- Telegram → @Myagentdenbot

---

*Roadmap is indicative, not a commitment. Priorities shift based on customer demand and market signals.*