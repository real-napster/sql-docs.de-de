---
title: Warteschlangenlese-Agent | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.queuereaderagent.f1
helpviewer_keywords:
- Queue Reader Agent dialog box
ms.assetid: f02d24b6-dcb5-4126-b56e-fab41cfe4337
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7f07c9be82be63d01d563499a80e049e572a4150
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127220"
---
# <a name="queue-reader-agent"></a>Warteschlangenlese-Agent
  Im Dialogfeld **Warteschlangenlese-Agent** werden detaillierte Informationen zum Warteschlangenlese-Agent, wie Status, Verlauf, Informationsmeldungen und alle Fehlermeldungen, angezeigt.  
  
## <a name="options"></a>Optionen  
 Wählen Sie im Menü **Ansicht** aus, welche Sitzungen des Warteschlangenlese-Agents angezeigt werden, und wählen Sie dann eine bestimmte Sitzung aus dem Raster mit der Bezeichnung **Sitzungen des Warteschlangenlese-Agents**aus. Detaillierte Informationen zu dieser Sitzung werden im Raster mit der Bezeichnung **Aktionen in der ausgewählten Sitzung**angezeigt. Wenn die ausgewählte Sitzung mit einem Fehler beendet wurde, wird auch der Textbereich mit der Bezeichnung **Fehlerdetails oder Meldung der ausgewählten Sitzung** angezeigt.  
  
 **Ansicht**  
 Wählen Sie aus, welche Sitzungen des Warteschlangenlese-Agents angezeigt werden. Da der Warteschlangenlese-Agent in der Regel kontinuierlich ausgeführt wird, kann möglicherweise nur eine Sitzung angezeigt werden.  
  
 **Status**  
 Status des Warteschlangenlese-Agents. In der folgenden Liste sind die möglichen Statuswerte aufgeführt:  
  
-   Fehler  
  
-   Fehlgeschlagener Befehl wird wiederholt  
  
-   Wird nicht ausgeführt  
  
-   Wird ausgeführt  
  
 **Startzeit**  
 Startzeit der Sitzung.  
  
 **Beendigungszeit**  
 Beendigungszeit der Sitzung. Wenn der Agent noch nicht beendet wurde, ist dieses Feld leer.  
  
 **Dauer**  
 Zeitspanne, für die der Warteschlangenlese-Agent in dieser Sitzung ausgeführt wurde. Dieser Wert stellt die bisher abgelaufene Zeit dar, wenn der Agent immer noch ausgeführt wird, und die Gesamtzeit, wenn die Agentsitzung beendet ist.  
  
 **Fehlermeldung**  
 Wenn eine Sitzung mit einem Fehler beendet wurde, wird in diesem Feld die Fehlermeldung angezeigt, die vom Warteschlangenlese-Agent protokolliert wurde. Wurde die Sitzung nicht mit einem Fehler beendet, ist dieses Feld leer.  
  
 **Aktionsmeldung**  
 Alle Informationsmeldungen und Fehlermeldungen, die der Warteschlangenlese-Agent während der ausgewählten Sitzung protokolliert hat.  
  
 **Aktionszeit**  
 Zeit, zu der die unter **Aktionsmeldung** beschriebene Aktion ausgeführt wurde.  
  
 **Fehlerdetails oder Meldung der ausgewählten Sitzung**  
 Wird nur angezeigt, wenn in der ausgewählten Sitzung in der **Status** -Spalte der Wert **Fehler** angezeigt wird. Dieser Textbereich zeigt detaillierte Fehlerinformationen sowie den Befehl an, der zum Zeitpunkt des Fehlers auszuführen versucht wurde. Er enthält außerdem Links zu weiteren Informationen, die sich auf den Fehler beziehen.  
  
## <a name="see-also"></a>Siehe auch  
 [Starten des Replikationsmonitors](monitor/start-the-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben mithilfe des Replikationsmonitors](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Überwachen der Replikation](monitoring-replication.md)   
 [Übersicht über Replikations-Agents](agents/replication-agents-overview.md)  
  
  
