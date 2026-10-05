---
title: Erste Schritte mit Push-Benachrichtigungen mit der Android™-Mobile-App
description: Dieses Tutorial führt Sie durch die Schritte, die für das Senden von Push-Benachrichtigungen in Adobe Campaign und den Empfang dieser Benachrichtigungen in Ihrer Android™-Mobile-App erforderlich sind.
feature: Push
jira: KT-3846
doc-type: tutorial
activity: use
team: TM
recommendations: noDisplay
exl-id: 8dd772b2-b082-4e1e-842d-c5d6bcec564c
TQID: 'https://experienceleague.adobe.com/Ov4KKtdN-uhIr-TGldJCXw3GYFNUjap-SBE227dImfw'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: f5407121-8933-4ac3-8e06-a9b692a4e88a
    internal-label: Campaign Standard
feature_v2:
  - id: a4671286-a59f-47e3-b97b-90627a1977d5
    internal-label: Communication channels
subfeature_v2:
  - id: a4657621-810c-498b-8a27-7ced9c176dda
    internal-label: Push notifications
source-git-commit: 508c3590ce956401ccfba3a256000cbc5849a684
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 100%
---
# Erste Schritte mit Push-Benachrichtigungen mit der Android™-Mobile-App

Sie können mit Adobe Campaign personalisierte und segmentierte Push-Benachrichtigungen an iOS- und Android™-Mobilgeräte versenden.
Diese Nachrichten werden in Mobile Apps empfangen, die in Adobe Campaign unter Verwendung des Experience Cloud Mobile SDK V4 oder Experience Platform SDK eingerichtet werden.
Dieses Tutorial führt Sie durch die Schritte, die für das Senden von Push-Benachrichtigungen in Adobe Campaign und den Empfang dieser Benachrichtigungen in Ihrer Android™-Mobile-App erforderlich sind.

## Voraussetzungen

* Sie sollten die Eigenschaft &quot;launch&quot; mit der Adobe Campaign Standard-Erweiterung konfiguriert haben. Befolgen Sie die unten aufgeführte Online-Hilfe.
  * [Video-Tutorial](https://video.tv.adobe.com/v/26224?learn=on){transcript=true}
  * [Dokumentation](https://experienceleague.adobe.com/docs/campaign-standard-learn/tutorials/communication-channels/mobile/configure-mobile-apps-using-aep-sdk.html?lang=de)

* Vergewissern Sie sich, dass der Status der entsprechenden Eigenschaft in Adobe Campaign Standard auf „Konfiguriert“ gesetzt ist.
* [Ein aktives Google Firebase-Konto muss vorhanden sein.](https://firebase.google.com)
* [Die aktuelle Version von Android™ Studio muss installiert sein.](https://developer.android.com/studio)

## Tutorial-Schritte

* [Schritt 1: Erstellen einer Android™ Mobile App](/help/tutorial-push-notifications-android/create-android-app.md)
* [Schritt 2: Integrieren des Mobile SDK](/help/tutorial-push-notifications-android/integrating-with-mobile-sdk.md)
* [Schritt 3: Registrieren der Erweiterungen für Ihre Mobile App](/help/tutorial-push-notifications-android/register-mobile-extensions.md)
* [Schritt 4: Festlegen der Push-Kennung](/help/tutorial-push-notifications-android/set-push-identifier.md)
* [Schritt 5: Verbreiten von Benachrichtigungen](/help/tutorial-push-notifications-android/propagate-notification.md)
* [Schritt 6: Senden von Push-Benachrichtigungen](/help/tutorial-push-notifications-android/send-push-notification.md)
