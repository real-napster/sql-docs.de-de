---
title: Überwachen der DQS-Aktivitäten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.administration.activitymonitoring.f1
helpviewer_keywords:
- monitoring activity
- activity monitoring
ms.assetid: 1d4c76f3-0d7b-498e-b792-4db4a0349814
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a44434be6f3908ebf7837a80b188affe226d88f3
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035161"
---
# <a name="monitor-dqs-activities"></a>Überwachen der DQS-Aktivitäten
  In diesem Thema wird beschrieben, wie die folgenden Aktivitäten in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) zentral überwacht werden: Wissensermittlung, Domänenverwaltung, Abgleichsrichtlinie, Datenbereinigung, Datenabgleich und SSIS-Bereinigung.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
 Nur Benutzer mit der dqs_administrator-Rolle in der Datenbank DQS_Main können eine Aktivität oder einen Prozess innerhalb einer Aktivität beenden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
  
-   Sie müssen über die dqs_kb_editor- oder dqs_kb_operator-Rolle in der Datenbank DQS_MAIN verfügen, um die DQS-Aktivitäten anzuzeigen.  
  
-   Sie müssen über die dqs_administrator-Rolle in der Datenbank DQS_MAIN verfügen, um die DQS-Aktivitäten anzuzeigen und außerdem eine Aktivität oder einen Prozess innerhalb einer Aktivität zu beenden.  
  
##  <a name="View"></a> Anzeigen von DQS-Aktivitäten  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Aktivitätsüberwachung**. Der Bildschirm Aktivitätsüberwachung wird geöffnet.  
  
     ![Bildschirm „Aktivitätsüberwachung“](../../2014/data-quality-services/media/dqs-activitymonitoring.gif "Activity Monitoring screen")  
  
3.  Auf dem Bildschirm Aktivitätsüberwachung werden Informationen zu jeder Aktivität in einem Aktivitätsraster angezeigt. Das Aktivitätsraster zeigt die folgenden Informationen zu jeder DQS-Aktivität an:  
  
    |Information|Description|  
    |-----------------|-----------------|  
    |**ID**|Ein ganzzahliger Wert. Eindeutige Aktivitätsnummer, die das System für die Aktivitätsüberwachung generiert.|  
    |**Name**|Der Name der Wissensdatenbank oder des Data Quality-Projekts, die bzw. das für diese Aktivität verwendet wird.|  
    |**Ist aktiv**|Gibt an, ob die Aktivität derzeit aktiv ist. Die folgenden Werte sind möglich:<br /><br /> **Aktive**: Aktivität wird gerade ausgeführt.<br /><br /> **beendet**: Aktivität wurde beendet.<br /><br /> **Beendet**: Aktivität wurde beendet mit Bildschirm aktivitätsüberwachung vom DQS-Administrator oder die Aktivität wurde vom Benutzer abgebrochen, während der Ausführung im entsprechenden Funktionsbereich in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].|  
    |**Typ**|Gibt den Typ der Aktivität an. Folgenden werden Aktivitätstypen überwacht: **Wissensverwaltung**, **DQ-Projekt**, und **SSIS-Bereinigung**.|  
    |**Untertyp**|Gibt den jeweiligen Workflow an, der für einen Aktivitätstyp ausgeführt wird.<br /><br /> Ein **Wissensverwaltung** Aktivität verfügt über die folgenden Workflows oder Untertypen: **Wissensermittlung**, **Domänenverwaltung**, und **Abgleichsrichtlinie**.<br /><br /> Ein **DQ-Projekt** Aktivität verfügt über die folgenden Workflows oder Untertypen: **Bereinigung** und **übereinstimmende**.<br /><br /> Der Aktivitätstyp **SSIS-Bereinigung** kann nur den Workflow oder Untertyp **Bereinigung** aufweisen.|  
    |**Aktueller Status**|Zeigt den aktuellen Status einer Aktivität an. Der Aktivitätsstatus wird durch den zuletzt durchgeführten Berechnungsprozess bestimmt. Die folgenden Werte sind möglich:<br /><br /> **Ausführung**: Der Berechnungsprozess wird ausgeführt.<br /><br /> **Erfolgreich**: Bevor ein Berechnungsprozess ausgeführt wird, wird der Status auf gesetzt **erfolgreich**. Nachdem der Berechnungsprozess erfolgreich beendet wurde, wird der Status erneut auf **Erfolgreich**festgelegt.<br /><br /> **Fehler bei**: Im Berechnungsprozess ist ein Fehler aufgetreten.<br /><br /> **Beendet**: Der Berechnungsprozess wurde beendet.<br /><br /> <br /><br /> Hinweis: So wie der Ermittlungsprozess (im Rahmen der Wissensermittlungsaktivität) kann auch der Berechnungsprozess für eine Aktivität mehrmals ausgeführt werden. Aus diesem Grund kann sich der Status während der Lebensdauer einer Aktivität mehrere Male ändern.|  
    |**DQKB**|Name der Wissensdatenbank, die für die Aktivität verwendet wird.|  
    |**Benutzer**|Der Name des Benutzers, der die Aktivität initiiert hat, oder der letzte Benutzer, der die Aktivität verwendet hat (falls es sich dabei nicht um denselben Benutzer handelt).|  
    |**Startzeit der Aktivität**|Datum und Uhrzeit beim Start der Aktivität|  
    |**Verstrichene Zeit**|Die verstrichene Zeit seit dem Start der Aktivität. Dies wird in der Schreibweise HH:MM:SS angezeigt.|  
    |**Endzeit der Aktivität**|Datum und Uhrzeit bei der Beendigung der Aktivität.|  
  
