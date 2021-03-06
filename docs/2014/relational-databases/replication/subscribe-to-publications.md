---
title: Abonnieren von Veröffentlichungen | Microsoft Dokumentation
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.conc.subtopubs.f1
helpviewer_keywords:
- subscriptions [SQL Server replication], about subscriptions
- pull subscriptions [SQL Server replication]
- subscriptions [SQL Server replication]
- push subscriptions [SQL Server replication], about push subscriptions
- merge replication subscribing [SQL Server replication]
- merge replication subscribing [SQL Server replication], about subscribing
- publications [SQL Server replication], subscribing
- push subscriptions [SQL Server replication]
- pull subscriptions [SQL Server replication], about pull subscriptions
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: 088ee30a-05ab-47c4-92ed-316b93e12445
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3aa122e19d890b0b994e4403dcc59b3131571d7c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62629694"
---
# <a name="subscribe-to-publications"></a>Abonnieren von Veröffentlichungen
  Bei einem Abonnement handelt es sich um eine Anforderung einer Kopie von Daten und Datenbankobjekten in einer Veröffentlichung. Mit einem Abonnement wird definiert, welche Veröffentlichung empfangen wird und wo und wann sie empfangen wird. Bei der Planung von Abonnements sollten Sie berücksichtigen, wo die Agentverarbeitung stattfinden soll. Durch den ausgewählten Abonnementtyp wird gesteuert, wo der Agent ausgeführt wird. Bei einem Pushabonnement wird der Merge-Agent oder der Verteilungs-Agent auf dem Verteiler ausgeführt, während die Agents bei Pullabonnements auf den Abonnenten ausgeführt werden. Nach der Erstellung eines Abonnements kann der zugehörige Abonnementtyp nicht mehr geändert werden.  
  
|Abonnement|Merkmale|Verwendung|  
|------------------|---------------------|--------------|  
|Pushabonnement|Bei einem Pushabonnement gibt der Verleger Änderungen an einen Abonnenten weiter, ohne dass ein Abonnent dies angefordert hat. Änderungen können bei Bedarf, kontinuierlich oder auf einen Zeitplan basierend per Push an den Abonnenten weitergegeben werden. Der Verteilungs-Agent oder der Merge-Agent wird auf dem Verteiler ausgeführt.|Daten werden normalerweise kontinuierlich oder im Rahmen eines sich regelmäßig wiederholenden Zeitplans synchronisiert.<br /><br /> Veröffentlichungen erfordern Bewegungen von Daten nahezu in Echtzeit.<br /><br /> Der höhere Prozessoroverhead auf einem Verteiler wirkt sich nicht auf die Leistung aus.<br /><br /> Wird am häufigsten mit Momentaufnahme- und Transaktionsreplikationen verwendet.|  
|Pullabonnement|Bei einem Pullabonnement fordert der Abonnent die auf dem Verleger vorgenommene Änderungen an. Mithilfe von Pullabonnements können Benutzer auf dem Abonnenten bestimmen, wann die Datenänderungen synchronisiert werden. Der Verteilungs-Agent oder der Merge-Agent wird auf dem Abonnenten ausgeführt.|Daten werden normalerweise bei Bedarf oder im Rahmen eines Zeitplans synchronisiert anstatt kontinuierlich.<br /><br /> Die Veröffentlichung verfügt über eine hohe Anzahl an Abonnenten, und bzw. oder es wäre zu ressourcenintensiv, alle Agents auf dem Verteiler auszuführen.<br /><br /> Abonnenten sind unabhängig, getrennt und bzw. oder mobil. Die Abonnenten bestimmen, wann eine Verbindung hergestellt wird und Synchronisierungsänderungen vorgenommen werden.<br /><br /> Wird am häufigsten für Mergereplikationen verwendet.|  
  
## <a name="merge-replication-subscription-types"></a>Abonnementtypen für Mergereplikationen  
 Für alle Replikationstypen sind Push- und Pullabonnements zulässig. Bei Mergereplikationen werden zur Unterscheidung von Abonnements zwei zusätzliche Begriffe verwendet: Client- und Serverabonnements. Mit Push- und Pullabonnements können sowohl Client- als auch Serverabonnements verwendet werden. Clientabonnements sind für die meisten Abonnenten geeignet, während Serverabonnements in der Regel für Abonnenten verwendet werden, die Daten auf anderen Abonnenten erneut veröffentlichten. Die Auswahl des Abonnements hat Auswirkungen auf die Konfliktlösung.  
  
## <a name="non-sql-server-subscribers"></a>Nicht-SQL Server-Abonnenten  
 Oracle und IBM DB2 können mithilfe von Pushabonnements Momentaufnahme- und Transaktionsveröffentlichungen abonnieren. Weitere Informationen finden Sie unter [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md).  
  
## <a name="creating-subscriptions"></a>Erstellen von Abonnements  
 Zum Erstellen eines Abonnements geben Sie folgende Informationen an:  
  
-   Der Name der Veröffentlichung.  
  
-   Den Namen des Abonnenten und der Abonnementdatenbank.  
  
-   Ob der Verteilungs-Agent oder der Merge-Agent auf dem Verteiler bzw. Abonnenten ausgeführt wird.  
  
-   Ob der Verteilungs-Agent oder Merge-Agent kontinuierlich, auf einem Zeitplan basierend oder nur bei Bedarf ausgeführt wird.  
  
-   Ob der Momentaufnahme-Agent eine aktualisierte Anfangsmomentaufnahme für das Abonnement erstellen und der Verteilungs-Agent oder Merge-Agent diese Momentaufnahme auf dem Abonnenten anwenden soll.  
  
-   Die Konten, unter denen der Verteilungs-Agent oder der Merge-Agent ausgeführt wird.  
  
-   Bei Mergereplikationen den Abonnementtyp: Server oder Client.  
  
 **So erstellen Sie ein Pushabonnement**  
  
 [Erstellen eines Pushabonnements](create-a-push-subscription.md)  
  
 **So können Sie Eigenschaften von Pushabonnements anzeigen und ändern**  
  
 [Anzeigen und Ändern der Eigenschaften von Pushabonnements](view-and-modify-push-subscription-properties.md)  
  
 **So löschen Sie ein Pushabonnement**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Löschen eines Pushabonnements](delete-a-push-subscription.md)  
  
> [!NOTE]  
>  Durch das Löschen eines Abonnements werden veröffentlichte Objekte nicht vom Abonnenten gelöscht.  
  
 **So erstellen Sie ein Pullabonnement**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Erstellen eines Pullabonnements](create-a-pull-subscription.md)  
  
 **So können Sie Eigenschaften von Pullabonnements anzeigen und ändern**  
  
 [Anzeigen und Ändern der Eigenschaften von Pullabonnements](view-and-modify-pull-subscription-properties.md)  
  
 **So löschen Sie ein Pullabonnement**  
  
 [Löschen eines Pullabonnements](delete-a-pull-subscription.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern des Abonnenten](security/secure-the-subscriber.md)   
 [Abonnementablauf und -deaktivierung](subscription-expiration-and-deactivation.md)  
  
  
