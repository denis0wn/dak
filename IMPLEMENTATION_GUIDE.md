# DAK Implementation Guide

**For:** Trial users, new customers, solution architects  
**Audience:** Engineers implementing DAK in their stack

---

## Quick Start (5 Minutes)

```bash
# 1. Download your trial binary
# Linux:
curl -L -o dak https://github.com/denis0wn/dak/releases/download/v0.2.0/dak-linux-x86_64
# macOS:
curl -L -o dak https://github.com/denis0wn/dak/releases/download/v0.2.0/dak-macos-aarch64

# 2. Make executable
chmod +x dak

# 3. Verify installation
./dak doctor

# 4. Run your first task
./dak run "Add error handling to payment service"

# 5. Verify deterministic replay
./dak replay <session-id> --verify
```

**Expected Output:**
```
✅ SUCCESS • 4 steps • 1,847ms • Cache: 100% hit
📸 Snapshot: task_abc123_snap_001
🔐 Receipt: blake3:a1f4b2e5c3d6e7f8...
🔁 Replay: dak replay task_abc123 --verify
```

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                     YOUR AGENT FRAMEWORK                    │
│  (LangGraph, CrewAI, AutoGen, Custom — unchanged)           │
└─────────────────────────────┬───────────────────────────────┘
                              │ DAK Provider Interface
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    DAK EXECUTION KERNEL                     │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │  Planner    │  │ Scheduler   │  │  Executor   │         │
│  │ (validated) │  │ (DAG +      │  │ (compile/   │         │
│  │  LLM out)   │  │  leases)    │  │  test/lint) │         │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘         │
│         │                │                │                  │
│         └────────────────┼────────────────┘                  │
│                          ▼                                    │
│              ┌───────────────────────┐                        │
│              │  RECEIPT GENERATOR    │                        │
│              │  (blake3 + Merkle)    │                        │
│              └───────────┬───────────┘                        │
│                          ▼                                    │
│              ┌───────────────────────┐                        │
│              │  EVENT STORE (SQLite) │                        │
│              │  Append-only, signed  │                        │
│              └───────────────────────┘                        │
└─────────────────────────────────────────────────────────────┘
```

---

## Integration Patterns

### Pattern 1: LangGraph Wrapper (Recommended)

```python
# pip install dak-langgraph  (v0.4+)
from dak_langgraph import DAKWorker

# Your existing LangGraph chain
from langgraph.graph import StateGraph

graph = StateGraph(MyState)
graph.add_node("agent", my_agent)
graph.add_node("tool", my_tool)
graph.set_entry_point("agent")

# Wrap in DAK worker — zero code changes to your logic
worker = DAKWorker(
    graph=graph.compile(),
    session_id="prod-payment-{{timestamp}}",
    enable_tracing=True,
    enable_replay=True
)

# Execute with deterministic guarantees
result = worker.invoke({"input": "Process refund for order #12345"})

# Verify replay
receipt = worker.get_receipt()
assert receipt.replay_valid == True
```

### Pattern 2: CLI Subprocess (Any Language)

```python
import subprocess
import json

def run_dak_task(task: str, session_id: str) -> dict:
    result = subprocess.run(
        ["./dak", "run", task, "--session", session_id, "--json"],
        capture_output=True,
        text=True
    )
    return json.loads(result.stdout)

# Usage
output = run_dak_task(
    "Generate SQL migration for new payments table",
    session_id=f"migration-{timestamp}"
)

# Verify replay
verify_result = subprocess.run(
    ["./dak", "replay", output["session_id"], "--verify", "--json"],
    capture_output=True,
    text=True
)
assert json.loads(verify_result.stdout)["replay_valid"] == True
```

### Pattern 3: REST API (v0.4+)

```bash
# Start DAK API server
./dak serve --port 8080 --enable-tracing

# Execute task
curl -X POST http://localhost:8080/execute \
  -H "Content-Type: application/json" \
  -d '{"task": "Refactor authentication module", "session_id": "auth-refactor-001"}'

# Verify replay
curl -X POST http://localhost:8080/replay/auth-refactor-001/verify

# Get compliance report
curl -X POST http://localhost:8080/compliance/auth-refactor-001 \
  -d '{"framework": "soc2"}'
```

---

## Configuration

### `~/.dak/config.toml`

```toml
# Execution settings
[execution]
max_steps = 100
timeout_seconds = 300
enable_snapshots = true
snapshot_interval = 5  # steps

# Tracing & Replay
[tracing]
enabled = true
storage_path = "~/.dak/traces"
retention_days = 90

# Replay verification
[replay]
verify_on_completion = true
strict_mode = true  # Fail if any deviation detected

# Providers
[providers.openai]
api_key = "${OPENAI_API_KEY}"
model = "gpt-4o"
temperature = 0.0  # Deterministic!

[providers.anthropic]
api_key = "${ANTHROPIC_API_KEY}"
model = "claude-3-5-sonnet-20241022"

[providers.local]
endpoint = "http://localhost:11434"
model = "llama3.1:70b"

