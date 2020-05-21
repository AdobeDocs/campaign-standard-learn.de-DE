---
title: Einführung in In-App-Nachrichten
description: Mit dem In-App-Nachrichten-Kanal (Adobe Campaign Standard, ACS) können Sie dem Benutzer kontextrelevante In-App-Nachrichten präsentieren, die auf das Echtzeitverhalten eines Kunden innerhalb der Mobilanwendung reagieren.
feature: In-App
topics: Mobile
kt: 1911
doc-type: feature video
activity: use
team: TM
translation-type: tm+mt
source-git-commit: 82fb2d39dc61a55c0aa20ca1fa215f35a7dd9088
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 10%

---


# Einführung in [!UICONTROL In-App] -Nachrichten {#introduction}

The [!UICONTROL In-App Messaging] channel allows you to display a message when the user is active within the mobile application. This channel requires mobile applications to be integrated with [!UICONTROL Adobe Experience Platform SDK].

In diesem Lernprogramm werden die Schritte erläutert, die zum Einrichten der mobilen Eigenschaften, der [!UICONTROL Start] -Erweiterung für den [!UICONTROL In-App-Nachrichten] -Kanal sowie zum Vorbereiten, Anpassen und Senden von [!UICONTROL In-App] -Nachrichten in Adobe Campaign Standard erforderlich sind. Über die Links gelangen Sie zu den Videoschulungen zu den einzelnen Themen.

## Voraussetzungen {#prerequisites}

