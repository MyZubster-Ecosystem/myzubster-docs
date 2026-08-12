# MyZubster API Documentation

## Overview

The MyZubster API provides programmatic access to the MyZubster ecosystem including bounties, marketplace, and wallet operations.

Base URL: `https://api.myzubster.com/v1`

## Authentication

All API requests require an API key passed in the `Authorization` header:

```
Authorization: Bearer YOUR_API_KEY
```

Generate your API key from Dashboard → Settings → API Keys.

## Rate Limits

- 100 requests per minute per API key
- 1000 requests per hour per IP

## Endpoints

### Bounties

#### List Bounties
```http
GET /bounties
```

| Parameter | Type | Description |
|-----------|------|-------------|
| status | string | Filter: open, in_progress, completed |
| reward_min | integer | Minimum MYZ reward |
| page | integer | Page number (default: 1) |
| limit | integer | Items per page (default: 20, max: 100) |

**Response**
```json
{
  "data": [
    {
      "id": 864,
      "title": "Guide: How to Start Without Monero",
      "status": "open",
      "reward": 100,
      "currency": "MYZ",
      "labels": ["documentation", "easy"],
      "created_at": "2025-08-01T00:00:00Z",
      "url": "https://github.com/MyZubster-Ecosystem/MyZubsterGateway/issues/864"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 45
  }
}
```

#### Get Bounty
```http
GET /bounties/:id
```

#### Claim Bounty
```http
POST /bounties/:id/claim
```

### Marketplace

#### List Listings
```http
GET /marketplace
```

| Parameter | Type | Description |
|-----------|------|-------------|
| category | string | Filter by category |
| sort | string | price_asc, price_desc, newest |
| search | string | Full-text search |

#### Create Listing
```http
POST /marketplace
```

**Request Body**
```json
{
  "title": "Premium Theme Pack",
  "description": "A collection of 5 responsive blog themes",
  "price": 150,
  "currency": "MYZ",
  "category": "themes"
}
```

### Wallet

#### Get Balance
```http
GET /wallet/balance
```

**Response**
```json
{
  "balance": 1250,
  "currency": "MYZ",
  "pending": 300,
  "address": "12Nbmmm5g...U4"
}
```

#### Get Transactions
```http
GET /wallet/transactions
```

#### Send MYZ
```http
POST /wallet/send
```

**Request Body**
```json
{
  "to": "12Nbmmm5g...U4",
  "amount": 50,
  "currency": "MYZ",
  "memo": "Payment for bounty #864"
}
```

## Error Codes

| Code | Description |
|------|-------------|
| 400 | Bad request — malformed parameters |
| 401 | Unauthorized — missing or invalid API key |
| 403 | Forbidden — insufficient permissions |
| 404 | Not found — resource doesn't exist |
| 429 | Rate limited — too many requests |
| 500 | Internal server error |

## SDKs

### JavaScript/TypeScript
```bash
npm install @myzubster/sdk
```

```typescript
import { MyZubsterClient } from '@myzubster/sdk';

const client = new MyZubsterClient({ apiKey: 'YOUR_KEY' });
const bounties = await client.bounties.list({ status: 'open' });
```

### Python
```bash
pip install myzubster-sdk
```

```python
from myzubster import MyZubsterClient

client = MyZubsterClient(api_key='YOUR_KEY')
bounties = client.bounties.list(status='open')
```
