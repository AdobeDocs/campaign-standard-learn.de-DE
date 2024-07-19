---
title: 'Schritt 3: Registrieren der Erweiterungen für Ihre Mobile App'
description: In diesem Teil fügen wir den Code zur Registrierung der UserProfile-, Identity-, Lifecycle- und Signal-Erweiterungen hinzu.
feature: Push
user: Admin
level: Experienced
jira: KT-4827
doc-type: tutorial
activity: use
team: TM
exl-id: d8c0d8c6-2e04-4c27-b27a-d0de79dd953b
source-git-commit: 9be31e056800b806c49a2c5ffbf9f9f42b001d4c
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 14%

---

# Schritt 3: Registrieren der Erweiterungen für Ihre Mobile App

In diesem Teil fügen wir den Code hinzu, um die Erweiterungen Benutzerprofil, Identität, Lebenszyklus und Signal zu registrieren. Wir müssen auch die Adobe Campaign Standard-Erweiterung registrieren, wie im folgenden Code dargestellt.

Öffnen Sie Ihr Projekt in [!DNL Android] Studio. Löschen Sie den gesamten Code in MainApp **mit Ausnahme der ersten Zeile, die Ihre Paketanweisung** ist.

Fügen Sie den folgenden Code in MainApp ein

<!--
Removed `{.line-numbers}` below
-->

```java
import [!DNL android].app.Application;
import android.util.Log;

import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Campaign;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.InvalidInitException;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.UserProfile;

public class MainApp extends Application {

@Override
public void onCreate() {
super.onCreate();

MobileCore.setApplication(this);
MobileCore.setLogLevel(LoggingMode.DEBUG);

try{
    Campaign.registerExtension();
    UserProfile.registerExtension();
    Identity.registerExtension();
    Lifecycle.registerExtension();
    Signal.registerExtension();
    MobileCore.start(new AdobeCallback () {
        @Override
        public void call(Object o) {
            MobileCore.configureWithAppID("copy your launch property id here");
        }
    });
} catch (InvalidInitException e) {
    Log.d("ACS Exception", "exception");
}
}
}
```

In Zeile 32 müssen Sie die Umgebungs-Datei-ID der Eigenschaft[!UICONTROL  Launch] angeben. Der Zugriff darauf erfolgt über die Registerkarte [!UICONTROL Umgebung] Ihrer Eigenschaft [!UICONTROL Launch] .

![launch-id](assets/launch-id-property.PNG)
