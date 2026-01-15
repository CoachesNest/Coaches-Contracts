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

## 🛠 Tech Stack

- Rust
- Soroban SDK
- Stellar CLI

## ⚙️ Setup & Deployment

### Prerequisites
- Rust
- Soroban CLI
- Stellar Testnet Account

### Build Contracts
```bash
soroban contract build
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
contracts/
├── Cargo.toml           # workspace or contract top-level (if multiple modules)
├── src/
│   ├── lib.rs           # main ink! contract entry (Coaches)
│   ├── modules/         # modular contract components (separate Rust modules)
│   │   ├── user.rs
│   │   ├── escrow.rs
│   │   ├── reputation.rs
│   │   └── dispute.rs
│   └── utils.rs
├── tests/
│   └── unit_tests.rs    # Rust unit tests (ink! off-chain tests)
├── README.md            # This file
└── .env.example         # Environment / deployment template (RPC endpoints, accounts)

```





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



