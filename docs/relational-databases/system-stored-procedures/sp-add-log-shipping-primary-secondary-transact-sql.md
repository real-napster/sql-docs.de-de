---
title: Sp_add_log_shipping_primary_secondary (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_primary_secondary_TSQL
- sp_add_log_shipping_primary_secondary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_primary_secondary
ms.assetid: 23b3e100-5318-410e-b8f3-51c89b2dd777
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0aac9866026949b278e9a8eba4310f158254a521
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2019
ms.locfileid: "58494052"
---
# <a name="spaddlogshippingprimarysecondary-transact-sql"></a>sp_add_log_shipping_primary_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Diese gespeicherte Prozedur fügt einen Eintrag für eine sekundäre Datenbank auf dem primären Server hinzu.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_add_log_shipping_primary_secondary  
[ @primary_database = ] 'primary_database',  
[ @secondary_server = ] 'secondary_server',   
[ @secondary_database = ] 'secondary_database'  
```  
  
## <a name="arguments"></a>Argumente  
`[ @primary_database = ] 'primary_database'` Ist der Name der Datenbank auf dem primären Server. *primary_database* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
`[ @secondary_server = ] 'secondary_server',` Ist der Name des sekundären Servers. *secondary_server* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
`[ @secondary_database = ] 'secondary_database'` Ist der Name der sekundären Datenbank. *secondary_database* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 None  
  
## <a name="remarks"></a>Hinweise  
 **sp_add_log_shipping_primary_secondary** muss aus der **master** -Datenbank auf dem primären Server ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können diese Prozedur ausführen.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird das Verwenden von **sp_add_log_shipping_primary_secondary** zum Hinzufügen eines Eintrags für die sekundäre Datenbank **LogShipAdventureWorks** auf dem sekundären Server FLATIRON veranschaulicht.  
  
```  
EXEC master.dbo.sp_add_log_shipping_primary_secondary   
@primary_database = N'AdventureWorks'   
, @secondary_server = N'flatiron'   
, @secondary_database = N'LogShipAdventureWorks' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Über den Protokollversand &#40;SQLServer&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
