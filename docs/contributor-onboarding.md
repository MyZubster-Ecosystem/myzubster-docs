# MyZubster Contributor Onboarding Guide (#32)

Welcome to the MyZubster ecosystem! This guide will help you get started as a contributor.

## 1. What is MyZubster?

MyZubster is a decentralized ecosystem where autonomous robots work for real clients and get paid in MYZ (Tari token) and XMR (Monero). It's fully open-source (MIT licensed).

## 2. Ecosystem Overview

| Repo | Purpose | Tech Stack |
|------|---------|------------|
| [MyZubsterGateway](https://github.com/MyZubster-Ecosystem/MyZubsterGateway) | API gateway (auth, payments, escrow, bounties) | Node.js, Express, MongoDB |
| [MyZubster](https://github.com/MyZubster-Ecosystem/MyZubster) | Core platform (dashboard, rewards, governance) | Node.js, Express, MongoDB |
| [MyZubster-App](https://github.com/MyZubster-Ecosystem/MyZubster-App) | Mobile app (job gateway, chat, map) | Node.js, mobile |
| [MyZubster-Robot](https://github.com/MyZubster-Ecosystem/MyZubster-Robot) | Robot SDK (Arduino, DNA, self-replication) | C++, Node.js |
| [MyZubsterWeb](https://github.com/MyZubster-Ecosystem/MyZubsterWeb) | Web frontend | Node.js, Express |
| [myzubster-docs](https://github.com/MyZubster-Ecosystem/myzubster-docs) | Documentation | Markdown |
| [MyZubster-Marketplace](https://github.com/MyZubster-Ecosystem/MyZubster-Marketplace) | Marketplace for robot services | Node.js |

## 3. Prerequisites

- **Node.js** 18+ (for backend repos)
- **MongoDB** (local or MongoDB Atlas free tier)
- **Git** and **GitHub** account
- **Monero wallet** (for XMR payments - optional for development)

## 4. Getting Started

### Step 1: Choose a repo
Browse the repos above and pick one that matches your skills:
- **Backend developers**: MyZubsterGateway or MyZubster
- **Frontend developers**: MyZubsterWeb or MyZubster-App
- **Robot/C++ developers**: MyZubster-Robot
- **Technical writers**: myzubster-docs

### Step 2: Find a bounty
1. Go to the repo's [Issues](https://github.com/MyZubster-Ecosystem/MyZubsterGateway/issues)
2. Filter by label `BOUNTY` (or look for issues with MYZ rewards)
3. Find one that matches your skills
4. Comment "I claim this bounty"
5. Wait for maintainer acknowledgment

### Step 3: Fork and develop
```bash
# Fork the repo on GitHub, then:
git clone https://github.com/YOUR-USERNAME/REPO-NAME.git
cd REPO-NAME
npm install  # for Node.js repos
cp .env.example .env  # configure environment variables
npm start  # or npm run dev
```

### Step 4: Implement the feature
- Follow existing code conventions
- Add tests where applicable
- Update documentation if needed

### Step 5: Submit a PR
```bash
git checkout -b feature/your-feature
git add .
git commit -m "feat: your feature description"
git push origin feature/your-feature
```
Then open a Pull Request on GitHub with `Closes #ISSUE_NUMBER` in the description.

### Step 6: Get paid
After your PR is merged, you'll receive MYZ tokens to your wallet address.

## 5. Development Environment

### Local MongoDB
```bash
# Install MongoDB Community Edition
# Start MongoDB
mongod --dbpath /path/to/data
```

### Environment Variables
```env
PORT=10000
MONGODB_URI=mongodb://localhost:27017/myzubster
JWT_SECRET=your-secret-key
ENABLE_PAYMENTS=false
ENABLE_ANIMAL_REGISTRY=true
ENABLE_PLANT_REGISTRY=true
ENABLE_BOUNTY_PROGRAM=true
MONERO_MAIN_WALLET_ADDRESS=your-wallet-address
CORS_ORIGIN=*
```

### Testing
```bash
npm test  # if test script exists
# or run manually
node tests/your-test-file.js
```

## 6. Code Conventions

- **Language**: JavaScript (Node.js)
- **Style**: 2-space indentation, single quotes for strings
- **Naming**: camelCase for variables/functions, PascalCase for models/classes
- **File structure**: `src/models/`, `src/controllers/`, `src/routes/`
- **Auth**: JWT for protected routes, admin middleware for sensitive operations
- **Error handling**: try/catch with proper HTTP status codes
- **Comments**: Minimal - code should be self-documenting

## 7. Bounty Rules

1. **One bounty at a time** - complete one before claiming another
2. **PR within 48h** - submit your PR within 48 hours of claiming
3. **Link the issue** - use `Closes #NUMBER` in your PR description
4. **Payment after merge** - MYZ is paid via the Gateway after merge
5. **Quality matters** - follow acceptance criteria exactly

## 8. Communication

- **GitHub Issues**: Primary communication channel
- **Telegram**: @Myzubster_bot for community chat
- **Be respectful**: We welcome contributors of all skill levels

## 9. Common Issues

### "npm install fails"
- Check Node.js version (18+)
- Delete `node_modules/` and `package-lock.json`, retry
- Check for network issues

### "MongoDB connection error"
- Ensure MongoDB is running
- Check MONGODB_URI in .env
- Try MongoDB Atlas as alternative

### "JWT authentication fails"
- Ensure JWT_SECRET is set in .env
- Check token format (Bearer token in Authorization header)

## 10. Next Steps

After your first PR is merged:
1. Claim more bounties
2. Review other contributors' PRs
3. Suggest new features (open an issue)
4. Join the Telegram community
5. Help improve this documentation

## License

MIT - see [LICENSE](../LICENSE) file
