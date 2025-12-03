# 🎰 Solana Casino Jackpot Smart Contract

[![Solana](https://img.shields.io/badge/Solana-9945FF?style=for-the-badge&logo=solana&logoColor=white)](https://solana.com)
[![Anchor](https://img.shields.io/badge/Anchor-0.30.1-blue?style=for-the-badge)](https://anchor-lang.com)
[![Rust](https://img.shields.io/badge/Rust-1.18.18-orange?style=for-the-badge&logo=rust)](https://www.rust-lang.org)
[![License: ISC](https://img.shields.io/badge/License-ISC-green.svg?style=for-the-badge)](https://opensource.org/licenses/ISC)

> **Provably Fair Jackpot Casino on Solana** - A decentralized, transparent, and secure blockchain-based casino jackpot system built with Anchor framework on Solana blockchain.

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [How It Works](#-how-it-works)
- [Technical Architecture](#-technical-architecture)
- [Prerequisites](#️-prerequisites)
- [Installation](#-installation)
- [Quick Start](#-quick-start)
- [Usage Guide](#-usage-guide)
- [Smart Contract Functions](#-smart-contract-functions)
- [Security Features](#-security-features)
- [Development](#-development)
- [Testing](#-testing)
- [Deployment](#-deployment)
- [CLI Commands](#-cli-commands)
- [Contributing](#-contributing)
- [Contact & Support](#-contact--support)
- [License](#-license)

## 🎯 Overview

**Solana Casino Jackpot Smart Contract** is a fully decentralized casino jackpot system built on the Solana blockchain using the Anchor framework. This smart contract enables transparent, provably fair, and automated jackpot rounds where players can join with SOL deposits, and winners are selected using verifiable random functions (VRF) from ORAO Network.

Perfect for:
- 🎲 **Decentralized Casino Platforms** on Solana
- 🏆 **Jackpot Gaming dApps** with transparent winner selection
- 💰 **DeFi Gaming** applications requiring provably fair randomness
- 🎰 **Blockchain Casino Games** with automated prize distribution
- 🌐 **Web3 Gambling** platforms on Solana

### Why Choose This Solana Casino Jackpot?

- ✅ **Provably Fair**: Uses ORAO VRF for verifiable random winner selection
- ✅ **Transparent**: All game logic on-chain, fully auditable
- ✅ **Automated**: Smart contract handles all game operations
- ✅ **Secure**: Built with Anchor framework best practices
- ✅ **Low Fees**: Benefits from Solana's high-speed, low-cost transactions
- ✅ **Customizable**: Flexible round parameters for different game modes

## ✨ Key Features

### 🎮 Core Casino Features

- **Multi-Round Jackpot System**: Create unlimited jackpot rounds with custom parameters
- **Flexible Betting**: Configurable minimum deposit amounts and maximum participants
- **Automated Winner Selection**: Provably fair winner selection using ORAO VRF
- **Instant Prize Distribution**: Winners can claim rewards immediately after selection
- **Time-Based Rounds**: Customizable round duration (seconds to hours)
- **Admin Controls**: Secure admin functions for game management

### 🔐 Security & Fairness

- **VRF Integration**: ORAO Solana VRF ensures unpredictable, verifiable randomness
- **On-Chain Validation**: All game rules enforced by smart contract
- **Authority Verification**: Admin-only functions protected by wallet verification
- **Overflow Protection**: Built with safe math operations
- **Access Control**: Proper PDA (Program Derived Address) usage

### ⚡ Technical Features

- **Optimized for Solana**: Takes advantage of Solana's speed and low fees
- **Anchor Framework**: Built with industry-standard Anchor v0.30.1
- **TypeScript SDK**: Full CLI for easy interaction
- **Event Logging**: Track all game events on-chain
- **Modular Architecture**: Clean, maintainable code structure

## 🎲 How It Works

### Game Flow

```
1. Admin Creates Round
   └─> Set: round_time, min_deposit, max_joiners

2. Players Join
   └─> Deposit SOL (≥ min_deposit)
   └─> Round countdown starts when 2nd player joins

3. Round Timer Expires
   └─> No more entries accepted

4. Winner Selection
   └─> ORAO VRF generates random winner
   └─> Winner determined by weighted probability

5. Prize Claim
   └─> Winner claims total jackpot
   └─> SOL transferred to winner's wallet
```

### Winner Selection Algorithm

The smart contract uses **ORAO VRF (Verifiable Random Function)** to select winners fairly:

- Each player's chance = (their deposit / total pool)
- Higher deposits = higher winning probability
- Random selection is cryptographically verifiable
- No central party can manipulate results

## 🏗️ Technical Architecture

### Smart Contract Structure

```
jackpot_smart_contract/
├── instructions/
│   ├── admin/
│   │   ├── configure.rs      # Initialize contract config
│   │   ├── create_game.rs    # Create new jackpot round
│   │   └── set_winner.rs     # Trigger winner selection
│   └── user/
│       ├── join_game.rs      # Player joins a round
│       └── claim_reward.rs   # Winner claims prize
├── state/
│   ├── config.rs            # Global configuration
│   └── gameground.rs        # Round state management
├── constants.rs             # Contract constants
├── errors.rs               # Custom error types
├── utils.rs                # Helper functions
└── lib.rs                  # Program entry point
```

### Key Data Structures

#### Config Account
- Stores admin public key
- Sets global min/max deposit limits
- Defines max joiners per round
- Tracks total rounds created

#### GameGround Account
- Round-specific state
- Player list and deposits
- Winner information
- Round timing and status
- Prize pool tracking

## 🛠️ Prerequisites

Before you begin, ensure you have the following installed:

- **[Rust](https://www.rust-lang.org/tools/install)** - Version 1.75+
- **[Solana CLI](https://docs.solana.com/cli/install-solana-cli-tools)** - Version 1.18+
- **[Anchor](https://anchor-lang.com/docs/installation)** - Version 0.30.1 (recommended)
- **[Node.js](https://nodejs.org/)** - Version 16+ (for CLI tools)
- **[Yarn](https://yarnpkg.com/)** - Package manager

### Verify Installation

```bash
rustc --version              # Should show rustc 1.75+
solana --version             # Should show solana-cli 1.18+
anchor --version             # Should show anchor-cli 0.30.1
node --version               # Should show v16+
yarn --version               # Should show 1.22+
```

## 📦 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/Solana-Casino-Jackpot-Smart-Contract.git
cd Solana-Casino-Jackpot-Smart-Contract
```

### 2. Install Dependencies

```bash
yarn install
```

### 3. Configure Solana CLI

```bash
# Set to devnet for testing
solana config set --url devnet

# Or set to mainnet-beta for production
solana config set --url mainnet-beta

# Verify configuration
solana config get
```

### 4. Generate Wallet

```bash
# Create admin wallet
solana-keygen new -o ./keys/admin.json

# Get your wallet address
solana-keygen pubkey ./keys/admin.json

# Airdrop SOL on devnet
solana airdrop 5 $(solana-keygen pubkey ./keys/admin.json) -u devnet
```

## ⚡ Quick Start

### Build the Smart Contract

```bash
# Build with nightly toolchain (required for optimal compilation)
RUSTUP_TOOLCHAIN="nightly-2024-11-19" anchor build

# Sync program IDs
anchor keys sync

# Rebuild after key sync
RUSTUP_TOOLCHAIN="nightly-2024-11-19" anchor build
```

### Deploy to Devnet

```bash
# Deploy the program
anchor deploy

# Note the Program ID from output
# Update it in lib.rs if needed
```

### Initialize Configuration

```bash
# Initialize the jackpot contract
yarn script config
```

**🎉 Your Solana Casino Jackpot is now live!**

## 📖 Usage Guide

### For Casino Operators

#### 1. Create a Jackpot Round

```bash
yarn script create -t <ROUND_TIME> -d <MIN_DEPOSIT> -j <MAX_JOINERS>
```

**Example**: 5-minute round, 0.1 SOL minimum, 100 max players
```bash
yarn script create -t 300 -d 100000000 -j 100
```

**Parameters**:
- `-t` **ROUND_TIME**: Duration in seconds (e.g., 300 = 5 minutes)
- `-d` **MIN_DEPOSIT**: Minimum bet in lamports (1 SOL = 1,000,000,000 lamports)
- `-j` **MAX_JOINERS**: Maximum number of players allowed

#### 2. Select Winner (After Round Ends)

```bash
yarn script winner -g <ROUND_NUMBER>
```

**Example**:
```bash
yarn script winner -g 0
```

### For Players

#### Join a Jackpot Round

```bash
yarn script join -a <AMOUNT> -g <ROUND_NUMBER>
```

**Example**: Join round 0 with 0.5 SOL
```bash
yarn script join -a 500000000 -g 0
```

**Parameters**:
- `-a` **AMOUNT**: Deposit amount in lamports
- `-g` **ROUND_NUMBER**: Round index to join (starts at 0)

**Important**: Round countdown starts when the second player joins!

#### Claim Your Winnings

```bash
yarn script claim -g <ROUND_NUMBER>
```

**Example**:
```bash
yarn script claim -g 0
```

**Note**: Only the winner can claim rewards, and only after winner selection.

## 🔧 Smart Contract Functions

### Admin Functions

#### `configure`
Initialize or update global contract configuration.

```rust
pub fn configure(ctx: Context<Configure>, new_config: Config) -> Result<()>
```

**Access**: Admin only

#### `create_game`
Create a new jackpot round with custom parameters.

```rust
pub fn create_game(
    ctx: Context<CreateGame>,
    force: [u8; 32],
    round_time: i64,
    min_deposit_amount: u64,
    max_joiner_count: u64,
) -> Result<()>
```

**Access**: Admin only

#### `set_winner`
Trigger VRF-based winner selection for a completed round.

```rust
pub fn set_winner(ctx: Context<SetWinner>, round_num: u64) -> Result<()>
```

**Access**: Admin only
**Requirement**: Round time must be expired

### User Functions

#### `join_game`
Join an active jackpot round with a SOL deposit.

```rust
pub fn join_game(ctx: Context<JoinGame>, round_num: u64, amount: u64) -> Result<()>
```

**Access**: Any wallet
**Requirements**:
- Round must be active
- Amount ≥ minimum deposit
- Player limit not reached

#### `claim_reward`
Claim the jackpot prize (winner only).

```rust
pub fn claim_reward(ctx: Context<ClaimReward>, round_num: u64) -> Result<()>
```

**Access**: Winner wallet only
**Requirement**: Winner must be selected

## 🔒 Security Features

### Implemented Security Measures

- ✅ **Admin Authentication**: All admin functions verify authority
- ✅ **PDA Security**: Proper use of Program Derived Addresses
- ✅ **Overflow Protection**: Safe math operations throughout
- ✅ **State Validation**: Comprehensive checks on all state transitions
- ✅ **VRF Integration**: Unpredictable, verifiable randomness from ORAO
- ✅ **Access Control**: Function-level permission enforcement
- ✅ **Anchor Security**: Built with Anchor framework best practices

### Best Practices

- 🔐 Store admin keys securely (hardware wallet recommended)
- 🔐 Test thoroughly on devnet before mainnet deployment
- 🔐 Monitor contract events for unusual activity
- 🔐 Regular security audits recommended for production
- 🔐 Use multi-sig for admin functions in production

## 👨‍💻 Development

### Project Structure

```
.
├── programs/
│   └── jackpot_smart_contract/     # Rust smart contract
│       ├── src/                    # Source code
│       └── Cargo.toml              # Rust dependencies
├── cli/                            # TypeScript CLI tools
│   └── command.ts                  # CLI implementation
├── keys/                           # Wallet keys (gitignored)
├── idl/                            # Generated IDL files
├── target/                         # Build artifacts
├── Anchor.toml                     # Anchor configuration
├── package.json                    # Node.js dependencies
└── README.md                       # This file
```

### Environment Setup

Configure your `Anchor.toml` for different environments:

**Devnet**:
```toml
[provider]
cluster = "https://api.devnet.solana.com"
wallet = "./keys/admin.json"
```

**Mainnet**:
```toml
[provider]
cluster = "https://api.mainnet-beta.solana.com"
wallet = "./keys/admin.json"
```

### Building from Source

```bash
# Clean previous builds
anchor clean

# Build with specific toolchain
RUSTUP_TOOLCHAIN="nightly-2024-11-19" anchor build

# Generate TypeScript client
anchor build
```

## 🧪 Testing

### Run Tests

```bash
# Run Anchor tests
anchor test

# Run specific test file
anchor test tests/casino.test.ts

# Run with logs
anchor test --skip-build --skip-deploy
```

### Manual Testing on Devnet

Follow the [Usage Guide](#-usage-guide) section with devnet configuration.

## 🚀 Deployment

### Deploy to Devnet

```bash
# Set cluster
solana config set --url devnet

# Build and deploy
anchor build
anchor deploy

# Initialize configuration
yarn script config
```

### Deploy to Mainnet

⚠️ **Mainnet Deployment Checklist**:

1. ✅ Complete security audit
2. ✅ Extensive testing on devnet
3. ✅ Prepare sufficient SOL for deployment (~5-10 SOL)
4. ✅ Backup all wallet keys securely
5. ✅ Verify program ID in lib.rs

```bash
# Set to mainnet
solana config set --url mainnet-beta

# Build for production
RUSTUP_TOOLCHAIN="nightly-2024-11-19" anchor build

# Deploy (requires ~5-10 SOL for rent)
anchor deploy

# Verify deployment
solana program show <PROGRAM_ID>
```

### Post-Deployment

1. Initialize contract configuration
2. Create test round with small amounts
3. Verify all functions work correctly
4. Monitor for any issues
5. Gradually increase limits

## 💻 CLI Commands

### Configuration Commands

```bash
# Initialize contract
yarn script config

# View help
yarn script --help
```

### Game Management

```bash
# Create round: 10 min, 1 SOL min, 50 players max
yarn script create -t 600 -d 1000000000 -j 50

# Join round 2 with 2.5 SOL
yarn script join -a 2500000000 -g 2

# Select winner for round 2
yarn script winner -g 2

# Claim winnings from round 2
yarn script claim -g 2
```

### Solana CLI Utilities

```bash
# Check balance
solana balance

# Get account info
solana account <ACCOUNT_ADDRESS>

# View recent transactions
solana transaction-history <SIGNATURE>

# Monitor logs (useful for debugging)
solana logs <PROGRAM_ID>
```

## 🎯 Use Cases

### Casino Platforms
Integrate this smart contract into your Solana-based casino platform for transparent, provably fair jackpot games.

### Lottery dApps
Build decentralized lottery applications with customizable round parameters and automated prize distribution.

### Gaming Platforms
Add jackpot mechanics to Web3 games, with on-chain verification and instant payouts.

### DeFi Gaming
Combine yield farming with gaming mechanics for innovative DeFi gaming experiences.

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add some AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

### Development Guidelines

- Follow Rust and Anchor best practices
- Add tests for new features
- Update documentation
- Ensure all tests pass before submitting PR
- Keep commits atomic and well-described

## 📞 Contact & Support

For questions, support, or business inquiries:

**Telegram**: [RRR](https://t.me/idioRusty)

### Getting Help

- 📖 Check the documentation thoroughly
- 🐛 Report bugs via GitHub Issues
- 💬 Join our community for discussions
- 📧 Contact us for custom development

## 📄 License

This project is licensed under the **ISC License**.

## 🙏 Acknowledgments

- **[Solana](https://solana.com)** - High-performance blockchain
- **[Anchor](https://anchor-lang.com)** - Solana development framework
- **[ORAO Network](https://www.orao.network/)** - VRF provider for randomness
- **Solana Developer Community** - Support and resources

## 🔗 Resources

### Official Documentation
- [Solana Documentation](https://docs.solana.com/)
- [Anchor Book](https://book.anchor-lang.com/)
- [Solana Cookbook](https://solanacookbook.com/)

### Related Projects
- [ORAO VRF](https://github.com/orao-network/solana-vrf) - Verifiable Random Function
- [Solana Program Library](https://spl.solana.com/) - SPL Token Standard

### Learning Resources
- [Solana Bootcamp](https://www.soldev.app/)
- [Anchor Examples](https://github.com/coral-xyz/anchor/tree/master/tests)

---

## 📊 Statistics

- **Program ID**: `DZQyG4Xsgt8vGvaWEPHyTgzmHYz4V9qrw7eirpBidXU9`
- **Anchor Version**: 0.30.1
- **Solana Version**: 1.18.18
- **Language**: Rust + TypeScript

---

## ⚠️ Disclaimer

This smart contract is provided as-is for educational and development purposes. Use at your own risk. Always conduct thorough security audits before deploying to mainnet. Online gambling may be subject to regulations in your jurisdiction.

---

<div align="center">

**Built with ❤️ on Solana**

[⬆ Back to Top](#-solana-casino-jackpot-smart-contract)

</div>
