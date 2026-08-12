# MyZubster Architecture Guide

## System Overview

MyZubster is a decentralized bounty and marketplace platform built on the Monero ecosystem. It consists of several microservices:

```
┌──────────────────────────────────────────┐
│              MyZubster Gateway             │
│  (Next.js — API + Web UI)                  │
└──────┬──────────┬──────────┬──────────────┘
       │          │          │
┌──────▼──┐ ┌─────▼────┐ ┌───▼──────────┐
│ Bounty  │ │Marketplace│ │ Wallet       │
│ Service │ │ Service   │ │ Service      │
│ (Node)  │ │ (Node)    │ │ (Rust/Tari)  │
└─────────┘ └──────────┘ └──────────────┘
       │          │          │
┌──────▼──────────▼──────────▼────────────┐
│           PostgreSQL + Redis             │
│           (Data + Cache)                 │
└─────────────────────────────────────────┘
```

## Components

### Gateway (Next.js)
- **Port**: 3000
- **Responsibilities**: API routing, authentication, SSR, WebSocket connections
- **Tech**: Next.js 14, React 18, Tailwind CSS

### Bounty Service
- **Port**: 3001
- **Responsibilities**: Bounty CRUD, claim workflow, reward distribution
- **Tech**: Node.js, Express, PostgreSQL

### Marketplace Service
- **Port**: 3002
- **Responsibilities**: Listing management, order matching, escrow
- **Tech**: Node.js, Express, Redis

### Wallet Service
- **Port**: 3003
- **Responsibilities**: MYZ token management, transactions, Tari network integration
- **Tech**: Rust, Tari SDK

## Data Flow

### Bounty Lifecycle
1. Creator posts bounty → Gateway → Bounty Service → PostgreSQL
2. Hunter claims bounty → Bounty Service validates → Status: in_progress
3. Hunter submits PR → Bounty Service tracks → Status: under_review
4. PR merged → Bounty Service triggers → Wallet Service for payout
5. MYZ transferred → Wallet Service updates → Status: completed

### Marketplace Flow
1. Seller creates listing → Marketplace Service → PostgreSQL
2. Buyer places order → Marketplace Service → Escrow created
3. Seller delivers → Buyer confirms → Escrow released
4. MYZ transferred → Wallet Service → Status: completed

## Deployment

### Docker Compose
```yaml
version: '3.8'
services:
  gateway:
    build: ./gateway
    ports: ['3000:3000']
    environment:
      - DATABASE_URL=postgresql://...
      - REDIS_URL=redis://...
  bounty-service:
    build: ./services/bounty
    ports: ['3001:3001']
  marketplace:
    build: ./services/marketplace
    ports: ['3002:3002']
  wallet:
    build: ./services/wallet
    ports: ['3003:3003']
  postgres:
    image: postgres:16
    volumes: ['pgdata:/var/lib/postgresql/data']
  redis:
    image: redis:7-alpine
volumes:
  pgdata:
```

## Security

- All API calls authenticated via Bearer tokens
- Rate limiting at gateway level (100 req/min per key)
- Wallet operations require 2FA
- Escrow uses 2-of-3 multisig on Monero network
- Secrets managed via environment variables (never in code)
- Regular security audits
