Get notified the moment a customer places an order. This app connects your Shopware 6 shop to
the **Shopware Shop Manager** Android app and delivers an instant push notification for every
new order — so you never miss a sale, even when you are away from the back office.

## Why install this

- **Real-time order alerts** — the notification arrives within seconds of checkout, straight on
  your phone.
- **Order at a glance** — each push shows the order number, the customer name and the order
  total, so you know what came in before you even open the app.
- **Tap to open** — opening the notification takes you directly to the order detail screen in
  the Shopware Shop Manager app.
- **Multiple devices** — every device signed in to your shop receives the alert, so the whole
  team stays in the loop.

## How it works

The app registers a secure connection between your shop and the push gateway. When a customer
completes checkout (`checkout.order.placed`), your shop notifies the gateway, which forwards a
push notification to all Android devices registered for your shop. Order data never leaves your
control — the gateway only relays the notification.

## Requirements

- Shopware 6.6 or newer.
- The free **Shopware Shop Manager** app installed on your Android device.
- The device must be signed in to this shop inside the Shop Manager app, which registers it to
  receive push notifications.

## Privacy

The gateway only processes the minimal order information needed to build the notification
(order number, customer name, total) and the device tokens of your registered devices. No order
history or customer database is stored.