##  <a name="Filter"></a> Filtern von DQS-Aktivitätsinformationen  
 Sie können im Filterbereich des Bildschirms Aktivitätsüberwachung (**Filtern nach**, **Wert**, **Ab Datum**und **Bis Datum**) die erforderlichen Aktivitäten nach bestimmten Kriterien filtern und anzeigen. So filtern Sie Aktivitätsdatensätze:  
  
1.  Legen Sie das Filterkriterium fest: Sie können die Aktivitätsdatensätze basierend auf einem Wert in einer der Spalten im Aktivitätsraster (wertbasiert) und/oder basierend auf einem Datumsbereich filtern.  
  
    1.  **Werten basierende Filterung**: Wählen Sie ein Filterkriterium in der **Filtern nach** aus, und wählen Sie dann den entsprechenden Wert zum Filtern nach in die **Wert** Liste. Wenn Sie in der Liste **Filtern nach** eine Option ausgewählt haben, wird die Liste **Wert** mit den möglichen Werten aktualisiert. Sie können durch die folgenden Felder in den Aktivitätsdatensätzen filtern: **Ist aktiv**, **Typ**, **Untertyp**, **aktueller Status**, **DQKB**, und **Benutzer**.  
  
    2.  **Datumsfilterung bereichsbasierte**: Auswählen der entsprechende Daten in die **ab Datum** und **bis Datum** Datumssteuerelemente. Standardmäßig liegt das im Feld **Ab Datum** angezeigte Datum zwei Tage vor dem aktuellen Datum, und in **Bis Datum** ist das aktuelle Datum angegeben. Die Filterung erfolgt nicht basierend auf den *Ab* - und *Bis* -Daten, sondern basierend auf dem Datumsbereich. Dies bedeutet, dass jede Aktivität, die während des ausgewählten Datumsbereichs ausgeführt wurde, angezeigt wird.  
  
2.  Klicken Sie auf das Symbol **Aktivitätsliste aktualisieren** , um den Filter anzuwenden, und zeigen Sie nur die gefilterten DQS-Aktivitäten an.  
  
##  <a name="ActivityDetails"></a> Anzeigen von DQS-Aktivitätsdetails  
 Sie können ausführliche Informationen zu einer DQS-Aktivität, z. B. Aktivitätsschritte und Profiler-Informationen im Bildschirm Aktivitätsüberwachung anzeigen. Gehen Sie folgendermaßen vor:  
  
1.  Wählen Sie eine DQS-Aktivität im Aktivitätsraster (im oberen Bereich) aus.  
  
2.  Im unteren Bereich werden die Aktivitätsdetails der ausgewählten Aktivität auf den beiden folgenden Registerkarten angezeigt:  
  
    -   **Aktivitätsschritte**: Zeigt ein Raster mit den berechnungsprozessen (aktivitätsschritten), die der ausgewählten Aktivität zugeordnet sind. Auf dieser Registerkarte können mehrere Aktivitätsschritte für eine Aktivität angezeigt werden. Dies ist dann der Fall, wenn der gleiche Aktivitätsschritt innerhalb der Aktivität mehrere Male vom Benutzer ausgeführt wurde. Beispielsweise kann der Aktivitätsschritt beendet und wieder gestartet worden sein. Das Raster auf dieser Registerkarte zeigt die folgende Informationen für jeden Aktivitätsschritt an der Aktivität zugeordnet: **Typ**, **aktueller Status**, **Startzeit**, **verstrichene Zeit**, und **Endzeit**.  
  
    -   **Profiler**: Zeigt die Informationen für die profilerstellung für aktuelle und vergangene Aktivitäten an. Für aktuelle Aktivitäten werden die Informationen teilweise, jedoch konsistent, angezeigt. Die Profilerstellungsdaten einer Aktivität werden in eine Excel-Datei exportiert, wenn Sie die entsprechenden Aktivitätsdetails in eine Excel-Datei exportieren. Die Informationen sind in der exportierten Excel-Datei in den Arbeitsblättern **Profiler – Quelle** und **Profiler – Felder** verfügbar.  
  
##  <a name="Export"></a> Exportieren von DQS-Aktivitätsdetails  
 Sie können die Aktivitätseigenschaften, Aktivitätsprozesse und Profilerstellungsdaten einer Aktivität im Überwachungsbildschirm in eine Excel-Datei exportieren. Gehen Sie hierzu wie folgt vor:  
  
1.  Wählen Sie eine Aktivität im Aktivitätsraster (im oberen Bereich) aus.  
  
