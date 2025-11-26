---
layout: default
---

# 1. Erste Schritte
---
&nbsp;

## **1.1 Login im IBM Cloud Portal**

Der erste Schritt zur Arbeit mit der IBM Cloud ist die Anmeldung im IBM Cloud Portal

1. Öffnen Sie die Login-Seite: [IBM Cloud Login](cloud.ibm.com/login)
2. Geben Sie ihre Zugangsdaten (Benutzername und Passwort) ein
3. Bestätigen Sie die Anmeldung, um Zugriff auf das IBM Cloud Dashboard zu erhalten

<img src="{{ site.baseurl }}/screenshots/IBMCloud_Login.png" alt="IBM Cloud Login" width="550">


## **1.2 Multi-Faktor-Authentisierung (MFA) aktivieren**

Nach der Anmeldung im IBM Cloud Account sollte der nächste Schritt die Aktivierung der Multi-Faktor-Authentifizierung (MFA) sein.

**Warum MFA?** 

Ein ausschließlich passwortgeschütztes Konto erfüllt heutzutage nicht mehr die gängigen Sicherheitsanforderungen. MFA ist in vielen Bereichen wie Banking oder sozialen Netzwerken bereits Standard und wird auch in der IBM Cloud **als Best Practice empfohlen**.

**Um MFA zu aktivieren befolgen Sie folgende Schritte:**

1. Navigieren Sie in der oberen Leiste zu ``Manage`` und wählen Sie den Unterpunkt ``Access (IAM)``
2. In der linken Seitenleiste klicken Sie auf ``Settings``
3. Unter ``Settings`` wechseln Sie zu ``Authentication``

**Hier können Sie nun auswählen, wie die MFA eingerichtet werden soll. Die empfohlene Einstellung ist:**

- **MFA for a user with an IBMid**  
- **Either**, MFA für federated und non-federated User aktivieren


<img src="{{ site.baseurl }}/screenshots/MFA1:2.png" alt="MFA" width="1500">

<img src="{{ site.baseurl }}/screenshots/MFA2:2.png" alt="MFA" width="1500">

&nbsp;

## **1.3 Account-Einstellungen / Aktivieren einer Subscription**

Um wichtige Informationen wie den Account-Namen oder die Account-ID herauszufinden, sowie um Subscriptions einzulösen und andere Einstellungen wie:

- Financial Services Validated
- EU Supported
- HIPAA Supported
- Enterprise-managed IAM
- Commercial Proof of Concept (PoC)
- Virtual Routing and Forwarding
- Service Endpoints

**zu verwalten, gehen Sie wie folgt vor:**

1. Navigieren Sie in der oberen Leiste zu ``Manage`` und 
2. Wählen Sie den Unterpunkt ``Account``
2. Klicken Sie in der Seitenleiste auf ``Account Settings``

&nbsp;

<img src="{{ site.baseurl }}/screenshots/Settins1-2.png" alt="AccSettings" width="1500">

<img src="{{ site.baseurl }}/screenshots/Settings2-2.png" alt="AccSettings" width="1500">

&nbsp;

# 2 Arbeiten mit Ressorucengruppen
---
&nbsp;

## **2.1 Ressourcengruppen erklärt** 

Ressourcengruppen sind **logische Container**, die zusammengehörige Cloud-Ressourcen (VMs, Datenbanken etc.) organisieren. Sie dienen als zentrale Ankerpunkte, um **IAM-Zugriffsrichtlinien auf die gesamte Gruppe anzuwenden** und so die Berechtigungsverwaltung zu vereinfachen. Zudem ermöglichen sie eine **klare Kostenverfolgung (Billing)** und die **einfache, isolierte Verwaltung** des gesamten Lebenszyklus der enthaltenen Ressourcen.


<img src="{{ site.baseurl }}/screenshots/Ressourcengruppen.png" alt="Ressoucengruppen_explained" width="1500">

&nbsp;

Der physische Standort der Ressourcen ist für die Gruppierung dabei irrelevant. Eine Ressourcengruppe kann Ressourcen enthalten, die über verschiedene geografische Zonen und Regionen verteilt bereitgestellt wurden.

&nbsp;

<img src="{{ site.baseurl }}/screenshots/res_grp_zonen.png" alt="Ressoucengruppen_explained" width="1500">

&nbsp;

## **2.2 Ressourcengruppen anlegen** 

Planen Sie Ihre Hierarchie, bevor Sie die erste Ressourcengruppe anlegen. Überlegen Sie, ob eine Gliederung nach Umgebungen (Dev/Test), Projekten oder Teams für Ihren Fall am besten geeignet ist. Berücksichtigen Sie dabei, wie Sie Berechtigungen vererben, Kosten zuordnen und Ressourcen im Team verwalten möchten.

Eine Ressourcengruppe wird wie folgt angelegt: 

1. Navigieren Sie in der oberen Leiste zu ``Manage`` und 
2. Wählen Sie den Unterpunkt ``Account``
3. Klicken Sie auf der linken Leiste auf ``Account resources``
4. Navigieren Sie in den Unterpunkt ``Resource groups``
5. Auf der rechten Seite können Sie nun auf ``Create +`` klicken

&nbsp;

<img src="{{ site.baseurl }}/screenshots/create_rc_grp.png" alt="Ressoucengruppen_explained" width="1500">

&nbsp;


# 3. Identity and Access Management (IAM)
---
&nbsp;

## **3.1 IAM-Überblick** 

**Identitätsverwaltung (Manage Identities)**

- **Trusted Profiles:** Ermöglichen eine sichere, passwortlose Authentifizierung für Compute-Ressourcen (z. B. Cluster, VPCs) oder föderierte Nutzer. Sie machen die Verwaltung langlebiger Credentials in Anwendungen überflüssig.

- **Service IDs:** Identitäten für Anwendungen, Tools und automatisierte Prozesse. Da sie von menschlichen Benutzern entkoppelt sind, bleiben Workflows auch bei Mitarbeiterwechseln stabil.

- **API Keys:** Berechtigungsnachweise für die Authentifizierung über CLI oder API. Sie können entweder einem persönlichen Benutzerkonto oder einer Service-ID zugeordnet werden, um Aktionen programmatisch auszuführen.

- **Identity Providers:** Ermöglicht die Anbindung externer Firmenverzeichnisse (z. B. via SAML oder OpenID Connect). Benutzer authentifizieren sich mit ihren bestehenden Unternehmens-Zugangsdaten (Single Sign-On).

**Zugriffssteuerung (Manage Access)**

- **Access Groups:** Das wichtigste Instrument für effiziente Rechteverwaltung. IAM-Richtlinien werden einmalig der Gruppe zugewiesen; alle Mitglieder (Benutzer, Service-IDs) erben diese Berechtigungen automatisch.

- **Authorizations:** Regeln den direkten Zugriff zwischen IBM Cloud Services (Service-zu-Service), ohne dass eine Benutzeridentität involviert ist (z. B. ein Kubernetes-Cluster darf auf eine Container Registry zugreifen).

- **Roles:** Definieren die spezifisch erlaubten Aktionen. IBM unterscheidet dabei zwischen ``Plattform-Rollen`` (Verwaltung des COS, z. B. Erstellen/Löschen) und ``Service-Rollen`` (Nutzung des COS , z. B. Daten lesen/schreiben).


<img src="{{ site.baseurl }}/screenshots/IAM_overview.png" alt="IAM_overview" width="1500">