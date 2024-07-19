---
title: 'SCHRITT 4: Festlegen der Pushidentifier'
description: Der **pushIdentifier** ist eine Zeichenfolge, die das Geräte-Token für Push-Benachrichtigungen enthält. Es handelt sich um dasselbe Token, das von Firebase gesendet und mithilfe der MobileCore.setPushIdentifier -Methode an das SDK übergeben wird.
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
source-wordcount: '224'
ht-degree: 0%

---

# Schritt 4: Festlegen von [!DNL pushidentifier]

Der **[!DNL pushidentifier]** ist eine Zeichenfolge, die das Geräte-Token für [!DNL Push] -Benachrichtigungen enthält. Es ist dasselbe Token, das von [!DNL Firebase] gesendet und mithilfe der [!DNL MobileCore.setPushIdentifier] -Methode an das SDK übergeben wird.

Öffnen Sie Ihr Projekt in [!DNL Android™]studio. Löschen Sie den gesamten Code in [!DNL MainActivity] **mit Ausnahme der ersten Zeile, die Ihre Paketanweisung** ist.

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

## App testen

Jetzt ist eine gute Zeit, Ihre App zu testen, bevor Sie weitermachen.

* Führen Sie Ihre App aus, indem Sie auf den grünen Pfeil klicken oder **[!DNL Run->Run'app']** auswählen.
* Der [!DNL Android™]-Emulator sollte starten und Sie sollten sehen, wie Ihre App mit [!DNL "Hello World"]text ausgeführt wird.
* Öffnen Sie das Fenster &quot;[!DNL logcat]&quot;. Suchen Sie nach &quot;[!DNL Got]&quot;. Das Token, das von [!DNL Firebase] empfangen wurde, sollte wie unten gezeigt in das Protokoll geschrieben sein. Die lange Zeichenfolge nach &quot;[!DNL Got token]&quot; ist die [!DNL pushidentifier], die an Adobe Campaign gesendet wird.

![logcat-token](assets/logcat-got-token.PNG)

### Mobile-App-Abonnenten überprüfen

Melden Sie sich bei Ihrer Adobe Campaign Standard-Instanz an.
Navigieren Sie zu **[!UICONTROL Administration->Kanäle->Mobile App(Experience Platform SDK)]**. Öffnen Sie die entsprechende Mobile App. Registerkarte auf der Registerkarte [!UICONTROL Mobile-App-Abonnenten] . Es sollte ein [!UICONTROL Registrierungstoken]aufgelistet sein.

![mobile-application-subscribers](assets/mobile-application-subscribers.PNG)

>[!NOTE]
>
>Wenn Sie das Anmeldetoken nicht auf der Registerkarte [!UICONTROL Mobile-App-Abonnenten] sehen, STOP hier , bevor Sie fortfahren.
