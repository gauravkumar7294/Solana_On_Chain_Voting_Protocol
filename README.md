# 🗳️ Solana On-Chain Voting Protocol

A decentralized voting protocol built on the Solana blockchain using the Anchor framework and Rust. This project demonstrates how to create polls, register candidates, and cast votes entirely on-chain while leveraging Solana's high-performance and low-cost infrastructure.

The project also includes a comprehensive integration test suite powered by LiteSVM, enabling fast and deterministic testing of program behavior without requiring a live validator.

---

# 📖 Overview

Traditional voting systems often rely on centralized databases and trusted intermediaries. This project showcases how voting logic can be executed and verified directly on-chain using Solana smart contracts.

The protocol allows:

* Poll creation
* Candidate registration
* Secure vote casting
* Time-based voting restrictions
* Transparent vote counting
* Deterministic account management using Program Derived Addresses (PDAs)

All voting data is stored on-chain, making the process transparent, auditable, and tamper-resistant.

---

# ✨ Features

## Poll Management

* Create and initialize polls
* Configure poll name and description
* Define voting start and end timestamps
* Store poll metadata on-chain

## Candidate Registration

* Register multiple candidates for a poll
* Automatically track candidate count
* Associate candidates with specific polls

## Voting

* Cast votes securely on-chain
* Increment candidate vote counts
* Validate voting periods
* Prevent voting before the poll starts
* Prevent voting after the poll ends

## Account Architecture

* PDA-based account generation
* Deterministic account addresses
* Efficient state management
* Secure account ownership validation

## Testing

* Integration testing with LiteSVM
* Local Solana runtime simulation
* Success-path and failure-path testing
* Account state verification

---

# 🏗️ Tech Stack

| Component     | Technology         |
| ------------- | ------------------ |
| Blockchain    | Solana             |
| Framework     | Anchor             |
| Language      | Rust               |
| Testing       | LiteSVM            |
| Client        | TypeScript         |

---

# 📂 Project Structure

```text
.
├── Anchor.toml
├── Cargo.toml
├── package.json
├── programs
│   └── voting
│       └── src
│           └── lib.rs
├── tests
│   └── litesvm.rs
├── target
└── migrations
```

### Important Files

#### `programs/voting/src/lib.rs`

Contains the core on-chain voting logic including:

* Poll initialization
* Candidate initialization
* Vote casting
* Account validation
* Custom error handling

#### `tests/litesvm.rs`

Contains integration tests built using LiteSVM.

Tests verify:

* Poll creation
* Candidate creation
* Vote casting
* Voting period validation
* Program state updates
* Error handling

---

# 🧠 Program Architecture

## Poll Account

Stores:

```rust
poll_id
poll_name
poll_description
poll_voting_start
poll_voting_end
poll_option_index
```

### Responsibilities

* Maintain poll metadata
* Track voting window
* Track registered candidates

---

## Candidate Account

Stores:

```rust
candidate_name
candidate_votes
```

### Responsibilities

* Candidate information
* Vote tally management

---

# 🔐 Program Derived Addresses (PDAs)

The protocol uses PDAs to create deterministic account addresses.

## Poll PDA

Seeds:

```rust
[
    b"poll",
    poll_id.to_le_bytes()
]
```

This ensures that each poll has a unique and predictable address.

---

## Candidate PDA

Seeds:

```rust
[
    poll_id.to_le_bytes(),
    candidate_name.as_bytes()
]
```

This guarantees uniqueness for each candidate within a poll.

---

# ⚙️ Instructions

## Initialize Poll

Creates a new poll account.

### Parameters

```rust
poll_id
start_time
end_time
name
description
```

### Responsibilities

* Create poll PDA
* Store metadata
* Configure voting window

---

## Initialize Candidate

Creates a candidate account linked to a poll.

### Parameters

```rust
poll_id
candidate_name
```

### Responsibilities

* Create candidate PDA
* Register candidate
* Update candidate count

---

## Vote

Allows users to cast votes for a candidate.

### Parameters

```rust
poll_id
candidate_name
```

### Responsibilities

* Validate poll timing
* Increment vote count
* Persist updated state

---

# 🧪 Testing with LiteSVM

This project includes comprehensive LiteSVM integration tests.

LiteSVM provides:

* Fast execution
* Local Solana runtime simulation
* Deterministic test results
* No external validator dependency

---

## Test Coverage

### Poll Initialization

Verifies:

* Poll creation
* Metadata storage
* Initial state correctness

---

### Candidate Initialization

Verifies:

* Candidate account creation
* Candidate registration
* Candidate counter updates

---

### Voting

Verifies:

* Vote casting
* Vote counter increments
* State persistence

---

### Voting Before Start Time

Verifies:

```rust
VotingNotStarted
```

error is thrown correctly.

---

### Voting After End Time

Verifies:

```rust
VotingEnded
```

error is thrown correctly.

---

# 🚀 Getting Started

## Prerequisites

Install:

* Rust
* Solana CLI
* Anchor CLI
* Node.js
* Yarn

---

## Clone Repository

```bash
git clone https://github.com/<your-username>/Solana_On_Chain_Voting_Protocol.git

cd Solana_On_Chain_Voting_Protocol
```

---

## Install Dependencies

```bash
yarn install
```

or

```bash
npm install
```

---

## Build Program

```bash
anchor build
```

---

## Program Deployment

```bash
anchor deploy --provider.cluster devnet
```

---

## Run Tests

```bash
cargo test
```



# 🎯 Learning Outcomes

This project demonstrates:

* Solana Program Development
* Anchor Framework Fundamentals
* PDA Derivation
* Account Initialization
* State Management
* Custom Errors
* Integration Testing
* LiteSVM Runtime Simulation
* On-Chain Voting Mechanics

---

# 🔮 Future Improvements

Potential enhancements include:

* One wallet, one vote enforcement
* Vote delegation
* Token-weighted voting
* DAO governance integration
* Frontend dashboard
* Real-time analytics
* Vote privacy mechanisms
* Multi-choice polls

---
---

Built with ❤️ using Solana, Anchor, Rust, and LiteSVM.
