---
title: Sys. availability_groups_cluster (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_cluster
- availability_groups_cluster
- availability_groups_cluster_TSQL
- sys.availability_groups_cluster_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: d0f4683f-cdf0-4227-8b68-720ffe58f158
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1173764b8726aebc2e53cef103f341b95e8c82fa
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2018
ms.locfileid: "52511082"
---
# <a name="sysavailabilitygroupscluster-transact-sql"></a>sys.availability_groups_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede AlwaysOn-verfügbarkeitsgruppe in der Windows Server Failover Clustering (WSFC) zurück. Jede Zeile enthält die Metadaten der Verfügbarkeitsgruppe aus dem WSFC-Cluster.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Eindeutiger Bezeichner (GUID) der Verfügbarkeitsgruppe.|  
|**name**|**sysname**|Der Name der Verfügbarkeitsgruppe. Dies ist ein vom Benutzer angegebener Name, der innerhalb des Windows Server-Failoverclusters (WSFC) eindeutig sein muss.|  
|**resource_id**|**nvarchar(40)**|Ressourcen-ID für die WSFC-Clusterressource.|  
|**resource_group_id**|**nvarchar(40)**|Ressourcengruppen-ID für die WSFC-Clusterressourcengruppe der Verfügbarkeitsgruppe.|  
|**failure_condition_level**|**int**|Benutzerdefinierte Fehlerbedingungsebene, unter der ein automatisches Failover ausgelöst werden muss, einer der folgenden ganzzahligen Werte:<br /><br /> 1: Gibt an, dass in einem der folgenden Fälle ein automatisches Failover initiiert werden muss: <br />– Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Dienst ist nicht verfügbar.<br />– Die Lesedauer der verfügbarkeitsgruppe für die Verbindung mit WSFC-Failovercluster läuft ab, da keine ACK-Meldung von der Serverinstanz empfangen wird. Weitere Informationen finden Sie unter [How It Works: SQLServer AlwaysOn LeaseTimeout](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).<br /><br /> 2: Gibt an, dass in einem der folgenden Fälle ein automatisches Failover initiiert werden muss:  <br />– Die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keine Verbindung zu Cluster und der vom Benutzer angegebene **Health_check_timeout** -Schwellenwert der verfügbarkeitsgruppe wurde überschritten. <br />– Das verfügbarkeitsreplikat ist in einem fehlerhaften Zustand. <br />3: Gibt an, dass ein automatisches Failover bei kritischen internen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlern initiiert werden soll, z. B. verwaisten Spinlocks, schwerwiegenden Schreibzugriffsverletzungen oder zu vielen Sicherungen. Dies ist der Standardwert. <br />4: Gibt an, dass ein automatisches Failover bei mittelschweren internen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlern initiiert werden soll, z. B. bei dauerhaft unzureichendem Arbeitsspeicher im internen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ressourcenpool.<br />5: Gibt an, dass ein automatisches Failover bei sämtlichen qualifizierten Fehlerbedingungen initiiert werden soll, einschließlich:<br />– Erschöpfung der SQL Engine-Arbeitsthreads. <br />– Erkennung eines unlösbaren Deadlocks.<br /><br /> Die Fehlerbedingungsebenen (1–5) reichen von der Ebene 1 mit den wenigsten Einschränkungen bis zur Ebene 5 mit den meisten Einschränkungen. Jede Bedingungsebene umfasst stets auch sämtliche weniger restriktiven Ebenen. Daher schließt die strengste Bedingungsebene 5 die vier Bedingungsebenen mit weniger Einschränkungen (1-4) ein, Ebene 4 schließt die Ebenen 1-3 ein usw.<br /><br /> Um diesen Wert zu ändern, verwenden Sie die FAILURE_CONDITION_LEVEL-Option von der [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung.|  
|**health_check_timeout**|**int**|Wartezeit (in Millisekunden) für die [Sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) gespeicherten Systemprozedur Serverzustand Informationen zurückgegeben werden, bevor die Server-Instanz davon ausgegangen, dass ist langsam oder blockiert werden. Der Standardwert ist 30000 Millisekunden (oder 30 Sekunden).<br /><br /> Um diesen Wert zu ändern, verwenden Sie die HEALTH_CHECK_TIMEOUT-Option der [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung.|  
|**automated_backup_preference**|**tinyint**|Bevorzugter Speicherort zum Durchführen von Sicherungen auf den Verfügbarkeitsdatenbanken in dieser Verfügbarkeitsgruppe. Einer der folgenden Werte:<br /><br /> 0: Primär. Sicherungen sollten immer auf dem primären Replikat erfolgen.<br />1: Nur sekundär. Die Durchführung von Sicherungen auf einem sekundären Replikat wird bevorzugt.<br />2: Sekundär bevorzugen. Die Durchführung von Sicherungen auf einem sekundären Replikat wird bevorzugt, aber die Durchführung von Sicherungen auf dem primären Replikat wird akzeptiert, wenn kein sekundäres Replikat für Sicherungsvorgänge verfügbar ist. Dies ist das Standardverhalten.<br />3: Beliebiges Replikat. Keine Präferenz, ob Sicherungen auf dem primären Replikat oder einem sekundären Replikat durchgeführt werden.<br /><br /> Weitere Informationen finden Sie unter [aktive sekundäre Replikate: Sicherung auf sekundären Replikaten &#40;Always On-Verfügbarkeitsgruppen&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).|  
|**automated_backup_preference_desc**|**nvarchar(60)**|Beschreibung der **Automated_backup_preference**, eine von:<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> Keine|  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW ANY DEFINITION-Berechtigung für die Serverinstanz.  
  
## <a name="see-also"></a>Siehe auch  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Überwachen von Verfügbarkeitsgruppen (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Überwachen von Verfügbarkeitsgruppen &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
