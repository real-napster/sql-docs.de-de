---
title: Überwachen (Replikation) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], about monitoring replication
- transactional replication, monitoring
- monitoring [SQL Server replication]
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
- replication [SQL Server], monitoring
- administering replication, monitoring
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c65f93054125090f92eb4924e1007d5b9075c0f4
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2019
ms.locfileid: "54128190"
---
# <a name="monitoring-replication"></a>Überwachen (Replikation)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Die Überwachung einer Replikationstopologie ist ein wichtiger Aspekt bei der Bereitstellung der Replikation. Da die Replikationsaktivität verteilt ist, ist es außerordentlich wichtig, die Aktivität und den Status auf allen an der Replikation beteiligten Computern nachzuverfolgen. Sie können verschiedene Überwachungstools verwenden, um häufig gestellte Fragen wie die folgenden zu beantworten: 

-   Arbeitet das System fehlerfrei?
-   Welche Abonnements sind langsam?
-   Wie weit ist das Transaktionsabonnement in Verzug?
-   Wie lange dauert es bei der Transaktionsreplikation, bis eine Transaktion, für die ein Commit ausgeführt wurde, den Abonnenten erreicht?
-   Warum ist das Mergeabonnement langsam?
-   Warum wird ein Agent nicht ausgeführt?  
  

Zum Überwachen der Replikation stehen die folgenden Tools zur Verfügung:  
  
-   **SQL Server-Replikationsmonitor:** das wichtigste Tool für die Überwachung der Replikation. Es bietet eine verlegerfokussierte Sicht auf die gesamte Replikationsaktivität. Weitere Informationen finden Sie unter [Monitoring Replication](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md). 
-   **SQL Server Management Studio:** bietet Zugriff auf den Replikationsmonitor. Darüber hinaus können Sie über dieses Tool den aktuellen Status und die letzte Meldung anzeigen lassen, die von den folgenden Agents protokolliert wurde, sowie die Agents starten und beenden: Protokolllese-Agent, Momentaufnahmen-Agent, Merge-Agent bzw. Verteilungs-Agent. Weitere Informationen finden Sie unter [Monitor Replication Agents](../../../relational-databases/replication/monitor/monitor-replication-agents.md).  
  
-   **Transact-SQL (T-SQL) und Replikationsverwaltungsobjekte (Replication Management Objects, RMO):** Über beide Schnittstellen können Sie alle Replikationstypen des Verteilers überwachen. Bei Mergereplikationen haben Sie außerdem die Möglichkeit, die Replikation vom Abonnenten aus zu überwachen.  
  
-   **Warnungen für Replikations-Agentereignisse:** Die Replikation bietet eine Reihe vordefinierter Warnungen für Replikations-Agent-Ereignisse. Darüber hinaus können Sie bei Bedarf auch zusätzliche Warnungen erstellen. Warnungen können verwendet werden, um eine automatische Antwort auf ein Ereignis auszulösen und/oder einen Administrator zu benachrichtigen. Weitere Informationen finden Sie unter [Verwenden von Warnungen für Replikations-Agentereignisse](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
-   **Systemmonitor:** nützlich für die Überwachung der Leistung; stellt eine Reihe von Zählern für die Replikation bereit. Weitere Informationen finden Sie unter [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md).  
  

## <a name="see-also"></a>Weitere Informationen  
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   

  
  