2.  Klicken Sie auf das Symbol **Ausgewählte Aktivität nach Excel exportieren** . Klicken Sie alternativ mit der rechten Maustaste auf eine Aktivität im Aktivitätsraster, und klicken Sie anschließend im Kontextmenü auf **Aktivität exportieren** .  
  
3.  Sie werden aufgefordert, einen Namen und einen Speicherort für die zu speichernde Excel-Datei anzugeben. Die exportierte Excel-Datei enthält folgende Arbeitsblätter:  
  
    |Blattname|Description|  
    |----------------|-----------------|  
    |Aktivität|Enthält Informationen (Spalten) zur Aktivität wie das Aktivitätsraster.|  
    |Prozesse|Enthält Informationen (Spalten) zu den Prozessen in der Aktivität wie die Registerkarte **Aktivitätsschritte** .|  
    |Profiler – Quelle|Für die **Bereinigung** Untertyp, enthält die folgenden Informationen zur Aktivität:   Datensätze, richtige Datensätze, korrigierte Datensätze und ungültige Datensätze.<br /><br /> Für **Wissensermittlung**, **Domänenverwaltung**, **Abgleichsrichtlinie**, und **übereinstimmende** Untertypen, die Folgendes enthält Informationen zur Aktivität:   Datensätze, Gesamtwerte, neue Werte, eindeutige Werte und neue eindeutige Werte.|  
    |Profiler – Felder|Für **Bereinigung** und **SSIS-Bereinigung** Untertypen, enthält die folgenden Informationen zur Aktivität:   Feld, Domäne, korrigierte Werte, Werte, Vollständigkeit und Genauigkeit empfohlen.<br /><br /> Für **Wissensermittlung**, **Domänenverwaltung**, **Abgleichsrichtlinie**, und **übereinstimmende** Untertypen, die Folgendes enthält Informationen zur Aktivität:   Feld, Domäne, neu, eindeutig, in die Domäne und Vollständigkeit gültig.|  
  
##  <a name="Terminate"></a> Beenden einer DQS-Aktivität  
 DQS-Administratoren (dqs_administrator-Rolle) können eine ausgeführte (aktive) Aktivität beenden, die nicht vom Typ **SSIS-Bereinigung**ist. Wenn eine Aktivität beendet wird, werden alle ausgeführten Prozesse in der Aktivität beendet und alle mit der Aktivität verbundenen Elemente entfernt. Dieser Vorgang kann nicht rückgängig gemacht werden. Das Beenden einer Aktivität im Bildschirm Aktivitätsüberwachung ist damit vergleichbar, die entsprechende Aktivität abzubrechen, indem Sie auf **Abbrechen** klicken, während die Aktivität im Funktionsbereich in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]ausgeführt wird. So beenden Sie eine Aktivität:  
  
1.  Wählen Sie eine Aktivität, die ausgeführt wird, im Aktivitätsraster (im oberen Bereich) aus.  
  
2.  Klicken Sie auf das Symbol **Ausgewählte Aktivität beenden** . Klicken Sie alternativ mit der rechten Maustaste auf die Aktivität im Aktivitätsraster, und klicken Sie anschließend im Kontextmenü auf **Aktivität beenden** .  
  
3.  Eine Meldung wird angezeigt, um die Aktion zu bestätigen. Klicken Sie auf **Ja**.  
  
##  <a name="Stop"></a> Beenden eines Prozesses in einer DQS-Aktivität  
 DQS-Administratoren (dqs_administrator-Rolle) können einen ausgeführten (aktiven) Prozess in einer Aktivität beenden, die nicht vom Typ **SSIS-Bereinigung**ist. Das Beenden eines Prozesses im Bildschirm Aktivitätsüberwachung ist damit vergleichbar, den Prozess innerhalb der entsprechenden Aktivität im Funktionsbereich in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]zu beenden. Beispiele: das Beenden des computergestützten Bereinigungsprozesses innerhalb einer Bereinigungsaktivität oder das Beenden des Abgleichsprozesses innerhalb einer Abgleichsaktivität. Ein beendeter Prozess kann nicht im Bildschirm Aktivitätsüberwachung neu gestartet werden. Sie müssen den Prozess im entsprechenden Funktionsbereich im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]neu starten. In dem Fall wird auf der Registerkarte **Aktivitätsschritte** eine zusätzliche Zeile zum Prozessraster hinzugefügt. Der Status des beendeten Prozesses wird weiterhin als **Beendet** angezeigt. So beenden Sie einen Prozess:  
  
1.  Wählen Sie einen Prozess, der ausgeführt wird, im Raster Aktivitätsdetails (im unteren Bereich) aus.  
  
2.  Klicken Sie auf das Symbol **Ausgewählten Prozess beenden** . Klicken Sie alternativ mit der rechten Maustaste auf den Prozess im Raster Aktivitätsdetails, und klicken Sie anschließend im Kontextmenü auf **Prozess beenden** .  
  
3.  Eine Meldung wird angezeigt, um die Aktion zu bestätigen. Klicken Sie auf **Ja**.  
  
  
