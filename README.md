# Coaches — Smart Contracts

Soroban smart contracts for the **Coaches** mentorship platform, built on the Stellar network with the Soroban SDK.

## Overview

These contracts power the on-chain logic for the Coaches mentorship platform, including membership, verification, and platform operations. The workspace is built with Rust and targets `wasm32-unknown-unknown` for deployment to the Stellar network.

## Repository Layout

```
crates/
  contracts/
    core/        Core Soroban contract crate
soroban.toml     Network profiles (testnet / mainnet) and configuration
Makefile         Development and build automation
```

## Prerequisites

- [Rust](https://rustup.rs/) with the `wasm32-unknown-unknown` target
- [Soroban CLI](https://soroban.stellar.org/docs/getting-started/setup)

Install all dependencies automatically:

```bash
make install-deps
```

## Development

```bash
# Build the workspace
make build

# Build the contract as a WASM artifact
make wasm

# Run the test suite
make test

# Format and lint
make fmt
make lint
```

## Network Configuration

Networks are managed through `soroban.toml`, which defines profiles for `testnet` and `mainnet`. Select a profile with the `SOROBAN_NETWORK` environment variable:

```bash
SOROBAN_NETWORK=testnet soroban contract deploy ...
```

See `SOROBAN.md` / `TEST_IMPLEMENTATION.md` for detailed network and deployment documentation.

## License

Proprietary — all rights reserved.