---
title: "Custom Integrations"
slug: "custom-integrations"
excerpt: "Connect Airdope to your existing tools — Shopify, Stripe, Zapier, and more."
date: "2026-02-18"
author:
  name: "Airdope Team"
tags: ["developer", "integrations"]
category: "Developer"
order: 72
emoji: "🔗"
published: true
---

## Integrations Overview

Airdope connects with your existing tools so you can build powerful workflows across your entire stack.

## Native Integrations

### Shopify

Connect your Shopify store to:
- Automatically create drops from new products
- Track merch sales attributed to Airdope notifications
- Add wallet pass signup to your checkout flow

**Setup:** Settings → Integrations → Shopify → Connect

### Stripe

Connect Stripe to:
- Track revenue from drop CTAs
- Attribute sales to specific notifications
- View revenue analytics in your Airdope dashboard

**Setup:** Settings → Integrations → Stripe → Connect

### Instagram

See the [Instagram Integration guide](/guides/instagram-integration) for full details.

## Zapier

Connect Airdope to 5,000+ apps through Zapier:

**Popular Zaps:**
- New Airdope fan → Add to Mailchimp list
- New Shopify order → Send Airdope notification
- New Airdope fan → Add row to Google Sheets
- Spotify new release → Create Airdope drop

**Setup:**
1. Go to [zapier.com](https://zapier.com)
2. Search for "Airdope"
3. Connect your Airdope account using your API key
4. Build your Zap

## Building Custom Integrations

Use the [Airdope API](/guides/api-getting-started) and [Webhooks](/guides/webhooks) to build custom integrations:

### Example: Sync fans to your email platform

```javascript
// Listen for new fan webhook
app.post('/webhooks/airdope', (req, res) => {
  const { type, data } = req.body;

  if (type === 'fan.created' && data.email) {
    // Add to your email platform
    await emailPlatform.addSubscriber({
      email: data.email,
      name: data.name,
      tags: ['airdope'],
    });
  }

  res.sendStatus(200);
});
```

### Example: Auto-create drops from your CMS

```javascript
// When a new blog post is published
async function onNewBlogPost(post) {
  await airdope.drops.create({
    title: post.title,
    description: post.excerpt,
    coverImage: post.featuredImage,
    ctaText: 'Read Now',
    ctaUrl: post.url,
    startsAt: new Date(),
    endsAt: null, // No end date
  });
}
```

## Rate Limits & Best Practices

- Respect API rate limits (see [API guide](/guides/api-getting-started))
- Use webhooks instead of polling when possible
- Cache API responses when appropriate
- Use idempotency keys for POST requests to prevent duplicates

---

*Need help building an integration? Contact us at dev@airdope.com.*
