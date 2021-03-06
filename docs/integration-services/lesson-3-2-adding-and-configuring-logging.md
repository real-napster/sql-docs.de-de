---
title: 'Schritt 2: Hinzufügen und Konfigurieren der Protokollierung | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a6ba2488aff0efdb6ed0d1c4ae03ec46ba6a6a25
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277909"
---
# <a name="lesson-3-2-add-and-configure-logging"></a>Lektion 3.2: Hinzufügen und Konfigurieren der Protokollierung

In dieser Aufgabe aktivieren Sie die Protokollierung für den Datenfluss im Paket „Lesson 3.dtsx“. Anschließend konfigurieren Sie einen Protokollanbieter für Textdateien, um die Ereignisse „PipelineExecutionPlan“ und „PipelineExecuteTrees“ zu protokollieren. Der Protokollanbieter für Textdateien erstellt Protokolle, die auf einfache Weise angezeigt werden können und portabel sind. Die Einfachheit dieser Protokolldateien ist während der grundlegenden Testphase eines Pakets nützlich. Sie können die Protokolleinträge auch im Fenster **Protokollereignisse** des [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designers anzeigen.  
  
## <a name="add-logging-to-the-package"></a>Hinzufügen der Protokollierung zu einem Paket  
  
1.  Klicken Sie im Menü **SSIS** auf **Protokollierung**.  
  
2.  Achten Sie darauf, dass im Dialogfeld **Configure SSIS Logs** (SSIS-Protokolle konfigurieren) innerhalb des Bereichs **Container** das oberste Objekt ausgewählt ist. Dieses Objekt stellt das Paket aus Lektion 3 dar.
  
3.  Wählen Sie auf der Registerkarte **Anbieter und Protokolle** im Feld **Anbietertyp** die Option **SSIS-Protokollanbieter für Textdateien**aus, und klicken Sie anschließend auf **Hinzufügen**.  
  
    Von Integration Services wird ein neuer Protokollanbieter für Textdateien mit dem Standardnamen **SSIS-Protokollanbieter für Textdateien** dem Paket hinzugefügt. Sie können jetzt den neuen Protokollanbieter konfigurieren.  
  
4.  Geben Sie in der Spalte **Name** die Zeichenfolge **Protokolldatei für Lektion 3** ein.  
  
5.  Ändern Sie optional **Beschreibung**.  
  
6.  Klicken Sie in der Spalte **Konfiguration** auf **\<Neue Verbindung>**, um anzugeben, wohin [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] die Protokollinformationen schreibt.  
  
    Wählen Sie im Dialogfeld **Dateiverbindungs-Manager-Editor** für **Verwendungstyp** die Option **Datei erstellen** aus, und klicken Sie anschließend auf **Durchsuchen**. Standardmäßig wird vom Dialogfeld **Datei auswählen** der Projektordner geöffnet, aber Sie können Protokollinformationen an beliebigen Speicherorten speichern.  
  
7.  Geben Sie im Dialogfeld **Datei auswählen** innerhalb des Felds **Dateiname** den Namen **Tutorialprotokoll.log**, und klicken Sie auf **Öffnen**.
  
8.  Klicken Sie auf **OK**, um das Dialogfeld **Dateiverbindungs-Manager-Editor** zu schließen.  
  
9. Erweitern Sie im **Container** -Bereich alle Knoten der Paketcontainerhierarchie, und deaktivieren Sie anschließend alle Kontrollkästchen, einschließlich des Kontrollkästchens für **Extract Sample Currency Data** . Aktivieren Sie jetzt das Kontrollkästchen für **Extract Sample Currency Data** , um nur die Ereignisse für diesen Knoten abzurufen.  
  
    > [!NOTE]  
    > Wenn der Status des Kontrollkästchens **Extract Sample Currency Data** abgeblendet anstatt ausgewählt ist, verwendet die Aufgabe die Protokolleinstellungen des übergeordneten Containers. In diesem Fall können Sie die aufgabenspezifischen Protokollereignisse nicht aktivieren. Deaktivieren Sie das übergeordnete Kontrollkästchen, um das Problem zu beheben.
  
10. Wählen Sie auf der Registerkarte **Details** in der Spalte **Ereignisse** die Ereignisse **PipelineExecutionPlan** und **PipelineExecutionTrees** aus.  
  
11. Klicken Sie auf **Erweitert**, um sich die Details anzusehen, die der Protokollanbieter für jedes Ereignis in das Protokoll schreibt. Standardmäßig werden alle Informationskategorien für die Ereignisse ausgewählt, die Sie angeben.  
  
12. Klicken Sie auf **Basic** (Einfach), um die Informationskategorien auszublenden.  
  
13. Wählen Sie auf der Registerkarte **Anbieter und Protokolle** in der **Name** -Spalte **Lesson 3 Log File**aus. Nach dem Erstellen eines Protokollanbieters für Ihr Paket können Sie diesen optional deaktivieren, um die Protokollierung zu deaktivieren, ohne dass Sie einen Protokollanbieter löschen und dann neu erstellen müssen.  
  
14. Wählen Sie **OK**.  
  
## <a name="go-to-next-task"></a>Weiter zur nächsten Aufgabe  
[Schritt 3: Testen des Tutorialpakets aus Lektion 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
