# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- **CLI v2** (`dak`): Modern command-line interface with subcommands, JSON output, shell completions
- **Provider Architecture**: Pluggable LLM, Storage, and Embedding backends behind traits
- **Task Input Enums**: `TaskInput::Direct`, `TaskInput::CompileError`, `TaskInput::TestFailure`, `TaskInput::LintReport`
- **Code Fix Commands**: `--compile-error`, `--test-failure`, `--lint-report` flags for automated fixing
- **Planner Hardening**: `--planner-hardening` flag for enhanced LLM planning validation
- **Doctor Command**: System health checks (Ollama, models, memory, disk)
- **Verify Command**: Replay validation for any task ID
- **Compare Command**: Side-by-side task execution comparison
- **Init Command**: Project scaffolding with `.dak/` config
- **Shell Completions**: Bash, Zsh, Fish completion generation
- **Kernel API**: Public `Kernel`, `KernelConfig`, `ExecutionResult`, `DoctorReport`, `SnapshotInfo`, `CapsuleSummary`, `CapsuleComparison`
- **Compat Module**: Centralized domain types (`StepKind`, `WorkerCapability`, `StepOutcome`, `TaskClass`) with serde support
- **Quickstart Example**: `examples/quickstart.rs` demonstrating basic usage
- **CodeFix Example**: `examples/codefix.rs` end-to-end bug fix demonstration with audit trail

### Changed
- **BREAKING**: Moved `StepKind`, `WorkerCapability`, `StepOutcome`, `TaskClass` to `compat` module
- **BREAKING**: Storage provider now uses generic constructor `SqliteStorage::new(path)`
- **BREAKING**: All direct `std::fs` calls replaced with `StorageProvider` trait
- **BREAKING**: All direct LLM calls routed through `LlmProvider` trait
- **BREAKING**: `SystemTime::now()` replaced with logical clock in scheduler
- **BREAKING**: `exec_spec` ↔ `contract` cycle broken via `compat` module
- Improved test reliability with `#[tokio::test(flavor = "multi_thread")]`
- Updated `architecture_invariants` tests for stricter primitive kind enforcement

### Fixed
- Fixed planner memoization test flakiness
- Fixed replay validation race conditions
- Fixed snapshot artifact reference handling
- Fixed semantic bias replay equivalence

### Security
- Added `cargo-audit` to CI pipeline
- Added dependency license checking with `cargo-deny`
- Added secret scanning in CI

## [0.2.0] - 2025-10-19

### Added
- **CodeFix Flow**: Automated bug fixing from compile errors, test failures, and lint reports
- **PatchCode Primitive**: `repo.apply_patch.canonical` for applying unified diffs
- **Planner Hardening Flow**: Validated LLM-generated plans with critic review
- **Enhanced Worker Assignment**: Deterministic capability-based routing (`default_worker_for_step`)
- **Artifact Writing Loop**: Persistent artifact storage with generation tracking
- **Extended CLI**: `dak` binary with 18 subcommands + shell completions
- **Binary Distribution**: `cargo-dist` config for cross-platform binaries (tar.gz, zip, Homebrew, npm, MSI)

### Changed
- Quickstart example updated to use Planner Hardening flow
- Worker assignment centralized in `compat::required_capability_for_step`
- Event bus schema versioning with `event_bus/schema.sql` included in package
- Semantic bias artifacts now included in snapshots

### Fixed
- Missing primitive binding for `ExecuteChanges` and `PatchCode` steps
- Artifact writing now uses `get_filesystem` provider correctly
- All clippy warnings resolved (unused, dead_code)
- Test determinism across seed permutations

### Security
- No known vulnerabilities
- All dependencies pass `cargo audit`

## [0.1.0] - 2025-10-18

### Added
- Initial release of Deterministic AI Kernel
- Event bus with SQLite persistence
- Scheduler with deterministic selection
- Worker with lease-based ownership
- Execution runtime with effect handling
- Workflow compiler with LLM planning
- Replay engine with capsule validation
- Snapshot system with versioned state
- Semantic artifact system (analysis_seed, retrieval_result, classification)
- Model registry with local model management
- Runtime manager for MLX/Ollama processes
- Developer test runner (`./ct`)
- Comprehensive test suite (138 unit tests + 19 architecture invariant tests)

### Security
- No known vulnerabilities at release

---

## Release Process

Releases are automated via `cargo-dist`:

1. Update version in `Cargo.toml`
2. Update this CHANGELOG.md
3. Create and push tag: `git tag vX.Y.Z && git push origin vX.Y.Z`
4. GitHub Actions builds cross-platform binaries
5. Homebrew tap updated automatically
6. Cargo publish (when configured)
7. GitHub Release created with artifacts

## Links

- [GitHub Releases](https://github.com/denis0wn/deterministic_ai_kernel/releases)
- [GitHub Commits](https://github.com/denis0wn/deterministic_ai_kernel/commits/main)
- [Compare v0.1.0...HEAD](https://github.com/denis0wn/deterministic_ai_kernel/compare/v0.1.0...HEAD)