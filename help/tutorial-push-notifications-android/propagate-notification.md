---
title: 'Schritt 5: Verbreiten von Benachrichtigungen'
description: In diesem Teil propagieren wir die von Adobe Campaign empfangene Nachricht mithilfe von Android Notification Manager.Firebase
feature: Push
jira: KT-4829
user: Admin
level: Experienced
doc-type: tutorial
activity: use
team: TM
exl-id: b0e01224-4ddc-4999-b8c6-794e49245428
source-git-commit: 200dcb4d6698c174f7fde508779609b11043d031
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Service hinzufügen, um Benachrichtigung zu senden

In diesem Teil propagieren wir die von Adobe Campaign empfangene Nachricht mithilfe von [!DNL Android Notification Manager]. [!DNL Notification manager] wird verwendet, um Benutzende über eingetretene Ereignisse zu informieren.
Auf diese Weise können Sie dem Benutzer mitteilen, dass im Hintergrund etwas passiert ist:

* [!DNL Android Studio] starten
* *[!DNL ACSPushTutorial]* Projekt öffnen
* Projektstruktur erweitern
* Klicken Sie mit der rechten Maustaste auf den Paketordner ([!DNL com.example.acspushtutorial]) und [!DNL New ->Java Class] Sie
* Benennen Sie diese Klasse *[!DNL MyService]* und stellen Sie sicher, dass sie [!DNL FirebaseMessagingService] erweitert
* Erstellen Sie *[!DNL sendNotification]* Methode in dieser Klasse. Bei dieser Methode müssen Sie den Inhalt und den Kanal der Benachrichtigung mithilfe eines [!DNL NotificationCompat.Builder]-Objekts festlegen. Damit die Benachrichtigung angezeigt wird, rufen Sie [!DNL NotificationManagerCompat.notify()] auf und übergeben Sie ihr eine eindeutige ID für die Benachrichtigung und das Ergebnis der [!DNL NotificationCompat.Builder.build()].

<!--
Removed `{.line-numbers}` below
-->

```java
package com.example.pushmessaging;
import android.app.NotificationChannel;
import android.app.NotificationManager;
import android.app.PendingIntent;
import android.content.Context;
import android.content.Intent;
import android.media.RingtoneManager;
import android.net.Uri;
import android.os.Build;
import android.util.Log;

import androidx.core.app.NotificationCompat;

import com.google.firebase.messaging.FirebaseMessagingService;
import com.google.firebase.messaging.RemoteMessage;

import java.util.Map;

public class MyService extends FirebaseMessagingService {
@Override
public void onMessageReceived(RemoteMessage remoteMessage)
{
Map<String,String> data  = remoteMessage.getData();
Log.d("data payload: ", data.toString());
sendNotification(remoteMessage);
}


private void sendNotification(RemoteMessage message) {
Intent intent = new Intent(this, MainActivity.class);
intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
PendingIntent pendingIntent = PendingIntent.getActivity(this, 0 /* Request code */, intent, PendingIntent.FLAG_ONE_SHOT);

String channelId = "0";
Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
NotificationCompat.Builder notificationBuilder =
        new NotificationCompat.Builder(this, channelId)
                .setSmallIcon(R.drawable.ic_launcher_background)
                .setContentTitle("Message from AEM")
                .setContentText(message.getData().get("body"))
                .setAutoCancel(true)
                .setSound(defaultSoundUri)
                .setContentIntent(pendingIntent);

NotificationManager notificationManager =
        (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);

// Since android Oreo notification channel is needed.
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
    NotificationChannel channel = new NotificationChannel(channelId,
            "Channel human readable title",
            NotificationManager.IMPORTANCE_DEFAULT);
    notificationManager.createNotificationChannel(channel);
}

notificationManager.notify(0 /* ID of notification */, notificationBuilder.build());
}
}
```

## [!DNL AndroidManifest.xml] ändern

Fügen Sie den erstellten Service zu Ihrem [!DNL AndroidManifest.xml] hinzu. Die endgültige [!DNL AndroidManifest.xml] sollte wie folgt aussehen:

<!--
Removed `{.line-numbers}` below
-->

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.pushmessaging">

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

    <application
        android:name=".MainApp"
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <service
            android:name=".MyService"
            android:exported="false">
            <intent-filter>
                <action android:name="com.google.firebase.MESSAGING_EVENT" />
            </intent-filter>
        </service>

        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

## Ausführen der App

Führen Sie die App aus, indem Sie auf **Symbolleiste oder** Menü [!DNL Run] auf den grünen Pfeil klicken.
