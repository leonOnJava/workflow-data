Kontext & Problemstellung:
    Die aktuelle Abbruchrate beim Login ist zu hoch, da Nutzer ihre Zugangsdaten vergessen und der Prozess zur Wiederherstellung unvollständig ist. Um den Support zu entlasten und die Benutzerfreundlichkeit zu erhöhen, muss das System um eine automatisierte Self-Service-Wiederherstellung erweitert werden.

    System-Anforderungen (Functional Requirements):

        Einstiegspunkt: Die bestehende Login-Maske benötigt ein klickbares Element („Passwort vergessen?“), das den Nutzer auf eine separate Eingabeseite weiterleitet.

        Identifikation & Validierung: Auf der Folgeseite ist die Eingabe der registrierten E-Mail-Adresse erforderlich. Das System muss im Hintergrund prüfen, ob zu dieser Adresse ein aktiver Account existiert.

        Sicherheits-Richtlinie (User Enumeration): Aus Datenschutzgründen darf die Systemantwort keine Rückschlüsse darüber zulassen, ob die eingegebene E-Mail-Adresse im System existiert oder nicht. Die Benutzeroberfläche muss in beiden Fällen exakt dieselbe Erfolgsmeldung ausgeben („Falls ein Konto existiert, wurde eine E-Mail versendet“).

        Token-Generierung & Ablauf: Wenn das Konto existiert, generiert das System einen kryptografisch sicheren Validierungs-Token. Dieser Token darf eine maximale Lebensdauer von genau 120 Minuten besitzen. Nach Ablauf der Zeit ist der Link ungültig und ein Aufruf führt zu einer Fehlermeldung auf der Plattform.

        Kommunikations-Schnittstelle: Die Zustellung des Tokens erfolgt asynchron per E-Mail. Die Nachricht enthält einen personalisierten Link, der den Token als Parameter übergibt.

        Passwort-Änderung & Restriktionen: Nach Klick auf den Link gelangt der Nutzer auf ein Formular zur Vergabe des neuen Passworts. Hierbei greift die globale Passwort-Richtlinie der Plattform:

            Mindestlänge: 12 Zeichen

            Mindestens 1 numerisches Zeichen (0-9)

            Mindestens 1 Sonderzeichen (z. B. !, @, #, $, %)

        Abschluss: Nach erfolgreicher Änderung wird der Token sofort serverseitig invalidiert, sodass er kein zweites Mal verwendet werden kann. Der Nutzer wird zur Login-Seite weitergeleitet.
