# DAK ROI Calculator

**Use this template to quantify DAK value for prospects. Customize per conversation.**

---

## The Math: Cost of NOT Having DAK

### 1. Lost Enterprise Deals (Direct Revenue Impact)

| Metric | Your Input | Calculation |
|--------|------------|-------------|
| Enterprise deals in pipeline | ___ | |
| Avg deal size (ARR) | $___ | |
| % Deals blocked by security/compliance review | ___% | |
| **Annual revenue at risk** | | `Deals × Deal Size × % Blocked` |

**Example:** 5 deals × $200K × 40% = **$400K/year at risk**

---

### 2. Extended Sales Cycles (Time Value)

| Metric | Your Input | Calculation |
|--------|------------|-------------|
| Current avg sales cycle | ___ days | |
| Extension due to security review | ___ days | |
| Deals/year | ___ | |
| **Revenue delayed per year** | | `Deals × Deal Size × (Extension/365)` |

**Example:** 10 deals × $150K × (90/365) = **$370K delayed revenue**

---

### 3. Engineering Opportunity Cost (Build vs Buy)

| Role | Count | Fully Loaded Cost/yr | Months to Build | Total Cost |
|------|-------|---------------------|-----------------|------------|
| Senior Rust Engineer | ___ | $___ | ___ | $___ |
| Platform Engineer | ___ | $___ | ___ | $___ |
| Security/Compliance Eng | ___ | $___ | ___ | $___ |
| **Total Build Cost** | | | | **$___** |
| **DAK Professional (5 seats)** | | | | **$14,950/yr** |
| **Savings (Year 1)** | | | | **$___** |

**Example:** 3 engineers × $250K × 12 months = **$750K build cost** vs **$15K DAK** = **$735K savings**

---

### 4. Flaky CI/CD Costs

| Metric | Your Input | Calculation |
|--------|------------|-------------|
| CI runs/day | ___ | |
| Flake rate | ___% | |
| Avg debug time per flake | ___ min | |
| Engineer cost/hour | $___ | |
| **Annual flaky CI cost** | | `Runs × 250 × Flake% × DebugMin/60 × HourlyCost` |

**Example:** 200 runs × 250 × 15% × 30min × $150 = **$1.69M/year**

---

### 5. Compliance Remediation & Audit Risk

| Risk | Probability | Cost if Realized | Expected Value |
|------|-------------|------------------|----------------|
| Audit finding (SOC 2) | ___% | $___ | $___ |
| HIPAA violation | ___% | $___ | $___ |
| PCI-DSS non-compliance | ___% | $___ | $___ |
| GDPR fine (4% revenue) | ___% | $___ | $___ |
| **Total Expected Risk Cost** | | | **$___** |

---

## The DAK Investment

### Pricing Tiers

| Tier | Annual Cost | Best For |
|------|-------------|----------|
| **Trial** | Free (30 days / 1K execs) | Evaluation |
| **Professional** | $2,990/yr/seat | Teams 1-10, source under NDA |
| **Enterprise** | $14,990/yr (10 seats) | Teams 10+, compliance, SLA |
| **Custom/OEM** | Negotiated | Platform embedding, white-label |

---

## ROI Scenarios

### Scenario A: FinTech Startup (Series B, 50 engineers)
- **Pain:** First enterprise customer demands SOC 2, security review blocking deal
- **Deals at risk:** 3 × $200K = $600K ARR
- **Build cost:** 2 engineers × 12 months = $600K
- **DAK Professional (5 seats):** $14,950/yr
- **ROI:** **3,900%** (Year 1) | **Payback:** < 1 week

### Scenario B: HealthTech (Series C, 100 engineers)
- **Pain:** HIPAA audit controls for AI clinical agents, 6-year retention
- **Audit risk:** HIPAA fines up to $1.5M/violation
- **Build cost:** 3 engineers × 18 months = $1.35M
- **DAK Enterprise:** $14,990/yr
- **ROI:** **8,900%** (Year 1) | **Payback:** Immediate

### Scenario C: AI Infrastructure Platform (Series B, 30 engineers)
- **Pain:** Customers (enterprises) demand deterministic agents for their compliance
- **OEM Opportunity:** Embed DAK in platform, charge premium
- **Build cost:** 4 engineers × 12 months = $1.2M
- **DAK Custom/OEM:** $100K-200K/yr (negotiated)
- **ROI:** **500-1,000%** + new revenue stream

---

## Quick ROI Formula for Conversations

```
ROI = (Revenue Protected + Engineering Savings + Risk Reduction) / DAK Annual Cost
```

**Typical Range:** **500% — 10,000%+** depending on vertical and deal size

---

## How to Present in Demo/Call

1. **Ask discovery questions** to fill the calculator
2. **Show their numbers** back to them
3. **Compare:** "You're risking $X/year. DAK costs $Y/year. That's Z% ROI."
4. **Anchor:** "One closed deal pays for 5-10 years of DAK."

---

## Customization per Vertical

### FinTech
- Focus: PCI-DSS, SOX, lost deals due to security review
- Metric: Revenue delayed per deal × deals in pipeline

### HealthTech
- Focus: HIPAA 6-year retention, FDA SaMD, patient safety
- Metric: Audit risk ($1.5M/violation) vs DAK cost

### LegalTech
- Focus: EU AI Act, ABA Model Rules, privilege protection
- Metric: Deal velocity (60-120 day security review reduction)

### AI Infra / Platform
- Focus: OEM embedding, customer demand for deterministic agents
- Metric: New revenue stream + customer retention

---

*Bring this calculator to every demo. Fill it live with the prospect.*