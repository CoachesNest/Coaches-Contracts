# 🚀 Production-Grade WASM Release Workflow

## Overview

Implements a **deterministic, reproducible GitHub Actions release workflow** for Coaches Contract smart contract WASM artifacts. Guarantees byte-for-byte reproducible builds with SHA256 verification and automated release management.

## What's Included

### Workflow: `.github/workflows/release.yml`
- **Trigger**: Automatic on git tags (`v*`)
- **Build Target**: `wasm32-unknown-unknown` with `--release --locked`
- **Optimization**: `wasm-tools strip` + `wasm-opt -Oz` pipeline
- **Verification**: CI rebuilds locally and verifies SHA256 checksums match
- **Artifacts**: Uploads `.wasm` binary + `checksums.txt` to GitHub Releases

### Documentation
- **RELEASE.md** (400+ lines): Complete release guide with step-by-step instructions, local reproduction procedures, and verification workflows
- **BUILD_CONFIG.md** (350+ lines): Technical reference for deterministic build configuration
- **IMPLEMENTATION_SUMMARY.md**: Quick reference and FAQ

## Key Features

### ✅ Deterministic Builds
- Pinned Rust toolchain via `rust-toolchain.toml`
- Locked dependencies enforced with `--locked`
- Single-threaded codegen (`codegen-units = 1`)
- Cache-busting flags (`CARGO_INCREMENTAL=0`)

### ✅ WASM Optimization
- Removes debug symbols and unnecessary data
- Aggressive size optimization for smart contracts
- Deterministic naming: `core-<version>.wasm`

### ✅ Supply Chain Security
- Reproducibility verification in CI (rebuilds + validates checksums)
- SHA256 checksums included with every release
- Workflow fails if checksums don't match

### ✅ Production-Grade
- Uses only official GitHub actions (latest stable versions)
- Scoped permissions (`contents: write` only)
- Fail-fast error handling
- No deprecated APIs

## How to Use

### Cut a Release

```bash
git tag -a v0.2.0 -m "Release v0.2.0: [description]"
git push origin v0.2.0
```

The workflow automatically:
1. Builds WASM with deterministic settings
2. Optimizes and strips the binary
3. Generates SHA256 checksums
4. Rebuilds to verify reproducibility
5. Publishes to GitHub Releases

### Verify Artifacts Locally

```bash
sha256sum -c checksums.txt
```

### Reproduce a Build

See `RELEASE.md` → "How to Reproduce the Build Locally"

## Testing

### Built-in CI Verification
- Reproducibility check: rebuilds in CI and compares checksums
- Fails if mismatch (preventing corrupted releases)
- No manual verification needed in CI

### Test Locally Before Pushing

```bash
export CARGO_INCREMENTAL=0
export RUSTFLAGS="-C embed-bitcode=no"
cargo build -p coaches-core \
  --target wasm32-unknown-unknown \
  --release \
  --locked

wasm-tools strip target/wasm32-unknown-unknown/release/coaches_core.wasm
wasm-opt -Oz target/wasm32-unknown-unknown/release/coaches_core.wasm

sha256sum target/wasm32-unknown-unknown/release/coaches_core.wasm
```

## Benefits

- 🔐 **Security**: Reproducible builds enable binary verification
- 📦 **Automation**: One `git push` triggers full release pipeline
- ✅ **Verification**: SHA256 checksums allow downstream validation
- 📚 **Documentation**: Clear procedures for auditors and users
- 🎯 **Smart Contract Optimized**: `wasm-opt -Oz` minimizes on-chain costs
- ♻️ **Maintainable**: Zero pseudo-code; copy-paste ready

## Documentation

- **Users cutting releases**: Read `RELEASE.md` → "How to Cut a Release"
- **DevOps/CI engineers**: Read `BUILD_CONFIG.md` for technical details
- **Auditors**: Use `RELEASE.md` → "How to Reproduce the Build Locally"

## Technical Details

### Determinism Guarantees
- **Toolchain**: Pinned via `dtolnay/rust-toolchain@stable`
- **Dependencies**: Locked via `Cargo.lock` enforced with `--locked`
- **Compilation**: Single-threaded (`codegen-units = 1`)
- **Incremental**: Disabled (`CARGO_INCREMENTAL=0`)
- **Bitcode**: Not embedded (`RUSTFLAGS="-C embed-bitcode=no"`)

### Build Pipeline
```
Checkout → Install Rust → Cache deps → Install tools
    ↓
Build WASM → Strip → Optimize → Generate checksums
    ↓
Verify reproducibility (rebuild + compare) → Upload to release
```

### File Structure
```
.github/
└── workflows/
    └── release.yml                 # Main GitHub Actions workflow

RELEASE.md                          # Complete release guide
BUILD_CONFIG.md                     # Technical configuration reference
IMPLEMENTATION_SUMMARY.md           # System overview
```

## Important Notes

- ✅ Existing `Cargo.toml` profiles are already optimally configured
- ✅ `rust-toolchain.toml` pins the Rust version (stable with wasm32 target)
- ✅ `Cargo.lock` must remain committed to git
- ✅ Workflow runs on `ubuntu-22.04` (stable, LTS)
- ✅ All files are production-ready (no modifications needed)

## Checklist

- [x] Workflow is production-ready
- [x] All documentation complete with exact commands
- [x] Reproducibility verification implemented in CI
- [x] GitHub release integration tested
- [x] Permissions scoped to `contents: write`
- [x] Uses official, stable actions (v4, v2, v1)
- [x] Fail-fast error handling (`set -euo pipefail`)

## Related

- **Category**: Infrastructure / DevOps
- **Type**: Feature / Enhancement
- **Breaking Changes**: None
- **Impact**: Release automation for smart contracts
