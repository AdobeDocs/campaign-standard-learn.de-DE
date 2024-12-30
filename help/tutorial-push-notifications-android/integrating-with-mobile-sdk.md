---
title: 'Schritt 2: Integrieren des Mobile SDK'
description: In diesem Teil integrieren wir die Android-App mit Mobile SDK. Integrieren von Mobile SDK mit der Android-App
feature: Push
user: Admin
level: Experienced
jira: KT-4826
doc-type: tutorial
activity: use
team: TM
recommendations: noDisplay
exl-id: 0fa53536-8330-4e96-be2f-afc078609bcd
source-git-commit: 913d2c08dc63e2073b3abd1de6b6b16711d817da
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# SCHRITT 2: Integrieren von [!UICONTROL Mobile SDK] mit der Android-App

In diesem Teil integrieren wir die [!DNL Android] App mit [!UICONTROL Mobile SDK]. Um [!UICONTROL Mobile SDK] mit der [!DNL Android] App zu integrieren, führen Sie die folgenden Schritte aus:

* Öffnen Sie das Projekt *ACSPushTutorial* in [!DNL Android Studio]
* Erstellen Sie eine neue Java-Klasse mit dem Namen *MainApp*, die [!DNL android.app.Application] erweitert
* Ihre Projektstruktur sollte jetzt wie folgt aussehen

![main-app](assets/android-main-app.PNG)

* Erweitern Sie den Ordner [!DNL Gradle Scripts] . Doppelklicken Sie auf die [!DNL build.gradle] des Moduls. Fügen Sie die folgenden Abhängigkeiten in den Abschnitt „Abhängigkeiten“ der [!DNL build.gradle] ein. Ihre [!DNL build.gradle] sollte jetzt wie folgt aussehen

<!--
Removed `{.line-numbers}` below
-->

```java
implementation 'com.adobe.marketing.mobile:campaign:1.+'
implementation 'com.adobe.marketing.mobile:userprofile:1.+'
implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
```

![module-gradle](assets/module-build-gradle.PNG)

* Synchronisieren Sie Ihr [!DNL Android] Projekt, indem Sie auf die Schaltfläche Jetzt synchronisieren klicken, um das Projekt zu synchronisieren

## [!DNL AndroidManifest.xml] ändern{#modify-android-manifest}

Öffnen Sie *AndroidManifest.xml* und fügen Sie die folgenden zwei Zeilen nach dem manifest-Element und vor dem application-Element ein. Dadurch kann Ihre App mit der Außenwelt kommunizieren

<!--
Removed `{.line-numbers}` below
-->

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

Kopieren Sie die folgende Zeile in das Anwendungselement
[!DNL android:name=".MainApp"]
[!DNL AndroidManifest.xml] speichern
Ihr [!DNL AndroidManifest.xml] sollte wie folgt aussehen

<!--
Removed `{.line-numbers}` below
-->

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.acspushtutorial">
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

<activity android:name=".MainActivity">
<intent-filter>
    <action android:name="android.intent.action.MAIN" />
    <category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
</activity>
</application>

</manifest>
```
