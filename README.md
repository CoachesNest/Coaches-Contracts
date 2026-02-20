## Coaches Contracts 🔗
*Soroban smart contracts for the Coaches platform*

## 📌 About
**Coaches Contracts** contains the smart contracts that power decentralized mentorship agreements on Coaches.

These contracts are written using **Soroban** and deployed on the **Stellar network**, enabling trustless escrow, payments, and reputation tracking.

## ⚙️ Core Contracts
- Mentorship Escrow Contract
- Payment Release Logic
- Reputation & Rating Registry
- Platform Fee Management
- Session Completion Gate

## 🛠 Tech Stack

- Rust
- Soroban SDK
- Stellar CLI

## ⚙️ Setup & Deployment

### Prerequisites
- Rust
- Stellar CLI
- Stellar Testnet Account

### Build Contracts
```bash
# Add WASM target (one-time setup)
rustup target add wasm32-unknown-unknown

# Build the core contract for WASM
cargo build -p coaches-core --target wasm32-unknown-unknown --release

# Build all workspace members
cargo build --release

# Build CLI tools only
cargo build -p coaches-tools --release
```

### Run CLI Tools
```bash
# Deploy contract
cargo run -p coaches-tools -- deploy --network testnet -- wasm target/wasm32-unknown-unknown/release/coaches_core.wasm

# Check configuration
cargo run -p coaches-tools -- config --validate

# Build contracts via CLI
cargo run -p coaches-tools -- build --profile release
```
### Installation
* Install rustup
* ```
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   rustup update stable
   rustup target add wasm32-unknown-unknown

* Install cargo-contract (ink! tool)
* ```
   cargo install cargo-contract --vers ^2.0.0

* (Optional) Install cargo-make
   cargo install cargo-make
  
# To run a local dev node:
```
   * Get a node for local dev (one-off)
      git clone https://github.com/paritytech/substrate-contracts-node
      cd substrate-contracts-node
      cargo build --release
   * Run node in a separate terminal:
      ./target/release/substrate-contracts-node --dev

````

## Project Structure

```
Coaches_Contracts/
├── Cargo.toml              # Workspace configuration
├── README.md               # This file
├── .gitignore              # Git ignore patterns
├── crates/
│   ├── contracts/
│   │   └── core/           # Core Soroban contract library
│   │       ├── Cargo.toml  # Contract dependencies
│   │       └── src/
│   │           └── lib.rs  # Main contract implementation
│   └── tools/              # CLI utilities
│       ├── Cargo.toml      # Tools dependencies
│       └── src/
│           └── main.rs     # CLI entry point
└── target/                 # Build artifacts (gitignored)
```

## Workspace Layout

This is a Cargo workspace containing:
- **crates/contracts/core**: Main Soroban smart contract library
- **crates/tools**: CLI utilities for deployment and configuration management





## DEPLOYMENT

# deploy command (example)
```
cargo +stable contract instantiate \
  --constructor new \
  --suri "//Alice" \
  --endowment 1000000000000000 \
  --salt 0x00 \
  --manifest-path target/ink/metadata.json \
  --wasm target/ink/coaches.wasm



