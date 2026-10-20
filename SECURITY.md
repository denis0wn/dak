# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 0.1.x   | ✅ Yes             |
| < 0.1   | ❌ No              |

## Reporting a Vulnerability

**Please do NOT report security vulnerabilities through public GitHub issues.**

Instead, please report them via email to: **security@dak.dev**

You should receive a response within 48 hours. If for some reason you do not, please follow up via email to ensure we received your original message.

Please include the following information in your report:

1. **Description** of the vulnerability
2. **Steps to reproduce** the issue
3. **Potential impact** (what could an attacker achieve?)
4. **Suggested fix** (if you have one)
5. **Your contact information** for follow-up

## Response Process

1. **Acknowledgment** - We'll confirm receipt within 48 hours
2. **Assessment** - We'll evaluate the severity and impact
3. **Fix Development** - We'll develop and test a fix
4. **Disclosure Coordination** - We'll coordinate disclosure timeline with you
5. **Release** - We'll release a patched version
6. **Public Disclosure** - We'll publish a security advisory (typically 7-30 days after fix)

## Security Best Practices for Users

### Configuration
- Store configuration files (`.dak/config.toml`) outside of version control
- Use environment variables for sensitive settings
- Review `dak doctor` output regularly for security-relevant issues

### API Keys & Tokens
- Never commit API keys, tokens, or credentials to git
- Use secret management (1Password, Bitwarden, HashiCorp Vault)
- Rotate keys periodically

### Execution Safety
- DAK executes code in isolated contexts, but always review generated code before running in production
- Use `--dry-run` to preview execution plans
- Enable `enable_tracing = true` in config for audit trails

### Replay Integrity
- Replay validation uses cryptographic hashes (BLAKE3)
- Verify `replay_valid: true` in execution results
- Store snapshots securely for audit purposes

## Threat Model

DAK is designed with the following threat model:

| Threat | Mitigation |
|--------|------------|
| Supply chain attack | Cargo.lock pinned, `cargo audit` in CI, minimal dependencies |
| Malicious LLM output | Sandbox execution, capability-based permissions, human review gates |
| State tampering | Cryptographic receipts, BLAKE3 hashing, append-only event log |
| Data exfiltration | No network access by default, explicit provider configuration required |
| Replay manipulation | Deterministic seeds, Merkle proofs, snapshot versioning |

## Security-Related Dependencies

We minimize dependencies and regularly audit:

- `ring` / `aws-lc-rs` - Cryptography (BLAKE3, Ed25519)
- `rusqlite` - SQLite with security updates
- `reqwest` - HTTP client (TLS via `rustls`)
- `tokio` - Async runtime
- `clap` - CLI parsing

Run `cargo audit` locally to check current status.

## Disclosure Timeline

| Severity | Target Fix | Public Disclosure |
|----------|------------|-------------------|
| Critical | 7 days     | 7 days after fix  |
| High     | 14 days    | 14 days after fix |
| Medium   | 30 days    | 30 days after fix |
| Low      | 90 days    | 90 days after fix |

## Bug Bounty

We don't currently have a formal bug bounty program, but we recognize and credit security researchers in our release notes and security advisories.

## Contact

- Security email: security@dak.dev
- PGP Key: Available on keys.openpgp.org (search for security@dak.dev)
- GitHub Security Advisories: https://github.com/denis0wn/deterministic_ai_kernel/security/advisories