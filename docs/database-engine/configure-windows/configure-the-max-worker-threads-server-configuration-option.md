---
title: Konfigurieren der Serverkonfigurationsoption „Maximale Anzahl von Arbeitsthreads“ | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/23/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- worker threads [SQL Server]
- max worker threads option
ms.assetid: abeadfa4-a14d-469a-bacf-75812e48fac1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6088e603405a41d5bffbc1425b9f6f5495096f18
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2019
ms.locfileid: "59429336"
---
# <a name="configure-the-max-worker-threads-server-configuration-option"></a>Konfigurieren der Serverkonfigurationsoption Maximale Anzahl von Arbeitsthreads
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **Max. Anzahl von Arbeitsthreads** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]konfiguriert wird. Sie können mithilfe der Option **Max. Anzahl von Arbeitsthreads** die Anzahl von Arbeitsthreads konfigurieren, die für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozesse zur Verfügung stehen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet die systemeigenen Threaddienste der Betriebssysteme, sodass jedes Netzwerk, das gleichzeitig von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt wird, von mindestens einem Thread unterstützt wird. Ein weiterer Thread verarbeitet die Datenbank-Prüfpunkte, und ein Threadpool verarbeitet alle Benutzer. Der Standardwert für **Max. Anzahl von Arbeitsthreads** ist 0. Auf diese Weise kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Anzahl der Arbeitsthreads beim Starten automatisch konfigurieren. Die Standardeinstellung ist für die meisten Systeme am besten geeignet. Abhängig von der Konfiguration des Systems kann durch Festlegen von **Max. Anzahl von Arbeitsthreads** auf einen bestimmten Wert manchmal die Leistung verbessert werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
     [Security](#Security)  
  
-   **So konfigurieren Sie die Option Maximale Anzahl von Arbeitsthreads mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Konfigurieren der Option „Max. Anzahl von Arbeitsthreads“](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn die tatsächliche Anzahl von Abfrageanforderungen geringer als der für **Max. Anzahl von Arbeitsthreads**festgelegte Wert ist, werden alle Abfrageanforderungen von einem Thread verarbeitet. Wenn die tatsächliche Anzahl von Abfrageanforderungen jedoch den für **max worker threads**festgelegten Wert überschreitet, erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Pool von Arbeitsthreads, damit die Anforderung vom nächsten verfügbaren Arbeitsthread verarbeitet werden kann.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Diese Option ist eine erweiterte Option und sollte ausschließlich von einem erfahrenen Datenbankadministrator oder einem zertifizierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Experten geändert werden. Wenn Sie ein Leistungsproblem vermuten, ist es wahrscheinlich nicht die Verfügbarkeit von Arbeitsthreads. Eine wahrscheinlichere Ursache ist z.B. E/A, die ein Warten der Arbeitsthreads bewirkt. Sinnvollerweise sollten Sie die Grundursache eines Leistungsproblems ermitteln, bevor Sie die Einstellung für die maximale Anzahl der Arbeitsthreads ändern.  
  
-   Threadpools erleichtern das Optimieren der Leistung, wenn sehr viele Clients mit dem Server verbunden sind. Üblicherweise wird ein separater Betriebssystemthread für jede Abfrageanforderung erstellt. Wenn jedoch bei Hunderten von Verbindungen mit dem Server weiterhin ein Thread pro Abfrageanforderung verwendet wird, kann dabei eine große Menge an Systemressourcen verbraucht werden. Die Option **Max. Anzahl von Arbeitsthreads** ermöglicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das Erstellen eines Pools mit Arbeitsthreads, der eine große Anzahl von Abfrageanforderungen versorgen kann und so zur Verbesserung der Leistung beiträgt.  
  
-   In der folgenden Tabelle werden die automatisch konfigurierte maximale Anzahl von Arbeitsthreads für verschiedene Kombinationen von CPUs und Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dargestellt.  
  
    |Anzahl von CPUs|32-Bit-Computer|64-Bit-Computer|  
    |------------|------------|------------|  
    |\<= 4 Prozessoren|256|512|  
    |8 Prozessoren|288|576|  
    |16 Prozessoren|352|704|  
    |32 Prozessoren|480|960|  
    |64 Prozessoren|736|1472|  
    |128 Prozessoren|4224|4480|  
    |256 Prozessoren|8320|8576| 
    
    Verwenden Sie die folgende Formel:
    
    |Anzahl von CPUs|32-Bit-Computer|64-Bit-Computer|  
    |------------|------------|------------| 
    |\<= 4 Prozessoren|256|512|
    |\> 4 Prozessoren und \< 64 Prozessoren|256 + ((logische CPUs - 4) * 8)|512 + ((logische CPUs – 4) * 16)|
    |\> 64 Prozessoren|256 + ((logische CPUs – 4) * 32)|512 + ((logische CPUs – 4) * 32)|
  
    > [!NOTE]  
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann nicht mehr unter einem 32-Bit-Betriebssystem installiert werden. Werte für 32-Bit-Computer sind zur Unterstützung von Kunden aufgeführt, die [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und früher nutzen. Als maximale Anzahl von Arbeitsthreads auf einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz, die auf einem 32-Bit-Computer ausgeführt wird, wird der Wert 1.024 empfohlen.  
  
    > [!NOTE]  
    > Empfehlungen zur Verwendung von mehr als 64 CPUs finden Sie unter [Bewährte Methoden zum Ausführen von SQL Server auf Computern mit mehr als 64 CPUs](../../relational-databases/thread-and-task-architecture-guide.md#best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus).  
  
-   Wenn alle Arbeitsthreads aktiviert sind, kann es sein, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei Abfragen mit langer Ausführungszeit scheinbar nicht mehr reagiert, bis ein Arbeitsthread abgeschlossen wird und verfügbar ist. Dies ist zwar kein Fehler, aber in bestimmten Situationen unerwünscht. Wenn ein Prozess scheinbar nicht mehr reagiert und keine neuen Abfragen verarbeitet werden können, stellen Sie mithilfe der dedizierten Administratorverbindung (DAC) eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her, und brechen Sie den Prozess ab. Um diese Situation zu verhindern, erhöhen Sie den Wert für die maximale Anzahl von Arbeitsthreads.  
  
 Durch die Serverkonfigurationsoption **Max. Anzahl von Arbeitsthreads** werden nicht alle Threads begrenzt, die im System erzeugt werden können. Threads, die für Aufgaben wie Verfügbarkeitsgruppen, Service Broker, Sperren-Manager usw. erforderlich sind, gehen über dieses Limit hinaus. Wenn die Anzahl der konfigurierten Threads überschritten wird, bietet die folgende Abfrage Informationen zu den Systemtasks, durch die die zusätzlichen Threads erzeugt wurden.  
  
 ```sql  
 SELECT  s.session_id, r.command, r.status,  
    r.wait_type, r.scheduler_id, w.worker_address,  
    w.is_preemptive, w.state, t.task_state,  
    t.session_id, t.exec_context_id, t.request_id  
 FROM sys.dm_exec_sessions AS s  
 INNER JOIN sys.dm_exec_requests AS r  
    ON s.session_id = r.session_id  
 INNER JOIN sys.dm_os_tasks AS t  
    ON r.task_address = t.task_address  
 INNER JOIN sys.dm_os_workers AS w  
    ON t.worker_address = w.worker_address  
 WHERE s.is_user_process = 0;  
 ```  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Um **sp_configure** mit beiden Parametern auszuführen und eine Konfigurationsoption zu ändern oder die `RECONFIGURE`-Anweisung auszuführen, benötigt ein Benutzer die `ALTER SETTINGS`-Berechtigung auf Serverebene. Die `ALTER SETTINGS`-Berechtigung ist implizit in den festen Serverrollen **sysadmin** und **serveradmin** enthalten.  
  
##  <a name="SSMSProcedure"></a> Bei Verwendung von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>So konfigurieren Sie die Option Max. Anzahl von Arbeitsthreads  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und wählen Sie **Eigenschaften** aus.  
  
2.  Klicken Sie auf den Knoten **Prozessoren** .  
  
3.  Geben Sie im Feld **Max. Anzahl von Arbeitsthreads** einen Wert zwischen 128 und 32.767 ein, oder wählen Sie einen Wert aus.  
  
> [!TIP]
> Sie können mithilfe der Option **Max. Anzahl von Arbeitsthreads** die Anzahl von Arbeitsthreads konfigurieren, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozessen zur Verfügung stehen. Die Standardeinstellung für **Max. Anzahl von Arbeitsthreads** eignet sich für die meisten Systeme am besten. Abhängig von der Konfiguration des Systems kann die Leistung manchmal verbessert werden, indem **Max. Anzahl von Arbeitsthreads** auf einen niedrigeren Wert festgelegt wird.
> Unter [Empfehlungen](#Recommendations) auf dieser Seite finden Sie weitere Informationen.
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>So konfigurieren Sie die Option Max. Anzahl von Arbeitsthreads  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) verwendet wird, um die Option `max worker threads` auf `900`festzulegen.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'max worker threads', 900 ;  
GO  
RECONFIGURE;  
GO  
```  
  
##  <a name="FollowUp"></a>Nächster Schritt: Nach dem Konfigurieren der Option „Max. Anzahl von Arbeitsthreads“  
 Die Änderung wird nach dem Ausführen von [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md) sofort wirksam, ohne dass ein Neustart von [!INCLUDE[ssDE](../../includes/ssde-md.md)] erforderlich ist.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Diagnoseverbindung für Datenbankadministratoren](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
  
