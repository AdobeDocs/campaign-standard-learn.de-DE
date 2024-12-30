---
title: 'SCHRITT 4: Festlegen der Push-Kennung'
description: Der **pushIdentifier** ist eine Zeichenfolge, die das Geräte-Token für Push-Benachrichtigungen enthält. Es ist dasselbe Token, das von Firebase gesendet und mit der MobileCore.setPushIdentifier-Methode an die SDK übergeben wird.
feature: Push
user: Admin
level: Experienced
jira: KT-4828
doc-type: tutorial
activity: use
team: TM
exl-id: 08387b84-edaa-45ee-ae66-53bcbd5c7c39
source-git-commit: 757afce50981b96b7820c987308d639a73746c0c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Schritt 4: [!DNL pushidentifier] festlegen

Der **[!DNL pushidentifier]** ist eine Zeichenfolge, die das Geräte-Token für [!DNL Push]-Benachrichtigungen enthält. Es ist dasselbe Token, das von [!DNL Firebase] gesendet und mit der [!DNL MobileCore.setPushIdentifier]-Methode an den SDK übergeben wird.

Öffnen Sie Ihr Projekt in [!DNL Android™]studio. Löschen Sie den gesamten Code in [!DNL MainActivity] **mit Ausnahme der ersten Zeile, die Ihre Paketanweisung ist**.

Fügen Sie den folgenden Code in [!DNL MainActivity] ein:

<!--
Removed `{.line-numbers}` below
-->

```java
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;
import android.widget.Toast;

import com.adobe.marketing.mobile.MobileCore;
import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.firebase.iid.FirebaseInstanceId;
import com.google.firebase.iid.InstanceIdResult;

public class MainActivity extends AppCompatActivity {

@Override
protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);

registerToken();
}

void registerToken() {
FirebaseInstanceId.getInstance().getInstanceId()
    .addOnCompleteListener(new OnCompleteListener<InstanceIdResult>() {
        @Override
        public void onComplete(@NonNull Task<InstanceIdResult> task) {
            if (!task.isSuccessful()) {
                Log.w("Message App", "getInstanceId failed", task.getException());
                return;
            }

// Get new Instance ID token
String token = task.getResult().getToken();

Log.d("Got token", token);

MobileCore.setPushIdentifier(token);
}
});
}

@Override
public void onResume() {
super.onResume();
MobileCore.setApplication(getApplication());
MobileCore.lifecycleStart(null);
}

@Override
public void onPause() {
super.onPause();
MobileCore.lifecyclePause();
}
}
```

## Testen der App

Jetzt ist ein guter Zeitpunkt, um Ihre App zu testen, bevor Sie fortfahren.

* Führen Sie Ihre App aus, indem Sie auf den grünen Pfeil klicken oder **[!DNL Run->Run'app']** auswählen.
* Der [!DNL Android™]-Emulator sollte gestartet werden und die App sollte mit &quot;[!DNL "Hello World"]&quot; ausgeführt werden.
* Öffnen Sie das [!DNL logcat]. Suchen Sie nach &quot;[!DNL Got]&quot;. Sie sollten das Token sehen, das von [!DNL Firebase] empfangen wurde, das wie unten dargestellt in das Protokoll geschrieben wurde. Die lange Zeichenfolge nach &quot;[!DNL Got token]&quot; ist die [!DNL pushidentifier], die an Adobe Campaign gesendet wird.

![logcat-token](assets/logcat-got-token.PNG)

### Mobile-App-Abonnenten überprüfen

Melden Sie sich bei Ihrer Adobe Campaign Standard-Instanz an.
Navigieren Sie **[!UICONTROL Administration->Kanäle->Mobile App (Experience Platform SDK)]**. Öffnen Sie die entsprechende Mobile App. Wechseln Sie zur Registerkarte [!UICONTROL Mobile-App-Abonnenten] . Es sollte ein „Registrierungs[!UICONTROL Token“ ] werden.

![mobile-application-subscribers](assets/mobile-application-subscribers.PNG)

>[!NOTE]
>
>Wird das Anmelde-Token auf der Registerkarte [!UICONTROL Mobile-App-Abonnenten] hier nicht angezeigt, fahren Sie mit dem Vorgang fort.
