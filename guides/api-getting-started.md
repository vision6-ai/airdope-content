---
title: "API: Getting Started"
slug: "api-getting-started"
excerpt: "Introduction to the Airdope API — authentication, endpoints, and your first API call."
date: "2026-02-18"
author:
  name: "Airdope Team"
tags: ["developer", "api"]
category: "Developer"
order: 70
emoji: "🔑"
published: true
---

## Airdope API Overview

The Airdope API lets you programmatically manage fans, drops, wallet passes, and analytics. It's a REST API that returns JSON.

## Authentication

All API requests require an API key in the `Authorization` header:

```
Authorization: Bearer YOUR_API_KEY
```

### Getting Your API Key

1. Go to **Settings** → **Developer**
2. Click **Generate API Key**
3. Copy your key (it's only shown once)
4. Store it securely — never commit it to version control

## Base URL

```
https://api.airdope.com/v1
```

## Your First API Call

List your fans:

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" \
  https://api.airdope.com/v1/fans
```

Response:

```json
{
  "data": [
    {
      "id": "fan_abc123",
      "email": "fan@example.com",
      "name": "Jane Doe",
      "walletPassActive": true,
      "engagementScore": 85,
      "createdAt": "2026-01-15T10:30:00Z"
    }
  ],
  "pagination": {
    "total": 1250,
    "page": 1,
    "perPage": 50
  }
}
```

## Key Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/fans` | List all fans |
| GET | `/fans/:id` | Get a single fan |
| POST | `/drops` | Create a drop |
| GET | `/drops` | List all drops |
| POST | `/notifications` | Send a notification |
| GET | `/analytics/overview` | Get analytics summary |

## Rate Limits

- **Free plan:** 100 requests/minute
- **Pro plan:** 500 requests/minute
- **Business plan:** 2,000 requests/minute

Rate limit headers are included in every response:
```
X-RateLimit-Limit: 500
X-RateLimit-Remaining: 499
X-RateLimit-Reset: 1708300800
```

## SDKs

We provide official SDKs for:
- **JavaScript/TypeScript** — `npm install @airdope/sdk`
- **Python** — `pip install airdope`

---

*The API is available on Pro and Business plans.*
