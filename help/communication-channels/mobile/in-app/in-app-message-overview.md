---
title: Einführung in In-App-Nachrichten
description: Erfahren Sie, wie Sie dem Benutzer als Reaktion auf das Echtzeit-Verhalten eines Kunden in der Mobile App kontextuell relevante In-App-Nachrichten präsentieren.
feature: In App
kt: 1911
doc-type: feature video
activity: use
team: TM
exl-id: c51716eb-7239-4fc0-9ccf-9f5f0a5fae65
role: User
level: Beginner
source-git-commit: 57dbf456625d22cd2e4526d92e5a8c20a048d339
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 13%

---

# Einführung in [!UICONTROL In-App] messages {#introduction}

Die [!UICONTROL In-App-Nachrichten] -Kanal ermöglicht die Anzeige einer Nachricht, wenn der Benutzer in der Mobile App aktiv ist. Für diesen Kanal müssen mobile Anwendungen in integriert werden. [!UICONTROL Adobe Experience Platform SDK].

In diesem Tutorial werden die Schritte erläutert, die zum Einrichten der Eigenschaften für Mobilgeräte erforderlich sind. [!UICONTROL Launch] -Erweiterung für [!UICONTROL In-App-Nachrichten] Kanal und dessen Vorbereitung, Anpassung und Versand [!UICONTROL In-App] Nachrichten in Adobe Campaign Standard. Die Links führen zu den Video-Tutorials zu den einzelnen hervorgehobenen Themen.

## Voraussetzungen {#prerequisites}

1. Stellen Sie sicher, dass Sie auf die **[!UICONTROL In-App]** -Kanal. Wenn Sie keinen Zugriff auf diesen Kanal haben, kontaktieren Sie das für Ihr Konto zuständige Team.
1. Stellen Sie sicher, dass **Benutzer** verfügt über **Berechtigungen** in Adobe Campaign Standard und [!UICONTROL Launch].

   1. Stellen Sie in Adobe Campaign Standard sicher, dass der IMS-Benutzer Teil der [!UICONTROL Standardbenutzer] und [!UICONTROL Administrator] Gruppen.

      Dieser Schritt ermöglicht es dem Benutzer, sich bei Adobe Campaign Standard anzumelden, zur Experience Platform SDK-Seite für mobile Apps zu navigieren und die Eigenschaften der mobilen App anzuzeigen, die Sie in [!UICONTROL Launch].

   1. In [!UICONTROL Launch]stellen Sie sicher, dass Ihr IMS-Benutzer Teil eines [!UICONTROL Launch] Produktprofil. Dieser Schritt ermöglicht es dem Benutzer, sich bei [!UICONTROL Launch] , um die Eigenschaften zu erstellen und anzuzeigen. Im Produktprofil sollten keine Berechtigungen für das Unternehmen oder die Eigenschaften festgelegt sein, aber der Benutzer sollte sich trotzdem anmelden können.

1. In Adobe Experience Platform Launch:

   1. Erstellen Sie die Mobile App, indem Sie eine mobile Eigenschaft erstellen und Ihre Mobile App mit dem Experience Platform SDK instrumentieren.
   1. Installieren Sie die **Adobe Campaign Standard** Erweiterung für Ihre Mobile App.

Weitere Informationen zu Erweiterungen finden Sie unter [Konfigurieren der Campaign Standard-Erweiterung in Adobe Launch](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) in der Dokumentation.

## Schritte zum Einrichten [!UICONTROL In-App] messages {#steps-to-set-up}

1. [Konfigurieren einer Mobile App mithilfe von Adobe Experience Platform SDKs](/help/communication-channels/mobile/configure-mobile-apps-using-aep-sdk.md).
1. [Ereignisse konfigurieren](/help/communication-channels/mobile/in-app/configure-events.md).

## Erstellen, Verwalten und Veröffentlichen [!UICONTROL In-App] Sendungen {#create-manage-publish}

Sie können entweder einmalige In-App-Sendungen erstellen, indem Sie auf die Schaltfläche **[!UICONTROL In-App-Nachricht erstellen]** -Karte von der Startseite aus, aus dem [!UICONTROL Marketingaktivitäten]oder Sie können [Erstellen eines In-App-Versands innerhalb eines Workflows](/help/communication-channels/mobile/in-app/in-app-activity.md).

Beim Einrichten des Versands stehen Ihnen drei Optionen zur Verfügung, mit denen Sie aus unterschiedlichen Versandvorlagen auswählen können:

1. [**In-App-Broadcast-Nachricht senden**](/help/communication-channels/mobile/in-app/broadcast-in-app-message.md) , um alle Benutzer einer Mobile App anzusprechen.

   Mit diesem Nachrichtentyp können Sie Nachrichten an alle (aktuellen oder künftigen) Benutzer Ihrer Mobile App senden, selbst wenn in Adobe Campaign kein Profil existiert. Daher ist eine Personalisierung bei der Anpassung der Nachrichten nicht möglich, da das Benutzerprofil nicht unbedingt in Adobe Campaign vorhanden ist.

1. Targeting aller Benutzer auf der Basis ihres mobilen App-Profils.

   Mit diesem Nachrichtentyp können Sie alle bekannten oder anonymen Benutzer einer Mobile App auswählen, die über ein mobiles Profil in Adobe Campaign verfügen. Dieser Nachrichtentyp kann nur mit nicht-personenbezogenen und nicht-sensiblen Attributen personalisiert werden und benötigt auch keinen sicheren Handshake zwischen dem Mobile SDK und dem In-App-Messaging-Dienst von Adobe Campaign. Die Personalisierungsstrategie basiert also auf dem, was Sie über die Benutzer aus ihrer Interaktion mit dem Gerät gelernt haben. Geben Sie beispielsweise alle Benutzer als Ziel an, die ihre App in der letzten Woche mehr als fünfmal gestartet haben.

1. [**Ansprechen von Benutzern auf der Basis ihres Campaign-Profils**](/help/communication-channels/mobile/in-app/target-users-based-on-campaign-profile.md).

   Mit diesem Nachrichtentyp können Sie Adobe Campaign-Profile (CRM-Profile) auswählen, die sich für Ihre Mobile App angemeldet haben. Die Nachricht kann mit allen in Adobe Campaign verfügbaren Profilattributen personalisiert werden. Sie erfordert einen sicheren Handshake zwischen dem Mobile SDK und dem In-App-Messaging-Dienst von Campaign, um sicherzustellen, dass Nachrichten mit persönlichen und sensiblen Informationen nur von autorisierten Benutzern verwendet werden.

Diese Vorlage ist nützlich, um Anwendungsfälle für die kanalübergreifende Orchestrierung der Customer Journey zu unterstützen, bei denen Sie bereits Benutzer auf andere Kanäle wie E-Mail oder Push angesprochen haben. Je nach Antwort möchten Sie dann mit einer In-App-Nachricht interagieren.

## Berichte zu In-App-Sendungen erstellen {#report}

Sobald Ihr Versand veröffentlicht wurde, können Sie [Bericht zu Ihrem In-App-Versand](/help/communication-channels/mobile/in-app/in-app-reporting.md).