1. Make sure you can access the **[!UICONTROL In-App]** channel. Wenn Sie keinen Zugriff auf diesen Kanal haben, kontaktieren Sie das für Ihr Konto zuständige Team.
1. Verify that your **user** has the necessary **permissions** in Adobe Campaign Standard and [!UICONTROL Launch].

   1. Stellen Sie in Adobe Campaign Standard sicher, dass der IMS-Benutzer zur [!UICONTROL Standard-Benutzer] - und [!UICONTROL Administratorgruppe] gehört.\
      Dieser Schritt ermöglicht es dem Benutzer, sich bei Adobe Campaign Standard anzumelden, zur Experience Platform SDK-Seite für mobile Apps zu navigieren und die Eigenschaften für mobile Apps, die Sie in [!UICONTROL Launch]erstellt haben, Ansicht.
   1. Stellen Sie bei [!UICONTROL Launch]sicher, dass Ihr IMS-Benutzer Teil eines [!UICONTROL Launch] -Profils ist.\
      Dieser Schritt ermöglicht es dem Benutzer, sich bei [!UICONTROL Launch] anzumelden, um die Eigenschaften zu erstellen und Ansicht. Weitere Informationen zu Produkt-Profilen in [!UICONTROL Launch]finden Sie unter [Erstellen Sie Ihr Profil](https://docs.adobelaunch.com/launch-reference/administration/user-permissions#3-create-your-product-profile). Im Profil &quot;product&quot;sollten keine Berechtigungen für die Firma oder die Eigenschaften festgelegt sein, der Benutzer sollte sich aber dennoch anmelden können.

1. Starten der Adobe Experience Platform:

   1. Erstellen Sie die mobile Anwendung, indem Sie eine mobile Eigenschaft erstellen und Ihre mobile App mit dem Experience Platform SDK instrumentieren.
   1. Install the **Adobe Campaign Standard** extension for your mobile application.

For more on extensions, refer to the [Configure Campaign Standard extension in Adobe Launch](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) in [!UICONTROL Adobe Launch ]documentation.

## Schritte zum Einrichten von [!UICONTROL In-App] -Nachrichten {#steps-to-set-up}

1. [Konfigurieren einer mobilen Anwendung mit dem Adobe Experience Platform SDK](/help/communication-channels/mobile/configure-mobile-apps-using-aep-sdk.md).

1. [Konfigurieren Sie Ereignis](/help/communication-channels/mobile/in-app/configure-events.md).

## Erstellen, Verwalten und Veröffentlichen von [!UICONTROL In-App] -Versänden {#create-manage-publish}

Sie können entweder einmal In-App-Versand erstellen, indem Sie auf die Karte &quot;In-App-Nachricht **** erstellen&quot;auf der Homepage oder in den [!UICONTROL Marketing-Aktivitäten]klicken, oder Sie können einen In-App-Versand in einem Workflow [](/help/communication-channels/mobile/in-app/in-app-activity.md)erstellen.

Beim Einrichten des Versands haben Sie drei Möglichkeiten, die Zielgruppe Ihrer Benutzer aus verschiedenen Versandvorlagen zu wählen:

1. [**Senden Sie eine In-App-Nachricht **](/help/communication-channels/mobile/in-app/broadcast-in-app-message.md)an die Zielgruppe aller Benutzer einer mobilen App.

   Mit diesem Nachrichtentyp können Sie Nachrichten an alle Benutzer Ihrer mobilen Anwendung (aktuell oder zukünftig) senden, auch wenn sie kein vorhandenes Profil im Adobe Campaign haben. Eine Personalisierung ist daher nicht möglich, wenn die Nachrichten angepasst werden, da das Profil des Benutzers nicht unbedingt in Adobe Campaign vorhanden ist.

1. Zielgruppe aller Benutzer auf Grundlage ihres mobilen App-Profils.

   Dieser Nachrichtentyp ermöglicht die Zielgruppe aller bekannten oder anonymen Benutzer einer mobilen App, die über ein mobiles Profil in Adobe Campaign verfügen. Dieser Nachrichtentyp kann nur mit nicht-personenbezogenen und nicht-sensiblen Attributen personalisiert werden und benötigt auch keinen sicheren Handshake zwischen dem Mobile SDK und dem In-App-Messaging-Dienst von Adobe Campaign. Die Personalisierungsstrategie basiert auf dem, was Sie über die Benutzer aus ihrer Interaktion mit dem Gerät gelernt haben. Zielgruppe aller Benutzer, die ihre App in der letzten Woche mehr als fünfmal gestartet haben.

1. [**Nutzer der Zielgruppe auf der Basis ihres Campaign-Profils **](/help/communication-channels/mobile/in-app/target-users-based-on-campaign-profile.md).

   Dieser Nachrichtentyp ermöglicht Ihnen die Zielgruppe von Adobe Campaign-Profilen (CRM-Profilen), die Ihre Mobilanwendung abonniert haben. Die Nachricht kann mit allen verfügbaren Profil-Attributen in Adobe Campaign personalisiert werden, erfordert jedoch einen sicheren Handshake zwischen dem Mobile SDK und dem In-App-Nachrichtendienst der Kampagne, um sicherzustellen, dass Nachrichten mit persönlichen und sensiblen Informationen nur von autorisierten Benutzern verwendet werden.

Diese Vorlage ist hilfreich, um Anwendungsfälle für die Orchestrierung von Kanälen zu unterstützen, bei denen Sie bereits auf andere Kanal wie E-Mail oder Push abgestellt haben und die Benutzer anhand ihrer Antwort mit einer In-App-Nachricht interagieren möchten.

## Berichte zu In-App-Versänden {#report}

Sobald Ihr Versand veröffentlicht wurde, können Sie einen [Bericht über Ihren In-App-Versand](/help/communication-channels/mobile/in-app/in-app-reporting.md)erstellen.

## Zusätzliche Ressourcen

* [In-App-Bericht](https://docs.adobe.com/content/help/en/campaign-standard/using/reporting/list-of-reports/in-app-report.html)
* [Einrichten einer mobilen Eigenschaft](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property)
* [Konfigurieren einer mobilen Anwendung mit Adobe Experience Platform SDKs](https://helpx.adobe.com/de/campaign/kb/configuring-app-sdk.html)
* [In-App-Nachricht vorbereiten und senden](https://docs.adobe.com/content/help/en/campaign-standard/using/communication-channels/in-app-messaging/preparing-and-sending-an-in-app-message.html)
* [In-App-Nachricht anpassen](https://docs.adobe.com/content/help/en/campaign-standard/using/communication-channels/in-app-messaging/customizing-an-in-app-message.html)
* [In-App-Nachricht in einem Workflow senden](https://docs.adobe.com/content/help/en/campaign-standard/using/managing-processes-and-data/channel-activities/in-app-delivery.html)
* [Lebenszyklusmetriken aktivieren](https://aep-sdks.gitbook.io/docs/getting-started/initialize-the-sdk#enable-lifecycle-metrics)