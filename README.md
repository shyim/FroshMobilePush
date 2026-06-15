# Push Gateway

Get an instant push notification on your phone the moment a customer places an order in your
Shopware 6 shop.

This is the small server behind the **[Shopware Shop Manager](https://play.google.com/store/apps/details?id=de.shyim.shopware)**
Android app. When someone checks out in your shop, this gateway delivers a push notification to
every phone signed in to that shop — so you know about every new order in real time, without
keeping the admin open.

<p align="center">
  <a href="https://play.google.com/store/apps/details?id=de.shyim.shopware">
    <img src="https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png" alt="Get it on Google Play" height="64">
  </a>
</p>

## Getting started (shop owners)

1. **Install the app on your phone** from
   [Google Play](https://play.google.com/store/apps/details?id=de.shyim.shopware) and connect it
   to your shop.
2. **Install the "FroshMobilePush" Shopware app** in your shop (from the Shopware Store, or by
   uploading it from `FroshMobilePush/`). This is what lets your shop talk to the
   gateway.
3. **Turn on order notifications** in the app, under each shop's settings.

That's it — the next order triggers a notification. No server setup, no configuration on your side.

## How it works

The gateway is a [Cloudflare Worker](https://workers.cloudflare.com/) that acts as the Shopware
*app server*. It sits between your shop and Firebase Cloud Messaging (FCM):

```
Your shop ──(order placed)──▶ Push Gateway ──(push)──▶ your phone(s)
```

In more detail:

```
Shopware shop ──(app registration handshake)──▶ Gateway (stores shop credentials securely)
Phone app     ──(registers its push token)────▶ shop, then tells the gateway
Shopware shop ──(checkout.order.placed)───────▶ Gateway
Gateway       ──(FCM push, one per device)────▶ all phones signed in to that shop
```

Push tokens are cached so the order path stays fast — when an order comes in, the gateway pushes
straight from its cache without querying your shop first.

Live at `https://push-mobile.fos.gg`.

---

The rest of this document is for **developers** working on the gateway itself.

## Project layout

- `src/index.ts` — the Worker. A [Hono](https://hono.dev/) app wired through
  `@shopware-ag/app-server-sdk`, whose `configureAppServer` handles the registration handshake,
  app lifecycle webhooks, and request signing/verification under `/app/*`. The order webhook
  responds immediately and fans out the pushes in the background.
- `src/fcm.ts` — a minimal FCM HTTP v1 client: signs a short-lived JWT from the Firebase service
  account, caches the OAuth token, and reports tokens FCM considers stale so they can be cleaned up.
- `FroshMobilePush/` — the Shopware app that shops install. Its `manifest.xml`
  declares the registration URL, the `checkout.order.placed` webhook, and the required
  permissions; `Resources/entities.xml` defines the `ce_fcn` entity that stores each device's
  push token.

Shop credentials and cached OAuth tokens live in the `SHOP_STORAGE` KV namespace; device push
tokens are cached per shop in KV (`fcn_tokens_{shopId}`, refreshed on demand with a 15-minute
backstop). Tokens FCM reports as unregistered are removed from both the shop and the cache.

> **Note:** the gateway requires `@shopware-ag/app-server-sdk` >= 2.0.2. Earlier versions lost a
> security flag when persisting shops to KV, which weakened re-registration validation
> ([fixed upstream](https://github.com/shopware/app-sdk-js/pull/57)).

> **Why there's no `ce_fcn.written` webhook:** Shopware only allows webhooks on a fixed set of
> "hookable" entities (product, order, customer, …). App custom entities like `ce_fcn` are
> rejected at install, so the phone app pings the gateway directly after registering its token.

## App ↔ gateway contract

1. **Register a device** — `POST /api/ce-fcn` against the shop's Admin API with
   `{"token": "<fcm registration token>", "deviceName": "Pixel 9"}` (upsert with a stable id per
   install; ACL key `ce_fcn`).
2. **Notify the gateway** — `POST https://push-mobile.fos.gg/sync/{shopId}`, where `shopId` comes
   from `GET /api/_action/system-config?domain=core.app` → `core.app.shopId.value`. Without this,
   a new device starts receiving pushes within 15 minutes anyway.
3. **Receive the push** — the FCM `notification` carries `New order #1001 / <customer> • <amount>`;
   the `data` payload carries `event=order.placed`, `shopId`, `shopUrl`, `orderId`, `orderNumber`
   (all strings) for deep-linking into the order detail screen.
