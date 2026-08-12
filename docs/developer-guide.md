# MyZubster Developer Guide

## Getting Started

### Prerequisites
- Node.js 18+
- Rust 1.75+ (for wallet service)
- PostgreSQL 16
- Redis 7
- Docker (optional, for containerized development)

### Local Setup

1. Clone the repositories:
```bash
git clone https://github.com/MyZubster-Ecosystem/MyZubsterGateway.git
git clone https://github.com/MyZubster-Ecosystem/myzubster-docs.git
```

2. Install dependencies:
```bash
cd MyZubsterGateway
npm install
```

3. Set up environment:
```bash
cp .env.example .env.local
# Edit .env.local with your configuration
```

4. Start the database:
```bash
docker compose up -d postgres redis
```

5. Run migrations:
```bash
npm run migrate
```

6. Start development server:
```bash
npm run dev
```

The gateway will be available at `http://localhost:3000`.

## Project Structure

```
MyZubsterGateway/
├── app/              # Next.js App Router pages
├── components/       # React components
├── lib/              # Utility functions
├── prisma/           # Database schema + migrations
├── public/           # Static assets
├── services/         # Backend microservices
│   ├── bounty/       # Bounty service
│   ├── marketplace/  # Marketplace service
│   └── wallet/       # Wallet service (Rust)
└── tests/            # Test suites
```

## Testing

```bash
# Unit tests
npm test

# Integration tests
npm run test:integration

# E2E tests
npm run test:e2e

# With coverage
npm run test:coverage
```

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feat/my-feature`
3. Make your changes
4. Run tests: `npm test`
5. Commit with sign-off: `git commit -s -m "feat: description"`
6. Push and create a PR

### Commit Convention
- `feat:` — New feature
- `fix:` — Bug fix
- `docs:` — Documentation
- `style:` — Formatting
- `refactor:` — Code restructuring
- `test:` — Tests
- `chore:` — Maintenance

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| DATABASE_URL | PostgreSQL connection string | — |
| REDIS_URL | Redis connection string | redis://localhost:6379 |
| API_KEY | Internal API authentication | — |
| TARI_NODE_URL | Tari network node | — |
| NODE_ENV | Environment | development |
