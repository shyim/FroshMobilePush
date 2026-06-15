Setting up order push notifications takes just a few minutes.

## 1. Install the app in your shop

1. Open the Shopware Administration and go to **Extensions → My extensions**.
2. Find **Shopware Shop Manager Push Gateway** and click **Install**.
3. Click **Activate**. During activation Shopware connects your shop to the push gateway and
   asks you to confirm the requested permissions — accept them to complete the setup.

> The app only requests read access to orders, customers and currencies (to build the
> notification) plus access to its own device-registration storage. It never writes to your
> products, customers or orders.

## 2. Install the Shopware Shop Manager app

1. Install **Shopware Shop Manager** from the Google Play Store on your Android device.
2. Open the app and connect it to your shop using your admin login.
3. Once connected, the app automatically registers the device to receive push notifications for
   this shop. No further configuration is needed.

## 3. Test it

Place a test order in your shop (a real checkout through the storefront — imported orders do
not trigger the notification). Within a few seconds the registered device should receive a push
notification with the order number, customer name and total.

## Troubleshooting

- **No notification arrives** — make sure the app is activated in the Administration, the device
  is connected to the correct shop in the Shop Manager app, and notifications are enabled for
  the app in your Android system settings.
- **Notification arrives late** — newly registered devices may take up to 15 minutes before the
  first notification arrives; subsequent orders are delivered in real time.
- **Multiple devices** — repeat step 2 on each device. Every device connected to the shop
  receives its own notification.

## Uninstalling

Deactivating or uninstalling the app in **Extensions → My extensions** stops all push
notifications for the shop and removes the registered device data.
