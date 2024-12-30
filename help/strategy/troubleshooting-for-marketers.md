---
title: Fehlerbehebung für Marketing-Fachleute
description: Das Wissen um die häufigsten Fehler kann Ihnen helfen, Probleme schneller zu lösen und Ihre Produktivität zu steigern. Diese Tipps zur Fehlerbehebung helfen Ihnen dabei, ähnliche Fehler bei ihrem Auftreten effektiv zu beheben.
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

# Fehlerbehebung für Marketing-Fachleute: 5 allgemeine Workflow- und Bereitstellungsfehler

Von: [Suraj Patra](https://www.linkedin.com/in/suraj-p-51612053/){target="_blank"}, Senior Consultant, Meijer

Als Senior Engineer und Kundenexperte für Adobe Experience Cloud-Produkte während der letzten fünf Jahre versetze ich Business-Anwenderinnen und -Anwender bei [Meijer](https://www.meijer.com/){target="_blank"}, einer 1934 gegründeten amerikanischen Supercenter-Kette, in die Lage, komplexe Marketing- und Transaktionskampagnen mit ACS durchzuführen. Zu den Projekten, an denen ich gearbeitet habe, gehören benutzerdefinierte Kampagnen zum Speichern von Angeboten und Bestelldetails für die Personalisierung, die in Adobe Audience Manager integriert sind, und Kundeninformationen für die Segmentaufnahme.


In meiner Zeit bei der Verwendung von ACS sind Fehler aufgetreten, deren Behebung zeitaufwendig und frustrierend sein kann. Das Wissen um die häufigsten Fehler kann Ihnen helfen, Probleme schneller zu lösen und Ihre Produktivität zu steigern. Im Folgenden finden Sie meine Tipps zur Fehlerbehebung, die Ihnen dabei helfen, ähnliche Fehler bei ihrem Auftreten effektiv zu beheben.

## Fehler wegen nicht übereinstimmender Datentypen

**Fehlercode:**
`PGS-220000 PostgreSQL error: ERROR: operator does not exist: character varying = bigint`

**Ursache:**
Diese Fehlertypen treten in einem Workflow auf, wenn Sie versuchen, Felder mit verschiedenen Datentypen auszugleichen. Beispiel: Sie laden eine Datei mithilfe von „Datei laden“ hoch, die ein Zeichenfolgenfeld enthält, und versuchen, das Zeichenfolgenfeld mit einem Profilfeld abzustimmen, das den Datentyp „int“ hat.

![data-type-mismatch-error](/help/assets/kt-13256/data-type-mismatch.png)

**Lösung:**
Ändern Sie den Datentyp des Felds in der Aktivität „Datei laden“ in den Datentyp, mit dem Sie übereinstimmen. Öffnen Sie die Aktivität „Datei laden“. Wechseln Sie zur Registerkarte „SPALTENDEFINITION“ und ändern Sie den Datentyp des gewünschten Felds.


![data-type-mismatch-solution](/help/assets/kt-13256/data-type-mismatch-solution.png)

## Fehler beim Versand-Personalization

**Fehlercode:**
`The schema for profiles specified in the transition ('') is not compatible with the schema defined in the delivery template ('nms:recipient'). They should be identical.`

**Ursache:**
Dieser Fehler tritt auf, wenn Sie eine E-Mail an eine Adresse senden, die E-Mail-Adresse oder eine andere Kennung jedoch nicht mit einem Profil abgeglichen wird. Zum Senden einer E-Mail-Kommunikation sollte die E-Mail oder die Kennung immer mit einem Profil verknüpft sein.

![Workflow mit Aktivität „Abstimmung“](/help/assets/kt-13256/del-persn-error-wf.png)

**Lösung:**
Aus der geladenen Datei mit der Empfängertabelle muss eine gemeinsame ID vorhanden sein. Dieser gemeinsame Schlüssel verbindet die Ladedatei mit der Empfängertabelle innerhalb der Abstimmaktivität. E-Mails dürfen nicht an Datensätze gesendet werden, die nicht in der Empfängertabelle vorhanden sind. Dies erfordert diesen Abstimmschritt innerhalb des Workflows. Auf diese Weise würden Sie die eingehende Aktivität zum Laden von Dateien mit einer Kennung wie der E-Mail-ID aus dem Profil in Einklang bringen. Das `nms:recipient` bezieht sich auf die Profiltabelle und durch die Abstimmung der eingehenden Datensätze mit dem Profil wird diese bei der E-Mail-Vorbereitung verfügbar.

Siehe den Screenshot für die Aktivität „Abstimmung“, wie unten dargestellt.

![Workflow mit Abstimmdetails](/help/assets/kt-13256/del-persn-error-wf-solution.png)

Weitere Informationen über [Abstimmung](https://experienceleague.adobe.com/en/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/reconciliation).

## Fehler bei gemeinsamem Feld-Datensatz

**Fehlercode:**
`The document types of inbound events (''and'') are incompatible (step 'Exclusion'). Unable to perform the operation. `

**Ursache:**
Dieses Problem tritt bei der Verwendung der **Ausschlussaktivität** in ACS-Workflows auf, wenn ein Ausschluss basierend auf der ID durchgeführt wird und der Primäre Satz und der ausgeschlossene Satz nicht dieselben Feldnamen haben.


![Datensatzfehler im allgemeinen Feld](/help/assets/kt-13256/dataset-error.png)

**Lösung:**

Es gibt zwei Möglichkeiten, diesen Fehler zu beheben:

1. Verwenden Sie denselben Feldnamen sowohl im primären als auch im ausgeschlossenen Feld und verwenden Sie dieses Feld als ID.

   ODER

2. Verwenden Sie die JOIN-Ausschlussmethode, um das Feld auszuwählen, auf dessen Grundlage Sie die Datensätze ausschließen möchten.

![Datensatzfehler im allgemeinen Feld - Lösung ](/help/assets/kt-13256/dataset-error-solution.png)

## Fehler beim Löschen des Feldnamens

**Fehlercode:**
`XTK-170036 Unable to parse expression 'i__name'`

**Ursache:**

Fehlerpunkte können in einer „Anreicherungsaktivität **auftreten**. Eine der häufigsten wird unten angezeigt.

![Fehler „Feldname gelöscht](/help/assets/kt-13256/field-name-dropped-error.png)

Dies geschieht, wenn Sie einen Ausdrucksnamen in der Aktivität manuell bearbeiten. Das Bild zeigt, dass der Ausdruck von `name ` zu `i__name` geändert wurde.

**Lösung:**

Sie können diesen Fehler auf drei Arten beheben:

1. Ändern Sie den Namen wieder in den ursprünglich vorhandenen Ausdruck.

2. Wenn Sie einen neuen Namen verwenden möchten, ändern Sie die Werte in der Aktivität **Anreicherung**.

3. Wenn Sie sich nicht daran erinnern, was sich geändert hat, ist es am besten, die Aktivität neu zu erstellen.

## Fehler beim Löschen der temporären Tabelle 

**Fehlercode:**
`XTK-170024 The temporary schema "temp:deliveryEmail1" is not defined in the current context.`

**Ursache:**
Dies ist ein häufiger Fehler in komplizierten Workflows, bei denen es um Anreicherung oder andere Aktivitäten geht. Dies bedeutet wahrscheinlich, dass einige der Aktivitäts-Workflows bei mehreren Änderungen am Workflow nicht korrekt gespeichert werden.

![Fehler beim Löschen der temporären Tabelle ](/help/assets/kt-13256/temp-table-dropped-error.png)

**Lösung:**
Es gibt viele Möglichkeiten, wie dieser Fehler auftreten kann, sodass es keine einfache Lösung gibt. Wenn es sich um einen einfachen Workflow handelt, ist es besser, die Aktivität neu zu konfigurieren. In einem komplizierten Workflow ist es besser, die Workflow-Aktivitäten in einen neuen Workflow zu kopieren, zu speichern und erneut auszuführen.
