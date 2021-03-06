---
title: DBCC FREESYSTEMCACHE (Transact-SQL) | Microsoft Dokumentation
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FREESYSTEMCACHE_TSQL
- DBCC_FREESYSTEMCACHE_TSQL
- DBCC FREESYSTEMCACHE
- FREESYSTEMCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- clearing unused cache entries
- DBCC FREESYSTEMCACHE statement
- unused cache entries
- releasing unused cache entries
- freeing unused cache entries
- cleaning unused cache entries
ms.assetid: 4b5c460b-e4ad-404a-b4ca-d65aba38ebbb
author: pmasl
ms.author: umajay
manager: craigg
ms.openlocfilehash: 00b6ddce8d5c69e16913290b0300fc6828352147
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685677"
---
# <a name="dbcc-freesystemcache-transact-sql"></a>DBCC FREESYSTEMCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Gibt alle nicht verwendeten Cacheeinträge aus allen Caches frei. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] löscht nicht verwendete Cacheeinträge aktiv im Hintergrund und macht so neuen Speicherplatz für aktuelle Einträge verfügbar. Sie können mit diesem Befehl jedoch nicht verwendete Einträge aus jedem Cache oder aus einem angegebenen Cache für den Resource Governor-Pool löschen.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Themenlinksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
```sql
DBCC FREESYSTEMCACHE   
    ( 'ALL' [, pool_name ] )   
    [WITH   
    { [ MARK_IN_USE_FOR_REMOVAL ] , [ NO_INFOMSGS ]  }  
    ]  
```  
  
## <a name="arguments"></a>Argumente  
( 'ALL' [,_pool\_name_ ] )  
ALL gibt alle unterstützten Caches an.  
_pool\_name_ gibt einen Cache für den Resource Governor-Poolcache an. Nur diesem Pool zugeordnete Einträge werden freigegeben.  
  
MARK_IN_USE_FOR_REMOVAL  
Gibt zurzeit verwendete Einträge asynchron aus den jeweiligen Caches nach ihrer Verwendung frei. Nach der Ausführung von DBCC FREESYSTEMCACHE WITH MARK_IN_USE_FOR_REMOVAL im Cache neu erstellte Einträge sind nicht betroffen.  
  
NO_INFOMSGS  
Alle Informationsmeldungen werden unterdrückt.  
  
## <a name="remarks"></a>Remarks  
Durch das Ausführen von DBCC FREESYSTEMCACHE wird der Plancache für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelöscht. Durch das Löschen des Plancaches wird eine Neukompilierung aller nachfolgenden Ausführungspläne verursacht, und möglicherweise entsteht plötzlich eine temporäre Verringerung der Abfrageleistung. Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll enthält für jeden geleerten Cachespeicher im Plancache folgende Informationsmeldung: „[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat für den %2!s!-Cachespeicher (Bestandteil des Plancache) %1!s! Leerungen des Cachespeichers gefunden, die von DBCC FREEPROCCACHE- oder DBCC FREESYSTEMCACHE-Vorgängen ausgelöst wurden.“ Diese Meldung wird alle fünf Minuten protokolliert, solange der Cache innerhalb dieses Zeitintervalls geleert wird.

## <a name="result-sets"></a>Resultsets  
DBCC FREESYSTEMCACHE gibt Folgendes zurück: "Die DBCC-Ausführung wurde abgeschlossen. Falls DBCC Fehlermeldungen ausgegeben hat, wenden Sie sich an den Systemadministrator."
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die ALTER SERVER STATE-Berechtigung auf dem Server.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-releasing-unused-cache-entries-from-a-resource-governor-pool-cache"></a>A. Freigeben nicht verwendeter Cacheeinträge aus einem Cache für den Ressourcenkontrollenpool  
Im folgenden Beispiel wird veranschaulicht, wie Caches geleert werden, die einem angegebenen Ressourcenpool für die Ressourcenkontrolle zugeordnet sind.
  
```sql
-- Clean all the caches with entries specific to the resource pool named "default".  
DBCC FREESYSTEMCACHE ('ALL', default);  
```  
  
### <a name="b-releasing-entries-from-their-respective-caches-after-they-become-unused"></a>B. Freigeben von Einträgen aus den jeweiligen Caches nach ihrer Verwendung  
Im folgenden Beispiel wird die MARK_IN_USE_FOR_REMOVAL-Klausel dazu verwendet, alle Einträge von allen aktuellen Caches nach ihrer Verwendung freizugeben.
  
```sql
DBCC FREESYSTEMCACHE ('ALL') WITH MARK_IN_USE_FOR_REMOVAL;  
```  
  
## <a name="see-also"></a>Weitere Informationen  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[DBCC FREESESSIONCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)
  
  