# Compliance
[compliance]
frameworks = ["soc2", "hipaa", "pci-dss"]
evidence_retention_days = 2555  # 7 years for SOX

# CI/CD Integration
[ci]
fail_on_replay_mismatch = true
upload_artifacts = true
artifact_path = "dak-evidence/"
```

---

## CI/CD Integration

### GitHub Actions

```yaml
# .github/workflows/agent-test.yml
name: Agent Tests with DAK

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Download DAK
        run: |
          curl -L -o dak https://github.com/denis0wn/dak/releases/download/v0.2.0/dak-linux-x86_64
          chmod +x dak
          
      - name: Run Agent with DAK
        run: |
          ./dak run "Run test suite for payment module" \
            --session ci-${{ github.sha }} \
            --verify-replay \
            --config .dak/ci.toml
            
      - name: Upload Compliance Evidence
        uses: actions/upload-artifact@v4
        with:
          name: dak-evidence-${{ github.sha }}
          path: |
            dak-evidence/
            receipts.jsonl
            merkle-root.txt
            compliance-report.json
```

### GitLab CI

```yaml
# .gitlab-ci.yml
dak_test:
  stage: test
  image: rust:latest
  script:
    - curl -L -o dak https://github.com/denis0wn/dak/releases/download/v0.2.0/dak-linux-x86_64
    - chmod +x dak
    - ./dak run "Run integration tests" --session gitlab-$CI_COMMIT_SHA --verify-replay
  artifacts:
    paths:
      - dak-evidence/
    expire_in: 90 days
```

---

## Compliance Reporting

### Generate SOC 2 Evidence Package

```bash
# Single command generates full compliance artifact
./dak compliance-report <session-id> \
  --framework soc2 \
  --output soc2-evidence.json \
  --include-receipts \
  --include-merkle-proofs
```

**Output (`soc2-evidence.json`):**
```json
{
  "session_id": "task_abc123",
  "framework": "SOC 2",
  "criteria_mapped": {
    "CC6.1": ["receipt.actor", "receipt.policy_version", "receipt.authorization"],
    "CC7.2": ["continuous_receipts_stream", "merkle_root_anchoring"],
    "CC8.1": ["plan_hash", "code_hash", "test_hash"],
    "PI.1": ["replay_verification", "zero_deviations"]
  },
  "evidence": {
    "receipts_count": 47,
    "merkle_root": "0x7f3a9b1c...",
    "replay_status": "VERIFIED",
    "deviations": 0
  },
  "auditor_notes": "All execution steps cryptographically chained. Bit-for-bit replay verified."
}
```

### Supported Frameworks

| Framework | Command | Key Artifacts |
|-----------|---------|---------------|
| SOC 2 | `--framework soc2` | CC6.1, CC7.2, CC8.1, PI.1 mapping |
| HIPAA | `--framework hipaa` | 164.312(b) per-PHI-access receipts |
| PCI-DSS | `--framework pci-dss` | 12-month logs, tamper-evident flags |
| GDPR | `--framework gdpr` | Article 30 processing records |
| EU AI Act | `--framework eu-ai-act` | Technical docs, human oversight logs |
| ISO 27001 | `--framework iso27001` | Annex A control evidence |
| ISO 42001 | `--framework iso42001` | Clauses 8.4, 8.5, 9.1 |

---

## Troubleshooting

### Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| `dak: command not found` | Not in PATH | `export PATH=$PATH:$(pwd)` or move to `/usr/local/bin` |
| Replay verification fails | Non-deterministic provider | Set `temperature = 0.0`, pin model versions |
| "Permission denied" | Binary not executable | `chmod +x dak` |
| Out of memory | Large snapshots | Reduce `snapshot_interval` or disable snapshots |
| Provider auth failed | API key not set | Check `config.toml` or env vars |

### Debug Commands

```bash
# Full system check
./dak doctor --verbose

# Dry run (no execution, shows plan)
./dak run "Your task" --dry-run

# Inspect receipts
./dak receipts list --session <id>
./dak receipts show <receipt-id>

# Verify specific replay
./dak replay <session-id> --verify --verbose

# Export all traces
./dak export --format jsonl --output all-traces.jsonl
```

---

## Production Checklist

Before going live:

- [ ] **Provider keys** configured in env (not config file)
- [ ] **Temperature = 0.0** for all LLM providers
- [ ] **Model versions pinned** (e.g., `gpt-4o-2024-08-06`)
- [ ] **Tracing enabled** with retention policy
- [ ] **Replay verification** enabled in CI/CD
- [ ] **Compliance reports** automated for auditors
- [ ] **Snapshot storage** monitored (disk space)
- [ ] **Alerting** on replay failures
- [ ] **Backup** of event store (SQLite file)
- [ ] **Runbook** for incident response

---

## Support

- **Documentation:** https://github.com/denis0wn/dak
- **Trial Issues:** https://github.com/denis0wn/dak/issues/new?template=trial_request.yml
- **Email:** denis@smoliakov.dev
- **Telegram:** @Myagentdenbot
- **Demo Booking:** https://calendly.com/denis-smoliakov/dak-demo

---

*This guide covers v0.2.0. Check releases for updates.*