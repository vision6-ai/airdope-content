---
title: "Webhooks"
slug: "webhooks"
excerpt: "Receive real-time notifications when events happen in your Airdope account — fan signups, drop interactions, and more."
date: "2026-02-18"
author:
  name: "Airdope Team"
tags: ["developer", "webhooks"]
category: "Developer"
order: 71
emoji: "🔔"
published: true
---

## What Are Webhooks?

Webhooks send HTTP POST requests to your server when events happen in Airdope. Instead of polling the API, you get notified in real-time.

## Setting Up Webhooks

1. Go to **Settings** → **Developer** → **Webhooks**
2. Click **Add Endpoint**
3. Enter your endpoint URL (must be HTTPS)
4. Select the events you want to receive
5. Click **Save**

You'll receive a webhook signing secret — use it to verify that requests are genuinely from Airdope.

## Available Events

### Fan Events
- `fan.created` — A new fan was added to your CRM
- `fan.wallet_pass.added` — A fan added your wallet pass
- `fan.wallet_pass.removed` — A fan removed your wallet pass

### Drop Events
- `drop.published` — A drop was published
- `drop.viewed` — A fan viewed a drop
- `drop.clicked` — A fan clicked a drop's CTA

### Notification Events
- `notification.sent` — A notification was sent
- `notification.opened` — A fan opened a notification
- `notification.clicked` — A fan clicked a notification link

## Webhook Payload

All webhooks follow this format:

```json
{
  "id": "evt_abc123",
  "type": "fan.wallet_pass.added",
  "createdAt": "2026-02-18T14:30:00Z",
  "data": {
    "fanId": "fan_xyz789",
    "email": "fan@example.com",
    "source": "qr_code"
  }
}
```

## Verifying Webhooks

Every webhook includes a `X-Airdope-Signature` header. Verify it using HMAC-SHA256:

```javascript
import crypto from 'crypto';

function verifyWebhook(payload, signature, secret) {
  const expected = crypto
    .createHmac('sha256', secret)
    .update(payload)
    .digest('hex');
  return crypto.timingSafeEqual(
    Buffer.from(signature),
    Buffer.from(expected)
  );
}
```

## Retry Policy

If your endpoint returns a non-2xx status code, Airdope retries with exponential backoff:
- Retry 1: 1 minute
- Retry 2: 5 minutes
- Retry 3: 30 minutes
- Retry 4: 2 hours
- Retry 5: 24 hours

After 5 failed retries, the webhook is marked as failed and you'll receive an email alert.

---

*Webhooks are available on Pro and Business plans.*
