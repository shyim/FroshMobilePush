Die Einrichtung der Bestell-Push-Benachrichtigungen dauert nur wenige Minuten.

## 1. App in Ihrem Shop installieren

1. Öffnen Sie die Shopware-Administration und gehen Sie zu **Erweiterungen → Meine
   Erweiterungen**.
2. Suchen Sie **Shopware Shop Manager Push-Gateway** und klicken Sie auf **Installieren**.
3. Klicken Sie auf **Aktivieren**. Während der Aktivierung verbindet Shopware Ihren Shop mit dem
   Push-Gateway und bittet Sie, die angeforderten Berechtigungen zu bestätigen – akzeptieren Sie
   diese, um die Einrichtung abzuschließen.

> Die App fordert lediglich Lesezugriff auf Bestellungen, Kunden und Währungen an (zur Erstellung
> der Benachrichtigung) sowie Zugriff auf ihren eigenen Speicher für die Geräteregistrierung. Sie
> schreibt niemals in Ihre Produkte, Kunden oder Bestellungen.

## 2. Shopware Shop Manager App installieren

1. Installieren Sie **Shopware Shop Manager** aus dem Google Play Store auf Ihrem Android-Gerät.
2. Öffnen Sie die App und verbinden Sie sie über Ihre Admin-Anmeldedaten mit Ihrem Shop.
3. Nach der Verbindung registriert die App das Gerät automatisch für den Empfang von
   Push-Benachrichtigungen für diesen Shop. Es ist keine weitere Konfiguration erforderlich.

## 3. Testen

Geben Sie eine Testbestellung in Ihrem Shop auf (ein echter Checkout über den Storefront –
importierte Bestellungen lösen keine Benachrichtigung aus). Innerhalb weniger Sekunden sollte das
registrierte Gerät eine Push-Benachrichtigung mit Bestellnummer, Kundenname und Bestellwert
erhalten.

## Fehlerbehebung

- **Keine Benachrichtigung kommt an** – stellen Sie sicher, dass die App in der Administration
  aktiviert ist, das Gerät in der Shop-Manager-App mit dem richtigen Shop verbunden ist und
  Benachrichtigungen für die App in Ihren Android-Systemeinstellungen aktiviert sind.
- **Benachrichtigung kommt verspätet an** – neu registrierte Geräte können bis zu 15 Minuten
  benötigen, bis die erste Benachrichtigung eintrifft; nachfolgende Bestellungen werden in
  Echtzeit zugestellt.
- **Mehrere Geräte** – wiederholen Sie Schritt 2 auf jedem Gerät. Jedes mit dem Shop verbundene
  Gerät erhält seine eigene Benachrichtigung.

## Deinstallation

Das Deaktivieren oder Deinstallieren der App unter **Erweiterungen → Meine Erweiterungen** stoppt
alle Push-Benachrichtigungen für den Shop und entfernt die registrierten Gerätedaten.
