---
title: Kombinieren einer Failoverclusterinstanz mit Verfügbarkeitsgruppen
description: Verbessern Sie Ihre Hochverfügbarkeit und Notfallwiederherstellbarkeit, indem Sie die Funktionen einer SQL Server-Failoverclusterinstanz und einer Always On-Verfügbarkeitsgruppe kombinieren.
ms.custom: seodec18
ms.date: 07/02/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- clustering [SQL Server]
- Availability Groups [SQL Server], WSFC clusters
- Failover Cluster Instances [SQL Server], see failover clustering [SQL Server]
- quorum [SQL Server]
- failover clustering [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], Failover Cluster Instances
ms.assetid: 613bfbf1-9958-477b-a6be-c6d4f18785c3
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 7246ad4ef1aae3120b2e01563a8a849f8d421f9f
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/18/2019
ms.locfileid: "57974169"
---
# <a name="failover-clustering-and-always-on-availability-groups-sql-server"></a>Failoverclustering und AlwaysOn-Verfügbarkeitsgruppen (SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

   [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], die in [!INCLUDE[sssql11](../../../includes/sssql11-md.md)] eingeführte Lösung für hohe Verfügbarkeit und Notfallwiederherstellung, erfordert WSFC (Windows Server-Failoverclustering). [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ist zwar nicht von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclustering abhängig, Sie können aber dennoch eine FCI (Failoverclusterinstanz) verwenden, um ein Verfügbarkeitsreplikat für eine Verfügbarkeitsgruppe zu hosten. Es ist wichtig, dass Sie die Rolle jeder Clusteringtechnologie kennen, und wissen, welche Überlegungen Sie für den Entwurf Ihrer [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Umgebung anstellen müssen.  
  
> [!NOTE]  
>  Informationen zu [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Konzepten finden Sie unter [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
  
##  <a name="WSFC"></a> Windows Server Failover Clustering und Verfügbarkeitsgruppen  
 Für die Bereitstellung von [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ist ein Windows Server-Failovercluster (WSFC) erforderlich. Um für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] aktiviert werden zu können, muss sich eine Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf einem WSFC-Knoten befinden, und der WSFC sowie der WSFC-Knoten müssen online sein. Zudem muss sich jedes Verfügbarkeitsreplikat einer bestimmten Verfügbarkeitsgruppe auf einem anderen Knoten desselben WSFC befinden. Die einzige Ausnahme besteht darin, dass sich eine Verfügbarkeitsgruppe während der Migration zu einem anderen WSFC vorübergehend auf zwei Cluster erstrecken kann.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] basiert zur Überwachung und Verwaltung der aktuellen Rollen der Verfügbarkeitsreplikate, die zu einer gegebenen Verfügbarkeitsgruppe gehören, auf dem Windows-Failovercluster (WSFC) und bestimmt, wie sich ein Failoverereignis auf die Verfügbarkeitsreplikate auswirkt. Für jede erstellte Verfügbarkeitsgruppe wird eine WSFC-Ressourcengruppe erstellt. Der WSFC überwacht diese Ressourcengruppe, um die Integrität des primären Replikats auszuwerten.  
  
 Das Quorum für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] basiert unabhängig davon, ob ein bestimmter Clusterknoten Verfügbarkeitsreplikate hostet, auf allen Knoten des WSFC. Im Gegensatz zur Datenbankspiegelung ist in [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] keine Zeugenrolle verfügbar.  
  
 Die allgemeine Integrität des WSFC wird von den Abstimmungen eines Quorums der Clusterknoten bestimmt. Wird der WSFC wegen eines nicht geplanten Notfalls oder aufgrund eines persistenten Hardware- oder Kommunikationsfehlers offline geschaltet, ist manueller Eingriff durch den Administrator erforderlich. Ein Windows Server- oder WSFC-Administrator muss ein Quorum erzwingen und dann die überdauernden Clusterknoten in einer nicht fehlertoleranten Konfiguration wieder online schalten.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Registrierungsschlüssel sind Unterschlüssel des WSFC. Wenn Sie einen WSFC löschen und neu erstellen, müssen Sie das Feature [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] für jede Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deaktivieren und erneut aktivieren, auf der auf dem ursprünglichen WSFC ein Verfügbarkeitsreplikat gehostet wurde.  
  
 Informationen zum Ausführen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf WSFC-Knoten sowie zum WSFC-Quorum finden Sie unter [Windows Server-Failoverclustering &#40;WSFC&#41; mit SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md).  
  
##  <a name="SQLServerFC"></a> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Failoverclusterinstanzen (FCIs) und Verfügbarkeitsgruppen  
 Sie können auf Serverinstanzebene eine zweite Failoverebene einrichten, indem Sie eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-FCI zusammen mit dem WSFC implementieren. Ein Verfügbarkeitsreplikat kann von einer eigenständigen Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oder einer FCI-Instanz gehostet werden. Ein Replikat für eine Verfügbarkeitsgruppe kann jeweils nur von einem FCI-Partner gehostet werden. Bei Ausführung eines Verfügbarkeitsreplikats in einer FCI enthält die Liste möglicher Besitzer für die Verfügbarkeitsgruppe nur den aktiven FCI-Knoten.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] hängt von keiner Form eines gemeinsam verwendeten Speichers ab. Falls Sie jedoch eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz (FCI) zum Hosten von mindestens einem Verfügbarkeitsreplikats verwenden, ist für all diese FCIs der standardmäßigen Installation der SQL Server-Failoverclusterinstanz entsprechend gemeinsam verwendeter Speicher erforderlich.  
  
 Weitere Informationen zu zusätzlichen erforderlichen Komponenten finden Sie im Abschnitt „Voraussetzungen und Einschränkungen zum Hosten eines Verfügbarkeitsreplikats mithilfe einer SQL Server-Failoverclusterinstanz (FCI)“ von [Voraussetzungen, Einschränkungen und Empfehlungen für AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
### <a name="comparison-of-failover-cluster-instances-and-availability-groups"></a>Vergleich der Failoverclusterinstanzen und Verfügbarkeitsgruppen  
 Unabhängig von der Anzahl der Knoten in der FCI hostet eine ganze FCI ein einzelnes Replikat innerhalb einer Verfügbarkeitsgruppe. In der folgenden Tabelle werden die Unterschiede der Konzepte zwischen Knoten in einer FCI und Replikaten in einer Verfügbarkeitsgruppe beschrieben.  
  
||Knoten in einer FCI|Replikate in einer Verfügbarkeitsgruppe|  
|-|-------------------------|-------------------------------------------|  
|**Verwendet WSFC**|Ja|Ja|  
|**Schutzebene**|Instanz|Datenbank|  
|**Speichertyp**|Shared|Nicht freigegeben<br /><br /> Obwohl die Replikate in einer Verfügbarkeitsgruppe keinen Speicher gemeinsam verwenden, verwendet ein Replikat, das von einer FCI gehostet wird, gemäß der Anforderung dieser FCI eine gemeinsame Speicherlösung. Die Speicherlösung wird nur von Knoten in dieser FCI verwendet und nicht zwischen den Replikaten der Verfügbarkeitsgruppe.|  
|**Speicherlösungen**|Direkt angefügt, SAN, Einbindungspunkte, SMB|Hängt von Knotentyp ab|  
|**Lesbare sekundäre**|Nein*|Ja|  
|**Anwendbare Failoverrichtlinieneinstellungen**|WSFC-Quorum<br /><br /> FCI-spezifisch<br /><br /> Verfügbarkeitsgruppeneinstellungen**|WSFC-Quorum<br /><br /> Verfügbarkeitsgruppeneinstellungen|  
|**Failoverressourcen**|Server, Instanz und Datenbank|Nur Datenbank|  
  
 *Während synchrone sekundäre Replikate in einer Verfügbarkeitsgruppe stets in ihren jeweiligen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanzen ausgeführt werden, haben Sekundärknoten in einer FCI ihre jeweiligen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanzen tatsächlich nicht gestartet und sind daher nicht lesbar. In einer FCI startet ein sekundärer Knoten seine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz nur, wenn der Ressourcengruppenbesitz während eines FCI-Failovers an ihn übergeben wird. Wenn jedoch auf dem aktiven FCI-Knoten eine FCI-gehostete Datenbank zu einer Verfügbarkeitsgruppe gehört, ist die Datenbank lesbar, wenn das lokale Verfügbarkeitsreplikat als lesbares sekundäres Replikat ausgeführt wird.  
  
 **Failoverrichtlinieneinstellungen für die Verfügbarkeitsgruppe gelten für alle Replikate, unabhängig davon, ob sie in einer eigenständigen Instanz oder einer FCI-Instanz gehostet werden.  
  
> [!NOTE]  
>  Weitere Informationen zur **Anzahl der Knoten** innerhalb von FCIs sowie zu **Always On-Verfügbarkeitsgruppen** für verschiedene [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Editionen finden Sie unter [Features Supported by the Editions of SQL Server 2012 (Von den SQL Server 2012-Editionen unterstützte Features)](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473)).  
  
### <a name="considerations-for-hosting-an-availability-replica-on-an-fci"></a>Überlegungen zum Hosten eines Verfügbarkeitsreplikats auf einer FCI  
  
> [!IMPORTANT]  
>  Wenn Sie planen, in einer SQL Server-Failoverclusterinstanz (FCI) ein Verfügbarkeitsreplikat zu hosten, stellen Sie sicher, dass die Windows Server 2008-Hostknoten die AlwaysOn-Voraussetzungen und -Einschränkungen für Failoverclusterinstanzen (FCIs) erreichen. Weitere Informationen finden Sie unter [Voraussetzungen, Einschränkungen und Empfehlungen für AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)zu unterstützen.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Failoverclusterinstanzen (FCIs) unterstützen kein automatisches AlwaysOn-Failover durch Verfügbarkeitsgruppen. Daher können die Verfügbarkeitsreplikate, die von einer FCI gehostet werden, nur für manuelles Failover konfiguriert werden.  
  
 Möglicherweise muss ein WSFC so konfiguriert werden, dass er freigegebene Datenträger enthält, die nicht auf allen Knoten verfügbar sind. Denken Sie beispielsweise an ein WSFC über zwei Rechenzentren mit drei Knoten. Zwei der Knoten hosten im primären Rechenzentrum eine SQL Server-Failoverclusterinstanz (FCI) und haben Zugriff auf dieselben freigegebenen Datenträger. Der dritte Knoten hostet eine eigenständige Instanz von SQL Server in einem anderen Rechenzentrum und verfügt nicht über Zugriff auf die freigegebenen Datenträger vom primären Rechenzentrum. Diese WSFC-Konfiguration unterstützt die Bereitstellung einer Verfügbarkeitsgruppe, wenn die FCI das primäre Replikat hostet, und die eigenständige Instanz das sekundäre Replikat hostet.  
  
 Bei Auswahl einer FCI zum Hosten eines Verfügbarkeitsreplikats für eine angegebene Verfügbarkeitsgruppe muss gewährleistet sein, dass ein FCI-Failover nicht möglicherweise bewirkt, dass ein einzelner WSFC-Knoten versucht, zwei Verfügbarkeitsreplikate für dieselbe Verfügbarkeitsgruppe zu hosten.  
  
 Im folgenden Beispielszenario wird veranschaulicht, wie diese Konfiguration zu Problemen führen könnte:  
  
 Marcel konfiguriert einen WSFC mit zwei Knoten, `NODE01` und `NODE02`. Er installiert eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz, `fciInstance1`, auf `NODE01` und `NODE02` , wobei `NODE01` der aktuelle Besitzer für `fciInstance1`ist.  
 Auf `NODE02`installiert Marcel eine andere Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], `Instance3`, die eine eigenständige Instanz ist.  
 Auf `NODE01`aktiviert Marcel fciInstance1 für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Auf `NODE02`aktiviert er `Instance3` für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Dann richtet er eine Verfügbarkeitsgruppe ein, für die `fciInstance1` das primäre Replikat hostet, und `Instance3` hostet das sekundäre Replikat.  
 An einen bestimmten Punkt ist `fciInstance1` auf `NODE01`nicht mehr verfügbar, und der WSFC verursacht einen Failover von `fciInstance1` auf `NODE02`. Nach dem Failover ist `fciInstance1` eine [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]-fähige Instanz, die unter der primären Rolle auf `NODE02`ausgeführt wird. `Instance3` befindet sich jetzt jedoch auf demselben WSFC-Knoten wie `fciInstance1`. Dies verstößt gegen die [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Einschränkung.  
 Um das Problem in diesem Szenario zu beheben, muss sich die eigenständige Instanz, `Instance3`, auf einem anderen Knoten im selben WSFC wie `NODE01` und `NODE02`befinden.  
  
 Weitere Informationen zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-FCIs finden Sie unter [Always On-Failoverclusterinstanzen (SQL Server)](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
##  <a name="FCMrestrictions"></a> Einschränkungen bei Verwendung des WSFC-Failovercluster-Managers für Verfügbarkeitsgruppen  
 Verwenden Sie den Failovercluster-Manager nicht zum Bearbeiten von Verfügbarkeitsgruppen, beispielsweise:  
  
-   Fügen Sie im Clusterdienst (Ressourcengruppe) keine Ressourcen für die Verfügbarkeitsgruppe hinzu, bzw. entfernen Sie keine Ressourcen.  
  
-   Ändern Sie keine Verfügbarkeitsgruppeneigenschaften, z. B. die möglichen und bevorzugten Besitzer. Diese Eigenschaften werden automatisch von der Verfügbarkeitsgruppe festgelegt.  
  
-   **Verwenden Sie den Failovercluster-Manager nicht zum Verschieben von Verfügbarkeitsgruppen auf verschiedene Knoten oder zum Ausführen eines Failovers für Verfügbarkeitsgruppen.** Der Synchronisierungsstatus der Verfügbarkeitsreplikate ist dem Failovercluster-Manager nicht bekannt, sodass ein solcher Vorgang die Downtime verlängern kann. Sie müssen [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]verwenden.  

  >[!WARNING]
  > Die Verwendung des Failovercluster-Managers zum Verschieben einer *Failoverclusterinstanz*, die eine Verfügbarkeitsgruppe hostet, auf einen Knoten, der *bereits* ein Replikat derselben Verfügbarkeitsgruppe hostet, kann zum Verlust des Verfügbarkeitsgruppenreplikats führen, sodass dieses auf dem Zielknoten nicht online geschaltet werden kann. Ein einzelner Knoten eines Failoverclusters kann nicht mehr als ein Replikat für dieselbe Verfügbarkeitsgruppe hosten. Weitere Informationen dazu, wie eine solche Situation eintritt und wie sie gelöst werden kann, finden Sie im Blog [Replica unexpectedly dropped in availability group](https://blogs.msdn.microsoft.com/alwaysonpro/2014/02/03/issue-replica-unexpectedly-dropped-in-availability-group/) (Replikat in Verfügbarkeitsgruppe unerwartet gelöscht). 
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   **Blogs:**  
  
     [Konfigurieren von Windows-Failoverclustering für SQL Server (Verfügbarkeitsgruppe oder Failoverclusterinstanz) mit beschränkter Sicherheit](https://blogs.msdn.microsoft.com/sqlalwayson/2012/06/05/configure-windows-failover-clustering-for-sql-server-availability-group-or-fci-with-limited-security/)  
  
     [SQL Server Always On Team Blogs: The official SQL Server Always On Team Blog (SQL Server Always On-Teamblog: Der offizielle SQL Server Always On-Teamblog)](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server-Technikblogs](https://blogs.msdn.com/b/psssql/)  
  
-   **Whitepaper:**  
  
     [Always On-Architekturhandbuch: Erstellen einer Lösung für Hochverfügbarkeit und Notfallwiederherstellung unter Verwendung von Failoverclusterinstanzen und Verfügbarkeitsgruppen](https://msdn.microsoft.com/library/jj215886.aspx)  
  
     [Microsoft SQL Server Always On-Lösungshandbuch zu hoher Verfügbarkeit und Notfallwiederherstellung](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Microsoft-Whitepapers für SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Whitepapers des SQL Server-Kundenberatungsteams](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>Weitere Informationen  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Aktivieren und Deaktivieren von Always On-Verfügbarkeitsgruppen (SQL Server)](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)   
 [Überwachen von Verfügbarkeitsgruppen &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn-Failoverclusterinstanzen &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
  
