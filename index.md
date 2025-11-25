---
layout: default
---

# Erste Schritte 
---

## Login im IBM Cloud Portal

Der erste Schritt zur Arbeit mit der IBM Cloud ist die Anmeldung im IBM Cloud Portal.

1. Öffnen Sie die Login-Seite: [IBM Cloud Login](cloud.ibm.com/login)
2. Geben Sie ihre Zugangsdaten (Benutzername und Passwort) ein
3. Bestätigen Sie die Anmeldung, um Zugriff auf das IBM Cloud Dashboard zu erhalten

<img src="{{ site.baseurl }}/screenshots/IBMCloud_Login.png" alt="IBM Cloud Login" width="550">


## Multi-Faktor-Authentisierung (MFA) aktivieren

Nach der Anmeldung im IBM Cloud Account sollte der nächste Schritt die Aktivierung der Multi-Faktor-Authentifizierung (MFA) sein.

**Warum MFA?** 

Ein ausschließlich passwortgeschütztes Konto erfüllt heutzutage nicht mehr die gängigen Sicherheitsanforderungen. MFA ist in vielen Bereichen wie Banking oder sozialen Netzwerken bereits Standard und wird auch in der IBM Cloud **als Best Practice empfohlen**.

Um MFA zu aktivieren befolgen Sie folgende Schritte: 

1. . Navigieren Sie in der oberen Leiste zu **Manage** und wählen Sie den Unterpunkt **Access (IAM)**
2. In der linken Seitenleiste klicken Sie auf **Settings**
3. Unter **Settings** wechseln Sie zu **Authentication** 

Hier können Sie nun auswählen, wie die MFA eingerichtet werden soll.  Die empfohlene Einstellung ist:
- **MFA for a user with an IBMid**  
- Zusatzeinstellung: **Either**, MFA für federated udn non-federated User aktivieren

<img src="{{ site.baseurl }}/screenshots/MFA1:2.png" alt="IBM Cloud Login" width="550">

<img src="{{ site.baseurl }}/screenshots/MFA2:2.png" alt="IBM Cloud Login" width="550">

