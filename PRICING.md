# DAK — Pricing & Licensing Details

## License Tiers Comparison

| Feature | Trial | Professional | Enterprise | Custom/OEM |
|---------|-------|--------------|------------|------------|
| **Price** | Free | $2,990/yr/seat | $14,990/yr (10 seats) | Negotiated |
| **License Type** | Time-limited | Perpetual | Perpetual | Perpetual |
| **Executions** | 1,000 / 30 days | Unlimited | Unlimited | Unlimited |
| **Seats** | 1 | 1 | 10 | Custom |
| **Binary Access** | ✅ | ✅ | ✅ | ✅ |
| **Source Code (NDA)** | ❌ | ✅ | ✅ | ✅ |
| **Custom Providers** | ❌ | ✅ | ✅ | ✅ |
| **Support** | Email (best effort) | Email (24h SLA) | Slack + Email (4h SLA) | Dedicated |
| **On-Premise Deploy** | ❌ | Self-serve | Assisted | Full support |
| **Compliance Artifacts** | ❌ | ❌ | SOC2, GDPR, ISO | Custom |
| **Training/Onboarding** | Docs only | Video call (1h) | Workshop (1 day) | Custom |
| **Co-development** | ❌ | ❌ | ✅ (quarterly) | ✅ (ongoing) |
| **White-label** | ❌ | ❌ | ❌ | ✅ |
| **Revenue Share** | ❌ | ❌ | ❌ | ✅ |

---

## What's Included in Every Tier

### Binary Distributions
- Linux x86_64 (glibc 2.31+, musl optional)
- macOS ARM64 (Apple Silicon, macOS 12+)
- Windows x86_64 (Windows 10/11, signed)

### Core Features
- Deterministic task execution & replay
- Cryptographic receipts (blake3)
- Snapshots & time-travel debugging
- Planner hardening (LLM validation)
- Code fix automation (compile/test/lint)
- Provider architecture (LLM, Storage, Embeddings)
- `dak doctor` health checks
- JSON/YAML/Table output for CI/CD

### Documentation & Examples
- Complete CLI reference
- Integration guides (GitHub Actions, GitLab CI, Jenkins)
- Rust library API docs
- Architecture & specification docs

---

## License Terms Summary

### Trial License
- **Duration:** 30 days from first execution or 1,000 executions (whichever comes first)
- **Telemetry:** Anonymous usage ping on startup (version, platform, execution count)
- **Restrictions:** No production use, no redistribution, no reverse engineering
- **Conversion:** Trial key converts to full license on purchase

### Professional License
- **Perpetual:** License never expires. You own v0.2.x forever.
- **Updates:** 1 year of free updates (v0.2.x → v0.3.x, etc.)
- **Renewal:** $1,495/yr for continued updates (optional)
- **Source:** Available under NDA for audit/customization
- **Transfer:** License transferable within organization (notify us)

### Enterprise License
- **Everything in Professional** plus:
- **Multi-seat:** Up to 10 named developers
- **SLA:** 4-hour response during business hours (MSK)
- **Deploy:** On-premise, air-gapped, Kubernetes, VM
- **Compliance:** We provide SOC2 Type II mapping, GDPR DPA, ISO 27001 controls
- **Custom Workflows:** We co-develop 2 custom workflows/quarter

### Custom/OEM License
- **Source code licensing** (perpetual, royalty-free for internal use)
- **White-label:** Remove DAK branding, use your own
- **Embedding:** Distribute as part of your commercial product
- **Revenue share:** Negotiated percentage of your product revenue
- **Joint IP:** Co-owned improvements option

---

## Payment & Procurement

| Method | Details |
|--------|---------|
| **Wire Transfer** | Preferred for Enterprise/Custom (net 30) |
| **Credit Card** | Stripe link on invoice (Professional) |
| **Crypto** | USDC/USDT on Ethereum/Base (5% discount) |
| **Purchase Order** | Accepted for Enterprise+ (PO required) |
| **Reseller** | 20% margin for authorized partners |

**VAT:** Russian VAT (20%) applied for RU entities. Reverse charge for EU B2B with valid VAT ID.

---

## FAQ

### Can I try before buying?
Yes. Email `denis@smoliakov.dev` with subject "DAK Trial Request" — include:
- Company name & website
- Use case (1-2 sentences)
- Platform (Linux/macOS/Windows)
- Expected monthly executions

We'll send a personalized trial binary within 2 hours.

### What happens after trial expires?
The binary stops executing tasks and prints a license expiry message. Your data (snapshots, event logs) remains intact and accessible with a licensed binary.

### Can I run DAK in CI/CD without a seat license?
Yes. CI/CD runners don't count as seats. Only interactive developers need seats.

### Is there a volume discount?
- 5+ Professional seats: 15% off
- 10+ Professional seats: 25% off (consider Enterprise)
- Educational/Non-profit: 50% off (application required)

### What if I need a feature not in the roadmap?
Professional: Submit feature request — prioritized by demand.
Enterprise: Co-development included — we build it with you.
Custom: Dedicated engineering time available.

### Do you offer support for older versions?
Professional: Current + 1 previous minor version.
Enterprise: Current + 2 previous minor versions + security patches for 3 years.
Custom: Negotiated LTS (Long Term Support) available.

---

## Next Steps

1. **Trial Request:** `denis@smoliakov.dev` → receive binary in < 2 hours
2. **Technical Demo:** [Book 30-min call](https://calendly.com/denis-smoliakov/dak-demo)
3. **Quote/Invoice:** Reply to trial email with tier choice → receive invoice
4. **Onboarding:** License key + source access (if applicable) + Slack invite (Enterprise+)

---

## Contact

**Sales & Licensing:** denis@smoliakov.dev  
**Technical Questions:** [GitHub Discussions](https://github.com/denis0wn/deterministic_ai_kernel/discussions)  
**Security Issues:** security@smoliakov.dev (PGP: `0x...`)  
**Telegram:** [@Myagentdenbot](https://t.me/Myagentdenbot)

*All prices in USD. Subject to change. Licenses governed by Russian Federation law.*