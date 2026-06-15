Werden Sie benachrichtigt, sobald ein Kunde eine Bestellung aufgibt. Diese App verbindet Ihren
Shopware-6-Shop mit der **Shopware Shop Manager** Android-App und liefert für jede neue Bestellung
eine sofortige Push-Benachrichtigung – damit Ihnen kein Verkauf entgeht, auch wenn Sie gerade
nicht im Backoffice sind.

## Warum diese App installieren

- **Bestellbenachrichtigungen in Echtzeit** – die Benachrichtigung erreicht Sie innerhalb von
  Sekunden nach dem Checkout direkt auf Ihrem Smartphone.
- **Bestellung auf einen Blick** – jede Push-Nachricht zeigt die Bestellnummer, den Kundennamen
  und den Bestellwert, sodass Sie schon vor dem Öffnen der App wissen, was eingegangen ist.
- **Tippen und öffnen** – mit einem Tipp auf die Benachrichtigung gelangen Sie direkt zur
  Bestelldetailansicht in der Shopware-Shop-Manager-App.
- **Mehrere Geräte** – jedes in Ihrem Shop angemeldete Gerät erhält die Benachrichtigung, sodass
  das gesamte Team auf dem Laufenden bleibt.

## So funktioniert es

Die App stellt eine sichere Verbindung zwischen Ihrem Shop und dem Push-Gateway her. Wenn ein
Kunde den Checkout abschließt (`checkout.order.placed`), benachrichtigt Ihr Shop das Gateway,
welches eine Push-Nachricht an alle für Ihren Shop registrierten Android-Geräte weiterleitet.
Bestelldaten bleiben unter Ihrer Kontrolle – das Gateway leitet ausschließlich die
Benachrichtigung weiter.

## Voraussetzungen

- Shopware 6.6 oder neuer.
- Die kostenlose **Shopware Shop Manager** App auf Ihrem Android-Gerät.
- Das Gerät muss in der Shop-Manager-App bei diesem Shop angemeldet sein, wodurch es für den
  Empfang von Push-Benachrichtigungen registriert wird.

## Datenschutz

Das Gateway verarbeitet nur die für die Benachrichtigung erforderlichen Mindestinformationen
(Bestellnummer, Kundenname, Bestellwert) sowie die Gerätetoken Ihrer registrierten Geräte. Es
werden weder Bestellhistorie noch Kundendatenbank gespeichert.
