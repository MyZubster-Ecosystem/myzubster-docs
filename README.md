# MyZubster Ecosystem — Master README

**MyZubster** is an open-source self-replicating robot ecosystem powered by Monero (XMR). This is the central documentation hub for all MyZubster repositories.

---

## 📋 Project Overview

MyZubster is a modular ecosystem of repositories that work together to build a decentralized, Monero-powered robot network for environmental monitoring, data collection, and community-driven automation.

### Core Pillars

| Pillar | Description |
|--------|-------------|
| **Robotics** | Self-replicating robot DNA schema and hardware integration |
| **Payments** | Monero (XMR) micropayments via x402 protocol and escrow |
| **IoT** | Arduino garden sensors and environmental data collection |
| **Community** | Bounty system, seed exchange, and collaborative mapping |
| **Documentation** | Comprehensive guides, API references, and contributing guidelines |

---

## 🔗 Repositories

| Repository | Description | Status |
|------------|-------------|--------|
| [MyZubster-Robot](https://github.com/MyZubster-Ecosystem/MyZubster-Robot) | Main robot code, DNA schema | Active |
| [MyZubsterGateway](https://github.com/MyZubster-Ecosystem/MyZubsterGateway) | API Gateway, Monero payment engine, webhooks | Active |
| [myzubster](https://github.com/MyZubster-Ecosystem/myzubster) | Main monorepo, core ecosystem | Active |
| [MyZubster-App](https://github.com/MyZubster-Ecosystem/MyZubster-App) | React Native mobile app for Android | Active |
| [myzubster-docs](https://github.com/MyZubster-Ecosystem/myzubster-docs) | Documentation hub (this repo) | Active |
| [MyZubster-Marketplace](https://github.com/MyZubster-Ecosystem/MyZubster-Marketplace) | Marketplace for skills and services | Active |

---

## 📊 Project Status

| Feature | Status | Note |
|---------|--------|------|
| Robot DNA Schema | ✅ Complete | Production ready |
| x402 Micropayments | 🔄 In Progress | Testnet only |
| Monero Escrow | 🔄 In Progress | Testnet only |
| Self-Replication | 🧪 Simulation | Software simulation only |
| Arduino Garden API | ✅ Live | ESP8266/ESP32 support |
| Seed Exchange | 🚧 In Development | 6 open issues, some bountied |
| Mobile App | 🚧 In Development | React Native for Android |
| NFT Certificates | 🧪 Experimental | Tari blockchain, Monero-friendly |

---

## 🚀 Getting Started

### Prerequisites
- Node.js v18+
- npm v9+
- Docker (optional)
- Monero wallet (for bounty participation)

### Quick Start

```bash
# Clone a component
git clone https://github.com/MyZubster-Ecosystem/MyZubster-Marketplace.git
cd MyZubster-Marketplace

# Install dependencies
npm install

# Configure environment
cp .env.example .env
nano .env

# Start the server
node server.js
```

For detailed setup instructions, refer to the individual repository READMEs.

### Create a Free Monero Wallet

No XMR required to start contributing! See the [Getting Started Guide](guides/GETTING_STARTED_NO_XMR.md) for step-by-step instructions on creating a free wallet and earning your first XMR.

---

## 🤖 Transparency & Automation

This project uses automation to manage issues, PRs, and bounty tracking. See [CONTRIBUTING.md](CONTRIBUTING.md) for details on how automation works and how to identify automated comments.

---

## 📝 Contributing

Contributions are welcome! Please read the [CONTRIBUTING.md](CONTRIBUTING.md) guide before submitting a pull request.

### How to Contribute

1. Fork the repository you want to work on
2. Create a new branch for your feature or fix
3. Submit a pull request with a clear description
4. Wait for CI checks and human review

### Bounty System

MyZubster rewards contributors with XMR for completing tasks:

| Action | Reward |
|--------|--------|
| Animal/Plant registration | 0.001 XMR |
| Verify a registration | 0.002 XMR |
| Documentation contribution | 0.001 XMR |
| Valid bug report | 0.002 XMR |

---

## 🌐 Ecosystem Hub

- **Organization**: [MyZubster-Ecosystem](https://github.com/MyZubster-Ecosystem)
- **Maintained by**: Daniel Ioni and the MyZubster community
- **Primary payment**: Monero (XMR)

---

## 📜 License

All MyZubster components are released under the MIT License — free for everyone to use, modify, and distribute.
