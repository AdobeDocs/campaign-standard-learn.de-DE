---
title: Fehlerbehebung für Marketing-Fachleute
description: Das Wissen über die häufigsten Fehler kann bei der schnelleren Problemlösung helfen und Ihre Produktivität steigern. Diese Tipps zur Fehlerbehebung helfen Ihnen dabei, ähnliche Fehler wie sie auftreten effektiv zu beheben.
version: Standard
feature: Workflows
role: User
level: Beginner, Intermediate, Experienced
doc-type: Article
last-substantial-update: 2023-05-18T00:00:00Z
jira: KT-13256
thumbnail: KT-13256.jpeg
exl-id: 24a6815b-52d1-4bd6-9d27-522720a91f83
source-git-commit: cfa097e1ea0d5ca8c97c1062ea8717c37a51530d
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Fehlerbehebung für Marketingexperten: 5 häufige Workflow- und Bereitstellungsfehler

Von: [Suraj Patra](https://www.linkedin.com/in/suraj-p-51612053/){target="_blank"}, Senior Consultant, Meijer

Als Senior Engineer und Customer Experte für Adobe Experience Cloud-Produkte der letzten fünf Jahre habe ich es Geschäftsbenutzern ermöglicht, bei [Meijer](https://www.meijer.com/){target="_blank"}, einer 1934 gegründeten amerikanischen Supercenter-Kette, komplexe Marketing- und Transaktionskampagnen mit ACS durchzuführen. Zu den Projekten, an denen ich gearbeitet habe, zählen benutzerspezifische Kampagnen zum Speichern von Angeboten und Bestelldetails für die Personalisierung, die Integration in Adobe Audience Manager und Kundeneinblicke für die Segmentaufnahme.


In meiner Zeit mit ACS bin ich auf Fehler gestoßen, die zeitaufwendig und frustrierend sein können zu lösen. Das Wissen über die häufigsten Fehler kann bei der schnelleren Problemlösung helfen und Ihre Produktivität steigern. Im Folgenden finden Sie meine Tipps zur Fehlerbehebung, mit denen Sie ähnliche Fehler wirksam beheben können, sobald sie auftreten.

## Fehler bei Datentyp-Abweichung

**Fehlercode:**
`PGS-220000 PostgreSQL error: ERROR: operator does not exist: character varying = bigint`

**Ursache:**
Diese Fehlertypen werden in einem Workflow angezeigt, wenn Sie versuchen, die Abstimmung mit Feldern unterschiedlicher Datentypen durchzuführen. Wenn Sie beispielsweise eine Datei mit einer Datei laden, die ein Zeichenfolgenfeld enthält, und versuchen, das Zeichenfolgenfeld mit einem Profilfeld mit dem Datentyp int abzustimmen.

![data-type-mismatch-error](/help/assets/kt-13256/data-type-mismatch.png)

**Lösung:**
Ändern Sie den Datentyp des Felds in der Aktivität &quot;Datei laden&quot;in den Datentyp, mit dem Sie übereinstimmen. Öffnen Sie die Aktivität &quot;Datei laden&quot;. Wechseln Sie zum Tab &quot;SPALTENDEFINITION&quot;und ändern Sie den Datentyp des gewünschten Felds.


![data-type-mismatch-solution](/help/assets/kt-13256/data-type-mismatch-solution.png)

## Personalization-Versandfehler

**Fehlercode:**
`The schema for profiles specified in the transition ('') is not compatible with the schema defined in the delivery template ('nms:recipient'). They should be identical.`

**Ursache:**
Dieser Fehler wird angezeigt, wenn Sie eine E-Mail an eine Adresse senden, die E-Mail-Adresse oder eine andere Kennung jedoch nicht mit einem Profil abgestimmt ist. Um eine E-Mail-Kommunikation zu senden, sollte die E-Mail oder die Kennung stets mit einem Profil verknüpft sein.

![Workflow mit Abstimmungsaktivität](/help/assets/kt-13256/del-persn-error-wf.png)

**Lösung:**
In der geladenen Datei mit der Empfängertabelle muss eine gemeinsame ID vorhanden sein. Dieser gemeinsame Schlüssel fügt die Datei in die Empfängertabelle der Abstimmungsaktivität ein. E-Mails dürfen nicht an Datensätze gesendet werden, die nicht in der Empfängertabelle vorhanden sind. Dies erfordert diesen Abstimmungsschritt innerhalb des Workflows. Dadurch stimmen Sie die Aktivität &quot;Eingehende Datei laden&quot;mit einer Kennung wie der E-Mail-ID aus dem Profil ab. Das Schema `nms:recipient` bezieht sich auf die Profiltabelle, und durch die Abstimmung der eingehenden Datensätze mit dem Profil wird sie während der E-Mail-Vorbereitung verfügbar gemacht.

Siehe Screenshot der Abstimmungsaktivität wie unten dargestellt.

![Workflow mit Abstimmdetails](/help/assets/kt-13256/del-persn-error-wf-solution.png)

Erfahren Sie mehr über die [Abstimmung](https://experienceleague.adobe.com/en/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/reconciliation).

## Allgemeiner Fehler bei Felddatensätzen

**Fehlercode:**
`The document types of inbound events (''and'') are incompatible (step 'Exclusion'). Unable to perform the operation. `

**Ursache:**
Dieses Problem tritt bei der Verwendung der **Ausschlussaktivität** in ACS-Workflows auf, wenn ein Ausschluss anhand der ID ausgeführt wird, wenn der Primäre Satz und der ausgeschlossene Satz nicht dieselben Feldnamen haben.


![Fehler im allgemeinen Felddatensatz](/help/assets/kt-13256/dataset-error.png)

**Lösung:**

Es gibt zwei Möglichkeiten, diesen Fehler zu beheben:

1. Verwenden Sie denselben Feldnamen sowohl in der primären als auch in der ausgeschlossenen Datei und verwenden Sie dieses Feld als ID

   ODER

2. Verwenden Sie die Ausschlussmethode JOINS , um das Feld auszuwählen, auf dessen Grundlage Sie die Datensätze ausschließen möchten.

![Dataset-Fehler für gemeinsames Feld - Lösung ](/help/assets/kt-13256/dataset-error-solution.png)

## Fehler bei ausgelassenem Feldnamen

**Fehlercode:**
`XTK-170036 Unable to parse expression 'i__name'`

**Ursache:**

In einer **Anreicherungsaktivität** können Fehlerpunkte auftreten. Eine der häufigsten wird unten angezeigt.

![ Name des Dropped Fehlers ](/help/assets/kt-13256/field-name-dropped-error.png)

Dies geschieht, wenn Sie einen Ausdrucksnamen in der Aktivität manuell bearbeiten. Das Bild zeigt, dass der Ausdruck von `name `in `i__name` geändert wurde.

**Lösung:**

Sie können diesen Fehler auf drei Arten beheben:

1. Ändern Sie den Namen zurück in den ursprünglich vorhandenen Ausdruck.

2. Wenn Sie einen neuen Namen verwenden möchten, ändern Sie die Werte in der **Anreicherungsaktivität**.

3. Wenn Sie sich nicht erinnern, was sich geändert hat, wäre es am besten, die Aktivität neu zu erstellen.

## Temporärer Fehler bei übersprungener Tabelle 

**Fehlercode:**
`XTK-170024 The temporary schema "temp:deliveryEmail1" is not defined in the current context.`

**Ursache:**
Dies ist ein häufiger Fehler bei komplizierten Workflows, die eine Anreicherung oder eine andere Aktivität erfordern. Dies bedeutet wahrscheinlich, dass einige der Aktivitäts-Workflows bei mehreren Änderungen am Workflow nicht korrekt gespeichert werden.

![Fehler bei übersprungener temporärer Tabelle ](/help/assets/kt-13256/temp-table-dropped-error.png)

**Lösung:**
Dieser Fehler kann auf vielerlei Weise auftreten, sodass es keine einfache Korrektur gibt. Wenn es sich um einen einfachen Workflow handelt, ist es besser, die Aktivität neu zu konfigurieren. In einem komplizierten Workflow ist es besser, die Workflow-Aktivitäten in einen neuen Workflow zu kopieren, zu speichern und erneut auszuführen.
