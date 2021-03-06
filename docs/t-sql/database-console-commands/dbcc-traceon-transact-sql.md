---
title: DBCC TRACEON (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_TRACEON_TSQL
- TRACEON
- DBCC TRACEON
- TRACEON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC TRACEON statement
- trace flags [SQL Server], enabling
ms.assetid: 93085324-ebaa-4e38-aac8-5e57b4b0d36d
author: pmasl
ms.author: umajay
manager: craigg
ms.openlocfilehash: 1bc364890a2bb678b8ad9ef5dad5238656443acf
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685242"
---
# <a name="dbcc-traceon-transact-sql"></a>DBCC TRACEON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Aktiviert die angegebenen Ablaufverfolgungsflags.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Themenlinksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC TRACEON ( trace# [ ,...n ][ , -1 ] ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumente  
*trace#*  
Die Nummer des Ablaufverfolgungsflags, das aktiviert werden soll.  
  
*n*  
Ein Platzhalter, der anzeigt, dass mehrere Ablaufverfolgungsflags angegeben werden können.  
  
-1  
Schaltet die angegebenen Ablaufverfolgungsflags global ein.  
  
WITH NO_INFOMSGS  
Alle Informationsmeldungen werden unterdrückt.  
  
## <a name="remarks"></a>Remarks  
Auf einem Produktionsserver wird zur Vermeidung unvorhergesehenen Verhaltens empfohlen, dass Sie Ablaufverfolgungsflags nur mithilfe einer der folgenden Methoden serverweit aktivieren:
-   Verwenden Sie die Befehlszeilenstartoption **-T** von Sqlservr.exe. Dies wird als bewährte Methode empfohlen, da hiermit sichergestellt wird, dass alle Anweisungen bei aktiviertem Ablaufverfolgungsflag ausgeführt werden. Hierzu gehören auch Befehle in Startskripts. Weitere Informationen finden Sie unter [sqlservr Application](../../tools/sqlservr-application.md).  
-   Verwenden Sie DBCC TRACEON **(**_trace#_ [**,** ...*.n*]**,-1)** nur, solange keine Benutzer oder Anwendungen mehrere Anweisungen gleichzeitig auf dem System ausführen.  

Mithilfe von Ablaufverfolgungsflags können Sie die Funktionsweise von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beeinflussen und bestimmte Merkmale anpassen. Nach dem Aktivieren bleiben Ablaufverfolgungsflags auf dem Server aktiviert, bis sie durch die Ausführung der DBCC TRACEOFF-Anweisung deaktiviert werden. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt es zwei Typen von Ablaufverfolgungsflags: Sitzung und global. Ablaufverfolgungsflags des Typs Session werden für eine Verbindung aktiviert und sind nur für diese Verbindung sichtbar. Globale Ablaufverfolgungsflags werden auf Serverebene festgelegt und sind für jede Verbindung auf dem Server sichtbar. Mithilfe von DBCC TRACESTATUS können Sie den Status der Ablaufverfolgungsflags bestimmen. Verwenden Sie DBCC TRACEOFF, um Ablaufverfolgungsflags zu deaktivieren.
  
Führen Sie nach der Aktivierung eines Ablaufverfolgungsflags, das Abfragepläne beeinflusst, `DBCC FREEPROCCACHE;` aus, um zwischengespeicherte Pläne durch das neue den Plan beeinflussende Verhalten erneut zu kompilieren.
  
## <a name="result-sets"></a>Resultsets  
 DBCC TRACEON gibt das folgende Resultset zurück (Meldung):  
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .
  
## <a name="examples"></a>Beispiele  
Das folgende Beispiel deaktiviert die Hardwarekomprimierung für Bandtreiber durch Einschalten des Ablaufverfolgungsflags `3205`. Das Flag wird nur für die aktuelle Verbindung eingeschaltet.
  
```sql  
DBCC TRACEON (3205);  
GO  
```  
  
Das folgende Beispiel schaltet das Ablaufverfolgungsflags `3205` global ein.
  
```sql  
DBCC TRACEON (3205, -1);  
GO  
```  
  
Das folgende Beispiel schaltet die Ablaufverfolgungsflags `3205` und `260` global ein.
  
```sql  
DBCC TRACEON (3205, 260, -1);  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACESTATUS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[Ablaufverfolgungsflags &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
[Aktivieren eines SQL Server-Abfrageoptimiererverhaltens, das Pläne beeinflusst und über verschiedene Ablaufverfolgungsflags auf einer spezifischen Abfrageebene gesteuert werden kann.](https://support.microsoft.com/kb/2801413)
  
  
