---
title: Öffnen, Entsperren, Umbenennen und Löschen eines Data Quality-Projekts | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dqproject.opendqproject.f1
helpviewer_keywords:
- data quality project,delete
- data quality project,rename
- data quality project,unlock
- data quality project,open
ms.assetid: de8a2b04-4673-4beb-b4cf-96a28cdf3a93
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 72ac098f34438d35de4b0c1ac0ebef0ffc30a043
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62469651"
---
# <a name="open-unlock-rename-and-delete-a-data-quality-project"></a>Öffnen, Entsperren, Umbenennen und Löschen eines Data Quality-Projekts

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In diesem Thema wird beschrieben, wie ein Data Quality-Projekt mithilfe von [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] verwaltet wird, zum Beispiel das Öffnen, Entsperren, Umbenennen und Löschen eines Data Quality-Projekts.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
  
-   Sie können kein gesperrtes Projekt öffnen, das von einem anderen Benutzer erstellt wurde.  
  
-   Sie können kein Data Quality-Projekt entsperren, umbenennen oder löschen, das von einem anderen Benutzer erstellt wurde.  
  
-   Sie können kein gesperrtes Data Quality-Projekt löschen. Zum Löschen müssen Sie es zunächst entsperren.  
  
-   Sie können nur ein Data Quality-Projekt entsperren, das von Ihnen erstellt wurde.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Sie müssen mindestens ein Data Quality-Projekt verwalten.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die Rolle „dqs_kb_editor“ oder „dqs_kb_operator“ in der Datenbank DQS_MAIN verfügen, um ein Data Quality-Projekt zu verwalten.  
  
##  <a name="Open"></a> Öffnen eines Data Quality-Projekts  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Data Quality-Projekt öffnen**. Der Bildschirm **Projekt öffnen** wird angezeigt.  
  
     Sie können ein unter **Zuletzt verwendetes Data Quality-Projekt** aufgelistetes Data Quality-Projekt auch direkt öffnen, indem Sie darauf klicken.  
  
3.  Wählen Sie auf dem Bildschirm **Projekt öffnen** das zu öffnende Data Quality-Projekt durch Klicken aus, und klicken Sie auf **Weiter**.  
  
4.  Das Data Quality-Projekt wird mit demselben Aktivitätsstatus geöffnet, mit dem es zuletzt geschlossen wurde. Ein Data Quality-Projekt hat die folgenden Status:  
  
    -   Bei der **Bereinigung** kann ein Data Quality-Projekt die folgenden Status aufweisen: **Bereinigung - Zuordnen**, **Bereinigung - Bereinigen**, **Bereinigung - Ergebnisse verwalten und anzeigen**, **Bereinigung - Export**.  
  
    -   Beim **Abgleichen** kann ein Data Quality-Projekt die folgenden Status aufweisen: **Abgleich - Zuordnung**, **Abgleich - Übereinstimmung**, **Abgleich - Survivorship**, **Abgleich - Export**.  
  
##  <a name="Unlock"></a> Entsperren eines Data Quality-Projekts  
 Wenn Sie ein Data Quality-Projekt erstellen, ist es gesperrt, um zu verhindern, dass es von anderen Benutzern verwendet oder geändert wird. Sie müssen das Data Quality-Projekt entsperren, nachdem Sie die Arbeit abgeschlossen haben, wenn Sie möchten, dass andere Benutzer am Data Quality-Projekt arbeiten können. Ein Schlosssymbol wird für gesperrte Projekte angezeigt.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Data Quality-Projekt öffnen**. Der Bildschirm **Projekt öffnen** wird angezeigt.  
  
3.  Klicken Sie auf dem Bildschirm **Projekt öffnen** mit der rechten Maustaste auf ein gesperrtes Data Quality-Projekt, das von Ihnen erstellt wurde, und klicken Sie dann im Kontextmenü auf **Entsperren** . Ein grünes Häkchen wird für das Projekt angezeigt, das angibt, dass es entsperrt wurde.  
  
##  <a name="Rename"></a> Umbenennen eines Data Quality-Projekts  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Data Quality-Projekt öffnen**. Der Bildschirm **Projekt öffnen** wird angezeigt.  
  
3.  Klicken Sie auf dem Bildschirm **Projekt öffnen** mit der rechten Maustaste auf ein Data Quality-Projekt, das von Ihnen erstellt wurde, und klicken Sie dann im Kontextmenü auf **Umbenennen** .  
  
4.  Der Name des Data Quality-Projekts kann in der Spalte **Name** bearbeitet werden. Heben Sie einen neuen Namen ein, und drücken Sie die EINGABETASTE.  
  
##  <a name="Delete"></a> Löschen eines Data Quality-Projekts  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Data Quality-Projekt öffnen**. Der Bildschirm **Projekt öffnen** wird angezeigt.  
  
3.  Klicken Sie auf dem Bildschirm **Projekt öffnen** mit der rechten Maustaste auf ein entsperrtes Data Quality-Projekt, das von Ihnen erstellt wurde, und klicken Sie dann im Kontextmenü auf **Löschen** .  
  
4.  Eine Bestätigungsmeldung wird angezeigt. Klicken Sie auf **Ja**.  
  
  
